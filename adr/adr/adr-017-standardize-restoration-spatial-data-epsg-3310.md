---
status: accepted
date: 2026-05-14
decision-makers: Lucy Andrews
consulted:
informed:
---

# Standardize restoration spatial data to EPSG:3310

## Context and Problem Statement

Healthy Rivers and Landscapes (HRL) restoration project spatial data will be submitted by multiple agencies, programs, implementers, and partners. These data may arrive in different coordinate reference systems, file formats, and GIS workflows. To support validation, standardization, storage, analysis, mapping, and export, HRL needs a consistent coordinate reference system for the curated restoration project dataset.

Restoration project spatial data are expected to represent features in California, particularly central and northern California and the Bay-Delta watershed context relevant to HRL. The data will support program-level spatial analysis, mapping, integration with other California geospatial datasets, and storage in PostgreSQL/PostGIS.

If submitted datasets retain mixed coordinate reference systems in the authoritative operational store, spatial analysis, spatial querying, overlay, distance calculations, area calculations, validation checks, map display, and export workflows become more difficult to manage consistently. Mixed coordinate reference systems also increase the risk of errors during ingestion and downstream use.

HRL therefore needs to standardize restoration spatial data to a single coordinate reference system for canonical storage and program-level use.

## Decision Drivers

- Need for a consistent coordinate reference system for standardized restoration spatial data
- Need to support spatial validation, transformation, storage, analysis, mapping, and export workflows
- Need to reduce errors caused by mixed or missing coordinate reference systems
- Need to support California-focused spatial analysis and mapping
- Need to support accurate area, distance, and overlay operations for California restoration project geometries
- Need to align geometry validation and ingestion workflows with a clear target CRS
- Need to support PostgreSQL/PostGIS storage and reproducible export generation
- Need to make submission requirements and transformation behavior clear to data contributors
- Need to avoid storing canonical records in arbitrary source-data coordinate systems

## Considered Options

- Standardize restoration spatial data to EPSG:3310
- Store restoration spatial data in the submitted coordinate reference system
- Standardize restoration spatial data to EPSG:4326
- Standardize restoration spatial data to a local projected coordinate system selected by each project or region
- Require all submitters to provide data already projected to EPSG:3310

## Decision Outcome

Chosen option: **Standardize restoration spatial data to EPSG:3310** because HRL restoration project data are California-focused and need a consistent projected coordinate reference system for canonical storage, validation, analysis, and export workflows.

Under this decision, submitted restoration spatial data must include a defined coordinate reference system that can be transformed to EPSG:3310. During ingestion, geometries should be transformed to EPSG:3310 for canonical storage in PostgreSQL/PostGIS and for standardized HRL data products where a projected CRS is appropriate.

This decision does not require every submitted file to already be in EPSG:3310. Submitters may provide data in another valid, well-defined CRS if the ingestion workflow can reliably transform the data to EPSG:3310. However, submissions with missing, ambiguous, invalid, or incorrectly assigned CRS information should fail validation or require correction before ingestion.

This decision also does not prevent HRL from generating exports in other coordinate reference systems when needed for specific user communities, web mapping, interoperability, or publication. EPSG:3310 is the canonical CRS for standardized restoration spatial data, not necessarily the only CRS used for all access products.

### Consequences

Desirable:

- HRL has a clear canonical CRS for standardized restoration project spatial data
- Geometry validation, ingestion, storage, and analysis workflows can assume a consistent target CRS
- Spatial overlay, area, distance, and mapping workflows are easier to make reproducible
- PostgreSQL/PostGIS storage can use consistent geometry definitions and spatial indexes
- Export workflows can be generated from a known canonical CRS
- Submitter guidance can clearly state CRS expectations
- Data with missing or ambiguous CRS information can be rejected or corrected before entering the authoritative dataset
- The decision supports California-focused program-scale spatial analysis

Undesirable:

- Ingestion workflows must include CRS detection, validation, and transformation steps
- Submitters may need support to understand CRS requirements and correct invalid spatial files
- Some web mapping or external interoperability workflows may still require exports in other coordinate reference systems
- EPSG:3310 may not be ideal for every possible local analysis or every downstream user
- Incorrectly assigned source CRS information could still produce erroneous transformed geometries if not caught during validation
- Documentation must clearly distinguish canonical storage CRS from optional export or display CRSs

### Confirmation

Implementation of this decision can be confirmed by reviewing the restoration schema documentation, geometry policy, validation workflows, database schema, and export workflows to determine whether EPSG:3310 is used as the canonical CRS for standardized restoration spatial data.

Examples of confirmation include:

- Submission guidance requires spatial files to include a defined CRS
- Validation workflows check whether submitted geometries have a defined CRS
- Validation workflows reject or flag missing, ambiguous, invalid, or unsupported CRS information
- Ingestion workflows transform accepted geometries to EPSG:3310
- PostgreSQL/PostGIS tables store canonical restoration project geometries in EPSG:3310
- Geometry columns, metadata, or database constraints identify EPSG:3310 as the expected CRS
- Export workflows document whether outputs are in EPSG:3310 or another requested CRS
- User-facing documentation explains that EPSG:3310 is the canonical CRS for standardized HRL restoration spatial data

## Pros and Cons of the Options

### Standardize restoration spatial data to EPSG:3310

Transform accepted submitted geometries to EPSG:3310 for canonical storage and standardized HRL use.

Desirable:

- Provides one consistent CRS for canonical storage and spatial analysis
- Supports California-focused spatial workflows
- Reduces downstream uncertainty caused by mixed source CRSs
- Makes validation, transformation, database storage, and export generation easier to standardize
- Allows submitters to provide data in other valid CRSs if they can be transformed reliably
- Supports reproducible geometry handling in PostgreSQL/PostGIS and analytical workflows

Neutral:

- Other CRSs may still be used for specific exports, web maps, or external interoperability needs
- Submitters may still use their local CRS during project development before submission

Undesirable:

- Requires transformation during ingestion for submissions in other CRSs
- Requires validation logic to detect missing or invalid CRS information
- May not be the preferred CRS for every local-scale analysis
- Requires documentation and training for submitters unfamiliar with CRS concepts

### Store restoration spatial data in the submitted coordinate reference system

Preserve each submitted dataset's original CRS in canonical storage.

Desirable:

- Avoids transformation during ingestion
- Preserves submitted geometry coordinates as provided
- May be simpler for a single submission or one-time dataset

Neutral:

- Original source files and CRS information should still be preserved for provenance

Undesirable:

- Produces mixed CRS data in the authoritative operational store
- Makes spatial analysis, overlay, indexing, and export workflows harder to standardize
- Increases risk of errors in area, distance, or overlay operations
- Makes database constraints and geometry validation less consistent
- Makes program-level integration across submissions more difficult
- Pushes CRS transformation burden onto every downstream user or workflow

### Standardize restoration spatial data to EPSG:4326

Use WGS 84 geographic coordinates as the canonical CRS.

Desirable:

- Widely recognized and interoperable
- Common for web APIs, GPS data, and many geospatial tools
- Useful for web mapping and data exchange
- Familiar to many users

Neutral:

- EPSG:4326 may be useful for some exports or interoperability products

Undesirable:

- It is a geographic CRS, not a projected CRS optimized for California analysis
- Area and distance calculations require additional care
- Less appropriate as the canonical CRS for California-focused spatial analysis
- May encourage inappropriate geometric measurements in latitude/longitude coordinates
- Does not provide the same analysis-oriented projected coordinate foundation as EPSG:3310

### Standardize restoration spatial data to a local projected coordinate system selected by each project or region

Use different projected coordinate systems for different watersheds, regions, or project areas.

Desirable:

- Allows each project or region to use a locally appropriate CRS
- May support highly accurate local engineering or design workflows
- Aligns with some project-specific GIS practices

Neutral:

- Local CRSs may still be used in source project files or specialized project-level analyses

Undesirable:

- Produces mixed canonical storage CRSs
- Makes program-level integration and statewide or regional analysis harder
- Requires more complex validation, metadata, database, and export workflows
- Makes it harder for users to understand and combine datasets
- Creates avoidable inconsistency in shared HRL infrastructure

### Require all submitters to provide data already projected to EPSG:3310

Reject submissions unless the submitted files are already in EPSG:3310.

Desirable:

- Simplifies ingestion by reducing transformation needs
- Ensures submitted files match the canonical CRS
- Makes CRS expectations very clear

Neutral:

- Providing data in EPSG:3310 may be encouraged or recommended for submitters who can do so

Undesirable:

- Places additional burden on data submitters
- May create unnecessary barriers for agencies or implementers using other valid CRSs
- Increases risk that submitters will incorrectly reproject data before submission
- Reduces flexibility without eliminating the need to validate CRS metadata
- May discourage contributions from less technical partners

## More Information

This decision should be revisited if HRL expands substantially outside California, if EPSG:3310 becomes unsuitable for HRL restoration project spatial workflows, if DWR adopts a different enterprise CRS standard for California spatial data, or if specific data products require a different canonical CRS.

Related ADRs:

- [ADR-006: Use a DWR-hosted, PaaS-first Azure architecture for HRL data infrastructure](adr-006-dwr-hosted-paas-first-azure-architecture.md)
- [ADR-008: Use Azure Container Apps Jobs for validation and transformation workflows](adr-008-container-apps-jobs-validation-transformation.md)
- [ADR-009: Use PostgreSQL/PostGIS as the authoritative operational store for standardized spatial data](adr-009-postgresql-postgis-authoritative-operational-store.md)
- [ADR-010: Publish standardized export files alongside the authoritative database](adr-010-standardized-export-files.md)
- [ADR-014: Administer restoration project spatial data as a shared HRL program dataset with DWR as steward](adr-014-shared-restoration-project-spatial-data.md)
- [ADR-016: Use LinkML as the source-of-truth schema language for restoration spatial data](adr-016-linkml-source-of-truth-schema.md)