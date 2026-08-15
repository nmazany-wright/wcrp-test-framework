# ADR-0006: Use Structured Component Blocks for Editorial Content

- Status: Proposed
- Date: 2026-08-09
- Decision owners: WCRP project team

## Related PRD requirement

The PRD requires that editorial content may configure approved interactive components but must not execute arbitrary code or define component behavior. Editors control what a page says and which approved components are placed; the application controls how those components render and behave. This ADR proposes the technical mechanism for enforcing that boundary.

## Context

WCRP pages combine editorial narrative with data-backed dashboards, interactive barrier maps, and charts. Nontechnical editors need to control component placement and approved display options without writing application code or executable content.

## Decision

**Proposed:** Use structured component blocks in content front matter or companion YAML/JSON configuration to identify approved components and their supported options. The application will map component identifiers (such as `connectivity-dashboard`, `barrier-map`, and `habitat-accessibility-curve`) to developer-maintained implementations.

Developer-authored pages may use richer content formats (such as MDX with approved components) where appropriate, but arbitrary JSX, JavaScript, or component execution is not part of the nontechnical editor-facing workflow.

Build-time validation must reject unknown component types or invalid option schemas before deployment.

## Alternatives considered

- Allow unrestricted MDX/JSX in all editorial content
- Hard-code component placement in page templates (no editor configuration)
- Build all pages in a visual page-builder CMS
- Allow free-form HTML and JavaScript embeds

## Consequences

### Benefits

- Editors control which approved components appear and their configuration, satisfying the PRD requirement.
- Application developers retain control over component behavior, validation, accessibility, and security.
- Component configuration can be validated automatically during the build before deployment.

### Tradeoffs

- The team must define, document, and maintain approved component schemas.
- Editors have less freedom than with unrestricted MDX or a full visual page builder.

## Example

```yaml
components:
  - type: connectivity-dashboard
    status_types:
      - spawning_all
      - rearing_all
  - type: barrier-map
    data_source: barrier_extent
    default_filters:
      priority:
        - high
      structure_status:
        - priority
    show_top_labels: 25
```

## Open dependencies

- Define the approved component schema and validation rules.
- Define documentation and guidance for nontechnical editors.
