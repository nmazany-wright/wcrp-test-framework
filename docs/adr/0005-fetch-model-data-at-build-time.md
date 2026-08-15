# ADR-0005: Fetch Model Data at Build Time

- Status: Proposed
- Date: 2026-08-09
- Decision owners: WCRP project team

## Related PRD requirement

The PRD requires that pg_featureserv model data be fetched and validated during the build, and that no runtime API polling is required in the MVP. It also requires that each approved release represent a stable, internally consistent data snapshot. This ADR describes the proposed technical mechanism for fulfilling those requirements. The snapshot-retention design remains open.

## Context

WCRP model-data updates occur a small number of times per year and require QA/QC plus project-lead approval before public release. The PRD requires that each release show a reviewed, internally consistent data snapshot rather than live-changing model outputs.

## Decision

**Proposed:** Fetch and validate pg_featureserv model data during the application build for staging and production deployments. Build artifacts will include the approved data snapshot for dashboards, maps, charts, and generated reporting. The MVP will not use runtime API polling for model data.

The exact snapshot-retention mechanism (e.g., whether the fetched data is committed to the repository, stored as a build artifact, or another approach) remains an open decision.

## Alternatives considered

- Fetch model data dynamically at runtime on each page request
- Poll the API from the browser client
- Commit all model-data API responses into the repository before each build as the primary source
- Use a separate data warehouse or cache as the primary site data source

## Consequences

### Benefits

- A deployed release represents a stable, reviewable model-data snapshot (satisfying the PRD requirement).
- Public users are insulated from transient API outages and unreviewed source-data changes.
- Client-side interactions operate on deployed build-time data without repeated API calls.

### Tradeoffs

- New model data is not visible until a new build and approved release are completed.
- Builds require robust failure handling and data validation.
- The archival method for the exact approved input data remains to be designed.

## Open dependencies

- Define build failure behavior versus fallback to last approved data.
- Define snapshot retention, audit, and reproduction requirements (see also ADR-0008).
