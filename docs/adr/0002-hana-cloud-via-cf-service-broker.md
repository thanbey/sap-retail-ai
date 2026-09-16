# ADR 0002: Provision HANA Cloud through the CF service broker, not HANA Cloud Central

Date: 2026-09-16
Status: Accepted

## Context

The HANA Cloud Central subscription (app `hana-cloud-tools`, plan `tools`) on
trial subaccount `4d610be9-…` (us10) fails with SUBSCRIBE_FAILED. The btp CLI
shows the cause: SAP's tenant-mapping callback for cf-us10 returns HTTP 500.
Business Application Studio fails the same way. This is SAP-side, not our
configuration. Day 2 needs a HANA database, not the console.

## Options

1. Wait for SAP to fix the region. Unknown duration.
2. Create the database through the Cloud Foundry service broker
   (`cf create-service hana-cloud hana-free ...`), which does not depend on
   the console subscription.
3. Run Day 2 on the DuckDB fallback and defer HANA.

## Decision

Option 2. Instance `sap-retail-hana`, plan `hana-free`, 16 GB (free-tier cap),
service key `dev-key`. Connection values in `.env`. Retry the console
subscription at most once a day; nothing in the work plan needs it.

## Consequences

- No browser SQL console. Use `hdbcli` from Python, or the HANA Database
  Explorer once the subscription succeeds.
- Trial instances stop nightly. Start before work:
  `cf update-service sap-retail-hana -c '{"data":{"serviceStopped":false}}'`.
  Add `make hana-start` for this.
- cf CLI must be 8.x; 6.x fails against BTP with "Version string empty".
- Interview talking point: the console and the database are separate BTP
  artefacts (SaaS subscription vs service instance); the broker path is what
  CI/CD would use anyway.
