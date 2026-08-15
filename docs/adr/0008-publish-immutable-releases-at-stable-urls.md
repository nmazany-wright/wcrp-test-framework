# ADR-0008: Publish Immutable WCRP Releases at Stable Public URLs

- Status: Proposed
- Date: 2026-08-09
- Decision owners: WCRP project team

## Related PRD requirement

The PRD requires that every approved WCRP production release remain permanently publicly accessible at a stable URL. This is a hard product constraint: stakeholders and partners must be able to cite and return to historical releases. This ADR proposes the technical mechanism for fulfilling that constraint. The exact URL scheme, hosting strategy, and archive implementation remain open decisions.

## Context

Stakeholders need to access previous WCRP versions to understand changes in model outputs, narrative reporting, and restoration progress over time. The PRD establishes that historical releases must remain permanently publicly accessible and distinguishable from the current version.

## Decision

**Proposed:** Publish each approved WCRP production release as an immutable historical version that remains permanently publicly accessible at a stable URL. Associate releases with version metadata so the application can identify the current release and navigate to prior versions.

The detailed archive-hosting and URL implementation remains open but must ensure stable public access to every published version.

## Alternatives considered

- Replace the current site in place without retaining publicly accessible archives
- Retain only source-code tags without deployed public versions for historical releases
- Provide temporary preview deployments for old versions on request (not permanently public)
- Archive releases only as PDFs or downloadable artifacts without a deployed web version

## Consequences

### Benefits

- Stakeholders can cite and revisit the exact public version used at a point in time, satisfying the PRD constraint.
- Releases have a clear audit trail for content, configuration, and model-data presentation.
- The current site can provide a version selector linking to all historical releases.

### Tradeoffs

- The platform must retain deployment artifacts, routing, and hosting capacity for historical versions over time.
- Version naming conventions, metadata generation, and release validation must be standardized.
- The long-term archive hosting and routing implementation requires operational ownership.

## Open dependencies

- Define the stable URL scheme (e.g., subpaths, subdomains, or version-based routing).
- Define the hosting strategy for archived deployments.
- Define release-version naming conventions.
- Define the mechanism for retaining or reproducing the approved build-time data snapshot for each archived version (see ADR-0005).
