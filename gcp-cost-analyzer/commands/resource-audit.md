---
description: Audit all GCP resources across projects to find waste — idle instances, over-provisioned resources, and orphaned assets
argument-hint: "[service or 'all']"
---

# Resource Audit

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](../CONNECTORS.md).

Comprehensive audit of all GCP resources to identify waste, over-provisioning, idle resources, and orphaned assets.

## Usage

```
/resource-audit [service or 'all']
```

### Arguments

- `service` — Optional. Focus on a specific service:
  - `cloud-run` — Audit Cloud Run services
  - `cloud-sql` — Audit Cloud SQL instances
  - `gke` — Audit GKE clusters
  - `redis` — Audit Redis Memorystore
  - `compute` — Audit Compute Engine
  - `storage` — Audit Cloud Storage
  - `networking` — Audit networking resources
  - `all` — Audit everything (default)

## Workflow

### 1. Discover All Projects

```bash
# List all accessible projects
gcloud projects list --format="table(projectId,name,lifecycleState)"

# For each active project, scan resources
```

### 2. Cloud Run Audit

For each project, check Cloud Run services:

```bash
# List services with details
gcloud run services list --project=PROJECT \
  --format="table(name,region,status.url)"

# For each service, get detailed config
gcloud run services describe SERVICE \
  --project=PROJECT --region=REGION \
  --format="yaml(spec.template.spec.containers[0].resources,spec.template.metadata.annotations)"
```

**Checks:**

```
CLOUD RUN AUDIT
═══════════════════════════════════════════════════════════

✅ HEALTHY:
  agentman-studio-api (us-west2)
    CPU: 2, Memory: 4Gi, Min: 2, Max: 100
    Status: Receiving traffic

⚠️ OVER-PROVISIONED:
  some-service (us-west2)
    CPU: 4, Memory: 8Gi — Usage: avg 0.5 CPU, 1.2 GB RAM
    Recommendation: Reduce to 1 CPU / 2Gi
    Savings: ~$XXX/month

🔴 IDLE / ZERO TRAFFIC:
  old-test-service (us-west2)
    Last request: 45 days ago
    Min instances: 1 (costing money for nothing)
    Recommendation: Set min=0 or delete if unused
    Savings: ~$XX/month

📋 MIN INSTANCE REVIEW:
  Services with min > 0 that may not need it:
  - test-service (min=1, avg 2 requests/hour)
  - staging-api (min=1, no traffic in 7 days)
```

### 3. Cloud SQL Audit

```bash
# List instances
gcloud sql instances list --project=PROJECT

# Get instance details
gcloud sql instances describe INSTANCE --project=PROJECT

# Check recent connections (requires monitoring)
gcloud monitoring read \
  "metric.type=\"cloudsql.googleapis.com/database/network/connections\"" \
  --project=PROJECT
```

**Checks:**

```
CLOUD SQL AUDIT
═══════════════════════════════════════════════════════════

✅ RIGHT-SIZED:
  coa-studio-prod (db-custom-4-16384)
    CPU Usage: 35% avg, 60% peak
    Memory: 55% utilized
    Storage: 25 GB / 100 GB (25%)
    Connections: 45 avg, 120 peak

⚠️ OVER-PROVISIONED:
  [instance-name] (db-custom-4-16384)
    CPU Usage: 8% avg, 15% peak
    Recommendation: Downsize to db-custom-2-8192
    Savings: ~$XXX/month

🔴 POTENTIALLY UNUSED:
  [instance-name] (db-custom-2-8192)
    Active connections: 0 (last 7 days)
    Recommendation: Verify and delete if unused
    Savings: ~$XXX/month

📋 OPTIMIZATION OPPORTUNITIES:
  - Enable automatic storage increase (avoid over-provisioning)
  - Consider committed use discounts for stable instances
  - Check if HA is needed for all instances
  - Review backup retention policies
```

### 4. GKE Audit

```bash
# List clusters
gcloud container clusters list --project=PROJECT

# Get node pool details
gcloud container node-pools list --cluster=CLUSTER \
  --region=REGION --project=PROJECT

# Check node utilization
kubectl top nodes (requires cluster credentials)
```

**Checks:**

```
GKE AUDIT
═══════════════════════════════════════════════════════════

✅ ACTIVE:
  airflow-cluster-dec (us-west2)
    Nodes: 2x e2-standard-4
    Pods: 4 running (airflow namespace)
    CPU request: 45%, Memory request: 38%

🔴 UNUSED:
  [cluster-name] (us-west2)
    No active workloads
    Log bucket: DELETED
    Recommendation: Delete cluster
    Savings: ~$310/month

📋 OPTIMIZATION:
  - Consider Autopilot for variable workloads
  - Enable cluster autoscaler (min=1, max=3)
  - Right-size node machine types based on actual usage
  - Review if preemptible/spot VMs are acceptable
```

### 5. Redis Audit

```bash
gcloud redis instances list --project=PROJECT --region=REGION \
  --format="table(name,tier,memorySizeGb,host,port)"

# Check memory usage via redis-cli if accessible
redis-cli -h HOST info memory
```

**Checks:**

```
REDIS AUDIT
═══════════════════════════════════════════════════════════

⚠️ OVER-PROVISIONED:
  prod-agentlens-insights-redis (STANDARD_HA, 5 GB)
    Used memory: 1.2 GB (24% utilization)
    Note: 5 GB is minimum for STANDARD_HA
    If HA not needed: Switch to BASIC tier (save ~50%)

📋 REVIEW:
  - Check if STANDARD_HA is needed (data importance)
  - Review key expiration policies
  - Consider Redis Cluster for >10 GB workloads
```

### 6. Networking Audit

```bash
# Reserved IPs
gcloud compute addresses list --project=PROJECT

# Forwarding rules
gcloud compute forwarding-rules list --project=PROJECT

# Load balancers
gcloud compute url-maps list --project=PROJECT
gcloud compute backend-services list --project=PROJECT
```

**Checks:**

```
NETWORKING AUDIT
═══════════════════════════════════════════════════════════

🔴 UNUSED RESERVED IPs:
  34.XX.XX.XX (RESERVED, not in use)
    Charged: $7.20/month for unused static IP
    Recommendation: Release or attach to a resource

⚠️ ORPHANED LOAD BALANCER COMPONENTS:
  - Backend service with no backends
  - URL map pointing to deleted service
  Recommendation: Clean up orphaned resources

📋 REVIEW:
  - Check for unused forwarding rules
  - Review NAT gateway configuration
  - Audit VPC peering connections
```

### 7. Storage Audit

```bash
# List buckets and sizes
gsutil ls -L -b gs://BUCKET | grep "Storage size"

# Check lifecycle policies
gsutil lifecycle get gs://BUCKET
```

**Checks:**

```
STORAGE AUDIT
═══════════════════════════════════════════════════════════

⚠️ NO LIFECYCLE POLICY:
  gs://airflow-dags-bucket-dec (15 GB)
    No lifecycle policy set
    Recommendation: Add policy to delete old DAG versions

🔴 ORPHANED BUCKETS:
  gs://airflow-logs-bucket-test-two
    Status: DELETED (bucket no longer exists)
    Associated with deleted cluster

📋 REVIEW:
  - Set lifecycle policies on all buckets
  - Move cold data to Nearline/Coldline storage
  - Delete temporary/test buckets
  - Review Artifact Registry image retention
```

### 8. Other Services Audit

```
ADDITIONAL SERVICES AUDIT
═══════════════════════════════════════════════════════════

Cloud Composer:
  ✅ None running (previously deleted for savings)

Firestore:
  ✅ No unused databases (graphrag previously deleted)

Cloud Functions:
  Review: X functions found — check invocation counts
  gcloud functions list --project=PROJECT

Pub/Sub:
  Review: Check for unused topics/subscriptions

Cloud Scheduler:
  Review: Check for disabled or unused jobs
```

### 9. Summary Report

```
═══════════════════════════════════════════════════════════
RESOURCE AUDIT SUMMARY
Date: [Date]
Projects Scanned: X
═══════════════════════════════════════════════════════════

FINDINGS:
  🔴 Critical (delete/stop immediately):     X items
  ⚠️  Warning (right-size/optimize):          X items
  ✅ Healthy:                                 X items

TOTAL POTENTIAL SAVINGS: $X,XXX/month ($XX,XXX/year)

TOP ACTIONS:
  1. [Action] — $XXX/month savings
  2. [Action] — $XXX/month savings
  3. [Action] — $XXX/month savings

WASTE SCORE: X/10 (lower is better)
  1-3: Lean and efficient
  4-6: Room for improvement
  7-10: Significant waste detected
═══════════════════════════════════════════════════════════
```

## Scheduling

Run this audit:
- **Monthly**: For ongoing cost management
- **After major changes**: New deployments, migrations
- **Before budget reviews**: Identify savings before planning
- **Quarterly**: Comprehensive deep audit

## Related Commands

- `/bill-analysis` — Understand costs before auditing resources
- `/savings-finder` — Get specific savings with implementation steps
- `/project-costs` — Focus on a specific project
- `/cost-trend` — Track improvement over time
