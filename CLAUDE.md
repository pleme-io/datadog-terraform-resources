# datadog-terraform-resources -- TOML resource specs for Datadog

Declarative TOML specifications for 10 Datadog Terraform resources. Same pattern
as `akeyless-terraform-resources`. Consumed by iac-forge and pangea-forge to
generate code for all IaC platforms.

## Structure

```
provider.toml              # Provider config (api_key, app_key, api_url)
resources/
  monitors/
    monitor.toml           # datadog_monitor
  dashboards/
    dashboard.toml         # datadog_dashboard
    dashboard_json.toml    # datadog_dashboard_json
  slos/
    service_level_objective.toml  # datadog_service_level_objective
  synthetics/
    synthetics_test.toml   # datadog_synthetics_test
  logs/
    logs_index.toml        # datadog_logs_index
    logs_metric.toml       # datadog_logs_metric
    logs_pipeline.toml     # datadog_logs_pipeline
  apm/
    apm_retention_filter.toml  # datadog_apm_retention_filter
  integration/
    integration_aws.toml   # datadog_integration_aws
```

## Usage

```bash
# Generate Terraform provider code
iac-forge-cli generate --specs . --backend terraform

# Generate Pangea Ruby resources
iac-forge-cli generate --specs . --backend pangea

# Generate all backends
iac-forge-cli generate --specs . --backend all
```

## TOML Spec Format

Each `.toml` file defines one resource with `[resource]` metadata,
`[resource.attributes.*]` for fields (type, required, sensitive, computed),
and optional `[resource.nested.*]` for block types. Same schema as
`akeyless-terraform-resources`.

## Provider Auth

```toml
[provider.auth]
api_key = { type = "String", required = true, sensitive = true, env = "DD_API_KEY" }
app_key = { type = "String", required = true, sensitive = true, env = "DD_APP_KEY" }
api_url = { type = "String", required = false, default = "https://api.datadoghq.com" }
```

## Resources (10)

monitors, dashboards (2), SLOs, synthetics, logs (3), APM retention, AWS integration.
