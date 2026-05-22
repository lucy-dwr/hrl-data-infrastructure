# Define Data Producers, the Central Data Team, and Synthesis Teams as core governance roles

> **Status:** Accepted  
> **Date:** 2026-01-01  
> **Decision makers:** Lucy Andrews, Louise Conrad, Pascale Goertler  
> **Consulted:** HRL Science Committee, Ashley Vizek  
> **Informed:** HRL Science Committee

## Context and problem statement

Healthy Rivers and Landscapes (HRL) data infrastructure depends on coordinated work across data collection, data publication, ingestion and standardization, storage and serving, analysis and synthesis, and communication of results.

These activities cannot be managed effectively by a single undifferentiated group. Different participants have different responsibilities, expertise, authority, and proximity to the data. Data Producers often understand how data were collected and what limitations apply. The Central Data Team is responsible for shared infrastructure, standards, ingestion workflows, storage, and serving. Synthesis Teams draw on domain expertise and use published and standardized data to conduct analyses, produce decision-support products, and communicate findings.

Without explicit governance roles, HRL data work could suffer from unclear ownership, inconsistent standards, duplicated effort, unsupported handoffs, and ambiguity about who is responsible for data quality, publication, infrastructure, analysis, and long-term stewardship.

HRL therefore needs a clear role model for assigning responsibility across the data lifecycle.

## Decision drivers

- Need to clarify who is responsible for different stages of the HRL data lifecycle
- Need to distinguish data production responsibilities from infrastructure and synthesis responsibilities
- Need to support consistent data publication, ingestion, standardization, storage, serving, and reuse
- Need to reduce ambiguity around ownership, review, stewardship, and escalation
- Need to support collaboration among project teams, technical staff, analysts, and governance bodies
- Need to make data workflows understandable to both technical and non-technical participants
- Need to align HRL data governance with reproducibility, transparency, FAIR principles, and CARE principles

## Considered options

- Define Data Producers, the Central Data Team, and Synthesis Teams as core governance roles
- Treat all HRL participants as shared data stewards without distinguishing roles
- Organize responsibilities separately for each project or dataset
- Assign most data lifecycle responsibilities to the Central Data Team

## Decision outcome

Chosen option: **Define Data Producers, the Central Data Team, and Synthesis Teams as core governance roles** because HRL data work requires differentiated responsibilities across the data lifecycle.

This role model clarifies that Data Producers are responsible for producing, documenting, quality-checking, and publishing data products; the Central Data Team is responsible for shared infrastructure, standards, ingestion, standardization, storage, serving, and technical stewardship; and Synthesis Teams are responsible for using data to conduct analysis, synthesis, reporting, and decision-support work.

These roles are functional roles, not necessarily separate organizations or job titles. A person or team may play more than one role depending on the dataset, workflow, or project. However, each workflow should make clear which role is responsible for each lifecycle stage and handoff.

### Consequences

Desirable:

- Responsibilities across the HRL data lifecycle are easier to assign and communicate
- Data Producers have clear expectations for data documentation, quality control, and publication
- The Central Data Team has a defined role in maintaining shared infrastructure and standards
- Synthesis Teams have a clear role as users and interpreters of curated data products
- Handoffs between publication, ingestion, storage, and analysis are easier to define
- Governance discussions can focus on roles and responsibilities rather than individual tools or datasets
- The role model supports consistent onboarding, documentation, and workflow design

Undesirable:

- Some workflows may involve participants who occupy multiple roles, creating potential ambiguity
- The role model may require additional explanation for participants unfamiliar with data governance terminology
- Responsibilities may need to be revisited as HRL staffing, infrastructure, and governance mature
- Role definitions may not resolve all decision-rights questions without additional process documentation

### Confirmation

Implementation of this decision can be confirmed by reviewing HRL documentation, repository guidance, data publication workflows, infrastructure plans, and synthesis workflows to determine whether responsibilities are mapped to the core governance roles.

Examples of confirmation include:

- HRL documentation defines Data Producers, the Central Data Team, and Synthesis Teams
- Data lifecycle guidance identifies which role is responsible for each lifecycle stage
- Repository templates and workflow documentation identify the responsible role or owner
- Data publication workflows describe Data Producer responsibilities
- Ingestion and standardization workflows describe Central Data Team responsibilities
- Analysis and reporting workflows describe Synthesis Team responsibilities
- Governance or escalation pathways identify when decisions should be elevated beyond the working role

## Pros and cons of the options

### Define Data Producers, the Central Data Team, and Synthesis Teams as core governance roles

Use a functional role model to assign responsibilities across HRL data production, infrastructure, and synthesis work.

Desirable:

- Clarifies responsibilities across the data lifecycle
- Separates data production, infrastructure stewardship, and synthesis responsibilities
- Supports consistent handoffs between lifecycle stages
- Makes governance easier to explain and document
- Allows responsibilities to be mapped to workflows without requiring each role to correspond to a specific job title
- Supports cross-team collaboration while maintaining clear ownership

Neutral:

- A single person or group may occupy multiple roles in some workflows
- Additional governance processes may still be needed for approval, prioritization, and escalation

Undesirable:

- Requires participants to understand and use shared role terminology
- May require periodic updates as HRL governance and staffing evolve
- May not fully resolve conflicts where roles overlap or responsibilities are shared

### Treat all HRL participants as shared data stewards without distinguishing roles

Emphasize collective stewardship without defining differentiated responsibilities.

Desirable:

- Reinforces that all participants have responsibilities for data quality, ethics, and reuse
- Avoids creating rigid role boundaries
- May feel inclusive and collaborative

Neutral:

- Shared stewardship remains an important principle even with differentiated roles

Undesirable:

- Does not clearly assign responsibility for publication, ingestion, infrastructure, or synthesis
- Makes handoffs ambiguous
- Increases risk that important tasks are assumed to be someone else's responsibility
- Makes it harder to design workflows, templates, review processes, and escalation paths
- Does not scale well as HRL data infrastructure becomes more complex
- Does not recognize that expertise may not be universally available for certain data lifecycle stages

### Organize responsibilities separately for each project or dataset

Allow each project, dataset, or synthesis effort to define its own roles and responsibilities.

Desirable:

- Allows role assignments to reflect local project needs
- Gives project teams flexibility
- May work for small or isolated workflows

Neutral:

- Some project-specific variation will still be necessary within the broader role model

Undesirable:

- Produces inconsistent expectations across HRL
- Makes program-level governance harder
- Makes onboarding and review more difficult
- Increases support burden
- Makes it harder to build shared infrastructure and standards
- Makes cross-project synthesis and reuse more difficult

### Assign most data lifecycle responsibilities to a Central Data Team

Centralize responsibility for data publication, ingestion, standardization, storage, serving, analysis support, and possibly synthesis within a Central Data Team.

Desirable:

- Provides a clear point of responsibility for many technical tasks
- May reduce variation in infrastructure and data management practices
- Can simplify some coordination and support workflows

Neutral:

- The Central Data Team should still own shared infrastructure, standards, and technical stewardship

Undesirable:

- Creates an unsustainable bottleneck
- Separates data quality and documentation from the people closest to data collection
- Reduces Data Producer accountability for publication-ready data products
- May make Synthesis Teams overly dependent on the Central Data Team
- Does not scale well across many datasets, projects, and analysis needs
- Risks treating the Central Data Team as a service desk rather than a governance and infrastructure function

## More information

This decision should be revisited if HRL governance roles change substantially, if new standing teams are created, or if implementation shows that additional roles are needed to describe recurring responsibilities.

Related ADRs:

- [ADR-001: Adopt the HRL data lifecycle as the organizing framework](adr-001-hrl-data-lifecycle.md)
- [ADR-002: Require standardized, reproducible HRL repositories with GitHub, environment management, CI/CD, and governance files](adr-002-standardized-reproducible-hrl-repositories.md)
- [ADR-004: Require static publication of data before ingestion, with EDI as the default repository](adr-004-static-publication-before-ingestion.md)
- [ADR-005: Allow Central Data Team-managed publication pathways for large or complex datasets](adr-005-central-data-team-managed-publication-pathways.md)
