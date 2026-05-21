---
status: accepted
date: 2026-05-21
decision-makers: Lucy Andrews
consulted: Ashley Vizek
informed:
---

# Publish standardized export files alongside the authoritative database

## Context and Problem Statement

Healthy Rivers and Landscapes (HRL) data infrastructure uses PostgreSQL/PostGIS as the authoritative operational store for standardized spatial data. This database-centered approach supports controlled updates, spatial queries, relational structure, APIs, applications, maps, dashboards, and reproducible downstream workflows.

However, not all HRL users will access data through a database connection, API, or web application. Many users, including partner agency staff, GIS analysts, consultants, scientists, and public users, may need file-based access to standardized data. File exports are also useful for archiving, versioning, publication, reproducible analysis, offline use, and interoperability with desktop GIS and analytical tools.

If standardized data are available only through the operational database, HRL risks limiting access to users with the technical ability, permissions, or software needed to query the database. If exports are created manually or inconsistently, users may receive outdated, undocumented, or non-reproducible copies of the data.

HRL therefore needs a standard approach for publishing file-based exports generated from the authoritative database or documented database views.

## Decision Drivers

- Need to make standardized HRL data accessible to users who do not connect directly to databases
- Need to support desktop GIS, analytical workflows, reproducible research, and partner agency use
- Need to provide stable, portable snapshots of standardized datasets
- Need to distinguish authoritative operational storage from user-facing distribution formats
- Need to reduce manual, ad hoc, or inconsistent data exports
- Need to support metadata, provenance, versioning, and known-limitations documentation for exported data
- Need to support multiple file formats appropriate to different users and tools
- Need to align exports with the DWR-hosted Azure architecture and object storage backbone
- Need to preserve a clear relationship between database records, export files, and static publication records

## Considered Options

- Publish standardized export files alongside the authoritative database
- Require users to access standardized data only through PostgreSQL/PostGIS
- Require users to access standardized data only through APIs or applications
- Maintain manual or ad hoc export workflows
- Treat static publication repositories as the only source for downloadable files

## Decision Outcome

Chosen option: **Publish standardized export files alongside the authoritative database** because HRL needs both an authoritative operational database and accessible, portable, documented file-based data products.

Under this decision, PostgreSQL/PostGIS remains the authoritative operational store for standardized spatial records. Standardized export files should be generated from the authoritative database or documented database views and published to designated storage, catalog, or download locations.

Export formats may include GeoPackage, GeoJSON, CSV, GeoParquet, or other appropriate formats depending on the dataset, geometry, user community, and access needs. Export generation should be automated or reproducible where practical, and exports should include or link to relevant metadata, schema documentation, version information, provenance, and known limitations.

This decision does not make exports the operational source of truth. Exports are access products derived from the authoritative database.

### Consequences

Desirable:

- Users can access standardized data without direct database access
- Desktop GIS users, analysts, partner agencies, and public users can work with familiar file formats
- Export files can provide stable snapshots for analysis, reporting, archiving, and publication
- Exports can be generated reproducibly from the authoritative database or documented views
- The operational database remains the source of truth while exports serve as distribution products
- Export files can be stored in Azure Storage / ADLS Gen2 or other designated access locations
- Export workflows can reduce ad hoc manual copying and inconsistent data sharing
- Exports can support transparency and reuse beyond the immediate HRL technical environment

Undesirable:

- Export workflows must be designed, automated, documented, and maintained
- Exports can become stale if not regenerated or versioned appropriately
- Users may confuse exported snapshots with the live authoritative database
- Multiple export formats increase maintenance and testing burden
- Large exports may require storage, access, performance, and cost management
- Metadata and provenance must be kept synchronized with exported files

### Confirmation

Implementation of this decision can be confirmed by reviewing HRL export workflows, storage locations, documentation, and access products to determine whether standardized exports are generated from the authoritative database or documented views.

Examples of confirmation include:

- Export files are generated from PostgreSQL/PostGIS or documented database views
- Export workflows are scripted, automated, or otherwise reproducible
- Export files are written to designated Azure Storage / ADLS Gen2 locations, catalog locations, or public download locations
- Export files include or link to metadata, schema documentation, version information, and known limitations
- Export documentation identifies the authoritative database table or view used to generate each export
- Export files have clear timestamps, version identifiers, or release identifiers
- Export workflows include checks to reduce schema drift or incomplete exports
- User-facing documentation explains that exports are derived access products, not the operational source of truth

## Pros and Cons of the Options

### Publish standardized export files alongside the authoritative database

Generate documented file-based exports from the authoritative database or documented views.

Desirable:

- Broadens access to standardized HRL data
- Supports users who rely on desktop GIS, spreadsheets, R, Python, or offline workflows
- Preserves PostgreSQL/PostGIS as the operational source of truth
- Allows reproducible export generation from known database tables or views
- Supports stable snapshots for reporting, analysis, publication, and archiving
- Reduces ad hoc data sharing
- Supports multiple access patterns without weakening the database-centered architecture

Neutral:

- Export formats and schedules may vary by dataset
- Some users may still prefer APIs, applications, or direct database access
- Some exports may be public while others may be restricted

Undesirable:

- Requires export workflow maintenance
- Requires clear versioning and documentation to avoid confusion
- Adds storage and possibly egress costs
- May require format-specific testing and validation
- Can create stale copies if exports are not regenerated or labeled clearly

### Require users to access standardized data only through PostgreSQL/PostGIS

Provide access to standardized data only through direct database connections.

Desirable:

- Keeps users closest to the authoritative operational source
- Reduces need to maintain multiple export formats
- Avoids stale file copies when users query current database records
- Supports powerful SQL and spatial queries for advanced users

Neutral:

- Direct database access remains appropriate for some technical users, applications, and pipelines

Undesirable:

- Excludes or burdens users who do not have database tools, permissions, or expertise
- Makes offline, desktop GIS, and simple file-based workflows harder
- Can increase support burden for database access and query help
- May not be appropriate for broad public or partner-agency distribution
- Does not provide stable file snapshots for publication, archiving, or reproducible reporting

### Require users to access standardized data only through APIs or applications

Expose standardized data only through web APIs, dashboards, maps, or applications.

Desirable:

- Provides controlled and user-friendly access paths
- Can hide database complexity from users
- Supports application-specific views, filters, and permissions
- Can reduce the need for broad direct database access

Neutral:

- APIs and applications remain important access mechanisms for many HRL use cases

Undesirable:

- Does not meet all analytical, GIS, or archival needs
- Users may still need downloadable files for analysis, reporting, or integration with other systems
- APIs and applications require their own maintenance, documentation, and versioning
- Can limit reuse if users cannot obtain complete datasets in portable formats
- May be less useful for reproducible research than stable downloadable snapshots
- May exclude users who are unfamiliar with API- and application-based data access processes

### Maintain manual or ad hoc export workflows

Allow staff to create exports as needed using desktop GIS, database clients, scripts, or manual processes.

Desirable:

- Low initial infrastructure burden
- Flexible for one-off requests
- Familiar to many GIS and data staff
- May be acceptable for exploratory or temporary needs

Neutral:

- Manual exports may still occur for unusual, one-time, or internal requests

Undesirable:

- Produces inconsistent outputs
- Increases risk of stale, incomplete, or undocumented files
- Makes provenance and reproducibility harder
- Creates staff bottlenecks
- Makes it difficult to know which export a user received
- Does not scale well across recurring datasets and partner requests
- Can undermine trust in the authoritative database if uncontrolled copies circulate

### Treat static publication repositories as the only source for downloadable files

Use EDI or another static publication repository as the only location where users obtain downloadable standardized data files.

Desirable:

- Supports citation, preservation, metadata, and stable release practices
- Aligns with open science and static publication principles
- Provides durable access to published versions

Neutral:

- Static repositories remain important for source datasets and formal releases

Undesirable:

- Static repositories are not designed to reflect every operational database update
- Publication workflows may be too slow or formal for routine standardized exports
- Does not support internal, provisional, restricted, or frequently refreshed access products well
- Does not replace the need for exports generated from the current operational database
- May blur the distinction between source publication, operational storage, and derived access products

## More Information

This decision should be revisited if HRL users primarily access standardized data through APIs or applications and no longer need file exports, if export maintenance becomes unsustainable, if a catalog or data portal supersedes the proposed export mechanism, or if specific datasets require a different access model.

Related ADRs:

- [ADR-001: Adopt the HRL data lifecycle as the organizing framework](adr-001-hrl-data-lifecycle.md)
- [ADR-006: Use a DWR-hosted, PaaS-first Azure architecture for HRL data infrastructure](adr-006-dwr-hosted-paas-first-azure-architecture.md)
- [ADR-007: Use Azure Storage / ADLS Gen2 as the raw, intermediate, export, and archival object storage backbone](adr-007-azure-storage-adls-gen2-object-storage-backbone.md)
- [ADR-009: Use PostgreSQL/PostGIS as the authoritative operational store for standardized spatial data](adr-009-postgresql-postgis-authoritative-operational-store.md)
- [ADR-014: Administer restoration project spatial data as a shared HRL program dataset with DWR as steward](adr-014-shared-restoration-project-spatial-data.md)
- [ADR-017: Standardize restoration spatial data to EPSG:3310](adr-017-standardize-restoration-spatial-data-epsg-3310.md)