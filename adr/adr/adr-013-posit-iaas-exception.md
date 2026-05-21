---
status: accepted
date: 2026-05-7
decision-makers: Lucy Andrews
consulted: John Spendlove
informed: Louise Conrad
---

# Treat Posit as a deliberate IaaS exception to the PaaS-first principle

## Context and Problem Statement

Healthy Rivers and Landscapes (HRL) data infrastructure follows a DWR-hosted, PaaS-first Azure architecture. This means that HRL should prefer managed Azure services for shared data infrastructure wherever practical, including managed object storage, managed databases, managed container execution, managed application hosting, managed secrets, and managed monitoring.

However, Posit Workbench and Posit Connect do not fit cleanly into this PaaS-first pattern. Posit Workbench and Posit Connect are server-based products that require installation, configuration, administration, and operation on Linux server infrastructure. Posit's Azure reference architectures for Workbench and Connect use Azure Virtual Machines, with additional managed services such as Azure Database for PostgreSQL or Azure NetApp Files in load-balanced or more robust configurations.

HRL and DWR nevertheless need Posit Workbench and Posit Connect because they provide an integrated data science development and publishing platform for R, Python, Shiny, Quarto, dashboards, APIs, notebooks, scheduled reports, and other analytical products. Posit is also expected to serve DWR programs beyond HRL, making it a broader DWR data science platform rather than an HRL-specific data engineering component.

Without an explicit architectural decision, the use of Azure Virtual Machines for Posit could appear to contradict the PaaS-first principle. HRL therefore needs to document Posit as a deliberate, justified IaaS exception to the PaaS-first Azure architecture.

## Decision Drivers

- Need to preserve the PaaS-first principle for HRL data engineering infrastructure
- Need to acknowledge that Posit Workbench and Posit Connect require server-based deployment and administration
- Need to use Posit Workbench and Posit Connect for data science development and analytical publishing
- Need to support R, Python, Shiny, Quarto, R Markdown, dashboards, APIs, notebooks, scheduled reports, and related analytical products
- Need to recognize that Posit will serve broader DWR data science needs beyond HRL
- Need to avoid incorrectly treating Posit's IaaS deployment as a general precedent for HRL infrastructure
- Need to separate Posit's platform administration from HRL-specific data engineering infrastructure
- Need to align Posit deployment with DWR Azure hosting, security, identity, networking, procurement, and operations requirements
- Need to document why this exception is justified and bounded
- Need to allow other IaaS exceptions only when similarly justified

## Considered Options

- Treat Posit as a deliberate IaaS exception to the PaaS-first principle
- Avoid Posit because it requires IaaS deployment
- Treat Posit's IaaS deployment as a general precedent for HRL infrastructure
- Attempt to replace Posit with custom PaaS-based Azure services
- Use only local development environments and ad hoc publishing workflows

## Decision Outcome

Chosen option: **Treat Posit as a deliberate IaaS exception to the PaaS-first principle** because Posit Workbench and Posit Connect provide necessary data science development and publishing capabilities that are not available through a directly equivalent PaaS service, while their deployment model requires server-based infrastructure.

Under this decision, Posit Workbench and Posit Connect may be deployed on Azure Virtual Machines or other approved IaaS-based infrastructure consistent with Posit's administrator guidance and DWR enterprise requirements. This exception applies specifically to Posit as a data science development and publishing platform.

This decision does not weaken the broader PaaS-first principle for HRL data engineering infrastructure. HRL should continue to prefer managed Azure services for object storage, databases, validation and transformation jobs, APIs, monitoring, secrets, and other infrastructure components where practical.

This decision also does not mean that Posit is part of the HRL data engineering stack. Posit remains a separate DWR data science platform that can consume HRL data services and publish analytical products, while the HRL Azure data engineering stack remains responsible for HRL-specific ingestion, validation, standardization, storage, serving, exports, and operational data management.

### Consequences

Desirable:

- HRL and DWR can use Posit Workbench and Posit Connect for data science development and publishing
- The PaaS-first principle remains intact for HRL data engineering infrastructure
- Posit's IaaS deployment is documented as a deliberate exception rather than an accidental contradiction
- Posit can be administered, funded, scaled, and governed as a broader DWR platform serving multiple programs
- HRL-specific infrastructure remains separate from the DWR Posit platform
- Analysts can use a platform designed for R, Python, Shiny, Quarto, R Markdown, dashboards, APIs, notebooks, and scheduled reports
- Posit-hosted analytical products can consume authoritative HRL data from PostgreSQL/PostGIS, APIs, or standardized exports
- Future IaaS proposals can be evaluated against this documented exception rather than treated as automatically acceptable

Undesirable:

- DWR must operate and support IaaS resources for Posit, including virtual machines and related infrastructure
- Posit requires server administration, patching, upgrades, monitoring, backups, security configuration, and platform support
- Posit may require additional managed services in more robust or load-balanced configurations
- Posit's operational model differs from the HRL PaaS-first data engineering stack
- Users and administrators may need guidance to understand why Posit is an exception rather than the default pattern
- Posit introduces licensing, procurement, platform administration, and user-support responsibilities
- HRL may need to coordinate with broader DWR platform administrators for Posit priorities, access, and configuration

### Confirmation

Implementation of this decision can be confirmed by reviewing Posit deployment documentation, HRL architecture documentation, and platform operations guidance to determine whether Posit is clearly documented as an IaaS exception.

Examples of confirmation include:

- Posit Workbench and Posit Connect are documented as server-based platforms deployed separately from the HRL data engineering stack
- Posit deployment uses Azure Virtual Machines or another approved IaaS-based pattern
- Posit platform documentation identifies required administration responsibilities, including operating system maintenance, upgrades, backups, monitoring, identity, networking, and security configuration
- HRL architecture documentation continues to describe the HRL data engineering stack as PaaS-first
- New HRL infrastructure components are not moved to IaaS simply because Posit uses IaaS
- Posit-hosted applications and reports consume HRL data services rather than acting as the authoritative HRL storage or ingestion layer
- Posit platform costs, administration, and user management are tracked separately from HRL-specific data engineering resources
- Any additional IaaS exceptions are documented in separate ADRs with their own rationale

## Pros and Cons of the Options

### Treat Posit as a deliberate IaaS exception to the PaaS-first principle

Allow Posit Workbench and Posit Connect to be deployed using Azure Virtual Machines or other approved IaaS-based infrastructure while preserving the PaaS-first principle for HRL data engineering infrastructure.

Desirable:

- Accurately reflects Posit's server-based deployment model
- Preserves the PaaS-first principle for other HRL infrastructure components
- Allows DWR to use Posit for broad data science development and publishing needs
- Documents the exception clearly for architecture, procurement, and governance review
- Prevents Posit's deployment model from becoming an uncontrolled precedent for unrelated IaaS choices
- Supports separation between the DWR Posit platform and HRL-specific data engineering infrastructure

Neutral:

- Requires coordination between HRL data infrastructure staff, DWR platform administrators, and Posit administrators
- May require a phased deployment from single-server to more robust or load-balanced architecture as usage grows
- Some supporting services may still be PaaS or managed services even if the core Posit servers are IaaS-based

Undesirable:

- Requires VM administration and platform operations
- Requires licensing, procurement, and ongoing support
- Introduces an architectural exception that must be explained and governed
- Creates a separate operational model from the HRL PaaS-first stack

### Avoid Posit because it requires IaaS deployment

Do not procure or deploy Posit Workbench and Posit Connect because their deployment model does not align with a strict PaaS-first architecture.

Desirable:

- Preserves a strict PaaS-first architecture without exceptions
- Avoids VM administration for Posit
- Avoids Posit licensing and platform support responsibilities
- Reduces platform diversity

Neutral:

- Some analytical products could still be developed and deployed through other Azure services or local workflows

Undesirable:

- Loses a platform specifically designed for R, Python, Shiny, Quarto, R Markdown, dashboards, APIs, notebooks, and scheduled analytical products
- Forces HRL or DWR to find or build alternative publishing paths for common scientific computing workflows
- May slow development and publication of decision-support tools
- Increases reliance on local environments, custom deployments, or ad hoc hosting
- Treats deployment model as more important than functional need
- Does not support broader DWR demand for a shared data science platform

### Treat Posit's IaaS deployment as a general precedent for HRL infrastructure

Allow the use of Posit on VMs to justify broader use of self-managed virtual machines across HRL data infrastructure.

Desirable:

- Provides flexibility to use familiar server-based deployment patterns
- May simplify deployment of some tools that are easier to run on VMs
- Reduces the need to evaluate managed-service alternatives for each component

Neutral:

- Some IaaS exceptions may be justified in the future

Undesirable:

- Weakens the PaaS-first principle
- Increases operational burden for patching, security, backups, monitoring, and reliability
- Makes infrastructure more dependent on custom server configuration
- Risks uncontrolled growth of VM-based systems
- Makes it harder for a small Central Data Team to maintain infrastructure sustainably
- Blurs the distinction between justified exceptions and default architecture patterns

### Attempt to replace Posit with custom PaaS-based Azure services

Build an equivalent data science development and publishing platform from managed Azure services.

Desirable:

- Could align more closely with a strict PaaS-first Azure architecture
- Could be highly customized to DWR and HRL requirements
- Might reduce dependence on a specialized vendor platform

Neutral:

- Some Azure PaaS services may still be useful for specialized applications or data engineering workflows

Undesirable:

- Would require substantial engineering effort to reproduce Workbench and Connect capabilities
- Would require custom support for R, Python, Shiny, Quarto, R Markdown, notebooks, dashboards, APIs, scheduling, authentication, deployment, and user environments
- Could delay delivery of user-facing analytical tools
- Would increase maintenance burden on DWR and HRL technical staff
- Could produce a less mature and less user-friendly platform than Posit
- May still require IaaS or container infrastructure for some analytical workloads

### Use only local development environments and ad hoc publishing workflows

Allow analysts to develop locally and publish applications or reports through manual, project-specific, or ad hoc methods.

Desirable:

- Avoids centralized platform deployment
- Avoids Posit licensing and VM administration
- Preserves flexibility for individual analysts
- Low initial infrastructure burden

Neutral:

- Local development may still be appropriate for exploratory work or individual analysis

Undesirable:

- Does not provide a shared development and publishing platform
- Makes reproducibility and dependency management harder
- Makes application publishing, scheduling, and access control inconsistent
- Increases reliance on individual machines and staff-specific knowledge
- Makes HRL and DWR analytical products harder to maintain over time
- Does not meet the need for a durable platform for Shiny apps, Quarto reports, APIs, notebooks, and scheduled products

## More Information

This decision should be revisited if Posit provides a fully managed PaaS deployment model acceptable to DWR, if DWR adopts a different enterprise data science platform that meets the same functional needs without IaaS deployment, if Posit is no longer used beyond HRL, or if the operational burden of Posit's IaaS deployment becomes unsustainable.

Related ADRs:

- [ADR-006: Use a DWR-hosted, PaaS-first Azure architecture for HRL data infrastructure](adr-006-dwr-hosted-paas-first-azure-architecture.md)
- [ADR-011: Procure and use Posit Workbench and Posit Connect for data science and application publishing](adr-011-posit-workbench-connect.md)
- [ADR-012: Separate the Azure data engineering stack from the Posit data science platform](adr-012-separate-azure-data-engineering-stack-from-posit.md)