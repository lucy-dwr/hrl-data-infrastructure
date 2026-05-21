---
status: accepted
date: 2026-04-28
decision-makers: Lucy Andrews, Louise Conrad
consulted: DISE divisional leadership
informed:
---

# Procure and use Posit Workbench and Posit Connect for data science and application publishing

## Context and Problem Statement

Healthy Rivers and Landscapes (HRL) data infrastructure must support not only data storage and serving, but also the practical work of scientific computing, data analysis, reproducible reporting, and application publishing. HRL scientists, analysts, and data engineers need an environment where they can develop code, access shared data resources, collaborate on analytical workflows, and publish products such as Shiny applications, Quarto reports, dashboards, APIs, and scheduled analytical outputs.

HRL data science work is expected to rely heavily on open-source tools, especially R, Shiny, Quarto, Python, FastAPI, Plumber, and related scientific and geospatial libraries. Analysts need a platform that supports these tools directly and allows analytical products to move from development to publication without requiring each project to invent its own deployment pathway.

Local desktop environments alone are not sufficient for shared HRL data science and publishing needs. They make dependency management, shared access, scalable compute, scheduled execution, application hosting, and reproducibility harder to sustain across teams. General cloud infrastructure can host custom development and deployment environments, but would require HRL or DWR to assemble, secure, maintain, and support many pieces that Posit Workbench and Posit Connect already provide for open-source data science workflows.

HRL therefore needs a shared data science development and publishing platform that supports common open-source analytical workflows while integrating with DWR-hosted infrastructure.

## Decision Drivers

- Need to support R, Shiny, Quarto, Streamlit, Python, FastAPI, Plumber, and common open-source scientific libraries
- Need to provide hosted development environments for HRL data scientists, analysts, and developers
- Need to support publication of applications, dashboards, reports, APIs, notebooks, and scheduled jobs
- Need to reduce the burden of custom-building and maintaining development and publishing infrastructure
- Need to support reproducible analytical workflows and environment management
- Need to provide a clear path from analysis development to publication and sharing
- Need to support collaboration among technical users with varying levels of infrastructure expertise
- Need to integrate with DWR-hosted Azure infrastructure and shared HRL data services
- Need to support internal and potentially public-facing communication of data products and decision-support tools
- Need to select a platform that is well aligned with HRL's existing R-centered scientific computing practices

## Considered Options

- Procure and use Posit Workbench and Posit Connect for data science and application publishing
- Use local desktop development environments and manual publication workflows
- Build a custom cloud development and publishing platform from Azure services
- Use general-purpose notebook or machine learning platforms
- Use proprietary business intelligence or GIS application platforms as the primary publishing environment

## Decision Outcome

Chosen option: **Procure and use Posit Workbench and Posit Connect for data science and application publishing** because these products provide an integrated platform for open-source data science development and publishing that aligns with HRL's analytical workflows, existing R/Shiny/Quarto practices, and need for maintainable deployment paths.

Under this decision, Posit Workbench will serve as the shared cloud-hosted development environment for HRL data science and analytical development. Posit Connect will serve as the publishing platform for analytical products, including Shiny applications, Quarto reports, dashboards, APIs, notebooks, scheduled reports, and related decision-support products.

This decision does not mean that all HRL infrastructure will run on Posit. The Azure data engineering stack remains responsible for ingestion, validation, standardized storage, object storage, databases, and core data serving infrastructure. Posit is the analyst-facing development and publishing platform that consumes and publishes from the shared data infrastructure.

This decision also does not eliminate the use of GitHub, CI/CD, local development, or other deployment tools. Posit Workbench and Posit Connect provide the primary shared environment for HRL data science development and application publishing, while other tools continue to support source control, automation, infrastructure deployment, and specialized workflows.

### Consequences

Desirable:

- HRL data scientists and analysts have a shared cloud-hosted development environment
- HRL can support R, Shiny, Streamlit, Quarto, Python, FastAPI, Plumber, and common open-source analytical libraries
- Analytical products can be published through a standard platform rather than ad hoc hosting
- Shiny applications, reports, dashboards, APIs, notebooks, and scheduled outputs can share a common publishing workflow
- Posit Connect provides a clearer deployment path for scientific applications and decision-support tools
- Workbench can reduce dependence on local machine configuration for shared analytical workflows
- The platform aligns with HRL's existing R-centered scientific computing practices
- Analysts can consume curated data from the Azure data engineering stack without needing to administer Azure infrastructure directly
- The platform supports reproducibility and collaboration when paired with GitHub and environment management practices

Undesirable:

- Posit Workbench and Posit Connect require procurement, licensing, hosting, administration, and user support
- Posit introduces a specialized platform that DWR must operate or support
- The platform requires an IaaS deployment pattern that differs from the broader PaaS-first Azure architecture
- Users may need training on Workbench, Connect, publishing workflows, permissions, and deployment practices
- Posit is not a substitute for source control, data governance, database administration, or infrastructure-as-code
- Costs must be justified and managed as user counts, applications, and workloads grow
- HRL may become dependent on Posit-specific publishing workflows for some analytical products

### Confirmation

Implementation of this decision can be confirmed by reviewing HRL platform procurement, deployment, user guidance, and published analytical products to determine whether Posit Workbench and Posit Connect are being used as the primary shared data science development and publishing platform.

Examples of confirmation include:

- Posit Workbench and Posit Connect are procured, deployed, or approved for deployment
- HRL users have documented guidance for using Workbench for analytical development
- HRL users have documented guidance for publishing to Connect
- Shiny applications, Quarto reports, dashboards, APIs, notebooks, or scheduled reports are deployed through Connect
- Workbench environments are integrated with GitHub and appropriate dependency-management practices
- Posit-hosted applications or reports consume curated data from HRL shared infrastructure where appropriate
- Platform administration, user access, authentication, backups, and support responsibilities are documented
- The relationship between Posit and the Azure data engineering stack is documented clearly

## Pros and Cons of the Options

### Procure and use Posit Workbench and Posit Connect for data science and application publishing

Use Posit Workbench as the shared data science development environment and Posit Connect as the publishing platform for analytical products.

Desirable:

- Strong alignment with R, Shiny, Quarto, Python, FastAPI, Plumber, and open-source data science workflows
- Provides a coherent path from development to publishing
- Supports interactive applications, reports, dashboards, APIs, notebooks, and scheduled outputs
- Reduces the need for HRL to custom-build a data science publishing platform
- Supports collaboration and reproducibility when combined with GitHub and environment management
- Allows analysts to work in a managed environment closer to shared data resources
- Provides a platform familiar to many R-oriented scientific computing communities

Neutral:

- Requires integration with GitHub, authentication, storage, databases, and deployment practices
- Does not replace Azure data engineering infrastructure
- Some users may continue to develop locally or use other tools for specialized workflows

Undesirable:

- Requires licensing and procurement
- Requires hosting and administration
- May require IaaS-based deployment despite the broader PaaS-first principle
- Requires training and support for users and administrators
- Introduces platform dependency for publishing workflows

### Use local desktop development environments and manual publication workflows

Allow analysts to develop locally and publish products manually using whatever tools or hosting pathways are available.

Desirable:

- Low centralized platform cost
- Familiar to many analysts
- Flexible for individual workflows
- Does not require immediate platform procurement or deployment

Neutral:

- Local development may remain appropriate for some exploratory or individual work

Undesirable:

- Creates inconsistent development and publishing practices
- Makes dependency management and reproducibility harder
- Makes deployment of Shiny apps, dashboards, reports, APIs, and scheduled outputs ad hoc and often not possible
- Increases reliance on individual machine configuration
- Makes collaboration and onboarding harder
- Does not provide a durable shared publishing platform for HRL decision-support products
- Can increase support burden when products need to be shared beyond the analyst's machine
- Does not enable scalable compute

### Build a custom cloud development and publishing platform from Azure services

Assemble a custom platform using Azure virtual machines, containers, app hosting, identity services, storage, CI/CD, and custom deployment workflows.

Desirable:

- High flexibility
- Could be tailored to HRL-specific needs
- Could align tightly with Azure-native architecture
- Might avoid vendor-specific data science platform conventions

Neutral:

- Some custom Azure services will still be needed for data engineering and specialized applications

Undesirable:

- Requires substantial engineering and administration effort
- Would duplicate many capabilities already provided by Posit products
- Makes R/Shiny/Quarto publishing more complex for analysts
- Requires custom support for user environments, package management, deployment, scheduling, authentication, and application hosting
- Increases operational burden on the Central Data Team and DWR infrastructure staff
- Could slow delivery of user-facing analytical products

### Use general-purpose notebook or machine learning platforms

Use platforms oriented toward notebooks, machine learning, or general cloud analytics as the primary HRL development and publishing environment.

Desirable:

- May support Python, notebooks, scalable compute, and machine learning workflows well
- May integrate with cloud storage and data services
- Could be useful for specialized modeling or data science workflows

Neutral:

- General-purpose notebook or ML platforms may still be useful for specialized workflows in the future

Undesirable:

- Often less aligned with R/Shiny/Quarto publishing needs
- May not provide the same integrated publishing support for HRL's expected analytical products
- Could require additional work to support R package environments, Shiny deployment, Quarto publishing, scheduled reports, and APIs
- May be unfamiliar to HRL's R-oriented scientific computing users
- Could overemphasize machine learning workflows relative to HRL's broader data synthesis and decision-support needs

### Use proprietary business intelligence or GIS application platforms as the primary publishing environment

Use commercial BI, dashboarding, or GIS platforms as the main way to publish HRL data products and applications.

Desirable:

- May provide polished user interfaces and map/dashboard capabilities
- May be familiar to some agency users
- Can support low-code visualization for certain reporting needs
- May integrate with enterprise authentication and sharing workflows

Neutral:

- BI and GIS platforms may remain useful as downstream consumers or specialized presentation tools

Undesirable:

- Does not meet the full need for reproducible scientific computing and open-source analytical workflows
- May not support Shiny, Streamlit, Quarto, custom R/Python APIs, or scheduled scientific workflows well
- Can separate published products from the code-based analytical workflows that produce them
- May increase vendor lock-in
- May be less suitable for methods transparency, scientific reproducibility, and code-based review
- Does not replace the need for a data science development environment

## More Information

This decision should be revisited if Posit Workbench or Posit Connect no longer meet HRL needs, if procurement or licensing becomes infeasible, if DWR adopts another enterprise-standard data science platform that supports HRL's open-source scientific computing and publishing requirements, or if HRL's analytical workflows shift away from R, Shiny, Quarto, and related open-source tools.

Related ADRs:

- [ADR-001: Adopt the HRL data lifecycle as the organizing framework](adr-001-hrl-data-lifecycle.md)
- [ADR-002: Require standardized, reproducible HRL repositories with GitHub, environment management, CI/CD, and governance files](adr-002-standardized-reproducible-hrl-repositories.md)
- [ADR-006: Use a DWR-hosted, PaaS-first Azure architecture for HRL data infrastructure](adr-006-dwr-hosted-paas-first-azure-architecture.md)
- [ADR-012: Separate the Azure data engineering stack from the Posit data science platform](adr-012-separate-azure-data-engineering-stack-from-posit.md)
- [ADR-013: Treat Posit as a deliberate IaaS exception to the PaaS-first principle](adr-013-posit-iaas-exception.md)