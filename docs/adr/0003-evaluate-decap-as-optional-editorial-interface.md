# ADR-0003: Evaluate Decap CMS as an Optional Editorial Interface

- Status: Proposed
- Date: 2026-08-09
- Decision owners: WCRP project team

## Related PRD requirement

The PRD permits an optional browser-based editorial interface to be introduced for nontechnical editors after usability, authentication, and operational requirements are validated. The PRD does not commit to any specific editorial product; this ADR evaluates Decap CMS as the candidate.

## Context

The proposed MVP content architecture stores content in the repository (ADR-0002). Some editors may prefer a browser-based authoring interface over direct Markdown editing or the native Git web editor.

Decap CMS is a Git-based editor that can create commits or pull requests while keeping content in the repository. It does not replace the core content storage, review, or publishing workflow.

## Decision

**Proposed:** Treat Decap CMS as an open dependency and candidate optional editorial interface for the Git-based MVP. Do not make Decap a required MVP deliverable until the project team confirms editor needs, authentication requirements, and operational fit.

The native Git web editor and pull-request workflow remain a supported baseline, independent of this decision.

## Alternatives considered

- Require Decap CMS for all editors in the MVP
- Use only the native Git web editor and pull requests (no additional editor layer)
- Select another Git-based browser editor
- Adopt a self-hosted or hosted database-backed CMS as the editor interface

## Consequences

### Benefits

- The project can validate editor needs before committing to an additional operational component.
- Content remains portable and Git-based regardless of which editor is eventually adopted.
- An editorial interface can be added without changing the public content-rendering application.

### Tradeoffs

- The MVP editorial experience is not fully specified until this decision is accepted or rejected.
- Decap authentication, media handling, and editorial-workflow configuration require further evaluation before a commitment can be made.

## Open dependencies

- Identify the primary content editors and their comfort with Git-based workflows.
- Confirm authentication and authorization requirements for a browser-based editor.
- Confirm whether a visual editor interface is essential for the MVP or can follow in a later phase.
