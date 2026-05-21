---
status: accepted
date: 2026-05-11
decision-makers: Lucy Andrews
consulted: Ashley Vizek
informed:
---

# Use PostgreSQL/PostGIS as the authoritative operational store for standardized spatial data

## Context and Problem Statement

Healthy Rivers and Landscapes (HRL) data infrastructure must support standardized, queryable, and reusable spatial data for program-level analysis, synthesis, mapping, reporting, and application development. HRL workflows will include spatial datasets that begin as submitted files or external repository-hosted files, are validated and transformed through ingestion workflows, and then need to be stored in a form that supports reliable access by analysts, applications, APIs, and export processes.

File-based formats such as GeoPackage, GeoJSON, shapefiles, and GeoParquet are useful for submission, exchange, publication, and export. However, file-based storage alone is not sufficient as the authoritative operational store for standardized HRL spatial data. HRL needs a spatial database that can support relational structure, spatial indexing, query performance, controlled updates, provenance fields, application access, and repeatable generation of downstream exports.

PostgreSQL with the PostGIS extension is a widely used open-source spatial database platform that supports geospatial operations, relational modeling, spatial indexes, and integration with analytical tools, web applications, APIs, and GIS software.

Because HRL shared infrastructure is DWR-hosted in Azure and follows a PaaS-first architecture, PostgreSQL/PostGIS should be implemented using a managed Azure database service where practical.

## Decision Drivers

- Need for an authoritative operational store for standardized spatial data
- Need to distinguish raw submitted files from curated, standardized, queryable program data
- Need to support spatial queries, spatial indexing, relational constraints, and geospatial data integrity
- Need to support downstream APIs, maps, dashboards, applications, exports, and analysis workflows
- Need to preserve provenance from raw submissions and published source data to standardized records
- Need to support controlled updates, review, versioning, and stewardship of shared program datasets
- Need to avoid treating file-based formats as the only authoritative representation of operational spatial data
- Need to use open-source, broadly supported geospatial database technology
- Need to align with the DWR-hosted, PaaS-first Azure architecture

## Considered Options

- Use PostgreSQL/PostGIS as the authoritative operational store for standardized spatial data
- Use file-based spatial formats as the authoritative store
- Use a proprietary GIS platform as the authoritative store
- Store standardized spatial data only in Azure Storage / ADLS Gen2
- Store standardized spatial data only in static publication repositories such as EDI

## Decision Outcome

Chosen option: **Use PostgreSQL/PostGIS as the authoritative operational store for standardized spatial data** because HRL needs a durable, queryable, spatially enabled database for standardized program datasets after validation and transformation.

Under this decision, PostgreSQL/PostGIS will serve as the authoritative operational store for standardized spatial records used by HRL infrastructure, APIs, applications, exports, and analysis workflows. Raw submitted files and supporting artifacts may be stored in Azure Storage / ADLS Gen2, and static source datasets may be published through EDI or another approved pathway. However, the curated, standardized operational representation of spatial data will be stored in PostgreSQL/PostGIS.

This decision does not mean that PostgreSQL/PostGIS is the only access mechanism for HRL spatial data. Standardized exports, APIs, maps, dashboards, and application-specific views may be generated from the database to support different user needs.

### Consequences

Desirable:

- HRL has a clear authoritative operational store for standardized spatial records
- Standardized data can be queried, indexed, constrained, and served efficiently
- Spatial operations can be performed directly in the database
- Applications, APIs, maps, dashboards, and exports can use a consistent curated data source
- Provenance and stewardship fields can be managed alongside spatial records
- Data integrity can be supported through schemas, constraints, roles, and controlled update workflows
- The architecture separates raw object storage, static publication, operational storage, and downstream access products
- PostgreSQL/PostGIS is open-source and broadly supported across geospatial and data science tooling

Undesirable:

- The Central Data Team must administer database schemas, migrations, access controls, backups, and performance considerations
- Contributors may need support to understand the distinction between submitted files, published datasets, operational database records, and exports
- Database schema design requires care to avoid locking in immature data models too early
- PostGIS may not be the best storage mechanism for all large raster, imagery, LiDAR, or model-output datasets
- Operational database stewardship requires clear policies for updates, corrections, provenance, and versioning
- Additional tooling is needed to expose database contents to users who do not work directly with SQL or database connections

### Confirmation

Implementation of this decision can be confirmed by reviewing HRL infrastructure, database schemas, ingestion workflows, APIs, applications, and export processes to determine whether standardized spatial records are loaded into and served from PostgreSQL/PostGIS.

Examples of confirmation include:

- Validated and standardized spatial records are loaded into PostgreSQL/PostGIS
- Database schemas distinguish canonical fields, provenance fields, geometry columns, and system-managed fields
- Spatial indexes are created for geometry columns where appropriate
- Applications, APIs, dashboards, maps, or exports read from PostgreSQL/PostGIS rather than raw submission files
- Raw files remain stored separately in Azure Storage / ADLS Gen2 or another approved storage location
- Published source datasets remain linked through metadata, provenance fields, or catalog records
- Database migrations or schema-change processes are documented
- Access controls distinguish read-only users, data stewards, pipeline service accounts, and administrators
- Export files are generated from the authoritative database or from documented database views

## Pros and Cons of the Options

### Use PostgreSQL/PostGIS as the authoritative operational store for standardized spatial data

Store curated, standardized HRL spatial records in a spatially enabled relational database.

Desirable:

- Provides a clear operational source of truth for standardized spatial data
- Supports spatial indexing, spatial queries, relational constraints, and data integrity checks
- Integrates well with R, Python, GIS software, APIs, dashboards, and web applications
- Supports reproducible generation of exports and application-specific views
- Separates operational storage from raw file storage and static publication
- Uses open-source, widely adopted geospatial database technology
- Can be implemented through a managed Azure database service under the PaaS-first architecture

Neutral:

- Requires database design, access control, maintenance, and migration practices
- Some users may access data through exports or applications rather than direct database connections
- Some datasets may still require specialized storage outside PostGIS

Undesirable:

- Requires database administration capacity
- Requires clear schema governance and update workflows
- May be more complex than file-based storage for simple or one-time datasets
- Is not ideal as the primary storage mechanism for very large rasters, imagery, LiDAR, or other non-relational data products

### Use file-based spatial formats as the authoritative store

Treat files such as GeoPackage, GeoJSON, GeoParquet, or shapefiles as the authoritative representation of standardized spatial data.

Desirable:

- Simple to understand and exchange
- Works well for many GIS users
- Useful for publication, archiving, and downloads
- Avoids database administration for small or static datasets
- Supports offline or file-based workflows

Neutral:

- File-based formats remain important for submission, export, publication, and archival workflows

Undesirable:

- Makes controlled updates and concurrent access harder
- Does not provide the same support for relational constraints, spatial indexing, permissions, and query services
- Can lead to duplicated files and unclear authoritative versions
- Makes it harder to serve APIs, applications, dashboards, and maps from a consistent source
- Makes provenance and system-managed fields harder to enforce
- Does not scale well as a shared operational data store across multiple workflows and users

### Use a proprietary GIS platform as the authoritative store

Use a commercial GIS platform or hosted feature service as the primary authoritative store for standardized HRL spatial records.

Desirable:

- May provide familiar map editing, visualization, and sharing interfaces
- May integrate well with existing GIS users and workflows
- Can support hosted layers and web maps with less custom application development

Neutral:

- Proprietary GIS platforms may still be useful for visualization, editing interfaces, public maps, or derived services

Undesirable:

- Can increase vendor lock-in and costs
- May be less transparent or flexible for database-level stewardship, pipelines, and open-source workflows
- May complicate integration with R, Python, reproducible pipelines, and open-source data infrastructure
- May make schema migrations, provenance, and automated validation workflows more platform-specific
- May not align as well with the broader open, reproducible, database-centered HRL architecture

### Store standardized spatial data only in Azure Storage / ADLS Gen2

Store standardized spatial data as files in object storage, without loading curated records into a spatial database.

Desirable:

- Aligns with the Azure object storage backbone
- Supports durable storage of standardized exports and snapshots
- Avoids database administration
- Can handle large file-based datasets

Neutral:

- Azure Storage / ADLS Gen2 remains the appropriate storage layer for raw submissions, intermediate artifacts, validation reports, exports, and archives

Undesirable:

- Object storage is not a spatial relational database
- Does not provide native relational constraints, spatial indexes, SQL queries, or application-ready database views
- Makes controlled updates and record-level stewardship harder
- Requires additional systems to support APIs, maps, dashboards, and queryable access
- Blurs the distinction between file storage and operational data storage

### Store standardized spatial data only in static publication repositories such as EDI

Rely on static published data packages as the only authoritative representation of standardized spatial data.

Desirable:

- Supports citation, metadata, versioning, preservation, and discovery
- Aligns with static publication and open science practices
- Provides a durable source of record for published datasets

Neutral:

- Static repositories remain important for publication of source datasets and stable releases

Undesirable:

- Static repositories are not designed as operational databases
- Does not support dynamic querying, controlled operational updates, APIs, applications, or dashboards
- Makes it harder to manage current canonical records that may be updated over time
- Does not replace the need for ingestion, standardization, storage, and serving infrastructure
- May not support the access patterns needed for HRL program operations and interactive tools

## More Information

This decision should be revisited if PostgreSQL/PostGIS does not meet HRL needs for performance, scale, administration, security, geospatial functionality, or integration; if DWR adopts another enterprise spatial database standard; or if a specific dataset type requires a specialized authoritative store outside PostGIS.

Related ADRs:

- [ADR-001: Adopt the HRL data lifecycle as the organizing framework](adr-001-hrl-data-lifecycle.md)
- [ADR-005: Allow Central Data Team-managed publication pathways for large or complex datasets](adr-005-central-data-team-managed-publication-pathways.md)
- [ADR-006: Use a DWR-hosted, PaaS-first Azure architecture for HRL data infrastructure](adr-006-dwr-hosted-paas-first-azure-architecture.md)
- [ADR-007: Use Azure Storage / ADLS Gen2 as the raw, intermediate, export, and archival object storage backbone](adr-007-azure-storage-adls-gen2-object-storage-backbone.md)
- [ADR-008: Use Azure Container Apps Jobs for validation and transformation workflows](adr-008-container-apps-jobs-validation-transformation.md)
- [ADR-010: Publish standardized export files alongside the authoritative database](adr-010-standardized-export-files.md)
- [ADR-014: Administer restoration project spatial data as a shared HRL program dataset with DWR as steward](adr-014-shared-restoration-project-spatial-data.md)
- [ADR-017: Standardize restoration spatial data to EPSG:3310](adr-017-standardize-restoration-spatial-data-epsg-3310.md)