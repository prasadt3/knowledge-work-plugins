---
description: Find specific cost savings opportunities across GCP services with actionable recommendations and gcloud commands
argument-hint: "[service]"
---

# Savings Finder

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](../CONNECTORS.md).

Identify specific, actionable cost savings across your GCP infrastructure. Provides exact gcloud commands and Terraform changes to implement each saving.

## Usage

```
/savings-finder [service]
```

### Arguments

- `service` — Optional. Focus on a specific service:
  - `cloud-run` — Cloud Run services
  - `cloud-sql` — Cloud SQL instances
  - `gke` — GKE clusters
  - `redis` — Cloud Memorystore
  - `compute` — Compute Engine VMs
  - `storage` — Cloud Storage buckets
  - `all` — Analyze everything (default)

## Workflow

### 1. Inventory All Resources

Scan all projects for running resources:

```bash
# For each project:
gcloud run services list --project=PROJECT --format="table(name,region)"
gcloud sql instances list --project=PROJECT --format="table(name,tier,region)"
gcloud compute instances list --project=PROJECT
gcloud redis instances list --project=PROJECT --region=REGION
gcloud container clusters list --project=PROJECT
gcloud composer environments list --project=PROJECT --locations=all
gcloud functions list --project=PROJECT
gcloud storage ls --project=PROJECT
```

### 2. Analyze Each Service Category

#### Cloud Run Savings

```
CLOUD RUN SAVINGS
═══════════════════════════════════════════════════════════

1. RIGHT-SIZE INSTANCES
   ─────────────────────────────────────────────────────
   Service: agentman-studio-api (us-west2)
   Current: 8 vCPU / 16 GB RAM, min=4, max=50
   Recommended: 2 vCPU / 4 GB RAM, min=2, max=100
   Rationale: Horizontal scaling with smaller instances is cheaper
              and provides better fault tolerance
   Savings: ~$4,000/month

   Implementation:
   gcloud run services update agentman-studio-api \
     --project=PROJECT \
     --region=us-west2 \
     --cpu=2 --memory=4Gi \
     --min-instances=2 --max-instances=100 \
     --concurrency=40

   Or via Terraform (prod-lean.tfvars):
   studio_cpu = "2"
   studio_memory = "4Gi"
   studio_min_instances = 2
   studio_max_instances = 100

2. REDUCE MIN INSTANCES
   ─────────────────────────────────────────────────────
   Service: [low-traffic-service] (us-west2)
   Current: min-instances=2
   Recommended: min-instances=0 (if cold starts acceptable)
   Savings: ~$XX/month per service

   Implementation:
   gcloud run services update SERVICE \
     --min-instances=0 --region=us-west2

3. USE CPU ALLOCATION: ONLY DURING REQUESTS
   ─────────────────────────────────────────────────────
   For services that are idle most of the time:
   Current: CPU always allocated
   Recommended: CPU only during request processing
   Savings: Up to 50% on CPU costs for low-traffic services

   gcloud run services update SERVICE \
     --no-cpu-always-allocated
```

#### Cloud SQL Savings

```
CLOUD SQL SAVINGS
═══════════════════════════════════════════════════════════

1. RIGHT-SIZE INSTANCES
   ─────────────────────────────────────────────────────
   Instance: coa-studio-prod
   Current: db-custom-8-32768 (8 vCPU / 32 GB)
   Recommended: db-custom-4-16384 (4 vCPU / 16 GB)
   Check CPU: Should be <60% average to downsize safely
   Savings: ~$400/month

   gcloud sql instances patch coa-studio-prod \
     --project=PROJECT \
     --tier=db-custom-4-16384

2. COMMITTED USE DISCOUNTS (CUDs)
   ─────────────────────────────────────────────────────
   Instance: coa-studio-prod (runs 24/7)
   1-year commitment: 30% discount
   3-year commitment: 52% discount
   Savings (1-year): ~$XXX/month

   Purchase via Cloud Console > Billing > Commitments

3. DELETE UNUSED INSTANCES
   ─────────────────────────────────────────────────────
   Instance: [unused-instance]
   Last connection: 30+ days ago
   Savings: Full instance cost

   gcloud sql instances delete INSTANCE --project=PROJECT

4. REDUCE STORAGE OVER-PROVISIONING
   ─────────────────────────────────────────────────────
   Instance: coa-studio-prod
   Allocated: 100 GB, Used: 25 GB
   Recommendation: Enable autoresize, reduce initial size
   Savings: ~$XX/month
```

#### GKE Savings

```
GKE SAVINGS
═══════════════════════════════════════════════════════════

1. DELETE UNUSED CLUSTERS
   ─────────────────────────────────────────────────────
   Cluster: airflow-cluster-test
   Status: No active workloads / log bucket deleted
   Savings: ~$310/month (2 nodes + management fee)

   gcloud container clusters delete airflow-cluster-test \
     --region=us-west2 --project=PROJECT

2. USE AUTOPILOT MODE
   ─────────────────────────────────────────────────────
   Current: Standard mode (pay for nodes, even if idle)
   Recommended: Autopilot (pay only for pod resources)
   Savings: 20-40% for bursty workloads

3. RIGHT-SIZE NODE POOLS
   ─────────────────────────────────────────────────────
   Cluster: airflow-cluster-dec
   Current: 2x e2-standard-4 (4 vCPU / 16 GB each)
   Usage: Scheduler + webserver only need ~2 vCPU total
   Recommended: 2x e2-standard-2 (2 vCPU / 8 GB each)
   Savings: ~$100/month

4. ENABLE CLUSTER AUTOSCALER
   ─────────────────────────────────────────────────────
   Set min=1, max=3 nodes instead of fixed 2
   Scales down during off-peak hours
```

#### Redis Savings

```
REDIS SAVINGS
═══════════════════════════════════════════════════════════

1. RIGHT-SIZE MEMORY
   ─────────────────────────────────────────────────────
   Instance: prod-agentlens-insights-redis
   Current: 16 GB STANDARD_HA
   Usage: <2 GB actual memory used
   Recommended: 5 GB STANDARD_HA (minimum for HA with replicas)
   Savings: ~$400/month

   gcloud redis instances update INSTANCE \
     --project=PROJECT --region=REGION --size=5

2. SWITCH FROM HA TO BASIC (If HA not needed)
   ─────────────────────────────────────────────────────
   If data is ephemeral/cacheable and loss is acceptable:
   Current: STANDARD_HA (includes replicas)
   Recommended: BASIC (single node)
   Savings: ~50% of Redis cost
   Risk: Data loss on instance failure

3. USE REDIS CLUSTER MODE (For large workloads)
   ─────────────────────────────────────────────────────
   If >10 GB needed: Redis Cluster distributes across shards
   More cost-effective than single large instance
```

#### Other Services

```
OTHER SAVINGS OPPORTUNITIES
═══════════════════════════════════════════════════════════

CLOUD COMPOSER:
  If using self-managed Airflow on GKE, delete Composer
  Savings: ~$450/month
  gcloud composer environments delete ENV --location=REGION

FIRESTORE (DATASTORE MODE):
  Check for unused databases — Datastore mode bills as Spanner!
  gcloud firestore databases list --project=PROJECT
  Savings: Up to $1,000+/month for unused databases

SECURITY COMMAND CENTER:
  If not actively used, disable Premium tier
  Savings: ~$527/month

ARTIFACT REGISTRY:
  Clean up old container images:
  gcloud artifacts docker images list REPO --include-tags \
    --sort-by=CREATE_TIME --limit=100
  Set up lifecycle policies to auto-delete old images

CLOUD FUNCTIONS:
  Set min-instances=0 for infrequently used functions
  Review invocation counts — delete unused functions

NETWORKING:
  Review load balancer configurations
  Delete unused forwarding rules and IP addresses
  gcloud compute addresses list --filter="status=RESERVED"
```

### 3. Summary Report

```
═══════════════════════════════════════════════════════════
SAVINGS FINDER REPORT
Date: [Date]
Projects Analyzed: X
═══════════════════════════════════════════════════════════

💰 TOTAL POTENTIAL SAVINGS: $X,XXX/month ($XX,XXX/year)

BY PRIORITY:

🔴 IMMEDIATE (implement this week):
  1. [Action] — $XXX/month
  2. [Action] — $XXX/month
  Subtotal: $X,XXX/month

🟡 SHORT-TERM (implement this month):
  3. [Action] — $XXX/month
  4. [Action] — $XXX/month
  Subtotal: $XXX/month

🟢 STRATEGIC (plan for next quarter):
  5. [Action] — $XXX/month
  6. [Action] — $XXX/month
  Subtotal: $XXX/month

═══════════════════════════════════════════════════════════
```

## Notes

- Always verify resource usage before downsizing (check CPU/memory metrics)
- Test changes in dev/staging before applying to production
- Some changes (like CUDs) require commitments — ensure workload is stable
- Deleting resources is irreversible — double-check before executing

## Related Commands

- `/bill-analysis` — Understand current costs before optimizing
- `/project-costs` — Deep dive into a specific project
- `/resource-audit` — Audit all resources for waste
- `/cost-trend` — Track savings over time after optimization
