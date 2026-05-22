---
status: accepted
date: 2026-05-12
decision-makers: Lucy Andrews
consulted: Ashley Vizek
informed: HRL Habitat Implementation Team
---

# Use LinkML as the source-of-truth schema language for restoration spatial data

::: {.adr-metadata}
**Status:** Accepted  
**Date:** 2026-05-12  
**Decision makers:** Lucy Andrews  
**Consulted:** Ashley Vizek  
**Informed:** HRL Habitat Implementation Team
:::

## Context and problem statement

Healthy Rivers and Landscapes (HRL) needs a machine-readable schema for restoration project spatial data. The schema must define the expected structure of submitted and standardized restoration project records, including fields, descriptions, data types, required fields, allowable values, multivalued fields, and relationships among schema components.

The schema must support several audiences and uses. Data submitters need human-readable documentation and templates. Developers need machine-readable artifacts that can support validation and transformation workflows. Data stewards need a maintainable source of truth for field definitions and controlled vocabularies. Analysts and application developers need a stable data contract for working with standardized restoration project data.

The restoration project data model initially existed in spreadsheet form. Spreadsheets are useful for discussion, review, and early design, but they are not sufficient as the source of truth for automated validation, documentation generation, schema evolution, or reproducible data infrastructure. HRL therefore needs a schema language that can act as the authoritative source for both human-facing documentation and machine-facing validation artifacts.

LinkML provides a machine-readable schema language that can describe classes, slots, types, enumerations, required fields, multivalued fields, descriptions, and related metadata. It can also generate documentation and validation artifacts such as JSON Schema from a single schema source.

## Decision drivers

- Need for a machine-readable source of truth for the restoration project data model
- Need to move beyond spreadsheet-based schema management
- Need to support automated validation and transformation workflows
- Need to generate human-readable schema documentation from the same source as validation artifacts
- Need to define controlled vocabularies, field descriptions, data types, required fields, and multivalued fields consistently
- Need to support schema versioning, review, and change tracking through GitHub
- Need to support both submission-facing and canonical data models over time
- Need to align schema management with HRL repository, CI/CD, and reproducibility practices
- Need to keep the schema understandable and maintainable for a small technical team
- Need to support future interoperability with related data standards where practical

## Considered options

- Use LinkML as the source-of-truth schema language for restoration spatial data
- Continue maintaining the schema primarily in spreadsheets
- Use JSON Schema directly as the source-of-truth schema language
- Use a database schema or migration files as the source of truth
- Use documentation pages as the source of truth

## Decision outcome

Chosen option: **Use LinkML as the source-of-truth schema language for restoration spatial data** because it provides a maintainable, machine-readable schema source that can generate documentation and downstream validation artifacts while remaining more expressive and human-editable than lower-level validation formats.

Under this decision, the restoration project schema should be maintained in LinkML. The LinkML schema is the authoritative source for field names, descriptions, data types, required fields, allowable values, multivalued fields, and other schema-level definitions. Derived artifacts, such as JSON Schema, documentation pages, data dictionaries, templates, and validation configuration, should be generated from or synchronized with the LinkML source wherever practical.

Spreadsheets may continue to be used for review, discussion, stakeholder feedback, or simple data-entry templates, but they should not be treated as the authoritative schema source once the LinkML schema is established.

This decision does not mean that all validation logic must be encoded in LinkML. Some validation requirements, especially geospatial geometry checks, coordinate reference system checks, cross-field business rules, and database-specific constraints, may be enforced through validation and ingestion code that incorporates LinkML-derived artifacts.

### Consequences

Desirable:

- HRL has a machine-readable source of truth for the restoration project schema
- Field definitions, descriptions, data types, requirements, and enumerations can be maintained consistently
- Human-readable documentation and machine-readable validation artifacts can be generated from the same source
- Schema changes can be reviewed, versioned, and tracked in GitHub
- Validation and ingestion workflows can use generated artifacts such as JSON Schema
- Controlled vocabularies can be managed as part of the schema
- The schema becomes easier to maintain than disconnected spreadsheets, documentation pages, and code
- LinkML supports future extension toward related semantic, metadata, or interoperability use cases

Undesirable:

- Contributors must learn enough LinkML to review or modify the schema
- The Central Data Team must maintain the schema generation workflow
- Not all validation requirements can or should be expressed directly in LinkML
- Generated artifacts may create confusion if users do not understand that LinkML is the source of truth
- The schema repository must include clear guidance for editing, generating, validating, and publishing schema artifacts
- Some stakeholders may still prefer spreadsheet-based schema review, requiring translation between review formats and the LinkML source

### Confirmation

Implementation of this decision can be confirmed by reviewing the restoration schema repository, documentation site, validation workflows, and generated artifacts to determine whether LinkML is treated as the authoritative schema source.

Examples of confirmation include:

- The schema repository contains a LinkML schema file or files that define the restoration project model
- Data dictionary pages are generated from or synchronized with the LinkML schema
- JSON Schema or other validation artifacts are generated from the LinkML schema where practical
- Controlled vocabularies are maintained in the LinkML schema or generated from it
- Schema changes are reviewed through GitHub pull requests or equivalent change-control workflows
- Documentation identifies LinkML as the schema source of truth
- Validation and ingestion code reference LinkML-derived artifacts rather than independently maintained field definitions
- Spreadsheet representations, if used, are documented as review or communication artifacts rather than the authoritative schema

## Pros and cons of the options

### Use LinkML as the source-of-truth schema language for restoration spatial data

Maintain the restoration project schema in LinkML and generate documentation and validation artifacts from it.

Desirable:

- Provides a machine-readable and human-editable schema source
- Supports field definitions, types, required fields, descriptions, enumerations, and multivalued fields
- Can generate documentation and downstream validation artifacts
- Supports version control, review, and change tracking in GitHub
- Reduces duplication between documentation, validation code, and schema references
- Provides a stronger foundation for future interoperability than spreadsheets or ad hoc documentation
- Aligns with HRL reproducibility and infrastructure practices

Neutral:

- Requires a schema build/generation workflow
- Some users may interact only with generated documentation or templates, not the LinkML source
- Runtime validation code will still be needed for some business and geometry rules

Undesirable:

- Requires technical learning for contributors unfamiliar with LinkML
- Adds tooling that must be maintained
- May be more formal than needed for very simple datasets
- Generated artifacts must be kept synchronized and clearly documented

### Continue maintaining the schema primarily in spreadsheets

Use spreadsheets as the main schema source for fields, descriptions, types, allowable values, and requirements.

Desirable:

- Familiar to many non-technical contributors
- Easy to review in meetings or through simple comments
- Low initial tooling burden
- Useful for early data-model design and stakeholder feedback

Neutral:

- Spreadsheets may remain useful as review, communication, or template artifacts

Undesirable:

- Not a strong source of truth for automated validation
- Harder to version, diff, review, and test than text-based schema files
- Increases risk of divergence between documentation, validation code, and database schemas
- Makes generation of validation artifacts and documentation harder
- Does not support reproducible schema workflows as well as a machine-readable schema language

### Use JSON Schema directly as the source-of-truth schema language

Maintain JSON Schema files directly as the authoritative schema source.

Desirable:

- Directly supports JSON-oriented validation workflows
- Widely used and supported by many tools
- Avoids an additional schema-generation layer for JSON validation
- Machine-readable and version-controllable

Neutral:

- JSON Schema may still be an important generated artifact from LinkML

Undesirable:

- Less expressive as a high-level data-modeling and documentation source
- Harder for many contributors to read and maintain directly
- Less convenient for generating rich documentation and related artifacts
- Can become verbose and difficult to manage as the schema grows
- Does not provide the same modeling conventions for classes, slots, enumerations, and semantic metadata as LinkML

### Use a database schema or migration files as the source of truth

Treat PostgreSQL/PostGIS table definitions, migrations, constraints, or database models as the authoritative schema source.

Desirable:

- Directly reflects operational storage
- Can enforce database-level constraints
- Aligns with authoritative storage in PostgreSQL/PostGIS
- Useful for database administration and migrations

Neutral:

- Database schemas and migrations remain necessary for operational storage

Undesirable:

- Focuses on database implementation rather than submission guidance, documentation, and validation artifacts
- Does not easily generate user-facing data dictionaries or submission templates
- May conflate canonical operational storage with submission schema requirements
- Is not ideal for describing stakeholder-facing field definitions, controlled vocabularies, or multivalued submission fields
- Makes it harder to support validation before data reach the database

### Use documentation pages as the source of truth

Maintain field definitions and data model rules in Markdown, Quarto, or other documentation pages.

Desirable:

- Easy for users to read
- Simple to publish as a documentation site
- Good for explanations, examples, and guidance
- Accessible to non-technical contributors

Neutral:

- Documentation remains essential for schema communication and user guidance

Undesirable:

- Not machine-readable enough for validation and automation
- Increases risk of divergence between docs, code, generated artifacts, and database schemas
- Hard to test automatically
- Does not provide a strong source for generating validation artifacts
- Makes schema changes harder to review systematically

## More information

This decision should be revisited if LinkML becomes unsuitable for HRL needs, if the restoration project schema becomes too simple to justify LinkML tooling, if another schema language becomes a better fit for HRL validation and documentation workflows, or if implementation shows that LinkML-generated artifacts cannot support required validation and documentation workflows.

Related ADRs:

- [ADR-002: Require standardized, reproducible HRL repositories with GitHub, environment management, CI/CD, and governance files](adr-002-standardized-reproducible-hrl-repositories.md)
- [ADR-008: Use Azure Container Apps Jobs for validation and transformation workflows](adr-008-azure-container-apps-jobs.md)
- [ADR-009: Use PostgreSQL/PostGIS as the authoritative operational store for standardized spatial data](adr-009-postgresql-postgis-operational-store.md)
- [ADR-014: Administer restoration project spatial data as a shared HRL program dataset with DWR as steward](adr-014-restoration-spatial-data-shared-dataset.md)
- [ADR-015: Split the HRL spatial data pipeline across multiple repositories rather than a monorepo](adr-015-spatial-data-pipeline-multiple-repositories.md)
- [ADR-017: Standardize restoration spatial data to EPSG:3310](adr-017-standardize-restoration-spatial-data-epsg-3310.md)
