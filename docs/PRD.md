# Product Requirements Document (PRD)
## Horsefly Watershed Connectivity Restoration Plan (WCRP) – Platform Modernization

**Document Version:** 1.4 (Revised: PRD/ADR boundary enforcement; architecture decisions moved to ADRs)
**Last Updated:** August 10, 2026
**Status:** In Development
**Prepared By:** GitHub Copilot with CWF Team

> **Architecture decisions and their current status are recorded in [`docs/adr/`](./adr/).** All eight ADRs are Proposed pending formal team review. This PRD states product-level requirements, constraints, acceptance criteria, and authoritative external dependencies only. Implementation selections (framework, tooling, hosting, CMS product, CI/CD platform) are not settled in this document.

---

## Executive Summary

The Horsefly WCRP platform is transitioning from a static Quarto/R-notebook publishing workflow to a modern, interactive public web application. This migration enables staged review workflows, version-controlled content, interactive visualizations (maps, dashboards, charts), flexible content management, and scalability to additional watersheds.

### Key Objectives
1. Enable controlled content updates via a staged review workflow (preview → approved production)
2. Provide interactive watershed connectivity maps and data exploration
3. Maintain permanent, publicly accessible version history for stakeholder access to previous WCRP iterations
4. Establish a reusable configuration framework for additional watersheds
5. Improve performance, accessibility, and maintainability
6. Create a subscription-free-by-default editorial workflow for biologists and content editors

### Success Metrics
- Page load time < 2 seconds (90th percentile)
- Staging-to-production deployment time < 10 minutes
- Zero manual rendering steps required for content updates
- Support for 5+ watersheds from a single codebase configuration
- Mobile-responsive design (90+ Lighthouse score)
- WCAG 2.1 AA accessibility compliance
- Version history accessible and functional for 100% of users

---

## 1. Problem Statement

### Current Pain Points

#### 1.1 Rigidity in Content Formatting
- **Issue:** The Quarto/R-notebook publishing workflow limits visual customization
- **Impact:** The team cannot implement desired designs without significant overrides
- **Consequence:** High friction for stakeholder review and approval cycles

#### 1.2 Manual Rendering Process for Content Updates
- **Issue:** Narrative updates require a full document rebuild and redeployment
- **Impact:** Difficult to coordinate narrative updates with model data releases
- **Scalability Problem:** No incremental update path; render time grows with document size

#### 1.3 No Interactive Web Components
- **Issue:** Maps and visualizations are static images
- **Missing Capabilities:**
  - Interactive maps (barrier locations, habitat, connectivity status)
  - Dashboards with at-a-glance metrics
  - User-driven filtering (by priority, habitat type, status)
  - Data export

#### 1.4 Fragmented Build Dependencies
- **Issue:** Multiple-language build environment with manual synchronization
- **Risk:** Cross-language breakage; difficult onboarding for new contributors
- **Maintenance Burden:** Bottleneck for debugging on a small team

#### 1.5 Limited Multi-Watershed Scalability
- **Issue:** Fork-and-customize approach with no shared parameterization
- **Risk:** Each fork diverges; improvements are hard to propagate
- **Goal:** Deploy additional watershed WCRPs with 80% content/configuration reuse

#### 1.6 No Automated Validation
- **Issue:** Manual testing before deployment; no automated validation
- **Risk:** Broken links, data failures, or rendering errors reach production
- **Impact:** Reputational risk with public stakeholders

#### 1.7 Accessibility Concerns
- **Issue:** No WCAG compliance audit; limited alt-text and semantic HTML
- **Impact:** Excludes users with disabilities; potential legal and reputational risk

#### 1.8 No Version History or Archive
- **Issue:** Partners cannot access previous WCRP versions as model outputs evolve
- **Impact:** Loss of historical context for connectivity restoration progress

---

## 2. Solution Overview

### 2.1 High-Level Architecture

```
┌────────────────────────────────────────────────────────────┐
│                  PUBLIC-FACING WEB APPLICATION             │
│                                                            │
│  ┌──────────────────┐  ┌─────────────────┐  ┌──────────┐  │
│  │  Content Pages   │  │ Interactive Maps │  │Dashboards│  │
│  │  Narratives      │  │ Barrier popups  │  │Charts    │  │
│  │  Approved comps  │  │ Client filters  │  │Reporting │  │
│  └──────────────────┘  └─────────────────┘  └──────────┘  │
└────────────────────────────────────────────────────────────┘
                      ↑ loaded from build output
┌────────────────────────────────────────────────────────────┐
│                    APPLICATION BUILD PIPELINE              │
│  - Loads repository-managed editorial content (Markdown/   │
│    MDX, YAML, JSON)                                        │
│  - Loads watershed and approved-component configuration    │
│  - Fetches and validates pg_featureserv model data         │
│  - Produces build artifacts for all interactive components │
└────────────────────────────────────────────────────────────┘
                      ↑ reads and writes via repository
┌────────────────────────────────────────────────────────────┐
│              REPOSITORY CONTENT AND REVIEW WORKFLOW        │
│  - Editorial content managed in the repository             │
│  - Pull-request review produces staging/preview builds     │
│  - Version metadata associated with approved releases      │
└────────────────────────────────────────────────────────────┘
                      ↑ authoritative model data
┌────────────────────────────────────────────────────────────┐
│                    EXTERNAL MODEL DATA                     │
│  - pg_featureserv/PostGIS is authoritative for model data  │
│  - No runtime API polling required in the MVP              │
└────────────────────────────────────────────────────────────┘
```

**Content/Behavior Boundary:**
- Repository-managed editorial content identifies which approved components should appear and supplies their configuration; it does not contain application logic or arbitrary executable code.
- The application owns page rendering, component behavior, data fetching, validation, and interactive visualization.
- Model data is sourced from pg_featureserv and is fetched and validated during the build.
- Interactive maps, dashboards, and charts use build-time data; no runtime API polling is required in the MVP.

> Implementation technology selections for the application framework, build tooling, hosting, and CI/CD platform are recorded in [`docs/adr/`](./adr/) and are Proposed pending team decision.

### 2.2 Repository Content and Deployment Workflow

```
┌──────────────────────────────────────────────────────────┐
│  Editorial Update Cycle                                  │
│                                                          │
│  1. Editor updates narrative content or component        │
│     configuration in the repository                      │
│  2. A pull request opens for review + preview build      │
│  3. Reviewers approve and merge to trigger staging build │
└──────────────────────────────────────────────────────────┘
                          ↓
┌──────────────────────────────────────────────────────────┐
│  Model Update Cycle (Outside Repository)                 │
│                                                          │
│  1. Model runs                                           │
│  2. QA/QC validation                                     │
│  3. Project lead approves model results                  │
└──────────────────────────────────────────────────────────┘
                          ↓
┌──────────────────────────────────────────────────────────┐
│  Build and Validation                                    │
│                                                          │
│  1. Application build loads editorial content and config │
│  2. Build fetches and validates pg_featureserv data      │
│  3. Build produces static artifacts for the deployment   │
└──────────────────────────────────────────────────────────┘
                          ↓
┌──────────────────────────────────────────────────────────┐
│  STAGING / PREVIEW ENVIRONMENT                           │
│                                                          │
│  1. Full build completes (content, metrics, maps, charts)│
│  2. Internal team and trusted partners review            │
│  3. Issues resolved or build approved for production     │
└──────────────────────────────────────────────────────────┘
                          ↓ (approved promotion)
┌──────────────────────────────────────────────────────────┐
│  PRODUCTION ENVIRONMENT                                  │
│                                                          │
│  1. Live public site serves immutable build artifacts    │
│  2. Previous version archived at its stable public URL   │
│  3. Version selector enables access to prior releases    │
│  4. Interactive components operate on build-time data    │
└──────────────────────────────────────────────────────────┘
```

### 2.3 Architecture Principles

The following principles constrain implementation choices. Detailed technical selections and their rationale are recorded in [`docs/adr/`](./adr/).

| Principle | Product Constraint |
|---|---|
| **Repository-managed content** | Editorial content must be stored in portable, version-controlled formats in the repository. The MVP must not require a paid CMS subscription. |
| **Approved components only** | Editorial content may configure approved interactive components; it may not execute arbitrary code or define component behavior. |
| **Build-time model data** | pg_featureserv data must be fetched and validated during the build. No runtime polling is required in the MVP. |
| **Staged review and approval** | Content and data changes must be reviewable in a preview/staging environment before production publication. |
| **Immutable version archive** | Every approved production release must remain permanently publicly accessible at a stable URL. |
| **Subscription-free-by-default MVP** | The MVP editorial workflow must not require recurring CMS subscription fees. Managed paid CMS products may be considered only in future phases when their benefits justify cost. |

---

## 3. Scope Definition

### 3.1 MVP Features (Phase 1 – 3 months)

#### Application Pages and Components
- [ ] **Watershed Selection**
  - Dropdown/selector for different watersheds (Horsefly, Kettle, etc.)
  - Configuration-driven parameter switching
  - URL-based state (e.g., `?watershed=horsefly`)

- [ ] **Version History Selector**
  - Dropdown showing all published versions (v1.0, v1.1, v1.2, etc.)
  - Click to view that version's immutable content and data
  - Clear indication of which version is current
  - Historical versions cannot be edited

- [ ] **Connectivity Status Dashboard**
  - Metrics from pg_featureserv (fetched at build time):
    - Connected habitat (km) per configured connectivity status type
    - Disconnected habitat (km) per configured connectivity status type
    - % connectivity per configured connectivity status type
    - Priority barriers count
    - Structures requiring assessment count
    - Non-actionable barriers count
  - Displays build-time data (not live-polling)
  - Shows deployment timestamp ("Last updated: June 15, 2026")
  - Mobile-responsive layout

- [ ] **Interactive Barrier Map**
  - Interactive base map (satellite + vector tiles)
  - All barrier locations shown as interactive markers
  - Top 20–30 ranked structures labeled based on habitat/ranking outputs
  - Filter by barrier type, priority classification, passability status
  - Click-to-details popup with barrier information
  - Zoom to watershed boundary
  - Responsive for desktop and mobile

- [ ] **Habitat Accessibility Curve (HAC)**
  - Interactive chart: structures ranked by upstream habitat (x-axis) vs. cumulative habitat (y-axis)
  - Color-coded by priority
  - Tooltip on hover: structure name, km gain, priority
  - Habitat Accumulation Summary Table companion view (Component 3, Horsefly Table 8 structure)
  - Sortable/filterable structure rankings
  - Export to CSV

- [ ] **Repository-Managed Content Pages and Approved Components**
  - Project Overview (narrative from repository-managed content)
  - Glossary (multi-language ready, auto-generated index)
  - Methods and Restoration Status (editorial narrative plus approved component blocks)
  - Progress Reporting (narrative plus build-time data-backed metrics)
  - Structure List Status Tables grouped by structure status (Component 6, Horsefly Table 11 structure)
  - References (bibliography)
  - Structured component blocks for nontechnical editors; editorial content does not contain arbitrary executable code

- [ ] **Responsive Design**
  - Desktop, tablet, mobile breakpoints
  - Touch-friendly map controls
  - Accessible navigation

#### Build Pipeline and Workflow
- [ ] **Watershed Configuration System**
  - Configuration-driven plan entries (YAML) with shared reporting parameters
  - `plan_schema` identifies the database schema name for the plan
  - `target_species` supports backend processing; reporting output is primarily controlled by `connectivity_status_types`
  - `connectivity_status_types` accepts one or more values; each produces a corresponding Component 4 reporting sentence/metric output
  - Each configuration entry applies to all WCRPs created from that plan configuration

- [ ] **Build-Time Model Data Pipeline**
  - Fetch from pg_featureserv with error handling
  - Validate model payloads during the build
  - Materialize data as part of the build artifacts
  - No runtime API polling (data is static between deployments)

- [ ] **Repository Content Workflow**
  - Editorial content managed in the repository (Markdown/MDX, YAML, JSON)
  - Pull requests provide review and staging/preview builds
  - Approved components may be configured by editors; component behavior is owned by application code
  - Editorial content does not execute arbitrary JavaScript or JSX
  - Multi-language ready (English/French)

- [ ] **Staging and Production Environments**
  - Separate staging (preview) and production environments
  - Automated build and deployment to staging on workflow trigger
  - Manual approval step before promoting to production
  - Version metadata associated with each production release

- [ ] **Version Archive System**
  - Each approved production release receives version metadata
  - Build process generates version metadata accessible to the application
  - Application reads version metadata to populate the version selector
  - Previous versions remain permanently publicly accessible at stable URLs

- [ ] **Automated Validation and Deployment Workflow**
  - Automated validation checks (content, data schema, accessibility)
  - Automated build and deployment to staging
  - Manual approval for production promotion
  - Automated version metadata generation on production release
  - Rollback capability via prior approved releases

### 3.2 Out of Scope (Phase 2+)
- User authentication / login system
- Advanced reporting (PDF export, custom dashboards)
- Real-time data updates (polling not needed; data updates on deployment)
- Multi-language UI (English only; French content structure ready)
- Advanced analytics
- Administrative panel for managing watershed configuration
- Offline-first capabilities
- Automated model triggers (approval happens outside the repository)

### 3.3 Constraints
- **Browser Support:** Modern browsers (Chrome, Firefox, Safari, Edge) and mobile
- **Data Update Frequency:** 2–3 times per year (manual trigger)
- **Approval Workflow:** Staged (preview → manual approval → production)
- **Performance Budget:**
  - Largest bundle: < 250 KB (gzipped)
  - LCP (Largest Contentful Paint): < 2.5 s
  - CLS (Cumulative Layout Shift): < 0.1
- **Accessibility:** WCAG 2.1 AA minimum
- **SEO:** Proper meta tags, structured data, sitemaps
- **Version History:** All previous approved releases must remain permanently publicly accessible

---

## 4. Detailed Feature Specifications

### 4.1 Watershed Selection and Configuration

**User Story:**
*As a project partner viewing a WCRP, I want to see metrics, maps, and content specific to my watershed without manual URL changes.*

**Functional Requirements:**
1. Watersheds selectable from dropdown menu
2. Clicking a watershed loads all relevant content, map data, API parameters, and theme settings
3. URL reflects the current watershed selection (e.g., `/watershed/horsefly`)
4. Bookmark-friendly: returning to URL loads correct watershed

**Configuration Structure (example):**
```yaml
- plan_name: Horsefly
  plan_code: hors
  plan_schema: hors
  target_species: [CH, CO, SK]
  connectivity_status_types: [spawningrearing_all]
  filter_clause: >-
    watershed_group_code = 'HORS'
  api_config:
    barrier_extent: /functions/postgisftw.wcrp_barrier_extent/items.json
    habitat_connectivity: /functions/postgisftw.wcrp_habitat_connectivity_status/items.json
  map_bounds: [[-120.5, 51.8], [-119.5, 52.8]]
  center_coordinates: [-120.0, 52.3]
  zoom: 9
  theme:
    primary: "#008270"
```

- `plan_schema` is the database schema name used when resolving plan-specific queries
- `target_species` informs backend processing only; it does not by itself determine which reporting sentences appear
- `connectivity_status_types` determines Component 4 reporting outputs and may include multiple entries
- Each plan entry applies to all WCRP instances generated from that configuration

> Implementation details for how the configuration is loaded, how watershed state is managed at runtime, and how URL parameters are handled are architecture decisions recorded in `docs/adr/`.

---

### 4.2 Version History and Archive

**User Story:**
*As a stakeholder, I want to access previous WCRP versions to see how connectivity progress has improved over time.*

**Visual Design:**
```
┌───────────────────────────────────────────────┐
│  WCRP Version: [v1.2 (Current)           ↓]  │
│                                               │
│  Version History:                             │
│  • v1.2 – June 15, 2026 (Current)            │
│  • v1.1 – March 20, 2026                     │
│  • v1.0 – December 1, 2025                   │
│                                               │
│  [Click to view a different version]          │
└───────────────────────────────────────────────┘
```

**Requirements:**
1. Dropdown shows all approved published versions with dates
2. Clicking a version loads that immutable snapshot
3. Current version is clearly identified
4. URL reflects the selected version
5. All data and content match the approved state when that version was published
6. Historical versions cannot be edited
7. Version selector works on mobile

**Constraint:** Every published production release must remain permanently publicly accessible at a stable URL. The implementation mechanism for archiving and routing is an architecture decision recorded in `docs/adr/0008`.

---

### 4.3 Connectivity Status Dashboard

**User Story:**
*As a stakeholder, I want to see at-a-glance metrics showing current habitat connectivity status, updated when new model results are released.*

**Metrics Displayed:**
1. Connected habitat (km) for each configured `connectivity_status_type`
2. Disconnected habitat (km) for each configured `connectivity_status_type`
3. % connectivity for each configured `connectivity_status_type`
4. Count: Priority barriers
5. Count: Structures requiring assessment
6. Count: Non-actionable barriers

**Component 4 Reporting Rules:**
- The dashboard must generate one Component 4 sentence/metric output per configured `connectivity_status_type`
- `target_species` alone must not determine which connectivity metrics are shown; `connectivity_status_types` controls reporting output

**Data Source:**
- `GET https://cabd-pro.cwf-fcf.org/bcfishpass/functions/postgisftw.wcrp_habitat_connectivity_status/items.json?watershed_group_code=HORS&habitat_type=`
- Fetched at build time; data is static until the next approved deployment
- Show "Last updated" timestamp from build metadata

**Update Strategy:**
- Data updates only on deployment (no client-side polling)
- Error state if the pg_featureserv API is unavailable during build

**Accessibility:**
- Semantic HTML (main, article, section)
- Color contrast > 4.5:1 for all text
- Keyboard navigation for all interactive elements
- Screen reader friendly metric labels

---

### 4.4 Interactive Barrier Map

**User Story:**
*As a biologist planning restoration work, I want to see all barriers in the watershed on a map, filtered by priority, so I can identify restoration opportunities.*

**Map Features:**
1. **Base Layers:** Satellite imagery (default), vector street map, terrain view, togglable
2. **Marker Layers:**
   - All barrier locations from pg_featureserv (fetched at build)
   - Habitat zones and watershed boundary
   - Only the top 20–30 structures labeled based on ranking outputs
3. **Filtering:**
   - Barrier type, priority classification, passability status
   - Client-side filter updates (no page reload)
4. **Interaction:**
   - Click barrier → popup with name, type, upstream habitat, priority, status
   - Zoom controls; zoom to watershed boundary
5. **Responsive:** Full-screen on desktop; touch-friendly controls on mobile

**Map Symbolization Requirements (Component 1):**
- Ranked structure status colors:
  - Rehabilitated barrier: green
  - Non-actionable barrier: red
  - Priority barrier: yellow
  - Data-deficient barrier: purple
  - Unassessed structure: gray/white
- Connectivity model colors:
  - Connected habitat: blue
  - Disconnected habitat: red
- Accessibility model linework:
  - Naturally accessible waterbodies: dark lines
  - Naturally inaccessible waterbodies: light lines

**Data Source:**
- `GET https://cabd-pro.cwf-fcf.org/bcfishpass/functions/postgisftw.wcrp_barrier_extent/items.json?watershed_group_code=HORS&barrier_type=`
- Fetched and validated at build time; deployed as static map-ready data artifacts
- All filtering, zooming, popups, and label interactions operate client-side on build-time data

> Specific mapping library, implementation, and performance optimization choices are architecture decisions recorded in `docs/adr/`.

---

### 4.5 Habitat Accessibility Curve (HAC)

**User Story:**
*As a project manager, I want to see which structures would unlock the most habitat if removed, so I can communicate ROI to funders.*

**Visualization:**
- Interactive chart: x-axis = structures ranked by habitat upstream; y-axis = cumulative km of accessible habitat
- Color-coded by priority; tooltip on hover (structure name, km gain, priority)
- Cross-linked with barrier map: click structure → highlight on map

**Data Processing:**
- Fetch barrier extent data from pg_featureserv at build time
- Validate and materialize the deployment dataset during the build
- Ranking and cumulative calculation performed at build time

**Component 3: Habitat Accumulation Summary Table**
- Based on Horsefly WCRP Table 8
- Required columns: Barrier ID, Site Name, Structure Status, Structure Rank, Average Habitat Upstream (km), Actual Habitat Upstream (km)
- Average habitat upstream: habitat gain averaged across sets / potential gain if passage is restored
- Actual habitat upstream: amount of habitat currently upstream of the structure

**Interactivity:**
- Cross-link: click structure → highlight on map
- Hover for details popup
- Export to CSV
- Sorting/filtering operates client-side on build-time data

---

### 4.6 Repository-Managed Content Pages and Approved Components

**Core Principle:** Editorial content determines what a page says and which approved components it includes; the application determines how those components render and behave.

**Content Pages:**
1. **Project Overview** – history, goals, partners, watershed ecology, species focus
2. **Glossary** – auto-indexed terms, definitions with images, filterable A–Z
3. **Restoration Methods** – strategies, habitat assessments, best practices
4. **Progress Reporting** – narrative plus build-time data-backed metrics; connectivity status sentences generated from configured `connectivity_status_types`
5. **Structure List Status Tables (Component 6)** – based on Horsefly Table 11; grouped by structure status; required columns: Barrier ID, Site Name, Watershed Name, Structure Type, Assessment Step, Next Steps, Notes, Supporting Links
6. **References** – bibliography, report links, downloadable PDFs

**Content and Workflow Requirements:**
- Editorial content is stored in the repository in portable formats (Markdown/MDX, YAML, JSON)
- Content changes are reviewed through a pull-request workflow before staging/production publication
- Approved interactive components may be configured by editors using structured blocks (YAML/JSON); editors do not write application logic or arbitrary executable code
- Build-time validation must reject unknown component types or invalid configuration before deployment
- The application is not the source of truth for model outputs; pg_featureserv remains authoritative

**Representative Approved Component Configuration (example):**
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

**Content Management Requirements:**
- The MVP must use a version-controlled, repository-managed content workflow
- The MVP must avoid recurring CMS subscription fees
- Content must support narrative pages, images, tables, references, glossary entries, watershed-specific content, and configuration for approved interactive components
- Editorial updates must be reviewable through a staged workflow before production publication
- The content workflow must preserve portable, exportable source files and support immutable release history
- Editorial content must not permit arbitrary executable JavaScript or JSX
- An optional browser-based editorial interface may be introduced for nontechnical editors after usability, authentication, and operational requirements are validated; this interface is an open dependency (see `docs/adr/0003`)
- Managed paid CMS products may be considered only in future phases when their operational benefits justify recurring cost; no vendor is prescribed in this document

> Content workflow and editor interface implementation details are architecture decisions recorded in `docs/adr/0002` and `docs/adr/0003`.

---

### 4.7 Navigation and Layout

**Header:**
- Logo (configurable per watershed)
- Watershed selector (dropdown)
- Version selector (dropdown)
- Main navigation: Overview | Glossary | Methods | Progress | References
- Mobile: hamburger menu
- Accessibility: skip-to-content link, correct heading hierarchy

**Footer:**
- Canadian Wildlife Federation branding
- Links: Terms, Privacy, Accessibility Statement
- Contact information

---

## 5. User Stories and Acceptance Criteria

### US-001: View Horsefly WCRP Dashboard (Current Version)
**As a** public stakeholder
**I want to** see current connectivity status and barrier information for the Horsefly River
**So that** I understand progress toward restoration goals

**Acceptance Criteria:**
- [ ] Dashboard loads within 2 seconds
- [ ] Displays connected/disconnected habitat and barrier counts from build-time data
- [ ] Generates one Component 4 sentence/metric output for each configured `connectivity_status_type`
- [ ] Connectivity sentence outputs are controlled by `connectivity_status_types`, not by `target_species` alone
- [ ] "Last updated" timestamp shows the build/deployment date
- [ ] Page is mobile-responsive
- [ ] All text meets WCAG AA contrast requirements

---

### US-002: Access Previous WCRP Versions
**As a** project partner
**I want to** view previous WCRP versions to track connectivity progress over time
**So that** I can demonstrate improvements to stakeholders and funders

**Acceptance Criteria:**
- [ ] Version dropdown shows all approved published versions with dates
- [ ] Clicking a version loads that exact immutable snapshot
- [ ] Current version is clearly identified
- [ ] Deployment date is shown for each version
- [ ] Historical versions cannot be edited
- [ ] Version selector works on mobile
- [ ] All historical versions remain permanently accessible at stable public URLs

---

### US-003: Explore Barriers on Interactive Map
**As a** biologist or restoration planner
**I want to** filter barriers by type and priority on a map
**So that** I can identify restoration opportunities

**Acceptance Criteria:**
- [ ] Map displays all barriers by default
- [ ] Only the top 20–30 ranked structures are labeled
- [ ] Structure status, connectivity, and accessibility symbolization follow documented color/line conventions
- [ ] Filter controls work without page reload
- [ ] Clicking a barrier shows name, type, upstream habitat, priority
- [ ] Mobile: map is usable on small screens
- [ ] All controls are keyboard-navigable

---

### US-004: Prepare New Model Release for Public
**As a** repository manager
**I want to** trigger a build when the project lead approves new model results
**So that** partners can access updated connectivity data

**Acceptance Criteria:**
- [ ] An automated validation and deployment workflow can be manually triggered
- [ ] Workflow fetches the latest model data from pg_featureserv and validates it
- [ ] Workflow loads the latest repository-managed editorial content
- [ ] Build completes and deploys to the staging/preview environment
- [ ] Staging environment is accessible to internal team and trusted partners for review
- [ ] A manual approval step promotes the staging build to production
- [ ] Production deployment receives version metadata and the previous version is archived at its stable URL
- [ ] Version selector on the live site shows the new version as current

> A future CMS adapter may be used to facilitate editorial content updates without changing these public rendering requirements; no specific product is prescribed.

---

### US-005: Access WCRP Content on Mobile
**As a** field biologist
**I want to** view methods, glossary, and progress on my phone
**So that** I have reference material in the field

**Acceptance Criteria:**
- [ ] All pages render correctly on phones (320 px+)
- [ ] Touch targets are at minimum 44×44 px
- [ ] Text is readable without zooming
- [ ] Map controls are usable on mobile
- [ ] Images and tables scale appropriately
- [ ] Lighthouse Mobile score > 90

---

### US-006: Review WCRP Reporting Tables
**As a** restoration planner
**I want to** review the standard WCRP summary and status tables for the active plan
**So that** I can compare habitat opportunity, structure status, and assessment follow-up in a consistent format

**Acceptance Criteria:**
- [ ] Component 3 Habitat Accumulation Summary Table matches the Horsefly Table 8 column set
- [ ] Component 3 distinguishes average habitat upstream from actual habitat upstream
- [ ] Component 6 Structure List Status Tables are grouped by structure status
- [ ] Component 6 tables match the Horsefly Table 11 column set
- [ ] Notes and supporting/external assessment links are retained in Component 6 outputs

---

## 6. Success Metrics and KPIs

### Performance Metrics
| Metric | Target | Measurement |
|---|---|---|
| Page Load Time (LCP) | < 2.5 s | Lighthouse, real user monitoring |
| First Contentful Paint | < 1.2 s | Lighthouse |
| Cumulative Layout Shift | < 0.1 | Lighthouse |
| Bundle Size (JS) | < 250 KB gzip | Build output analysis |
| Staging-to-Production | < 10 min | Automated workflow log |

### User Engagement
| Metric | Target | Measurement |
|---|---|---|
| Bounce Rate | < 30% | Analytics |
| Avg. Session Duration | > 3 min | Analytics |
| Map Interaction Rate | > 40% of users | Event tracking |
| Mobile Traffic | > 40% | Analytics |
| Version History Access | > 20% of users | Event tracking |

### Reliability
| Metric | Target | Measurement |
|---|---|---|
| Uptime | 99.9% | Hosting monitoring |
| Build Success Rate | 99% | Automated validation log |
| API Data Accuracy | 100% | Manual QA on each deployment |

### Accessibility
| Metric | Target | Measurement |
|---|---|---|
| WCAG 2.1 AA Compliance | 100% | Automated and manual audit |
| Lighthouse Accessibility | > 95 | Lighthouse |
| Keyboard Navigation | 100% of UI | Manual testing |

### Business Metrics
| Metric | Target | Measurement |
|---|---|---|
| Stakeholder Satisfaction | > 4/5 | Post-launch survey |
| Code Reusability | 80% across watersheds | Review |
| Time to Deploy New Watershed | < 4 hours | Process tracking |
| Update Deployment Time | 15–30 min (staging build + review) | Workflow log + manual steps |

---

## 7. Timeline and Milestones

### Phase 1: MVP Development (12 weeks)

| Week | Milestone | Deliverables |
|---|---|---|
| 1–2 | Project Setup and Architecture | Repository structure, content directory conventions, development environment, ADR review |
| 3–4 | Watershed Configuration System | Configuration schema, build-time API client, theming |
| 5–6 | Repository Content Workflow | Content structure, editorial templates, build-time rendering, preview workflow |
| 7–8 | Dashboard, Metrics, and Version Archive | Metric cards, version selector, archive publication |
| 9–10 | Interactive Map | Interactive map integration, filtering, responsive layout |
| 11–12 | Automated Validation, Staging/Production, Accessibility | Automated validation workflows, accessibility audit, staging-to-production approval flow |
| 12 | Launch | Production deployment, documentation, team training |

### Phase 2: Enhancement (Quarters 2–3)
- Optional browser-based editorial interface for nontechnical editors (subject to ADR-0003 decision)
- Multi-language UI (French)
- Advanced analytics and reporting
- Automated data validation

### Phase 3: Scale (Quarter 4+)
- Deploy 2–3 additional watersheds
- Community feedback integration
- Advanced search and discovery

---

## 8. Architecture Constraints and Decision References

Detailed technology selections, alternatives considered, rationale, and current status for all architecture decisions are recorded in [`docs/adr/`](./adr/). All ADRs are **Proposed** pending formal team decision.

| ADR | Decision Area | Status |
|---|---|---|
| [ADR-0001](./adr/0001-replace-quarto-with-nextjs-for-publishing.md) | Application framework to replace Quarto publishing workflow | Proposed |
| [ADR-0002](./adr/0002-use-git-based-content-management.md) | Git-based content management for MVP | Proposed |
| [ADR-0003](./adr/0003-evaluate-decap-as-optional-editorial-interface.md) | Optional editorial interface evaluation | Proposed |
| [ADR-0004](./adr/0004-keep-pg-featureserv-authoritative.md) | pg_featureserv as authoritative model-data source | Proposed |
| [ADR-0005](./adr/0005-fetch-model-data-at-build-time.md) | Build-time model data fetching | Proposed |
| [ADR-0006](./adr/0006-use-structured-component-blocks.md) | Structured component blocks for editorial content | Proposed |
| [ADR-0007](./adr/0007-use-pull-requests-and-staging-previews.md) | Pull-request and staging-preview review workflow | Proposed |
| [ADR-0008](./adr/0008-publish-immutable-releases-at-stable-urls.md) | Immutable releases at stable public URLs | Proposed |

---

## 9. Risk Analysis

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| pg_featureserv API unavailability during build | Low | High | Fallback to last approved dataset; build failure notification |
| Editorial workflow learning curve | Medium | Medium | Documentation, templates, and optional browser-based editor interface (subject to ADR-0003) |
| Version archive complexity | Medium | Medium | Clear release naming conventions; automated version metadata generation |
| Tight timeline with small team | High | High | Clear scope, MVP prioritization, no scope creep |
| Performance issues with large datasets | Low | High | Build-time data materialization; progressive loading |
| Browser compatibility | Low | Medium | Standard cross-browser testing; progressive enhancement |

---

## 10. Glossary

| Term | Definition |
|---|---|
| **WCRP** | Watershed Connectivity Restoration Plan |
| **Barrier** | Structure (dam, weir, ford, etc.) that impedes fish passage |
| **Habitat Connectivity** | Degree to which spawning/rearing habitat is accessible to anadromous fish |
| **pg_featureserv** | PostGIS spatial data API serving watershed barrier and habitat data; authoritative external dependency for model-backed data |
| **Git-Based Content Workflow** | An editorial content workflow in which content is stored as files in a version-controlled repository, reviewed through pull requests, and published via an automated build pipeline |
| **Approved Interactive Component** | A developer-maintained interactive element (map, dashboard, chart) that editorial content may configure using structured data blocks; editors do not define component behavior |
| **Build-Time Data** | Model data fetched from pg_featureserv and validated during the application build, then deployed as static artifacts for client-side interaction |
| **Architecture Decision Record (ADR)** | A document recording a proposed or accepted implementation decision, the alternatives considered, the rationale, tradeoffs, and open dependencies. See `docs/adr/`. |
| **Staging/Preview Environment** | A non-public deployment used for review and approval before production publication |
| **Production Environment** | The live public site accessed by stakeholders |
| **Version Archive** | The set of all past approved WCRP releases, each permanently publicly accessible at a stable URL |
| **Stakeholder** | Public user, conservation partner, Indigenous group, or government agency viewing the WCRP |

---

## 11. Appendices

### A. API Response Examples

#### Barrier Extent API
**Request:**
```
GET https://cabd-pro.cwf-fcf.org/bcfishpass/functions/postgisftw.wcrp_barrier_extent/items.json?watershed_group_code=HORS&barrier_type=
```

**Response (GeoJSON):**
```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "id": "12345",
      "geometry": {
        "type": "Point",
        "coordinates": [-120.123, 52.456]
      },
      "properties": {
        "barrier_name": "Example Dam",
        "barrier_type": "dam",
        "priority": "high",
        "passability_status": "confirmed",
        "upstream_habitat_km": 45.3
      }
    }
  ],
  "numberMatched": 287,
  "numberReturned": 10
}
```

#### Habitat Connectivity API
**Request:**
```
GET https://cabd-pro.cwf-fcf.org/bcfishpass/functions/postgisftw.wcrp_habitat_connectivity_status/items.json?watershed_group_code=HORS&habitat_type=
```

**Response (JSON):**
```json
{
  "features": [
    {
      "properties": {
        "metric_name": "accessible_spawningrearing_all",
        "value": 245.3,
        "unit": "km"
      }
    },
    {
      "properties": {
        "metric_name": "disconnected_spawningrearing_all",
        "value": 67.8,
        "unit": "km"
      }
    },
    {
      "properties": {
        "metric_name": "priority_barriers",
        "value": 42,
        "unit": "count"
      }
    }
  ]
}
```

### B. Watershed Configuration Example

```yaml
- plan_name: Horsefly
  plan_code: hors
  plan_schema: hors
  description: The Horsefly River is a tributary of the Quesnel River in central British Columbia.
  region: Central BC
  target_species: [CH, CO, SK]
  connectivity_status_types: [spawning_all, rearing_all, spawningrearing_all]
  filter_clause: >-
    watershed_group_code = 'HORS'
  api_config:
    base_url: https://cabd-pro.cwf-fcf.org/bcfishpass/functions/postgisftw
    endpoints:
      barrier_extent: wcrp_barrier_extent/items.json
      habitat_connectivity: wcrp_habitat_connectivity_status/items.json
  map_config:
    center: [-120.0, 52.3]
    zoom: 9
    bounds: [[-120.5, 51.8], [-119.5, 52.8]]
  theme:
    primary: "#008270"
    secondary: "#2d6a6a"
    accent: "#e67e22"
    neutral: "#f6f6f6"
  content:
    logo: images/horsefly-logo.png
    partner_logo: images/partners.png
  status: active
  launch_date: 2026-08-15
```

- `plan_schema`: database schema name for the configured plan
- `target_species`: supports backend processing; does not alone determine reporting sentences
- `connectivity_status_types`: one or more entries; each produces a corresponding Component 4 reporting sentence/metric output
- Each configuration entry is shared by all WCRPs generated from that plan configuration

---

## 12. Sign-Off

| Role | Name | Date | Signature |
|---|---|---|---|
| Product Owner | CWF Team | Aug 10, 2026 | TBD |
| Lead Developer | TBD | TBD | TBD |
| Project Manager | TBD | TBD | TBD |

---

**Document Control**
- Version: 1.4 (Revised: PRD/ADR boundary enforcement; architecture decisions moved to ADRs)
- Status: In Review
- Last Modified: August 10, 2026
- Next Review: Post-ADR formal team decision
