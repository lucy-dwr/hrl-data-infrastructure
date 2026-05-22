# Adopt the HRL data lifecycle as the organizing framework

> **Status:** Accepted  
> **Date:** 2026-01-01  
> **Decision makers:** Lucy Andrews, Louise Conrad, Pascale Goertler  
> **Consulted:** HRL Science Committee, Ashley Vizek  
> **Informed:** HRL Science Committee

## Context and problem statement

Healthy Rivers and Landscapes (HRL) data infrastructure must support many different types of data work, including data collection, quality assurance, static publication, ingestion and standardization, storage and serving, analysis and synthesis, and communication of results.

Without a shared organizing framework, responsibilities across these activities can become ambiguous. Participating entities and people need a common model for understanding where data products are in the lifecycle and what standards apply at each stage.

The decision scope includes HRL program documentation, data governance, repository organization, infrastructure planning, data publication workflows, ingestion workflows, storage and serving patterns, and synthesis workflows.

## Decision drivers

- Need for a shared program-wide framework for data governance, data management, and infrastructure planning
- Need to support reproducible, citable, and reusable data products
- Need to distinguish data products at different stages of production, ranging from raw field collection to synthesis outputs
- Need to support both project-level data management and program-level synthesis
- Need to make HRL data workflows understandable to both technical and non-technical participants
- Need to align infrastructure design and data governance with FAIR and CARE principles

## Considered options

- Adopt the HRL data lifecycle as the organizing framework
- Organize HRL data work primarily by team or governance role
- Organize HRL data work primarily by technology platform or system
- Organize HRL data work separately for each project or dataset

## Decision outcome

Chosen option: **Adopt the HRL data lifecycle as the organizing framework** because it provides a shared model for describing how data move from collection through publication, ingestion, storage, synthesis, and use. This framework clarifies responsibilities, supports consistent governance, and allows infrastructure and documentation to be organized around durable stages of data work rather than around specific tools, teams, or individual projects.

### Consequences

Desirable:

- HRL participants have a shared vocabulary for discussing data work
- Responsibilities can be mapped to lifecycle stages
- The distinction between static publication and ongoing infrastructure-supported data services is made explicit
- Infrastructure planning can be tied to actual data workflows rather than individual technologies
- The framework supports consistent documentation, onboarding, and governance
- Lifecycle stages can be linked to standards, templates, repositories, and review processes

Undesirable:

- Some datasets or workflows may not fit neatly into a linear lifecycle
- The framework requires ongoing maintenance as HRL data systems and governance processes mature
- Participants may need guidance to understand how their work maps to the lifecycle

### Confirmation

Implementation of this decision can be confirmed by reviewing HRL documentation, repository organization, infrastructure plans, and workflow guidance to determine whether they consistently use the lifecycle stages as the organizing structure.

Examples of confirmation include:

- HRL documentation is organized around lifecycle stages
- Data governance roles are mapped to lifecycle responsibilities
- Data publication guidance distinguishes static publication from ingestion and storage/serving
- Infrastructure plans identify which components support which lifecycle stages
- Repository templates and workflow documentation refer to the relevant lifecycle stage or stages

## Pros and cons of the options

### Adopt the HRL data lifecycle as the organizing framework

Use a shared lifecycle model to organize HRL data governance, documentation, infrastructure, and workflows.

Desirable:

- Creates a common vocabulary across technical and non-technical participants
- Clarifies how project-level data products become program-level assets
- Separates durable data-management concepts from specific technologies
- Supports planning for infrastructure components that serve different lifecycle stages
- Makes it easier to identify gaps in standards, tooling, stewardship, and governance

Neutral:

- The lifecycle may need to be adapted for different data types and workflows

Undesirable:

- Lifecycle framing can appear more linear than real-world data work

### Organize HRL data work primarily by team or governance role

Organize documentation and infrastructure around the groups responsible for different activities, such as Data Producers, the Central Data Team, Synthesis Teams, and governance bodies.

Desirable:

- Responsibilities are visible
- Participants can quickly find guidance relevant to their role

Neutral:

- Role-based organization may still need lifecycle concepts to explain handoffs

Undesirable:

- It can obscure how data move across groups
- It may reinforce silos between data production, infrastructure, and synthesis
- Roles may evolve over time, making the structure less durable

### Organize HRL data work primarily by technology platform or system

Organize documentation and infrastructure around specific platforms, repositories, cloud services, databases, applications, and publication systems.

Desirable:

- Implementation details are easy to locate
- Technical teams can document operational responsibilities clearly

Neutral:

- Platform-specific documentation will still be needed within the broader architecture

Undesirable:

- Technology choices may change over time
- Platform-based organization can be difficult for non-technical participants to understand
- It may obscure governance responsibilities and data stewardship expectations
- It can focus attention on tools before clarifying the data workflow

### Organize HRL data work separately for each project or dataset

Allow each project, dataset, or synthesis effort to define its own workflow, documentation, and infrastructure approach.

Desirable:

- Project teams have flexibility
- Workflows can be tailored to specific scientific or operational needs

Neutral:

- Some project-specific variation will still be necessary

Undesirable:

- It creates inconsistent standards and expectations
- It makes program-level synthesis harder
- It increases support burden for the Central Data Team
- It makes data products less interoperable and harder to discover, reuse, and preserve
- It increases the risk of redundant or conflicting work and practices

## More information

This decision should be revisited if HRL data governance changes substantially, if the program adopts a different operating model, or if implementation shows that the lifecycle stages do not adequately describe HRL data workflows.

Related ADRs:

- [ADR-002: Require standardized, reproducible HRL repositories with GitHub, environment management, CI/CD, and governance files](adr-002-standardized-reproducible-hrl-repositories.md)
- [ADR-003: Define Data Producers, the Central Data Team, and Synthesis Teams as core governance roles](adr-003-governance-roles.md)
- [ADR-004: Require static publication of data before ingestion, with EDI as the default repository](adr-004-static-publication-before-ingestion.md)
- [ADR-005: Allow Central Data Team-managed publication pathways for large or complex datasets](adr-005-central-data-team-managed-publication-pathways.md)
- [ADR-006: Use a PaaS-first Azure architecture for HRL data infrastructure, hosted by DWR](adr-006-paas-first-azure-architecture.md)
