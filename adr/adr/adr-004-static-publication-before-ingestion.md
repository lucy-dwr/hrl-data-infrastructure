---
status: accepted
date: 2026-01-01
decision-makers: Lucy Andrews, Louise Conrad, Pascale Goertler
consulted: HRL Science Committee, Ashley Vizek
informed: HRL Science Committee
---

# Require static publication of data before ingestion, with EDI as the default repository

## Context and Problem Statement

Healthy Rivers and Landscapes (HRL) data infrastructure is intended to support program-level data reuse, synthesis, analysis, reporting, and decision support. To make this possible, data entering shared infrastructure must be well documented, quality-controlled, versioned, citable, and reproducible.

If datasets are ingested directly from informal working files, undocumented spreadsheets, ad hoc geospatial layers, or individual project folders, HRL risks building shared infrastructure on data products that are not stable, transparent, or reusable. This would make downstream ingestion, standardization, storage, serving, and synthesis harder to trust and harder to reproduce.

HRL therefore needs a default expectation that datasets are first published as static, citable data releases before they are ingested into shared program infrastructure. The [Environmental Data Initiative (EDI)](https://edirepository.org) is the default repository for HRL static data publication when it is appropriate for the data type and publication context.

## Decision Drivers

- Need to ensure that data entering shared HRL infrastructure are documented, quality-controlled, versioned, and citable
- Need to support reproducibility and long-term reuse of HRL data products
- Need to distinguish static publication from ongoing ingestion, standardization, storage, and serving
- Need to preserve provenance between original published data products and derived standardized datasets
- Need to reduce ambiguity about when a dataset is ready for program-level ingestion or synthesis
- Need to support FAIR-aligned data practices, including findability, accessibility, interoperability, and reuse
- Need to provide Data Producers with a clear publication target and review standard
- Need to avoid treating shared infrastructure as a substitute for proper data publication

## Considered Options

- Require static publication of data before ingestion, with EDI as the default repository
- Ingest data directly from project working files and publish later
- Allow each project or Data Producer to choose whether publication is required before ingestion
- Use HRL shared infrastructure as the primary publication location for all datasets

## Decision Outcome

Chosen option: **Require static publication of data before ingestion, with EDI as the default repository** because HRL needs stable, documented, versioned, and citable source data products before those data are transformed into shared program infrastructure.

Under this decision, static publication is the default prerequisite for ingestion into HRL shared infrastructure. Static publication means that a dataset has been prepared as a documented release with appropriate metadata, quality control, provenance, versioning, and citation information. EDI is the default repository for such publication when the dataset is appropriate for EDI and when no approved exception applies.

This decision does not mean that HRL infrastructure cannot store, standardize, or serve data. Instead, it clarifies that shared infrastructure generally operates downstream of publication: it ingests, standardizes, stores, serves, and supports reuse of data products that have already been made stable and citable.

Exceptions for large, complex, sensitive, operational, or otherwise unsuitable datasets are addressed separately.

### Consequences

Desirable:

- HRL ingestion workflows can rely on stable, citable source datasets
- Data Producers have clear expectations for preparing data before ingestion
- Data provenance is easier to track from published source data to standardized program datasets
- Downstream analyses and synthesis products are easier to reproduce
- Published data products are more discoverable and reusable outside HRL infrastructure
- Shared infrastructure is not used as a substitute for publication, documentation, or quality control
- Static publication creates a durable record of source data even if infrastructure systems change later

Undesirable:

- Data Producers may need additional time, support, and training to prepare publication-ready datasets
- Ingestion may be delayed until static publication is complete
- Some datasets may not fit neatly into EDI publication workflows
- Strict application of this rule may be impractical for very large, complex, sensitive, or continuously updated datasets
- Additional coordination is needed to manage exceptions and publication pathways

### Confirmation

Implementation of this decision can be confirmed by reviewing HRL ingestion workflows, repository documentation, data inventories, and published data records to determine whether ingested datasets have corresponding static published source records unless an approved exception applies.

Examples of confirmation include:

- Ingestion workflows reference a published data package, DOI, version, or release
- Data inventories distinguish source published datasets from standardized or derived infrastructure datasets
- Repository documentation identifies the publication source for ingested data
- Metadata and provenance records preserve links between published source data and standardized HRL datasets
- Data Producers are provided with guidance for preparing EDI-ready data packages
- Exceptions to EDI-first publication are documented and routed through an approved alternative pathway

## Pros and Cons of the Options

### Require static publication of data before ingestion, with EDI as the default repository

Require datasets to be published as stable, documented, citable releases before ingestion into shared HRL infrastructure, using EDI as the default repository when appropriate.

Desirable:

- Creates a stable source of record for datasets entering HRL infrastructure
- Supports reproducibility, citation, provenance, and long-term reuse
- Clarifies expectations for Data Producers
- Reduces risk that informal or poorly documented working files become program-level data assets
- Aligns with FAIR principles and open science practices
- Provides a clear boundary between publication and downstream infrastructure services
- Allows HRL infrastructure to focus on ingestion, standardization, storage, serving, and synthesis support

Neutral:

- Requires coordination between Data Producers and the Central Data Team
- Requires exceptions for data types that do not fit EDI or static publication well
- May be phased in as workflows, templates, and training mature

Undesirable:

- Adds upfront work before ingestion
- May slow early implementation for some datasets
- May be difficult for Data Producers unfamiliar with EDI, metadata, or versioned publication
- May create friction if publication requirements are treated as a compliance step rather than a stewardship practice

### Ingest data directly from project working files and publish later

Allow data to enter HRL shared infrastructure from spreadsheets, geospatial files, project folders, or other working locations before static publication is complete.

Desirable:

- Allows faster initial ingestion
- Reduces upfront burden on Data Producers
- May be practical for early prototypes or exploratory workflows
- Allows the Central Data Team to help identify data issues before publication

Neutral:

- May be acceptable for clearly marked pilot, test, or provisional datasets

Undesirable:

- Increases risk that undocumented or unstable data become embedded in shared infrastructure
- Makes provenance harder to reconstruct later
- Weakens reproducibility of downstream analyses
- Can create confusion about which version of a dataset is authoritative
- May shift publication and documentation burden from Data Producers to the Central Data Team
- Makes it harder to cite, discover, or reuse source data outside HRL systems

### Allow each project or Data Producer to choose whether publication is required before ingestion

Permit project teams to decide whether static publication is necessary before their data are ingested.

Desirable:

- Gives projects flexibility
- May reduce friction for teams with limited publication capacity
- Allows workflows to adapt to project-specific needs

Neutral:

- Some project-specific variation will still be necessary through an exceptions process

Undesirable:

- Produces inconsistent expectations across HRL
- Makes infrastructure readiness dependent on individual project practices
- Creates uneven data quality, metadata, and provenance
- Makes program-level synthesis harder
- Increases support burden for the Central Data Team
- Makes it harder to explain HRL data governance expectations to partners

### Use HRL shared infrastructure as the primary publication location for all datasets

Treat HRL infrastructure itself as the main location for publishing, storing, serving, and preserving program datasets.

Desirable:

- Centralizes data access within HRL systems
- Could provide a consistent program-branded access point
- May be necessary for some large, complex, sensitive, or operational datasets

Neutral:

- HRL infrastructure may still provide access, mirrors, derived products, or alternative publication pathways for some datasets

Undesirable:

- Blurs the distinction between publication and operational data services
- Requires HRL to provide repository-like functions such as citation, versioning, metadata, preservation, and discovery for all datasets
- Increases infrastructure and governance burden
- May duplicate functions better handled by established repositories such as EDI
- Makes long-term preservation more dependent on HRL-specific systems
- Could reduce interoperability with broader scientific data publication practices

## More Information

This decision should be revisited if EDI becomes unsuitable for HRL publication needs; if DWR or HRL adopts an official repository platform that provides equivalent or better support for citation, metadata, versioning, preservation, and discovery; or if implementation shows that the default publication-before-ingestion rule creates unacceptable delays or barriers.

Related ADRs:

- [ADR-001: Adopt the HRL data lifecycle as the organizing framework](adr-001-hrl-data-lifecycle.md)
- [ADR-002: Require standardized, reproducible HRL repositories with GitHub, environment management, CI/CD, and governance files](adr-002-standardized-reproducible-hrl-repositories.md)
- [ADR-003: Define Data Producers, the Central Data Team, and Synthesis Teams as core governance roles](adr-003-governance-roles.md)
- [ADR-005: Allow Central Data Team-managed publication pathways for large or complex datasets](adr-005-central-data-team-managed-publication-pathways.md)