# PRD Review Questions

This document is the traceability checklist used to review and refine the Product Requirements Document for the Horsefly WCRP platform modernization.

> **Note on scope:** Questions about specific frameworks, libraries, vendors, hosting platforms, CI/CD tooling, and build mechanisms are architecture-level decisions recorded in [`docs/adr/`](./adr/). This document focuses on product-level requirements and on the decisions that must be recorded before PRD or ADR updates proceed.
>
> **Gate condition:** All items in Section 8 must be recorded as **Answered** or formally **Deferred** before substantive edits to `docs/PRD.md` or any file in `docs/adr/` begin. Deferred items must include a rationale and a revisit date.
>
> **Checklist statuses:** `Open` · `Answered` · `Deferred` · `N/A`

---

## 1. Content ownership and editing

### Q1 · Identify the actual content editors

**Question:** Who will actually edit content: developers, biologists, project managers, communications staff, or external partners?

| Field | Value |
|---|---|
| PRD § | §2.2 Repository Content and Deployment Workflow; §3.1 Repository Content Workflow |
| ADR # | ADR-0002; ADR-0003 |
| Owner | Project Lead |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q2 · Retired — editor UX requirement consolidated into Q42

**Question:** Retired. Use Q42 as the authoritative checklist item for whether a browser-based visual editor is required for the MVP, and use Q1 to record who the editors are.

| Field | Value |
|---|---|
| PRD § | §2.2 Repository Content and Deployment Workflow; §3.1 Repository Content Workflow |
| ADR # | ADR-0003 |
| Owner | Project Lead |
| Status | N/A |
| Answer / Decision | Pointer only. Resolve editor-interface requirement in Q42 and editor roles in Q1. |
| Evidence / Source | Consolidated to avoid duplicate answer threads. |
| Resolved | N/A |

### Q3 · Confirm the editorial approval workflow

**Question:** Is editorial approval already handled through pull requests, or must the PRD define a new review and approval process?

| Field | Value |
|---|---|
| PRD § | §2.2 Repository Content and Deployment Workflow; §3.1 Repository Content Workflow |
| ADR # | ADR-0002; ADR-0007 |
| Owner | Repository Manager |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q4 · Define which branches require review and which roles can merge

**Question:** Which branches require pull-request-based review before merge, and which roles are permitted to merge changes that can promote to production?

| Field | Value |
|---|---|
| PRD § | §2.2 Repository Content and Deployment Workflow; §3.3 Constraints |
| ADR # | ADR-0007 |
| Owner | Repository Manager |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q5 · Confirm draft visibility requirements

**Question:** Does content need drafts that are invisible to everyone except selected reviewers?

| Field | Value |
|---|---|
| PRD § | §2.2 Repository Content and Deployment Workflow |
| ADR # | ADR-0002; ADR-0007 |
| Owner | Communications Lead |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q6 · Confirm scheduled publishing needs

**Question:** Do you need scheduled publishing, for example publishing a progress report on a specific date without a manual deployment trigger?

| Field | Value |
|---|---|
| PRD § | §3.2 Out of Scope; §3.3 Constraints |
| ADR # | ADR-0002 |
| Owner | Project Lead |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q7 · Define how narrative content and model-data updates are released together

**Question:** Should content changes and model-data updates be released together, or can they be released independently under a documented approval rule?

| Field | Value |
|---|---|
| PRD § | §2.2 Repository Content and Deployment Workflow; §3.1 Build-Time Model Data Pipeline; §4.2 Version History and Archive |
| ADR # | ADR-0005; ADR-0007; ADR-0008 |
| Owner | Project Lead |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q8 · Define the minimum production-release approval set

**Question:** What is the minimum required set of approvals for a production release: which roles must approve, how many approvals are required, and is co-approval required?

| Field | Value |
|---|---|
| PRD § | §2.2 Repository Content and Deployment Workflow; §3.3 Constraints; §12 Sign-Off |
| ADR # | ADR-0007 |
| Owner | Project Lead |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

---

## 2. Review and deployment workflow

### Q9 · Confirm the repository as system of record

**Question:** Is the repository the accepted system of record for narrative content, configuration, and release history?

| Field | Value |
|---|---|
| PRD § | §2.2 Repository Content and Deployment Workflow; §2.3 Architecture Principles; §3.1 Repository Content Workflow |
| ADR # | ADR-0002; ADR-0008 |
| Owner | Product Owner |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q10 · Define preview URL and preview-build requirements

**Question:** Are per-pull-request preview URLs required, and if so, should preview builds deploy automatically or only on manual request?

| Field | Value |
|---|---|
| PRD § | §2.2 Repository Content and Deployment Workflow; §3.1 Staging and Production Environments; §3.1 Automated Validation and Deployment Workflow |
| ADR # | ADR-0007 |
| Owner | Lead Developer |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q11 · Define the production deployment approval step

**Question:** Should production deployment happen automatically after merge, or require a separate manual approval step after staging review?

| Field | Value |
|---|---|
| PRD § | §2.2 Repository Content and Deployment Workflow; §3.1 Staging and Production Environments; §3.3 Constraints |
| ADR # | ADR-0007 |
| Owner | Repository Manager |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q12 · Confirm the intended hosting platform decision owner

**Question:** What hosting platform is the intended target, and who is responsible for making and recording that architecture decision?

| Field | Value |
|---|---|
| PRD § | §2.2 Repository Content and Deployment Workflow; §8 Architecture Constraints and Decision References |
| ADR # | ADR-0001; ADR-0007; ADR-0008 |
| Owner | Lead Developer |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q13 · Retired — preview URL requirement consolidated into Q10

**Question:** Retired. Use Q10 to record both whether per-pull-request preview URLs are required and whether their deployment is automatic or manual.

| Field | Value |
|---|---|
| PRD § | §2.2 Repository Content and Deployment Workflow; §3.1 Staging and Production Environments |
| ADR # | ADR-0007 |
| Owner | Lead Developer |
| Status | N/A |
| Answer / Decision | Pointer only. Resolve preview URL and preview trigger policy in Q10. |
| Evidence / Source | Consolidated to avoid dependency ordering between two separate items. |
| Resolved | N/A |

### Q14 · Define a machine-parseable version naming scheme

**Question:** How should production versions be named so the naming scheme is machine-parseable for the version selector and archive routing, and does the scheme encode model-data snapshot identity?

| Field | Value |
|---|---|
| PRD § | §3.1 Version Archive System; §4.2 Version History and Archive |
| ADR # | ADR-0008 |
| Owner | Lead Developer |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q15 · Define what must remain immutable

**Question:** What exactly must be immutable for each approved release: rendered pages, model-data snapshot, narrative content, configuration, media assets, or all of them?

| Field | Value |
|---|---|
| PRD § | §2.2 Repository Content and Deployment Workflow; §2.3 Architecture Principles; §4.2 Version History and Archive; §3.3 Constraints |
| ADR # | ADR-0005; ADR-0008 |
| Owner | Product Owner |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q16 · Define how historical releases are accessed

**Question:** How should old versions be accessed at stable public URLs: permanent subpaths, subdomains, or another routing approach that satisfies archival access requirements?

| Field | Value |
|---|---|
| PRD § | §4.2 Version History and Archive; §3.3 Constraints |
| ADR # | ADR-0008 |
| Owner | Lead Developer |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

---

## 3. Content structure

### Q17 · Define watershed-specific versus shared content boundaries

**Question:** Should each watershed have its own content directory, or should shared content be reused across watersheds under an agreed content-organization rule?

| Field | Value |
|---|---|
| PRD § | §3.1 Watershed Configuration System; §4.1 Watershed Selection and Configuration |
| ADR # | ADR-0002 |
| Owner | Lead Developer |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q18 · Separate editorial content from structured and model-backed data

**Question:** Which content is genuinely editorial narrative, and which should be structured data? For model-backed data covered by ADR-0004, editors must not be the source of truth; answer this separately for narrative pages, structure-status tables, glossary entries, and references.

| Field | Value |
|---|---|
| PRD § | §2.1 Content/Behavior Boundary; §3.1 Repository-Managed Content Pages and Approved Components; §4.6 Repository-Managed Content Pages and Approved Components; §10 Glossary |
| ADR # | ADR-0002; ADR-0004; ADR-0006 |
| Owner | Lead Developer |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q19 · Confirm whether barrier records are ever manually edited

**Question:** Will editors need to modify barrier records manually, or are all barrier and connectivity values always generated from pg_featureserv?

| Field | Value |
|---|---|
| PRD § | §2.1 High-Level Architecture; §3.1 Build-Time Model Data Pipeline; §4.3 Connectivity Status Dashboard; §4.4 Interactive Barrier Map |
| ADR # | ADR-0004; ADR-0005 |
| Owner | Biologist Lead |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q20 · Identify which tables must remain human-editable

**Question:** Which tables must be directly editable by humans, and which must always be generated from approved data or component configuration?

| Field | Value |
|---|---|
| PRD § | §3.1 Repository-Managed Content Pages and Approved Components; §4.5 Habitat Accessibility Curve; §5 US-006 |
| ADR # | ADR-0004; ADR-0006 |
| Owner | Biologist Lead |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q21 · Confirm the approved reusable content-component set

**Question:** Do content pages require reusable approved components such as callouts, metric cards, maps, charts, image galleries, or embedded reports, and which of those belong in the supported MVP set?

| Field | Value |
|---|---|
| PRD § | §3.1 Repository-Managed Content Pages and Approved Components; §4.3 Connectivity Status Dashboard; §4.4 Interactive Barrier Map; §4.5 Habitat Accessibility Curve |
| ADR # | ADR-0006 |
| Owner | Lead Developer |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q22 · Confirm whether Markdown conventions are sufficient as the content format

**Question:** Is Markdown or MDX with documented conventions sufficient as the content format for nontechnical editors, separate from whether a browser-based visual editor is required?

| Field | Value |
|---|---|
| PRD § | §3.1 Repository Content Workflow; §4.6 Repository-Managed Content Pages and Approved Components; §10 Glossary |
| ADR # | ADR-0002; ADR-0006 |
| Owner | Communications Lead |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q23 · Confirm repository media-storage limits

**Question:** Are images and PDFs small enough to store in the repository, or do you need external object storage for media?

| Field | Value |
|---|---|
| PRD § | §3.1 Repository-Managed Content Pages and Approved Components; §3.3 Constraints |
| ADR # | ADR-0002 |
| Owner | Lead Developer |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q24 · Confirm the citation and reference data model

**Question:** Do references need a formal citation model such as BibTeX, CSL JSON, DOI metadata, or manually maintained citation entries?

| Field | Value |
|---|---|
| PRD § | §3.1 Repository-Managed Content Pages and Approved Components; §4.6 Repository-Managed Content Pages and Approved Components |
| ADR # | ADR-0002 |
| Owner | Communications Lead |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q25 · Define glossary sharing rules

**Question:** Should glossary terms be globally shared, watershed-specific, or support both patterns?

| Field | Value |
|---|---|
| PRD § | §3.1 Repository-Managed Content Pages and Approved Components; §4.6 Repository-Managed Content Pages and Approved Components; §10 Glossary |
| ADR # | ADR-0002 |
| Owner | Communications Lead |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q26 · Define page reuse versus per-watershed independence

**Question:** Should the same page support multiple watersheds through configuration, or should each watershed have independent page content?

| Field | Value |
|---|---|
| PRD § | §3.1 Watershed Configuration System; §3.1 Repository-Managed Content Pages and Approved Components; §4.1 Watershed Selection and Configuration |
| ADR # | ADR-0002; ADR-0006 |
| Owner | Product Owner |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

---

## 4. Internationalization and accessibility

### Q27 · Confirm whether French is MVP scope

**Question:** Is French required for the MVP, or is it explicitly a future requirement only?

| Field | Value |
|---|---|
| PRD § | §3.1 Repository Content Workflow; §3.2 Out of Scope; §4.6 Repository-Managed Content Pages and Approved Components; §10 Glossary |
| ADR # | ADR-0002 |
| Owner | Product Owner |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q28 · Confirm future bilingual-structure readiness if French is deferred

**Question:** If French is deferred, does the current content structure still need to accommodate future bilingual content without requiring a major refactor of file layout, front matter, or routing?

| Field | Value |
|---|---|
| PRD § | §3.1 Repository Content Workflow; §3.2 Out of Scope; §4.6 Repository-Managed Content Pages and Approved Components; §10 Glossary |
| ADR # | ADR-0002 |
| Owner | Lead Developer |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q29 · Assign alt-text responsibility

**Question:** Who is responsible for writing and reviewing alt text for images and other non-text content?

| Field | Value |
|---|---|
| PRD § | §3.3 Constraints; §6 Accessibility |
| ADR # | — |
| Owner | Communications Lead |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q30 · Identify additional accessibility or governance requirements

**Question:** Are there specific Indigenous, governmental, partner, or data-governance requirements beyond WCAG 2.1 AA that must be reflected in the PRD?

| Field | Value |
|---|---|
| PRD § | §3.3 Constraints; §6 Accessibility; §9 Risk Analysis |
| ADR # | — |
| Owner | Product Owner |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q31 · Confirm Canadian accessibility compliance scope

**Question:** Does the site need to satisfy Canadian accessibility requirements in addition to WCAG 2.1 AA?

| Field | Value |
|---|---|
| PRD § | §3.3 Constraints; §6 Accessibility |
| ADR # | — |
| Owner | Product Owner |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

---

## 5. Model data and reporting

### Q32 · Confirm the authoritative source for each displayed metric

**Question:** What is the authoritative source for each displayed metric: pg_featureserv, precomputed files, manually reviewed tables, or a combination governed by an explicit rule?

| Field | Value |
|---|---|
| PRD § | §2.1 High-Level Architecture; §2.3 Architecture Principles; §3.1 Build-Time Model Data Pipeline; §4.3 Connectivity Status Dashboard |
| ADR # | ADR-0004; ADR-0005 |
| Owner | Biologist Lead |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q33 · Define build failure versus fallback behavior for pg_featureserv outages

**Question:** Should the build fail if pg_featureserv is unavailable, or should it fall back to the last approved dataset under a documented exception policy?

| Field | Value |
|---|---|
| PRD § | §3.1 Build-Time Model Data Pipeline; §3.1 Automated Validation and Deployment Workflow; §9 Risk Analysis |
| ADR # | ADR-0004; ADR-0005 |
| Owner | Lead Developer |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q34 · Confirm whether exact approved API snapshots are a hard product requirement

**Question:** Is retaining the exact approved API response used for each production release a hard product requirement for audit and reproducibility, or is retaining only the rendered output sufficient?

| Field | Value |
|---|---|
| PRD § | §2.3 Architecture Principles; §4.2 Version History and Archive |
| ADR # | ADR-0004; ADR-0005; ADR-0008 |
| Owner | Product Owner |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q35 · Confirm the out-of-repository model approval process

**Question:** How are model results approved outside the repository today, and what evidence of that approval must be retained before a public release?

| Field | Value |
|---|---|
| PRD § | §2.2 Model Update Cycle; §5 US-004 |
| ADR # | ADR-0005; ADR-0007 |
| Owner | Project Lead |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q36 · Confirm required build-time model-data validation

**Question:** Should model-data validation be automated during the build, and if so, which checks are mandatory: schema, row counts, nulls, geographic bounds, metric consistency, or others?

| Field | Value |
|---|---|
| PRD § | §3.1 Build-Time Model Data Pipeline; §3.1 Automated Validation and Deployment Workflow; §5 US-004; §6 Reliability |
| ADR # | ADR-0004; ADR-0005 |
| Owner | Lead Developer |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q37 · Confirm API contract stability expectations

**Question:** Are the pg_featureserv API endpoints stable enough to be treated as a long-term data contract, and if not, what change-management or versioning expectation applies?

| Field | Value |
|---|---|
| PRD § | §3.1 Build-Time Model Data Pipeline; §9 Risk Analysis |
| ADR # | ADR-0004; ADR-0005 |
| Owner | Lead Developer |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q38 · Retired — snapshot mechanism tracked as an ADR dependency

**Question:** Retired. The implementation mechanism for build-time fetching and snapshot retention belongs in the ADR dependency checklist in Section 9, especially ADR-0005 and ADR-0008.

| Field | Value |
|---|---|
| PRD § | §3.1 Build-Time Model Data Pipeline; §4.2 Version History and Archive |
| ADR # | ADR-0005; ADR-0008 |
| Owner | Lead Developer |
| Status | N/A |
| Answer / Decision | Pointer only. Record the product requirement in Q34 and the implementation dependency in Section 9. |
| Evidence / Source | Consolidated to separate product constraint from implementation mechanism. |
| Resolved | N/A |

### Q39 · Confirm whether users must compare versions side by side

**Question:** Can users compare two model versions side by side, or should the application support viewing only one approved version at a time?

| Field | Value |
|---|---|
| PRD § | §4.2 Version History and Archive; §5 US-002 |
| ADR # | ADR-0008 |
| Owner | Product Owner |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q40 · Define the editorial-versus-generated boundary for Component 3 and Component 6 tables

**Question:** Are the Component 3 and Component 6 tables generated from APIs, maintained as editorial content, or a hybrid with clearly documented ownership boundaries?

| Field | Value |
|---|---|
| PRD § | §3.1 Repository-Managed Content Pages and Approved Components; §4.5 Habitat Accessibility Curve; §5 US-006 |
| ADR # | ADR-0004; ADR-0006 |
| Owner | Biologist Lead |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

---

## 6. Content workflow boundaries

### Q41 · Confirm ADR-0002 reconsideration triggers and thresholds

**Question:** Has the team agreed to the reconsideration triggers defined in ADR-0002, and if so, what thresholds apply for scheduled publishing, relational content, editor population, media-library scale, and non-Git workflows?

| Field | Value |
|---|---|
| PRD § | §2.3 Architecture Principles; §3.2 Out of Scope |
| ADR # | ADR-0002 |
| Owner | Project Lead |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q42 · Define whether a browser-based visual editor is required for the MVP

**Question:** Given the identified editor roles and their comfort with repository workflows, is a browser-based visual editor required for the MVP, or can it follow in a later phase?

| Field | Value |
|---|---|
| PRD § | §3.1 Repository Content Workflow; §7 Timeline and Milestones |
| ADR # | ADR-0003 |
| Owner | Project Lead |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q43 · Confirm whether a self-managed editorial tool is acceptable

**Question:** Would hosting a self-managed editorial tool be acceptable if it has infrastructure cost but no subscription fee?

| Field | Value |
|---|---|
| PRD § | §2.3 Architecture Principles; §3.3 Constraints |
| ADR # | ADR-0003 |
| Owner | Product Owner |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q44 · Define the project's policy on paid services

**Question:** Are paid services prohibited entirely, or only recurring paid CMS subscriptions, given that hosting, mapping, analytics, and storage may also introduce cost?

| Field | Value |
|---|---|
| PRD § | §2.3 Architecture Principles; §3.3 Constraints |
| ADR # | ADR-0002; ADR-0003 |
| Owner | Product Owner |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q45 · Confirm whether vendor portability is a formal requirement

**Question:** Is vendor portability a formal requirement such that all content must remain exportable in portable formats regardless of future editorial tooling?

| Field | Value |
|---|---|
| PRD § | §2.3 Architecture Principles; §3.3 Constraints |
| ADR # | ADR-0002; ADR-0003 |
| Owner | Product Owner |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q46 · Define acceptable authentication for a future browser editor

**Question:** If a future browser-based editor is adopted, which authentication and authorization mechanisms are acceptable?

| Field | Value |
|---|---|
| PRD § | §3.1 Repository Content Workflow |
| ADR # | ADR-0003 |
| Owner | Lead Developer |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

---

## 7. Scope and priorities

### Q47 · Define the true MVP if the schedule tightens

**Question:** What is the minimum acceptable MVP scope if the 12-week schedule becomes constrained?

| Field | Value |
|---|---|
| PRD § | §3.1 MVP Features; §7 Timeline and Milestones |
| ADR # | — |
| Owner | Product Owner |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q48 · Separate first-release requirements from later-phase scope

**Question:** Which requirements are mandatory for the first public release, and which belong to demonstrations or later phases?

| Field | Value |
|---|---|
| PRD § | §3.1 MVP Features; §3.2 Out of Scope; §7 Timeline and Milestones |
| ADR # | — |
| Owner | Product Owner |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q49 · Confirm the release target

**Question:** Is the goal a production-ready public site, a technical prototype, or an internal stakeholder preview?

| Field | Value |
|---|---|
| PRD § | §1 Problem Statement; §7 Timeline and Milestones |
| ADR # | — |
| Owner | Product Owner |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q50 · Confirm stakeholder agreement on the KPI set

**Question:** Have stakeholders agreed that the KPI set in PRD §6 is complete, including any success criteria beyond Lighthouse scores, and are there missing KPIs such as data-validation pass rate or archive completeness?

| Field | Value |
|---|---|
| PRD § | §6 Success Metrics and KPIs |
| ADR # | — |
| Owner | Product Owner |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q51 · Retired — migration scope expanded into Section 11

**Question:** Retired. Use Section 11 as the authoritative migration-readiness checklist for redirects, assets, behaviors, content inventory, and SEO preservation.

| Field | Value |
|---|---|
| PRD § | §1 Problem Statement; §3.1 MVP Features |
| ADR # | ADR-0001 |
| Owner | Lead Developer |
| Status | N/A |
| Answer / Decision | Pointer only. Resolve migration readiness in Section 11. |
| Evidence / Source | Expanded into discrete checklist items for traceability. |
| Resolved | N/A |

### Q52 · Confirm whether current users or links depend on existing URLs or assets

**Question:** Are there current users, partners, citations, or external links that reference existing page URLs or assets that must not break during migration?

| Field | Value |
|---|---|
| PRD § | §1 Problem Statement; §4.2 Version History and Archive |
| ADR # | ADR-0001; ADR-0008 |
| Owner | Communications Lead |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

### Q53 · Confirm SEO and citation preservation requirements

**Question:** Does the new application need to preserve existing SEO metadata, indexed URLs, downloadable files, and citation-ready references?

| Field | Value |
|---|---|
| PRD § | §3.3 Constraints; §4.2 Version History and Archive; §4.6 Repository-Managed Content Pages and Approved Components |
| ADR # | ADR-0001; ADR-0008 |
| Owner | Communications Lead |
| Status | Open |
| Answer / Decision | — |
| Evidence / Source | — |
| Resolved | — |

---

## 8. Questions to resolve first

The answers to these items have the greatest impact on the PRD and on architecture decisions. Each item should point back to the detailed checklist entry where the full answer is recorded.

| Priority item | Primary checklist refs | PRD § / ADR # | Owner | Status | Answer / Decision | Evidence / Source | Resolved |
|---|---|---|---|---|---|---|---|
| Who are the editors, and what is their comfort level with repository-based workflows? | Q1, Q42 | §2.2; ADR-0002; ADR-0003 | Project Lead | Open | — | — | — |
| Is a browser-based visual editor required for the MVP, or can it follow in a later phase? | Q42 | §3.1; ADR-0003 | Project Lead | Open | — | — | — |
| What must be preserved from the current Quarto/R-notebook publishing workflow during migration? | Section 11; Q52; Q53 | §1; ADR-0001 | Lead Developer | Open | — | — | — |
| What hosting platform and preview-deployment approach does the team intend to use? | Q10, Q12 | §2.2; ADR-0001; ADR-0007; ADR-0008 | Lead Developer | Open | — | — | — |
| How are model data and narrative content versioned and released together? | Q7, Q34, Q35 | §2.2; §4.2; ADR-0005; ADR-0008 | Project Lead | Open | — | — | — |
| What must be immutable and permanently accessible at stable public URLs? | Q15, Q16 | §4.2; ADR-0008 | Product Owner | Open | — | — | — |
| Which tables are generated model data versus editorial content? | Q18, Q20, Q40 | §3.1; §4.5; ADR-0004; ADR-0006 | Biologist Lead | Open | — | — | — |
| What is the minimum scope for the first public release? | Q47, Q48, Q49 | §3.1; §7 | Product Owner | Open | — | — | — |

---

## 9. ADR open-dependencies checklist

Use this section to surface ADR follow-up items as discrete checklist rows rather than leaving them buried in the ADR prose.

| Item | PRD § | ADR # | Owner | Status | Answer / Decision | Evidence / Source | Resolved |
|---|---|---|---|---|---|---|---|
| Confirm the hosting platform selection. | §2.2; §8 | ADR-0001; ADR-0007; ADR-0008 | Lead Developer | Open | — | — | — |
| Define the detailed migration plan, content migration strategy, and redirect approach. | §1; §7 | ADR-0001 | Lead Developer | Open | — | — | — |
| Confirm the ADR-0002 reconsideration triggers and record agreed thresholds. | §2.3; §3.2 | ADR-0002 | Project Lead | Open | — | — | — |
| Identify the primary content editors and their comfort with Git-based workflows. | §2.2; §3.1 | ADR-0003 | Project Lead | Open | — | — | — |
| Confirm authentication and authorization requirements for a browser-based editor. | §3.1 | ADR-0003 | Lead Developer | Open | — | — | — |
| Confirm whether a visual editor is essential for the MVP or can follow later. | §3.1; §7 | ADR-0003 | Project Lead | Open | — | — | — |
| Define API contracts, build-time validation rules, and API-unavailable behavior. | §3.1; §6 Reliability | ADR-0004 | Lead Developer | Open | — | — | — |
| Define the approach for retaining or reproducing the approved data snapshot for each release. | §4.2 | ADR-0004; ADR-0005; ADR-0008 | Lead Developer | Open | — | — | — |
| Define build failure behavior versus fallback to the last approved data. | §3.1; §9 | ADR-0005 | Lead Developer | Open | — | — | — |
| Define snapshot retention, audit, and reproduction requirements. | §4.2; §6 Reliability | ADR-0005; ADR-0008 | Lead Developer | Open | — | — | — |
| Define the approved component schema and validation rules. | §3.1; §4.6 | ADR-0006 | Lead Developer | Open | — | — | — |
| Define documentation and guidance for nontechnical editors. | §3.1; §4.7 | ADR-0006 | Communications Lead | Open | — | — | — |
| Define required approvers and final production-release authority. | §2.2; §12 | ADR-0007 | Project Lead | Open | — | — | — |
| Select the hosting platform and preview-deployment automation tooling. | §2.2; §8 | ADR-0007 | Lead Developer | Open | — | — | — |
| Define whether production deployment is automatic after merge or separately approved. | §2.2; §3.3 | ADR-0007 | Repository Manager | Open | — | — | — |
| Define the stable URL scheme for archived releases. | §4.2 | ADR-0008 | Lead Developer | Open | — | — | — |
| Define the hosting strategy for archived deployments. | §4.2; §6 Reliability | ADR-0008 | Lead Developer | Open | — | — | — |
| Define release-version naming conventions. | §4.2 | ADR-0008 | Lead Developer | Open | — | — | — |
| Define the mechanism for retaining or reproducing the approved build-time data snapshot for each archived version. | §4.2; §6 Reliability | ADR-0008; ADR-0005 | Lead Developer | Open | — | — | — |

---

## 10. PRD internal consistency checks

Use this section to verify that the PRD remains internally aligned after edits and that traceable requirements are still testable.

| Check | PRD § | ADR # | Owner | Status | Answer / Decision | Evidence / Source | Resolved |
|---|---|---|---|---|---|---|---|
| Confirm that the MVP feature list in §3.1 matches the detailed feature specifications in §4.1–§4.7. | §3.1; §4.1–§4.7 | — | Product Owner | Open | — | — | — |
| Confirm that the constraints in §3.3 are reflected consistently across the feature specs and ADR references. | §3.3; §8 | ADR-0001–ADR-0008 | Product Owner | Open | — | — | — |
| Confirm that US-001 acceptance criteria are testable and assigned to a delivery milestone. | §5 US-001; §7 | — | Product Owner | Open | — | — | — |
| Confirm that US-002 acceptance criteria are testable and assigned to a delivery milestone. | §5 US-002; §7 | ADR-0008 | Product Owner | Open | — | — | — |
| Confirm that US-003 acceptance criteria are testable and assigned to a delivery milestone. | §5 US-003; §7 | — | Product Owner | Open | — | — | — |
| Confirm that US-004 acceptance criteria are testable and assigned to a delivery milestone. | §5 US-004; §7 | ADR-0005; ADR-0007; ADR-0008 | Product Owner | Open | — | — | — |
| Confirm that US-005 acceptance criteria are testable and assigned to a delivery milestone. | §5 US-005; §7 | — | Product Owner | Open | — | — | — |
| Confirm that US-006 acceptance criteria are testable and assigned to a delivery milestone. | §5 US-006; §7 | ADR-0004; ADR-0006 | Product Owner | Open | — | — | — |
| Confirm that the KPI set in §6 has explicit stakeholder agreement and covers performance, reliability, accessibility, and release quality. | §6 | — | Product Owner | Open | — | — | — |
| Confirm that the sign-off roles in §12 are current and that each stakeholder has acknowledged the role. | §12 | — | Product Owner | Open | — | — | — |

---

## 11. Migration readiness checklist

Use this section to track migration scope from the current Quarto/R-notebook workflow as discrete checklist items rather than a single broad question.

| Check | PRD § | ADR # | Owner | Status | Answer / Decision | Evidence / Source | Resolved |
|---|---|---|---|---|---|---|---|
| URL redirect inventory is complete for existing public routes that must not break. | §1 Problem Statement; §4.2 Version History and Archive | ADR-0001; ADR-0008 | Lead Developer | Open | — | — | — |
| Downloadable asset inventory is complete for files, reports, and other downloads that must remain accessible. | §1 Problem Statement; §4.6 Repository-Managed Content Pages and Approved Components | ADR-0001 | Communications Lead | Open | — | — | — |
| Interactive behavior inventory is complete for maps, charts, filters, embeds, and other user-visible interactions that must be reproduced or intentionally retired. | §1 Problem Statement; §4.3–§4.5 | ADR-0001 | Lead Developer | Open | — | — | — |
| Narrative and table content inventory is complete for Quarto-generated pages, structured tables, and editorial text that must move into repository-managed content. | §1 Problem Statement; §3.1 Repository-Managed Content Pages and Approved Components; §5 US-006 | ADR-0001; ADR-0002 | Communications Lead | Open | — | — | — |
| SEO metadata and citation-preservation inventory is complete for indexed URLs, metadata, structured data, and citation-ready references. | §3.3 Constraints; §4.6 Repository-Managed Content Pages and Approved Components | ADR-0001; ADR-0008 | Communications Lead | Open | — | — | — |

---

## Review Notes

Use this section to record answers, decisions, open questions, deferrals, and resulting PRD or ADR changes during review sessions.
