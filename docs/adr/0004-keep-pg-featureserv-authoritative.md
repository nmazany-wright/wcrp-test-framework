# ADR-0004: Keep pg_featureserv Authoritative for Model-Backed Data

- Status: Proposed
- Date: 2026-08-09
- Decision owners: WCRP project team

## Related PRD requirement

The PRD explicitly names pg_featureserv as the authoritative external dependency for model-backed data. It requires that editorial content must not become a second source of truth for scientific or model-derived data. This ADR records how that PRD constraint is implemented in the application and build architecture.

## Context

The WCRP displays model-backed information including barrier locations, habitat connectivity metrics, rankings, and related reporting outputs. The PRD establishes that editorial content may reference, configure presentation of, and contextualize model data, but must not be the source of truth for model outputs.

## Decision

**Proposed:** Treat pg_featureserv as the authoritative source for all model-backed data consumed by the WCRP platform. The build pipeline fetches and validates model data from pg_featureserv; the application renders it. Repository-managed editorial content may reference or configure the display of model data, but must not define or override model output values.

## Alternatives considered

- Maintain a manually curated copy of model outputs in repository content
- Use repository data files as the primary source of truth for displayed metrics
- Allow editors to modify displayed model values directly in content configuration

## Consequences

### Benefits

- Scientific and model-derived values have a clear authoritative source, satisfying the PRD constraint.
- Editors can update narrative content without modifying model outputs.
- The application can validate data consistently during builds before rendering maps, charts, dashboards, and tables.

### Tradeoffs

- The platform depends on documented pg_featureserv API contracts and availability during approved builds.
- API changes require monitoring, validation, and coordinated updates.

## Open dependencies

- Define API contracts, build-time validation rules, and behavior when the API is unavailable during a build.
- Define the approach for retaining or reproducing the approved data snapshot used for each release (see ADR-0005 and ADR-0008).
