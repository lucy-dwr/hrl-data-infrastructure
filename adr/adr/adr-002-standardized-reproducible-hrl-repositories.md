---
status: proposed
date: 2026-05-21
decision-makers: 
consulted: HRL Science Committee
informed: HRL Science Committee
---

# Require semi-standardized, reproducible HRL repositories with GitHub, environment management, CI/CD, and governance files

## Context and Problem Statement

Healthy Rivers and Landscapes (HRL) data infrastructure depends on many repositories for documentation, schemas, validation code, data product generation, data pipelines, databases, APIs, applications, and analysis workflows. These repositories are expected to support scientific reproducibility, long-term maintainability, collaboration across teams, and transparent stewardship of shared data products and program infrastructure.

Without shared repository expectations, HRL projects could develop inconsistent structures, missing documentation, unclear ownership, undocumented dependencies, unreproducible products, and uneven review practices. This would make repositories harder to reuse, maintain, onboard into, and evaluate for reproducibility or governance readiness.

HRL therefore needs a standard approach for repository organization and development practices. The standard should support reproducible computational work, clear governance, open-source readiness where appropriate, and consistent expectations for documentation, dependency management, review, and automation.

## Decision Drivers

- Need to make HRL repositories understandable, maintainable, and reusable across teams
- Need to support reproducible data publication, ingestion, analysis, and synthesis workflows
- Need to reduce variation in repository structure, documentation, and governance practices
- Need to make ownership, contribution pathways, licensing, and review expectations explicit
- Need to support CI/CD for automated checks, documentation builds, validation workflows, and deployment workflows
- Need to capture software and analytical dependencies so that workflows can be rerun in the future
- Need to support onboarding for contributors with varying levels of technical experience
- Need to align repository practices with HRL data governance, FAIR and CARE principles, and long-term stewardship

## Considered Options

- Require standardized, reproducible HRL repositories with GitHub, environment management, CI/CD, and governance files
- Recommend shared repository practices but allow each repository to decide which practices to adopt
- Allow each project or team to define its own repository structure and development practices

## Decision Outcome

Chosen option: **Require standardized, reproducible HRL repositories with GitHub, environment management, CI/CD, and governance files** because HRL repositories are part of the program's data infrastructure, not only individual project workspaces. Standardized repository practices make HRL work easier to review, maintain, reuse, and transfer across staff, teams, and governance contexts.

This decision does not require every repository to be identical. Repository templates, minimum required files, dependency management, and CI/CD workflows may vary by repository type. For example, a schema repository, a data publication repository, a validation code repository, and a web application repository may have different internal structures. Additionally, the requirements establish minimum patterns, and repositories may evolve beyond minimum standards as necessitated by functional requirements. However, each repository should follow shared HRL expectations for minimum documentation, reproducibility, governance, and maintainability.

### Consequences

Desirable:

- HRL repositories will be easier for contributors and reviewers to understand
- Repository ownership, contribution expectations, and licensing will be more explicit
- Reproducible workflows will be easier to rerun, review, audit, and modify
- Shared scaffolding will reduce setup time for new repositories
- CI/CD can provide automated checks for documentation, code quality, tests, schema validation, and deployment workflows
- Environment management will reduce dependency drift and improve long-term reproducibility
- Consistent repository practices will make HRL technical work more maintainable across staff transitions
- Repository standards will support open-source readiness and public transparency

Undesirable:

- Repository templates and template files will need to be created up front
- Contributors may need training in GitHub, dependency management, CI/CD, and repository governance files
- Some lightweight or exploratory projects may experience the standards as burdensome
- Standards and templates will require maintenance as HRL practices mature
- Over-standardization could discourage appropriate variation among different repository types

### Confirmation

Implementation of this decision can be confirmed by reviewing HRL repositories to determine whether they follow shared expectations for structure, documentation, reproducibility, governance, and automated checks.

Examples of confirmation include:

- Repositories include a clear `README.md`
- Repositories include license information when appropriate
- Repositories include contribution guidance when collaborative development is expected
- Repositories include governance or ownership files, such as `CODEOWNERS`, when appropriate
- Repositories include dependency/environment management, such as lockfiles, containers, requirements files, or equivalent tools
- Repositories include CI/CD workflows for relevant automated checks or deployment tasks
- Repositories include clear documentation for how to rerun important workflows
- Repositories use consistent directory structures or templates appropriate to their repository type
- Repositories distinguish exploratory work from production, publication, or infrastructure workflows

## Pros and Cons of the Options

### Require standardized, reproducible HRL repositories with GitHub, environment management, CI/CD, and governance files

Require HRL repositories to follow shared expectations for structure, documentation, dependency management, automated checks, and governance files.

Desirable:

- Creates consistent expectations across HRL technical work
- Supports reproducibility, maintainability, and review
- Makes repositories easier to onboard into and transfer across staff
- Enables automated checks and deployment workflows
- Supports open-source readiness and transparent stewardship
- Reduces the risk that important workflows depend on undocumented local environments or individual knowledge

Neutral:

- Repository standards may need to vary by repository type
- Some requirements may be phased in over time
- Some repositories may need exceptions when they are exploratory, temporary, or not intended for reuse

Undesirable:

- Requires more upfront effort than ad hoc repository creation
- Requires training and support for contributors unfamiliar with GitHub, CI/CD, or environment management
- Requires ongoing maintenance of templates and standards
- May feel overly formal for small or early-stage projects

### Recommend shared repository practices but allow each repository to decide which practices to adopt

Provide guidance, examples, and templates, but do not require repositories to follow them.

Desirable:

- Gives teams flexibility
- Reduces initial burden for small projects
- Allows standards to evolve through practice before becoming requirements
- May be easier to adopt in early stages of HRL infrastructure development

Neutral:

- Some repositories may voluntarily adopt strong practices
- This approach may be useful during an initial transition period

Undesirable:

- Leads to uneven repository quality and maintainability
- Makes reproducibility dependent on individual team practices
- Makes onboarding and review harder
- Increases long-term support burden for the Central Data Team
- Makes it harder to determine whether a repository is ready for publication, production use, or program-level reliance

### Allow each project or team to define its own repository structure and development practices

Allow repository structure, documentation, dependency management, and governance practices to be determined independently by each project or team.

Desirable:

- Maximizes local flexibility
- Allows teams to use familiar workflows
- Reduces centralized coordination needs in the short term

Neutral:

- May be acceptable for short-lived exploratory work that is not intended for reuse or publication

Undesirable:

- Produces inconsistent and hard-to-maintain repositories
- Makes program-level reproducibility difficult
- Increases dependency on individual staff knowledge
- Makes it harder to review, reuse, or publish work
- Increases the risk of missing licenses, contribution guidance, dependency records, or automated checks
- Makes it harder to build a coherent HRL technical ecosystem

## More Information

This decision should be revisited if HRL repository standards become too burdensome for common workflows, if DWR adopts organization-wide repository standards that supersede HRL-specific practices, or if implementation shows that different repository classes need separate ADRs.

Related ADRs:

- [ADR-001: Adopt the HRL data lifecycle as the organizing framework](adr-001-hrl-data-lifecycle.md)
- [ADR-003: Define Data Producers, the Central Data Team, and Synthesis Teams as core governance roles](adr-003-governance-roles.md)
- [ADR-004: Require static publication of data before ingestion, with EDI as the default repository](adr-004-static-publication-before-ingestion.md)
- [ADR-015: Split the HRL spatial data pipeline across multiple repositories rather than a monorepo](adr-015-multiple-repositories.md)