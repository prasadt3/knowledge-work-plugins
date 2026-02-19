---
name: cost-optimization-patterns
description: Proven patterns, playbooks, and strategies for reducing GCP costs across all major services. Use when right-sizing instances, eliminating waste, evaluating CUDs, or planning a cost optimization initiative.
---

# GCP Cost Optimization Patterns & Playbooks

## Overview

This skill provides battle-tested patterns for reducing GCP costs. Each pattern includes the problem, detection method, solution, expected savings, implementation steps, and risks.

## Pattern 1: Horizontal Scaling over Vertical Scaling (Cloud Run)

### Problem
Large Cloud Run instances (4-8 vCPU) are expensive and waste resources during low traffic.

### Detection
```bash
gcloud run services describe SERVICE --region=REGION \
  --format="yaml(spec.template.spec.containers[0].resources)"
# If CPU > 2 or Memory > 4Gi → candidate for horizontal scaling
```

### Solution
Replace large instances with smaller ones and increase max instances:

```
Before: 8 vCPU / 16 GB, min=4, max=50, concurrency=80
After:  2 vCPU / 4 GB,  min=2, max=100, concurrency=40
```

### Why It Works
- Smaller instances are more cost-effective per vCPU-second
- Lower concurrency forces scale-out, distributing load
- Better fault tolerance (failure of 1 small instance < failure of 1 large)
- Cloud Run autoscaling handles the rest

### Implementation

```bash
gcloud run services update SERVICE \
  --cpu=2 --memory=4Gi \
  --min-instances=2 --max-instances=100 \
  --concurrency=40 \
  --region=REGION --project=PROJECT
```

Or via Terraform tfvars:
```hcl
studio_cpu               = "2"
studio_memory            = "4Gi"
studio_min_instances     = 2
studio_max_instances     = 100
studio_concurrency       = 40
```

### Expected Savings
50-70% reduction in Cloud Run costs.

### Risks
- Cold start latency if min-instances too low
- Need to verify application works with lower concurrency
- Monitor for increased instance count (should be within max)

---

## Pattern 2: Right-Size Cloud SQL

### Problem
Cloud SQL instances provisioned at initial setup are often over-sized for actual workload.

### Detection
```bash
# Check current tier
gcloud sql instances describe INSTANCE --format="value(settings.tier)"

# Check CPU/memory utilization (Cloud Console > SQL > Instance > Metrics)
# Or via monitoring API:
gcloud monitoring read \
  "metric.type=\"cloudsql.googleapis.com/database/cpu/utilization\"" \
  --project=PROJECT --format=json
```

Rule of thumb:
- Average CPU < 40% → can downsize by 50%
- Average CPU < 20% → can downsize by 75%
- Average memory < 50% → can downsize RAM

### Solution

```
Tier Progression (smallest to largest):
  db-g1-small     → $25/month  (shared, 1.7 GB) — dev/test only
  db-custom-1-3840 → $50/month  (1 vCPU, 3.75 GB)
  db-custom-2-7680 → $100/month (2 vCPU, 7.5 GB)
  db-custom-2-8192 → $130/month (2 vCPU, 8 GB)
  db-custom-4-16384 → $260/month (4 vCPU, 16 GB)
  db-custom-8-32768 → $520/month (8 vCPU, 32 GB)

  HA doubles the cost.
```

### Implementation

```bash
# Downsize instance (causes brief restart)
gcloud sql instances patch INSTANCE \
  --tier=db-custom-4-16384 \
  --project=PROJECT

# Schedule during low-traffic window
```

### Expected Savings
30-60% per instance downsized.

### Risks
- Brief downtime during tier change (~1-2 minutes)
- May need to upsize if usage grows
- Monitor closely for 1-2 weeks after change

---

## Pattern 3: Eliminate Zombie Resources

### Problem
Resources left running after their purpose ends: test clusters, old instances, unused databases.

### Detection Checklist

```bash
# Cloud SQL: Check for zero connections
gcloud sql instances list --project=PROJECT
# Check metrics for each — 0 connections = likely unused

# GKE: Check for clusters with no workloads
gcloud container clusters list --project=PROJECT
# Check: kubectl get pods --all-namespaces

# Cloud Composer: Check if actually needed
gcloud composer environments list --locations=all --project=PROJECT
# Verify: Is your .env using USE_GCP_COMPOSER=true?

# Redis: Check memory usage
redis-cli -h HOST info memory
# If used_memory < 100MB on a 16GB instance → zombie or over-provisioned

# Compute Engine: Check for idle VMs
gcloud compute instances list --project=PROJECT
# Check CPU utilization — sustained <5% = likely unused

# Firestore: Check for unused databases
gcloud firestore databases list --project=PROJECT
# Datastore mode databases bill as Spanner!

# Static IPs: Check for unattached
gcloud compute addresses list --filter="status=RESERVED"
```

### Solution
Delete unused resources immediately. There's no partial savings — running is running.

### Expected Savings
$100-$1,000+/month per zombie resource.

### Risks
- Always verify the resource is truly unused before deleting
- Check with team members who may have created the resource
- Take backups of data if applicable before deletion

---

## Pattern 4: Redis Memory Right-Sizing

### Problem
Redis instances provisioned with much more memory than needed.

### Detection
```bash
# Check allocated size
gcloud redis instances describe INSTANCE --region=REGION --project=PROJECT \
  --format="value(memorySizeGb)"

# Check actual usage (if accessible)
redis-cli -h HOST info memory | grep used_memory_human
```

If `used_memory` < 25% of `memorySizeGb` → over-provisioned.

### Solution

```bash
# Resize Redis instance
gcloud redis instances update INSTANCE \
  --project=PROJECT --region=REGION \
  --size=NEW_SIZE_GB

# Note: STANDARD_HA minimum is 5 GB
# BASIC minimum is 1 GB
```

### Decision Tree

```
Is data ephemeral/cacheable?
  Yes → Consider BASIC tier (no HA needed)
  No → Keep STANDARD_HA

Current usage < 1 GB?
  Yes, BASIC → resize to 1 GB
  Yes, STANDARD_HA → minimum 5 GB

Current usage 1-4 GB?
  STANDARD_HA → set to 5 GB (minimum)
  BASIC → set to usage × 2 (headroom)
```

### Expected Savings
$30-70/GB/month reduced.

### Risks
- If data exceeds new size, eviction policies kick in
- Resize can cause brief unavailability (seconds to minutes)
- STANDARD_HA cannot go below 5 GB

---

## Pattern 5: Cloud Run Min-Instances Optimization

### Problem
Services with min-instances > 0 that have very low traffic, paying for idle capacity.

### Detection
```bash
# List services with min-instances
for svc in $(gcloud run services list --project=PROJECT --format="value(name)"); do
  min=$(gcloud run services describe $svc --region=REGION \
    --format="value(spec.template.metadata.annotations['autoscaling.knative.dev/minScale'])")
  echo "$svc: min=$min"
done
```

### Decision Matrix

```
Traffic Pattern          → Min Instances
─────────────────────────────────────────
Constant high traffic    → 2-4 (match baseline load)
Business hours only      → 1 (accept brief cold starts AM)
Sporadic (few per hour)  → 0 (cold starts acceptable)
Internal tools           → 0 (users can wait 2-5 seconds)
Customer-facing API      → 1-2 (minimize latency)
Webhooks/callbacks       → 1 (need fast response)
```

### Implementation
```bash
gcloud run services update SERVICE \
  --min-instances=0 \
  --region=REGION --project=PROJECT
```

### Expected Savings
$30-150/month per service set to min=0.

---

## Pattern 6: Committed Use Discounts (CUDs)

### Problem
Paying on-demand prices for stable, predictable workloads.

### When to Use CUDs

```
Good candidates:
  ✅ Cloud SQL instances running 24/7 (production databases)
  ✅ Stable Compute Engine VMs (always-on servers)
  ✅ GKE node pools with consistent base load
  ✅ Redis instances (always running)

Bad candidates:
  ❌ Cloud Run (auto-scales, usage varies)
  ❌ Cloud Functions (event-driven, unpredictable)
  ❌ Dev/test instances (may be deleted)
  ❌ Services you might migrate away from
```

### CUD Types

```
Resource-Based CUDs (Compute Engine/GKE):
  Commit to specific vCPU + memory amounts
  1-year: 37% discount
  3-year: 55% discount

Spend-Based CUDs (Cloud SQL, Redis, etc.):
  Commit to minimum spend per hour
  1-year: 25% discount
  3-year: 52% discount
```

### Implementation
Purchase via Cloud Console > Billing > Commitments.

### Expected Savings
25-55% on committed resources.

### Risks
- Locked in for 1-3 years
- If you reduce usage, still pay committed amount
- Non-refundable and non-transferable

---

## Pattern 7: Terraform-Managed Cost Control

### Problem
Infrastructure changes bypass cost review because they're made ad-hoc via gcloud or Console.

### Solution
Manage all infrastructure via Terraform with environment-specific tfvars:

```
terraform/environments/
  dev.tfvars          → Small instances, min=0
  prod.tfvars         → Standard production
  prod-lean.tfvars    → Cost-optimized production
  prod-workshop.tfvars → High-concurrency events
```

### Implementation

```hcl
# variables.tf
variable "studio_cpu" { default = "2" }
variable "studio_memory" { default = "4Gi" }
variable "studio_min_instances" { default = 2 }
variable "studio_max_instances" { default = 100 }

# prod-lean.tfvars
studio_cpu               = "2"
studio_memory            = "4Gi"
studio_min_instances     = 2
studio_max_instances     = 100
studio_concurrency       = 40
```

### Benefits
- Cost changes are code-reviewed (PR process)
- Easy to switch between profiles (lean vs workshop)
- Rollback is trivial (apply previous tfvars)
- Audit trail for all infrastructure changes

---

## Pattern 8: Network Cost Optimization

### Problem
Hidden networking costs from egress, load balancers, and unused IPs.

### Quick Wins

```bash
# Find unused static IPs ($7.20/month each)
gcloud compute addresses list --filter="status=RESERVED" --project=PROJECT

# Find orphaned forwarding rules
gcloud compute forwarding-rules list --project=PROJECT

# Check load balancer processing costs
gcloud compute backend-services list --project=PROJECT
```

### Solutions
- Release unused static IPs
- Delete orphaned load balancer components
- Use internal traffic where possible (no egress charges)
- Place resources in same region to avoid cross-region charges
- Use Cloud CDN for repeated external content delivery

---

## Pattern 9: Storage Lifecycle Policies

### Problem
Cloud Storage buckets accumulate data indefinitely, with all data at Standard (most expensive) tier.

### Solution

```bash
# Set lifecycle policy
cat > lifecycle.json <<EOF
{
  "rule": [
    {
      "action": {"type": "SetStorageClass", "storageClass": "NEARLINE"},
      "condition": {"age": 90}
    },
    {
      "action": {"type": "SetStorageClass", "storageClass": "COLDLINE"},
      "condition": {"age": 365}
    },
    {
      "action": {"type": "Delete"},
      "condition": {"age": 730}
    }
  ]
}
EOF

gsutil lifecycle set lifecycle.json gs://BUCKET
```

### Storage Class Pricing

```
Standard:   $0.020/GB/month (frequently accessed)
Nearline:   $0.010/GB/month (once a month access)
Coldline:   $0.004/GB/month (once a quarter access)
Archive:    $0.001/GB/month (once a year access)
```

### Expected Savings
50-90% on storage costs for data with proper lifecycle policies.

---

## Pattern 10: Artifact Registry Cleanup

### Problem
Old container images accumulate, consuming storage and billing.

### Solution

```bash
# List images sorted by creation time
gcloud artifacts docker images list REPO \
  --include-tags --sort-by=CREATE_TIME

# Delete images older than 90 days (keep last 10 per repo)
# Set up cleanup policy:
gcloud artifacts repositories set-cleanup-policies REPO \
  --project=PROJECT --location=REGION \
  --policy=cleanup-policy.json
```

### Expected Savings
$10-100/month depending on image count and size.

---

## Optimization Playbook: The 30-Day Plan

### Week 1: Discovery & Quick Wins
```
Day 1-2: Run /bill-analysis to understand current costs
Day 3-4: Run /resource-audit all to find waste
Day 5: Delete zombie resources (unused instances, test clusters)
         Set min-instances=0 on low-traffic services
         Release unused static IPs
         Expected savings: 10-20%
```

### Week 2: Right-Sizing
```
Day 6-8:  Right-size Cloud Run (horizontal scaling pattern)
Day 9-10: Right-size Cloud SQL (check CPU/memory utilization)
          Right-size Redis (check actual memory usage)
          Expected savings: 30-50% (cumulative)
```

### Week 3: Architecture & Commitments
```
Day 11-13: Evaluate CUDs for stable workloads
Day 14-15: Set up storage lifecycle policies
           Clean up Artifact Registry
           Configure billing budgets and alerts
           Expected savings: 40-60% (cumulative)
```

### Week 4: Verification & Process
```
Day 16-18: Run /cost-trend to verify savings
Day 19-20: Set up Terraform-managed cost profiles
           Document all changes
           Create monitoring dashboards
           Expected savings: 50-70% (sustained)
```

### Ongoing
```
Monthly: Run /resource-audit to catch new waste
Monthly: Review /cost-trend for anomalies
Quarterly: Evaluate CUD opportunities
Quarterly: Review architecture for cost efficiency
Annually: Renegotiate enterprise agreements
```

## Anti-Patterns (What NOT to Do)

### 1. Premature CUD Purchase
Don't buy CUDs for resources you might eliminate or significantly change.
Always optimize first, then commit.

### 2. Aggressive Downsizing Without Monitoring
Always check actual utilization before downsizing.
Monitor for 1-2 weeks after changes.
Have a quick rollback plan.

### 3. Ignoring Network Costs
Network egress is easy to overlook but can be significant.
Review cross-region traffic patterns.
Use internal IPs where possible.

### 4. Over-Optimizing Small Items
Don't spend 2 hours saving $5/month.
Focus on top 3-5 cost drivers (Pareto principle).
Minimum savings threshold: $50/month per action.

### 5. Optimizing Without Tracking
If you don't track, you don't know if it worked.
Always run /cost-trend after optimizations.
Set up billing budgets as guardrails.
