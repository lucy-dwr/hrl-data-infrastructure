# Use Azure Storage / ADLS Gen2 as the raw, intermediate, export, and archival object storage backbone

> **Status:** Proposed  
> **Date:** 2026-05-21  
> **Decision makers:** Lucy Andrews  
> **Consulted:** Ashley Vizek, Jordan Hoang, Emanuel Rodriguez  
> **Informed:**

## Context and problem statement

Healthy Rivers and Landscapes (HRL) data infrastructure must support the movement of data through multiple lifecycle stages, including submission, validation, standardization, storage, serving, export, and archiving. Many HRL workflows will involve files that need to be preserved outside of databases, including submitted source files, validation reports, intermediate outputs, standardized exports, metadata records, and archival snapshots.

The infrastructure therefore needs a durable object storage backbone that can support both programmatic workflows and long-term data stewardship. This storage layer should support structured organization, access control, integration with Azure-based compute and database services, and clear separation between raw submissions, working/intermediate data, curated exports, reports, and archived records.

Because HRL shared infrastructure will be hosted by DWR in Azure, Azure Storage / Azure Data Lake Storage (ADLS) Gen2 is the appropriate default object storage service for this role.

## Decision drivers

- Need for durable storage of raw submissions, validation reports, intermediate files, standardized exports, and archival snapshots
- Need to preserve submitted source files separately from standardized, transformed, or derived products
- Need to support reproducible ingestion and validation workflows
- Need to support clear provenance across raw, intermediate, curated, exported, and archived data products
- Need for object storage that integrates with DWR-hosted Azure infrastructure
- Need to support both geospatial and non-geospatial file-based data products
- Need to support programmatic access from validation jobs, transformation workflows, databases, APIs, and applications
- Need to manage access controls, retention, backup, and lifecycle policies within the DWR Azure environment
- Need to avoid relying on local machines, network drives, or ad hoc file-sharing systems as infrastructure components

## Considered options

- Use Azure Storage / ADLS Gen2 as the raw, intermediate, export, and archival object storage backbone
- Store files primarily in PostgreSQL/PostGIS
- Store files primarily in GitHub repositories
- Store files primarily in EDI or other external repositories
- Store files on local machines, network drives, or ad hoc shared folders

## Decision outcome

Chosen option: **Use Azure Storage / ADLS Gen2 as the raw, intermediate, export, and archival object storage backbone** because HRL needs a durable, Azure-native object storage layer that supports file-based data movement across the infrastructure while keeping raw submissions, intermediate products, exports, reports, and archives organized and separable.

Under this decision, Azure Storage / ADLS Gen2 will be used as the default storage backbone for file-based objects in the HRL data infrastructure. PostgreSQL/PostGIS may serve as the authoritative operational store for standardized spatial records, but Azure Storage / ADLS Gen2 will store the surrounding file-based artifacts needed for ingestion, validation, provenance, export, and archiving.

This decision does not mean that all data products are published through Azure Storage / ADLS Gen2. Static publication through EDI remains the default pathway for appropriate datasets. Azure Storage / ADLS Gen2 supports HRL infrastructure workflows downstream of publication and supports Central Data Team-managed pathways for datasets requiring program-hosted storage or serving.

### Consequences

Desirable:

- Raw submitted files can be preserved separately from standardized or derived products
- Validation and transformation workflows can read from and write to a consistent storage layer
- Validation reports, logs, intermediate outputs, and standardized exports can be stored in predictable locations
- Provenance between raw inputs, transformed data, database records, and exports is easier to maintain
- Storage integrates with other DWR-hosted Azure services
- Access controls and lifecycle policies can be managed within Azure
- Large or complex file-based datasets can be stored outside the operational database
- The architecture avoids treating GitHub, EDI, local folders, or databases as general-purpose object storage

Undesirable:

- HRL must define and maintain clear storage conventions, folder structures, naming conventions, and lifecycle policies
- Access controls must be carefully configured to avoid accidental exposure or over-restriction
- Object storage can accumulate obsolete intermediate files if retention policies are not maintained
- Users may need guidance to understand the difference between object storage, static publication repositories, operational databases, and public exports
- Azure storage costs and data egress patterns must be monitored
- Additional tooling may be needed to make stored files discoverable to users who do not interact directly with Azure

### Confirmation

Implementation of this decision can be confirmed by reviewing HRL infrastructure configuration, pipeline code, storage conventions, and documentation to determine whether file-based artifacts are stored in Azure Storage / ADLS Gen2 according to defined lifecycle roles.

Examples of confirmation include:

- Raw submissions are stored in a designated Azure Storage / ADLS Gen2 location
- Validation reports are written to a designated reports location
- Intermediate transformation outputs are stored separately from raw and curated data
- Standardized export files are written to a designated exports location
- Archived snapshots are preserved in a designated archival location
- Pipeline code reads from and writes to Azure Storage / ADLS Gen2 rather than local paths or unmanaged shared folders
- Storage paths, naming conventions, retention rules, and access expectations are documented
- Access to raw, intermediate, curated, export, and archive areas is governed according to sensitivity and role
- Database records, metadata, or catalog entries preserve links to relevant stored files where appropriate

## Pros and cons of the options

### Use Azure Storage / ADLS Gen2 as the raw, intermediate, export, and archival object storage backbone

Use Azure-native object storage as the main file storage layer for HRL infrastructure workflows.

Desirable:

- Aligns with the DWR-hosted Azure architecture
- Provides durable storage for file-based artifacts outside the operational database
- Supports separation of raw, intermediate, curated, exported, and archived data products
- Integrates with Azure compute, database, application, identity, monitoring, and security services
- Supports large files and mixed file types
- Enables programmatic access for validation, transformation, export, and archival workflows
- Provides a foundation for lifecycle policies, access control, and backup strategies

Neutral:

- Storage structure and governance conventions must be defined by HRL
- Some datasets may also be published externally through EDI or other repositories
- Some users may access exports, APIs, or applications rather than the storage account directly

Undesirable:

- Requires Azure configuration and administration
- Requires cost monitoring
- Requires careful access control design
- Can become disorganized if folder structures, naming conventions, and lifecycle policies are not enforced
- Is not, by itself, a discovery catalog, metadata system, or publication repository

### Store files primarily in PostgreSQL/PostGIS

Store source files, intermediate files, exports, or archival objects directly in the operational database.

Desirable:

- Centralizes data in one system
- May simplify some transactional relationships between records and files
- Allows some metadata and file references to be managed together

Neutral:

- PostgreSQL/PostGIS remains the appropriate operational store for standardized spatial records and relational data

Undesirable:

- Databases are not ideal as general-purpose storage for raw files, reports, intermediate artifacts, large geospatial packages, imagery, or archives
- Increases database size and backup burden
- Makes file lifecycle management more difficult
- Blurs the distinction between operational records and supporting file artifacts
- May reduce performance or complicate database administration
- Does not provide the same object-storage features for large file handling and storage lifecycle policies

### Store files primarily in GitHub repositories

Use GitHub repositories as the main storage location for raw submissions, intermediate files, exports, and archives.

Desirable:

- Provides version control for code, documentation, schemas, and small text-based files
- Makes repository contents easy to review and discuss
- Supports open collaboration and change tracking for appropriate files

Neutral:

- GitHub remains appropriate for source code, documentation, schemas, configuration, and small examples

Undesirable:

- GitHub is not appropriate as the primary storage location for large data files or operational data artifacts
- Repository size can become difficult to manage
- Binary and geospatial files are not well suited to ordinary Git workflows
- Access controls may not align with all data sensitivity requirements
- Does not provide object-storage lifecycle policies, scalable storage tiers, or integration patterns needed for HRL infrastructure
- Can confuse source-code management with data storage

### Store files primarily in EDI or other external repositories

Use EDI or another external repository as the main location for raw, intermediate, export, and archival files used by HRL infrastructure.

Desirable:

- Supports publication, citation, metadata, and long-term preservation for appropriate datasets
- Provides discoverability and reuse beyond HRL infrastructure
- Aligns with static publication expectations for many datasets

Neutral:

- EDI remains the default static publication repository for appropriate source datasets

Undesirable:

- External repositories are not intended to function as the working object storage layer for validation, transformation, and operational infrastructure workflows
- Intermediate files and validation reports may not be appropriate for formal publication
- Programmatic read/write infrastructure workflows may not fit repository publication processes
- Large, complex, operational, or frequently changing datasets may require different serving patterns
- Does not replace the need for an Azure-native storage layer within HRL infrastructure

### Store files on local machines, network drives, or ad hoc shared folders

Use desktop storage, shared drives, or informal folders to manage raw submissions, intermediate files, exports, and archives.

Desirable:

- Familiar to many users
- Low setup burden
- May work for early exploration or one-time manual workflows
- Does not require cloud configuration at the outset

Neutral:

- Local or shared-drive workflows may still be used for temporary exploratory work before data enter shared infrastructure

Undesirable:

- Does not provide a durable infrastructure foundation
- Makes provenance, access control, automation, and reproducibility harder
- Increases risk of duplicated files, unclear versions, and broken file paths
- Does not integrate cleanly with Azure-based validation, transformation, storage, serving, and application workflows
- Makes program-level management, backup, retention, and auditing more difficult
- Does not scale well across HRL teams, agencies, and workflows

## More information

This decision should be revisited if DWR changes its enterprise cloud storage platform, if HRL adopts another approved object storage backbone, or if implementation shows that Azure Storage / ADLS Gen2 does not meet HRL needs for scale, access control, integration, cost, or data stewardship.

Related ADRs:

- [ADR-001: Adopt the HRL data lifecycle as the organizing framework](adr-001-hrl-data-lifecycle.md)
- [ADR-004: Require static publication of data before ingestion, with EDI as the default repository](adr-004-static-publication-before-ingestion.md)
- [ADR-005: Allow Central Data Team-managed publication pathways for large or complex datasets](adr-005-central-data-team-managed-publication-pathways.md)
- [ADR-006: Use a DWR-hosted, PaaS-first Azure architecture for HRL data infrastructure](adr-006-paas-first-azure-architecture.md)
- [ADR-008: Use Azure Container Apps Jobs for validation and transformation workflows](adr-008-azure-container-apps-jobs.md)
- [ADR-009: Use PostgreSQL/PostGIS as the authoritative operational store for standardized spatial data](adr-009-postgresql-postgis-operational-store.md)
- [ADR-010: Publish standardized export files alongside the authoritative database](adr-010-standardized-export-files.md)
