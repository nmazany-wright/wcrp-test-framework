# ADR-0002: Use Git-Based Content Management for the MVP

- Status: Proposed
- Date: 2026-08-09
- Decision owners: WCRP project team

## Related PRD requirement

The PRD requires that the MVP use a version-controlled, repository-managed content workflow and must avoid recurring CMS subscription fees by default. The PRD also requires that content remain portable, support staged review, and be compatible with the immutable release archive. The PRD does not specify which file formats, directory structure, or Git workflow conventions are used; those are the subject of this ADR.

## Context

The WCRP needs versioned narrative content, staged review, production approval, and permanently accessible historical releases. The PRD establishes that the MVP must avoid recurring CMS subscription fees and that editorial content must be stored in portable, version-controlled formats.

Editorial content includes narrative pages, glossary terms, references, images, tables, and configuration for approved interactive components.

## Decision

**Proposed:** Use repository-managed Markdown/MDX, YAML, and JSON files as the primary content architecture for the MVP. The repository's built-in version history, pull-request review, permissions, and workflow integration will serve as the editorial review mechanism.

The MVP will not require a separate CMS database or paid CMS subscription.

## Alternatives considered

- A hosted paid CMS with a Git sync connector
- A self-hosted FOSS database-backed CMS
- Direct Git editing without a dedicated editor layer (supported as a baseline regardless of this decision)

## Consequences

### Benefits

- No CMS subscription cost for the MVP; this satisfies the PRD constraint directly.
- Content changes are versioned, reviewable, and rollback-friendly.
- The content workflow aligns with staging previews and immutable releases (PRD requirements).
- Content remains portable rather than being locked into a SaaS provider.

### Tradeoffs

- Editors may need Git or repository-based editing training.
- Complex relational content and large media libraries may be less convenient than in a database-backed CMS.
- Content updates are published through commits and deployments rather than a live CMS API.

## Reconsideration triggers

Reassess this decision if the platform requires scheduled publishing, complex relational content, fine-grained non-Git workflows, a large editor population, a substantial media library, or frequent updates without build deployments.
