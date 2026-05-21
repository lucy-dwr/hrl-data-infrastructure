---
status: accepted
date: 2026-05-7
decision-makers: Lucy Andrews
consulted: John Spendlove
informed: Louise Conrad
---

# Separate the Azure data engineering stack from the Posit data science platform

## Context and Problem Statement

Healthy Rivers and Landscapes (HRL) data infrastructure must support two related but distinct categories of work.

First, HRL needs a data engineering stack for shared infrastructure functions such as data submission, validation, transformation, standardization, object storage, database storage, APIs, exports, and operational data serving. This stack is expected to be DWR-hosted in Azure and to use managed Azure services wherever practical.

Second, DWR needs a data science platform for analysts, scientists, and developers to conduct analysis, create reports, develop applications, publish dashboards, run scheduled analytical products, and communicate results. Posit Workbench and Posit Connect are intended to support this analyst-facing development and publishing work for HRL and for other DWR programs.

These two categories of work are connected, but they should not be collapsed into a single platform. The HRL Azure data engineering stack should provide curated, standardized, well-governed HRL data services. The Posit data science platform should consume those services and support reproducible analysis and publication across HRL and other DWR programs.

The platforms also differ in deployment model. The HRL data engineering stack follows a PaaS-first Azure architecture, while Posit Workbench and Posit Connect are expected to be deployed using IaaS-based infrastructure. This means Posit should be treated as a separate DWR platform with its own hosting, administration, cost model, access patterns, and operational responsibilities.

If the boundaries are unclear, Posit could be treated as a substitute for HRL data infrastructure, or the HRL Azure engineering services could become unnecessarily exposed to analysts who only need access to curated data. HRL-specific infrastructure could also become incorrectly coupled to a broader DWR data science platform that serves users and programs beyond HRL.

HRL therefore needs to explicitly separate the HRL Azure data engineering stack from the Posit data science platform while defining how the two interact.

## Decision Drivers

- Need to distinguish infrastructure for HRL data ingestion, validation, storage, and serving from infrastructure for analysis and publishing
- Need to recognize that Posit Workbench and Posit Connect will serve DWR programs beyond HRL
- Need to host and manage Posit separately from the HRL-specific data engineering stack
- Need to recognize that Posit is expected to use an IaaS deployment model, while the HRL data engineering stack is PaaS-first
- Need to prevent Posit Workbench and Posit Connect from being treated as the authoritative HRL data infrastructure layer
- Need to prevent the HRL Azure data engineering stack from becoming the primary user interface for analysts
- Need to support analysts with curated data access without requiring them to administer or understand Azure infrastructure
- Need to preserve clear responsibilities for the Central Data Team, analysts, application developers, data stewards, and platform administrators
- Need to support secure, governed access from Posit environments to curated data in Azure
- Need to maintain separation of concerns across storage, compute, databases, applications, and analytical products
- Need to support reproducible data science workflows while keeping shared HRL data infrastructure stable and maintainable
- Need to align with the DWR-hosted, PaaS-first Azure architecture and the decision to procure Posit Workbench and Posit Connect

## Considered Options

- Separate the HRL Azure data engineering stack from the DWR Posit data science platform
- Host Posit as part of the HRL data engineering stack
- Use Posit Workbench and Posit Connect as the primary HRL data infrastructure platform
- Use Azure data engineering services directly as the primary analyst development and publishing environment
- Build a single integrated platform that combines data engineering, analysis, and publishing responsibilities

## Decision Outcome

Chosen option: **Separate the HRL Azure data engineering stack from the DWR Posit data science platform** because HRL needs a stable, governed data infrastructure layer, while DWR also needs a broader analyst-facing data science development and publishing platform that serves HRL and other programs.

Under this decision, the HRL Azure data engineering stack is responsible for HRL-specific infrastructure functions such as object storage, validation, transformation, ingestion, PostgreSQL/PostGIS storage, custom APIs, exports, access controls, and operational data serving.

Posit Workbench and Posit Connect are responsible for analyst-facing development and publishing functions across HRL and other DWR programs, including R and Python development, Shiny applications, Quarto reports,dashboards, FastAPI and Plumber APIs, notebooks, scheduled reports, and other analytical products.

The two layers should integrate through governed access patterns. Posit environments may connect to curated HRL Azure data services, such as PostgreSQL/PostGIS, APIs, or standardized export files, but Posit should not become the authoritative storage or ingestion layer for HRL data. Likewise, HRL Azure infrastructure should support HRL data engineering and serving functions without requiring most analysts to interact directly with Azure resources.

Because Posit is expected to be IaaS-deployed and to serve broader DWR data science needs, it should be hosted and managed separately from the HRL PaaS-first data engineering stack. Its relationship to HRL should be as a DWR data science platform that can consume and publish HRL data products, not as an HRL-specific infrastructure component.

### Consequences

Desirable:

- HRL has a clearer separation of concerns between data engineering and data science work
- Posit can serve multiple DWR programs, not only HRL
- Posit can be governed, funded, administered, and scaled as a broader DWR data science platform
- HRL-specific data infrastructure is not tightly coupled to a platform serving broader DWR needs
- Posit's IaaS deployment model does not weaken the HRL data engineering stack's PaaS-first architecture
- Posit can focus on analysis, development, publishing, and communication
- Azure can focus on ingestion, validation, storage, serving, access control, and operational infrastructure
- Analysts can consume curated HRL data without needing to administer Azure resources
- The Central Data Team can maintain infrastructure boundaries and governance responsibilities
- Posit applications and reports can use authoritative data from PostgreSQL/PostGIS, APIs, or standardized exports
- The architecture avoids treating a publishing platform as a data infrastructure system
- The architecture avoids exposing unnecessary Azure complexity to analysts and scientists
- Security, access, and operational responsibilities can be documented separately for each layer

Undesirable:

- Integration between Posit and HRL Azure infrastructure must be designed, secured, documented, and maintained
- Users may need guidance to understand which platform is responsible for which function
- Some workflows may cross boundaries and require coordination between data engineers, analysts, and platform administrators
- Authentication, networking, database access, and secrets management may be more complex across layers
- Separate platforms may require separate support models, documentation, cost tracking, and operating procedures
- Data products can become confusing if authoritative sources, derived outputs, and published applications are not clearly labeled
- Because Posit serves broader DWR needs, HRL may not have full control over platform administration, governance, prioritization, or configuration decisions

### Confirmation

Implementation of this decision can be confirmed by reviewing HRL infrastructure documentation, Posit platform documentation, user guidance, deployment patterns, and published products to determine whether HRL Azure infrastructure and Posit have clearly separated responsibilities.

Examples of confirmation include:

- HRL Azure architecture documentation identifies storage, validation, transformation, database, API, and export responsibilities
- Posit documentation identifies Workbench as the DWR data science development environment and Connect as the DWR analytical publishing platform
- Posit is documented as serving HRL and other DWR programs, not as an HRL-only platform
- Posit hosting, administration, and cost tracking are documented separately from HRL-specific data engineering infrastructure
- Posit's IaaS deployment model is documented separately from the HRL PaaS-first Azure architecture
- Posit-hosted applications and reports connect to curated HRL data sources rather than unmanaged local files
- PostgreSQL/PostGIS, APIs, or standardized exports remain the authoritative sources for standardized HRL data consumed by Posit products
- Posit is not used as the primary location for HRL raw submissions, canonical operational records, or shared infrastructure storage
- Analysts have documented methods for connecting to approved Azure-hosted HRL data services
- Secrets, credentials, and access controls for cross-platform access are documented and governed
- System diagrams show HRL Azure data infrastructure and the DWR Posit data science/publishing platform as related but separate layers

## Pros and Cons of the Options

### Separate the HRL Azure data engineering stack from the DWR Posit data science platform

Use Azure for HRL-specific shared data engineering infrastructure and Posit for broader DWR analyst-facing development and publishing.

Desirable:

- Creates clear separation of concerns
- Keeps authoritative HRL data infrastructure independent from the analyst publishing platform
- Recognizes that Posit is a broader DWR platform, not HRL-only infrastructure
- Allows Posit to be hosted, governed, and administered independently from HRL-specific infrastructure
- Allows Posit's IaaS deployment model to remain a documented exception rather than changing HRL's PaaS-first data engineering architecture
- Allows each platform to do what it is best suited for
- Supports governed data access from analytical products
- Makes responsibilities easier to explain to technical and non-technical audiences
- Allows Azure infrastructure and Posit platform administration to evolve separately
- Reduces the risk of accidental platform sprawl or unclear ownership

Neutral:

- Requires integration work between the two platforms
- Some users may experience both systems as one workflow even though they are architecturally separate
- Some analytical products may require support from both data engineers and analysts

Undesirable:

- Requires clear documentation and user training
- Requires cross-platform authentication, networking, and secrets-management patterns
- May create coordination overhead between infrastructure and analytical publishing work
- Can produce confusion if derived analytical outputs are not clearly distinguished from authoritative data sources
- HRL may need to coordinate with broader DWR platform administrators for Posit-related decisions

### Host Posit as part of the HRL data engineering stack

Deploy and manage Posit Workbench and Posit Connect as components of the HRL data engineering stack.

Desirable:

- Could make Posit feel closely integrated with HRL data services
- Could simplify some HRL-specific cost tracking and governance decisions
- Could give HRL more direct control over Posit configuration for HRL workflows

Neutral:

- Posit should still integrate with HRL data services

Undesirable:

- Incorrectly treats a broader DWR data science platform as HRL-only infrastructure
- Couples HRL-specific data engineering services to a platform intended to serve multiple DWR programs
- Makes HRL responsible for a broader analyst platform beyond its own data infrastructure needs
- Blurs the boundary between PaaS-first HRL data engineering and IaaS-deployed Posit hosting
- Could create confusion about whether Posit is governed by HRL data infrastructure decisions or broader DWR platform decisions
- Makes future scaling, funding, access control, and administration harder to separate

### Use Posit Workbench and Posit Connect as the primary HRL data infrastructure platform

Use Posit not only for data science development and publishing but also as the main platform for storage, ingestion, validation, and operational data serving.

Desirable:

- Provides a familiar interface for R-oriented analysts
- Could simplify some workflows by keeping development, execution, and publication close together
- May reduce the number of systems users interact with for small workflows

Neutral:

- Posit may host scripts, reports, applications, APIs, and scheduled jobs that interact with data infrastructure

Undesirable:

- Posit is not designed to serve as the main object storage, database, ingestion, and infrastructure governance layer
- Could blur the distinction between analytical products and authoritative HRL data infrastructure
- Could make operational data storage dependent on analyst-facing publishing tools
- May complicate data governance, access control, provenance, and long-term stewardship
- Does not provide the same fit as Azure services for object storage, managed databases, infrastructure integration, and platform operations
- Could overload Posit administration with data engineering responsibilities

### Use Azure data engineering services directly as the primary analyst development and publishing environment

Ask analysts to use Azure services directly for development, application hosting, reporting, dashboards, and publication.

Desirable:

- Keeps development and infrastructure in one cloud environment
- Could use Azure-native services for identity, deployment, monitoring, and application hosting
- May be appropriate for some custom applications or specialized engineering workflows

Neutral:

- Some Azure-native application hosting will still be appropriate for products that do not fit Posit well

Undesirable:

- Requires analysts to understand and use cloud infrastructure concepts and Azure-specific resources that are not central to their scientific work
- Makes R/Shiny/Quarto publishing more complex
- Increases support burden for the Central Data Team and DWR infrastructure staff
- Could slow down analytical product development and publication
- Requires more custom engineering to reproduce what Posit provides for open-source data science workflows
- May be less accessible to analysts with limited cloud engineering experience

### Build a single integrated platform that combines data engineering, analysis, and publishing responsibilities

Design one unified HRL platform that manages ingestion, storage, validation, analysis, publishing, and applications.

Desirable:

- Could provide one conceptual platform for HRL users
- Might reduce perceived fragmentation
- Could allow tightly integrated workflows if designed and resourced well

Neutral:

- Users may still experience multiple services through a unified documentation or access layer

Undesirable:

- Increases complexity and operational risk
- Blurs important responsibility boundaries
- Requires HRL to build and maintain custom integration across many different functions
- Makes governance, access control, and platform ownership harder to define
- Could slow implementation by trying to solve all needs in one architecture
- Makes it harder to replace or evolve individual components over time
- Does not acknowledge that Posit is intended to serve broader DWR data science needs

## More Information

This decision should be revisited if Posit becomes capable of directly providing required data engineering infrastructure functions, if Azure services become unsuitable for HRL data engineering needs, if DWR adopts an enterprise platform that unifies these layers without sacrificing governance and reproducibility, if Posit is no longer used beyond HRL, or if implementation shows that the separation creates excessive operational burden.

Related ADRs:

- [ADR-001: Adopt the HRL data lifecycle as the organizing framework](adr-001-hrl-data-lifecycle.md)
- [ADR-006: Use a DWR-hosted, PaaS-first Azure architecture for HRL data infrastructure](adr-006-dwr-hosted-paas-first-azure-architecture.md)
- [ADR-007: Use Azure Storage / ADLS Gen2 as the raw, intermediate, export, and archival object storage backbone](adr-007-azure-storage-adls-gen2-object-storage-backbone.md)
- [ADR-009: Use PostgreSQL/PostGIS as the authoritative operational store for standardized spatial data](adr-009-postgresql-postgis-authoritative-operational-store.md)
- [ADR-010: Publish standardized export files alongside the authoritative database](adr-010-standardized-export-files.md)
- [ADR-011: Procure and use Posit Workbench and Posit Connect for data science and application publishing](adr-011-posit-workbench-connect.md)
- [ADR-013: Treat Posit as a deliberate IaaS exception to the PaaS-first principle](adr-013-posit-iaas-exception.md)