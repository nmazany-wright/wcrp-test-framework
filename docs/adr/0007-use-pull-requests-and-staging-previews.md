# ADR-0007: Use Pull Requests and Staging Previews for Editorial Review

- Status: Proposed
- Date: 2026-08-09
- Decision owners: WCRP project team

## Related PRD requirement

The PRD requires that content and data changes be reviewable in a preview/staging environment before production publication, that production releases require explicit approval, and that the review workflow be auditable. This ADR proposes the technical mechanism for fulfilling those requirements. The specific hosting platform, automation tooling, and CI/CD system remain open decisions.

## Context

WCRP releases require review of narrative accuracy, model data, maps, visualizations, accessibility, and stakeholder-facing presentation before publication. The platform also needs an auditable approval process for content and configuration changes.

## Decision

**Proposed:** Use pull requests as the primary review mechanism for editorial content, configuration, and application changes. Pull requests should trigger automated builds that produce staging or preview deployments for review before changes are merged or promoted to production.

The hosting platform, preview-deployment automation tooling, and CI/CD platform remain open dependencies.

## Alternatives considered

- Publish content directly from an editorial interface without a pull-request review step
- Require local review only before manual deployment
- Use a separate editorial approval system outside the repository
- Automatically publish every merge to production without a staging review step

## Consequences

### Benefits

- Review comments, approvals, and changes are recorded with the release inputs, satisfying the audit requirement.
- Reviewers can assess the rendered application rather than only source files.
- The workflow supports both developer and nondeveloper editorial contributions.

### Tradeoffs

- Contributors and reviewers need access to the repository and preview environments.
- The review process may add time to urgent updates.
- Branch-protection rules, required approvers, and production promotion rules need to be defined.

## Open dependencies

- Define required approvers and final production-release authority.
- Select the hosting platform and preview-deployment automation tooling (CI/CD system).
- Define whether production deployment is automatic after merge or separately approved.
