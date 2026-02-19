# Connectors

This plugin references external tools and data sources using placeholder names prefixed with `~~`. When you see these in commands or skills, they refer to the tool categories below.

## Required

### `~~gcloud CLI`

The Google Cloud CLI (`gcloud`) is the primary interface for querying live resource configurations, checking utilization, and implementing changes.

**Setup:**
```bash
gcloud auth login
gcloud config set project YOUR_PROJECT_ID
```

**Used by:** All commands and agents

**Alternatives:** Google Cloud Console (manual), Cloud Client Libraries (programmatic)

## Recommended

### `~~billing export`

GCP billing data exported as CSV or to BigQuery for detailed cost analysis.

**Setup:**
- **CSV**: Cloud Console > Billing > Reports > Download CSV
- **BigQuery**: Cloud Console > Billing > Billing Export > Enable BigQuery Export

**Used by:** `/bill-analysis`, `/project-costs`, `/cost-trend`, `cost-monitor` agent

### `~~cloud monitoring`

Google Cloud Monitoring API for resource utilization metrics (CPU, memory, connections).

**Setup:** Enabled by default in GCP projects. Requires `monitoring.viewer` IAM role.

**Used by:** `/resource-audit`, `/savings-finder`, `savings-advisor` agent

### `~~terraform`

Terraform CLI and state files for infrastructure-as-code cost management.

**Setup:**
```bash
cd terraform/gcp/cloud-run
terraform init
```

**Used by:** `/savings-finder` (generates tfvars changes), `cost-optimization-patterns` skill

## Optional

### `~~redis CLI`

Redis CLI for checking actual memory usage on Memorystore instances.

**Setup:** Requires network access to Redis instance (VPC or SSH tunnel).

**Used by:** `/resource-audit` (Redis audit section)

### `~~kubectl`

Kubernetes CLI for inspecting GKE cluster workloads and pod utilization.

**Setup:**
```bash
gcloud container clusters get-credentials CLUSTER --region REGION --project PROJECT
```

**Used by:** `/resource-audit` (GKE audit section)
