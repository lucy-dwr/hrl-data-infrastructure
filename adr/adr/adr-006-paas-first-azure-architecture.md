---
status: accepted
date: 2026-05-08
decision-makers: Lucy Andrews
consulted: Ashley Vizek, John Spendlove
informed: Louise Conrad
---

# Use a DWR-hosted, PaaS-first Azure architecture for HRL data infrastructure

## Context and Problem Statement

Healthy Rivers and Landscapes (HRL) data infrastructure must support data ingestion, validation, standardization, storage, serving, access, and analysis across multiple datasets and workflows. The infrastructure needs to support reproducible and maintainable data workflows while remaining manageable for the technical staff responsible for operating the system.

HRL is an interagency program, but the participating agencies do not have equivalent capacity to host, operate, secure, and maintain shared cloud-based data infrastructure. At this stage, DWR is the agency with the available technical, administrative, procurement, and enterprise cloud capacity to host the shared HRL data infrastructure.

DWR uses Microsoft Azure as its enterprise cloud environment. Therefore, if DWR is the hosting agency for HRL data infrastructure, Azure is the appropriate cloud platform for HRL-managed infrastructure components.

HRL could implement this infrastructure using self-managed virtual machines, managed cloud services, externally hosted platforms, another agency's infrastructure, or a mixture of approaches. A self-managed infrastructure model would give HRL more direct control over servers and runtime environments, but would also increase operational burden, patching responsibility, security maintenance, reliability management, and long-term administration.

HRL therefore needs a default infrastructure architecture that clearly identifies DWR as the hosting agency and uses DWR's Azure environment in a way that supports reliability, scalability, security, and maintainability while minimizing unnecessary server administration.

## Decision Drivers

- Need to identify a responsible hosting agency for shared HRL data infrastructure
- Need to host HRL data infrastructure within an agency environment that has sufficient technical, administrative, procurement, and enterprise cloud capacity
- Need to recognize that DWR is currently the agency with capacity to host and operate the shared infrastructure
- Need to align HRL infrastructure with DWR's enterprise cloud environment
- Need to reduce long-term operational burden on the Central Data Team
- Need to support reliable ingestion, validation, storage, serving, and access workflows
- Need to use services compatible with DWR enterprise cloud, security, procurement, and operations requirements
- Need to support geospatial data management, including object storage and PostgreSQL/PostGIS
- Need to support reproducible, automated, and containerized data workflows
- Need to avoid unnecessary maintenance of operating systems, patching, and manually administered servers
- Need to allow infrastructure components to scale as HRL data volume, access needs, and user communities grow

## Considered Options

- Use a DWR-hosted, PaaS-first Azure architecture for HRL data infrastructure
- Host HRL data infrastructure through another HRL partner agency
- Use a primarily IaaS-based Azure architecture with self-managed virtual machines
- Use externally hosted third-party data platforms outside DWR-managed Azure infrastructure
- Use local, desktop, or network-drive-based infrastructure for early implementation

## Decision Outcome

Chosen option: **Use a DWR-hosted, PaaS-first Azure architecture for HRL data infrastructure** because DWR is currently the HRL partner agency with the capacity to host and operate shared cloud-based data infrastructure, and DWR's enterprise cloud environment is Microsoft Azure.

Under this decision, DWR will serve as the hosting agency for HRL shared data infrastructure. HRL should prefer Azure platform-as-a-service or managed-service components for shared infrastructure wherever practical. This includes managed object storage, managed databases, managed container execution, managed application hosting, managed secrets, and managed monitoring where appropriate.

This decision does not mean that DWR is the sole owner of HRL data, science priorities, or governance decisions. HRL data infrastructure remains program-serving infrastructure. DWR's role is to host and operate the technical platform because it has the current capacity and enterprise cloud environment to do so.

This decision also does not prohibit all infrastructure-as-a-service components. Some tools may require virtual machines or marketplace deployments. However, IaaS should be treated as an exception rather than the default architecture for HRL data infrastructure.

### Consequences

Desirable:

- HRL has a clearly identified hosting agency for shared data infrastructure
- The infrastructure can use DWR's existing Azure enterprise cloud environment
- Hosting responsibility is not left ambiguous across HRL partner agencies
- HRL infrastructure can move forward without requiring another agency to develop new hosting capacity
- The Central Data Team can focus on data workflows, standards, validation, and stewardship rather than routine server administration
- Managed services reduce the need to patch and maintain operating systems directly
- Infrastructure components can be scaled, monitored, secured, and governed using Azure-native tools
- PaaS services support clearer separation of storage, compute, database, application, and access responsibilities
- The architecture can evolve incrementally as HRL needs mature
- The approach supports reproducible and automated workflows using managed cloud services

Undesirable:

- DWR takes on hosting, operational, procurement, staffing, and and infrastructure stewardship responsibilities
- Other HRL partner agencies may be dependent on DWR-hosted infrastructure for access to shared program data services
- HRL must work within DWR Azure governance, procurement, identity, networking, and security processes
- Some managed services may require learning new cloud concepts and operational patterns
- Some specialized software may not fit neatly into PaaS services and may require exceptions
- Cloud costs must be monitored and governed to avoid unexpected spending
- PaaS-first architecture may reduce low-level control compared with self-managed servers
- Vendor-specific Azure services may create some platform dependence

### Confirmation

Implementation of this decision can be confirmed by reviewing HRL infrastructure plans, deployment templates, architecture diagrams, and operating procedures to determine whether DWR is identified as the hosting agency and managed Azure services are used as the default infrastructure pattern.

Examples of confirmation include:

- HRL infrastructure documentation identifies DWR as the hosting agency
- Azure subscriptions, resources, permissions, and procurement pathways are managed through DWR
- Object storage is implemented using Azure Storage / ADLS Gen2 or equivalent managed Azure storage
- Databases are implemented using managed PostgreSQL/PostGIS services where practical
- Validation and transformation workflows are implemented using managed container execution or equivalent managed compute
- Secrets, access controls, monitoring, and logs use Azure-native managed services where appropriate
- New infrastructure proposals explain why any IaaS component is necessary
- IaaS components are documented as deliberate exceptions rather than default infrastructure
- Infrastructure documentation distinguishes Azure data engineering services from analyst-facing platforms such as Posit Workbench and Posit Connect

## Pros and Cons of the Options

### Use a DWR-hosted, PaaS-first Azure architecture for HRL data infrastructure

DWR serves as the hosting agency for HRL shared data infrastructure, and the architecture prefers managed Azure services, using IaaS only where necessary.

Desirable:

- Identifies a clear hosting agency for shared HRL infrastructure
- Uses the agency environment with current capacity to host and operate cloud infrastructure
- Aligns with DWR cloud hosting and enterprise governance
- Reduces operational burden compared with self-managed servers
- Supports managed storage, databases, compute, monitoring, identity, and security
- Allows the Central Data Team to focus on data infrastructure design rather than low-level server operations
- Provides a scalable foundation for ingestion, validation, standardization, storage, serving, and access
- Makes infrastructure easier to document, automate, and govern
- Allows deliberate exceptions for tools that require IaaS

Neutral:

- Requires Azure expertise and coordination with DWR cloud administrators
- Requires cost monitoring and service selection discipline
- Some services may need to be phased in as HRL implementation matures
- DWR hosting does not remove the need for interagency governance over data priorities, standards, and access expectations

Undesirable:

- Creates operational dependence on DWR-hosted infrastructure
- Requires DWR to sustain hosting, procurement, security, and infrastructure administration responsibilities
- Creates dependence on Azure service availability, pricing, and platform conventions
- May require changes to workflows originally designed for local or server-based environments
- May not fit all specialized scientific software without exceptions
- Can be more difficult to understand for participants unfamiliar with cloud service models

### Host HRL data infrastructure through another HRL partner agency

Another HRL partner agency would host the shared data infrastructure using its own cloud, server, or enterprise technology environment.

Desirable:

- Could distribute hosting responsibility outside DWR
- Could align infrastructure with another agency's internal systems if that agency had relevant capacity
- Could reduce DWR's operational responsibility

Neutral:

- This option may become more feasible in the future if another agency develops the necessary cloud hosting, staffing, procurement, and operations capacity

Undesirable:

- No other HRL partner agency currently has the same demonstrated capacity to host and operate the shared infrastructure
- Could delay implementation while hosting capacity, procurement, security review, and operations models are developed
- Could create uncertainty about platform choice, access model, support responsibilities, and long-term stewardship
- Might require HRL to adapt to another agency's cloud platform or technology standards
- Would still require a clear governance and cost-sharing model

### Use a primarily IaaS-based Azure architecture with self-managed virtual machines

Deploy HRL infrastructure primarily on virtual machines and manage software, operating systems, databases, and services directly.

Desirable:

- Provides direct control over server configuration
- Can support software that expects a traditional server environment
- May be familiar to some system administrators
- Can simplify migration of legacy server-based workflows

Neutral:

- Some IaaS components may still be needed for specific tools or exceptions

Undesirable:

- Increases operational burden for patching, security, backups, monitoring, scaling, and reliability
- Requires more system administration capacity than HRL may have
- Makes each infrastructure component more dependent on custom server configuration
- Can make reproducibility and deployment automation harder
- Increases risk that infrastructure becomes difficult to maintain over time
- Does not align with the PaaS-first goal of minimizing unnecessary server administration

### Use externally hosted third-party data platforms outside DWR-managed Azure infrastructure

Rely on externally hosted platforms or vendor-managed systems outside DWR Azure as the primary infrastructure for HRL data storage, serving, or analysis.

Desirable:

- May reduce some internal infrastructure responsibilities
- May provide specialized features for data management, visualization, or collaboration
- Could be faster to adopt for narrow use cases

Neutral:

- External platforms may still be appropriate for specific functions, such as scientific data repositories or public documentation hosting

Undesirable:

- May conflict with DWR hosting, security, procurement, access, or governance requirements
- Can fragment HRL infrastructure across systems with different identity, access, and stewardship models
- May limit integration with DWR-managed storage, databases, and cloud services
- May create vendor lock-in outside the enterprise cloud environment
- May make long-term stewardship and data access more dependent on third-party platform decisions

### Use local, desktop, or network-drive-based infrastructure for early implementation

Store and process HRL data using local machines, shared network drives, spreadsheets, desktop GIS files, or ad hoc scripts without shared cloud infrastructure.

Desirable:

- Low initial setup burden
- Familiar to many users
- Useful for early exploration, prototypes, and small local workflows
- Does not require immediate cloud procurement or deployment

Neutral:

- Local and desktop workflows may still be appropriate for exploratory analysis or one-time data preparation

Undesirable:

- Does not support reliable program-scale ingestion, storage, serving, or reuse
- Makes provenance, access control, versioning, and reproducibility harder
- Does not scale well across agencies, teams, datasets, or applications
- Increases risk of duplicated files and unclear authoritative versions
- Makes program-level synthesis and application publishing harder
- Does not provide a durable foundation for HRL data infrastructure

## More Information

This decision should be revisited if DWR changes its enterprise cloud hosting environment, if another HRL partner agency develops sufficient capacity to host shared infrastructure, if Azure managed services become unsuitable for HRL needs, if HRL infrastructure requirements exceed what DWR and the Central Data Team can manage under a PaaS-first approach, or if another approved enterprise platform provides a better fit.

Related ADRs:

- [ADR-001: Adopt the HRL data lifecycle as the organizing framework](adr-001-hrl-data-lifecycle.md)
- [ADR-005: Allow Central Data Team-managed publication pathways for large or complex datasets](adr-005-central-data-team-managed-publication-pathways.md)
- [ADR-007: Use Azure Storage / ADLS Gen2 as the raw, intermediate, export, and archival object storage backbone](adr-007-azure-storage-adls-gen2-object-storage-backbone.md)
- [ADR-008: Use Azure Container Apps Jobs for validation and transformation workflows](adr-008-container-apps-jobs-validation-transformation.md)
- [ADR-009: Use PostgreSQL/PostGIS as the authoritative operational store for standardized spatial data](adr-009-postgresql-postgis-authoritative-operational-store.md)
- [ADR-011: Procure and use Posit Workbench and Posit Connect for data science and application publishing](adr-011-posit-workbench-connect.md)
- [ADR-013: Treat Posit as a deliberate IaaS exception to the PaaS-first principle](adr-013-posit-iaas-exception.md)