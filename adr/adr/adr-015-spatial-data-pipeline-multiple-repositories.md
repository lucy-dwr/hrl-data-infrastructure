---
status: accepted
date: 2026-05-14
decision-makers: Lucy Andrews
consulted: Ashley Vizek
informed:
---

# Split the HRL spatial data pipeline across multiple repositories rather than a monorepo

## Context and Problem Statement

Healthy Rivers and Landscapes (HRL) spatial data infrastructure includes several related but distinct components. These include architecture documentation, schema definitions, validation code, ingestion and transformation workflows, database migrations, API or data-serving code, export workflows, map applications, and user-facing documentation.

These components are connected, but they do not all have the same purpose, audience, release cycle, ownership model, deployment pathway, or maturity level. For example, a schema repository may need careful review and versioning because changes affect data submitters and validation workflows. A validation-code repository may need automated tests and container builds. A database repository may need migration management. An application repository may need a separate deployment workflow. Documentation repositories may need editorial review and static-site publishing.

HRL therefore needs to decide whether to organize the spatial data pipeline in a single monorepo or across multiple repositories with clear boundaries.

## Decision Drivers

- Need to maintain separation of concerns across schemas, validation code, infrastructure, databases, APIs, applications, and documentation
- Need to support different release cycles for different components
- Need to allow repository-specific CI/CD workflows, tests, permissions, and review processes
- Need to avoid coupling schema changes, pipeline code changes, infrastructure changes, and application changes unnecessarily
- Need to make repositories easier for contributors to understand and maintain
- Need to support long-term stewardship by making ownership and responsibility clear
- Need to support open-source readiness where appropriate
- Need to avoid a large, complex repository that becomes difficult to navigate or govern
- Need to align repository structure with HRL reproducibility and governance standards

## Considered Options

- Split the HRL spatial data pipeline across multiple repositories rather than a monorepo
- Use a single monorepo for the entire HRL spatial data pipeline
- Use one repository per dataset, project, or application without a coordinated repository architecture
- Keep most spatial data pipeline code and documentation in local or informal working locations

## Decision Outcome

Chosen option: **Split the HRL spatial data pipeline across multiple repositories rather than a monorepo** because the pipeline includes distinct components with different responsibilities, audiences, and deployment patterns.

Under this decision, HRL spatial data infrastructure should be organized into a small set of purpose-specific repositories. Repository boundaries should reflect meaningful separation of concerns, not arbitrary fragmentation. Expected repository classes may include architecture and planning documentation, schema definitions, validation and ingestion code, database migrations, API or data-serving code, application code, and user-facing documentation.

This decision does not mean that every small component must have its own repository. Related components may be grouped when they share ownership, release cycles, deployment workflows, and development practices. However, components with substantially different purposes or operational requirements should not be forced into a single monorepo.

### Consequences

Desirable:

- Repository boundaries can reflect real architectural and governance boundaries
- Schemas, validation code, databases, applications, and documentation can evolve on appropriate timelines
- CI/CD workflows can be tailored to each repository's function
- Repository permissions and review expectations can be managed more precisely
- Contributors can work in smaller, more focused repositories
- Open-source readiness, licensing, and governance files can be handled appropriately by repository type
- Changes to one component are less likely to create unnecessary noise or risk in unrelated components
- The architecture remains easier to explain, maintain, and evolve over time

Undesirable:

- Cross-repository coordination is required when changes affect multiple components
- Version compatibility between schemas, validation code, database migrations, and applications must be managed explicitly
- Contributors may need guidance on which repository to use for different tasks
- Shared conventions, templates, and documentation must be maintained across repositories
- CI/CD and release automation may be duplicated unless common patterns are documented or templated
- Too many repositories could create fragmentation if boundaries are not carefully managed

### Confirmation

Implementation of this decision can be confirmed by reviewing the HRL spatial data infrastructure repositories to determine whether major components are organized into purpose-specific repositories with clear responsibilities and documented relationships.

Examples of confirmation include:

- The schema is maintained in a dedicated repository or clearly separated repository area
- Validation and ingestion code are maintained separately from user-facing documentation and application code
- Database migrations or database-management code are maintained in a repository with appropriate review and deployment controls
- Application repositories have deployment workflows distinct from schema or validation repositories
- Documentation explains how repositories relate to each other
- Repository README files identify each repository's purpose, maintainers, and role in the spatial data pipeline
- Cross-repository dependencies, such as schema versions used by validation code, are documented
- Repository templates or scaffolding enforce shared HRL expectations without requiring a monorepo

## Pros and Cons of the Options

### Split the HRL spatial data pipeline across multiple repositories rather than a monorepo

Organize the pipeline into multiple purpose-specific repositories with clear boundaries.

Desirable:

- Supports separation of concerns
- Allows different components to have different release cycles
- Makes repository ownership and review responsibilities clearer
- Allows tailored CI/CD workflows by repository type
- Keeps repositories smaller and easier to navigate
- Reduces unnecessary coupling between schemas, validation code, databases, applications, and documentation
- Supports open-source readiness and governance expectations by repository type

Neutral:

- Requires conventions for repository naming, documentation, dependency management, and cross-repository coordination
- Some repositories may remain small, especially early in implementation
- Some components may be grouped if they share ownership and release cycles

Undesirable:

- Requires explicit coordination across repositories
- Requires version compatibility management
- May create overhead if too many repositories are created too early
- Contributors may need onboarding to understand the repository ecosystem

### Use a single monorepo for the entire HRL spatial data pipeline

Place schemas, validation code, ingestion workflows, database code, APIs, applications, documentation, and infrastructure code in one repository.

Desirable:

- Provides one location for all related work
- Can simplify some cross-component changes
- Makes it easier to search across the full codebase
- May simplify initial setup for a small team

Neutral:

- A monorepo may work when components are tightly coupled, share contributors, and have the same release and deployment model

Undesirable:

- Blurs boundaries between components with different purposes and maturity levels
- Makes repository permissions and review workflows harder to tailor
- Can make CI/CD complex as more components are added
- Makes the repository harder to navigate for contributors who only need one component
- Increases risk that unrelated changes are bundled together
- Can make releases and versioning harder when components should evolve independently
- Does not fit well with separate schema, infrastructure, application, and documentation responsibilities

### Use one repository per dataset, project, or application without a coordinated repository architecture

Allow each dataset, project, or application to create its own repository independently, without a planned repository ecosystem.

Desirable:

- Gives teams flexibility
- Allows rapid repository creation for specific needs
- Keeps individual repositories narrowly scoped

Neutral:

- Some project- or dataset-specific repositories may still be appropriate

Undesirable:

- Produces inconsistent repository structures and practices
- Makes it harder to locate authoritative schemas, validation code, or shared infrastructure components
- Increases duplication of code and documentation
- Makes dependency management and cross-repository coordination harder
- Weakens shared HRL development standards
- Can create fragmentation and unclear stewardship responsibilities

### Keep most spatial data pipeline code and documentation in local or informal working locations

Use local folders, shared drives, desktop GIS projects, ad hoc scripts, or informal documentation instead of a managed repository architecture.

Desirable:

- Low initial overhead
- Familiar to users who are not comfortable with GitHub
- May be useful for early exploration or temporary drafting

Neutral:

- Local exploratory work may still occur before code or documentation is promoted into managed repositories

Undesirable:

- Does not support reproducible or maintainable infrastructure
- Makes code review, version control, collaboration, and automation difficult
- Increases risk of lost knowledge and undocumented dependencies
- Makes onboarding and handoff harder
- Does not support CI/CD, release management, or open-source readiness
- Is not appropriate for shared HRL program infrastructure

## More Information

This decision should be revisited if the repository ecosystem becomes too fragmented, if cross-repository coordination becomes a major implementation burden, if HRL adopts a broader organizational repository strategy that supersedes this approach, or if some components become tightly coupled enough to justify consolidation.

Related ADRs:

- [ADR-002: Require standardized, reproducible HRL repositories with GitHub, environment management, CI/CD, and governance files](adr-002-standardized-reproducible-hrl-repositories.md)
- [ADR-006: Use a DWR-hosted, PaaS-first Azure architecture for HRL data infrastructure](adr-006-dwr-hosted-paas-first-azure-architecture.md)
- [ADR-007: Use Azure Storage / ADLS Gen2 as the raw, intermediate, export, and archival object storage backbone](adr-007-azure-storage-adls-gen2-object-storage-backbone.md)
- [ADR-008: Use Azure Container Apps Jobs for validation and transformation workflows](adr-008-container-apps-jobs-validation-transformation.md)
- [ADR-009: Use PostgreSQL/PostGIS as the authoritative operational store for standardized spatial data](adr-009-postgresql-postgis-authoritative-operational-store.md)
- [ADR-016: Use LinkML as the source-of-truth schema language for restoration spatial data](adr-016-linkml-source-of-truth-schema.md)