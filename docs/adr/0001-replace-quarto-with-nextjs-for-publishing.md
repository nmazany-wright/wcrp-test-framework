# ADR-0001: Replace Quarto with Next.js for the Publishing Workflow

- Status: Proposed
- Date: 2026-08-09
- Decision owners: WCRP project team

## Related PRD requirement

The PRD requires a responsive public web application that replaces the current Quarto/R-notebook publishing workflow and supports interactive maps, dashboards, filtering, accessibility, mobile use, and staged review. The PRD does not specify which application framework is used; that is the subject of this ADR.

## Context

The current WCRP publication workflow uses Quarto and R notebooks to render a static document. The modernized platform requires responsive web pages, interactive maps and dashboards, reusable watershed configuration, staged deployments, and durable version history.

The project team has agreed to fully move away from Quarto and R notebooks in this repository's publishing workflow. This decision does not prescribe changes to analytical systems or model-processing workflows outside this repository.

## Decision

**Proposed:** Replace the repository's Quarto/R-notebook publishing workflow with a Next.js application using React and TypeScript. The Next.js application will render repository-managed editorial content, approved generated data, and interactive web components.

## Alternatives considered

- Retain Quarto and extend it with custom HTML, JavaScript, and embedded widgets
- Retain Quarto for narrative pages while adding a separate interactive application
- Use another modern static-site generator or application framework
- Build a fully client-rendered single-page application with a different framework

## Consequences

### Benefits

- A unified application supports static pages, interactive maps, dashboards, and reusable components.
- The publishing workflow can use pull-request previews, staged deployment, and versioned releases.
- Content and component configuration remain portable and version controlled.
- The platform can be reused for additional watersheds.

### Tradeoffs

- The team must migrate existing Quarto content, assets, routes, and publication conventions.
- Contributors need knowledge of the selected framework and TypeScript.
- Existing Quarto-specific rendering features must be replaced or intentionally retired.

## Open dependencies

- Hosting platform selection remains open.
- The detailed migration plan, content migration strategy, and redirect approach remain to be defined.
