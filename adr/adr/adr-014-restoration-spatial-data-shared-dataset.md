# Administer restoration project spatial data as a shared HRL program dataset with DWR as steward

> **Status:** Accepted  
> **Date:** 2026-05-07  
> **Decision makers:** Lucy Andrews  
> **Consulted:**  
> **Informed:** Louise Conrad, Pascale Goertler, Erik Loboschefsky, Josh Martinez, HRL Habitat Implementation Team

## Context and problem statement

Healthy Rivers and Landscapes (HRL) needs a shared spatial dataset representing restoration projects across the program. This dataset is expected to support planning, coordination, reporting, mapping, synthesis, and communication across HRL systems and partner agencies.

Restoration project spatial data are not a DWR dataset, even if DWR hosts and stewards the technical infrastructure. The data represent program-level restoration information contributed by multiple agencies, programs, implementers, and partners. The data include project locations, project types, implementation stages, responsible entities, target species, funding, and other attributes needed to understand restoration work across the HRL program.

If restoration project spatial data are treated as a collection of separate agency files, project-specific spreadsheets, or ad hoc map layers, HRL will have difficulty maintaining a consistent view of restoration implementation. If the data are treated as solely DWR-owned, HRL may create confusion about program governance, partner contributions, review expectations, and shared trust in the dataset.

HRL therefore needs to administer restoration project spatial data as a shared HRL program dataset, with DWR serving as the technical steward responsible for hosting, maintaining, standardizing, and publishing the dataset through the HRL data infrastructure.

## Decision drivers

- Need for a shared spatial dataset representing restoration projects across HRL
- Need to support program-level mapping, synthesis, reporting, coordination, and decision support
- Need to avoid fragmented restoration project records across agency files, spreadsheets, and one-off map layers
- Need to clarify that the dataset is program-serving, even though DWR hosts and stewards the technical implementation
- Need to provide a consistent schema, geometry policy, validation workflow, and update process
- Need to support partner agency contributions and review while maintaining a curated program dataset
- Need to distinguish data stewardship from scientific or policy ownership
- Need to support public, partner, and internal access products where appropriate
- Need to align restoration project data management with the HRL data lifecycle and DWR-hosted infrastructure architecture

## Considered options

- Administer restoration project spatial data as a shared HRL program dataset with DWR as steward
- Treat restoration project spatial data as a DWR-owned dataset
- Allow each partner agency or project team to maintain its own restoration project spatial data
- Treat the restoration project spatial dataset as a temporary map product rather than a maintained program dataset
- Outsource stewardship of the restoration project spatial dataset to another agency or external organization

## Decision outcome

Chosen option: **Administer restoration project spatial data as a shared HRL program dataset with DWR as steward** because HRL needs a consistent, trusted, program-level view of restoration projects while also needing a specific entity to steward the technical implementation.

Under this decision, the restoration project spatial dataset is treated as a shared HRL program dataset. DWR serves as the technical steward responsible for maintaining the data infrastructure, schema implementation, validation workflow, storage, exports, and access products. DWR stewardship does not mean that DWR is the sole scientific, policy, or program owner of the data. Partner agencies and HRL governance processes may still contribute to standards, review, priorities, access decisions, and interpretation.

The dataset should be maintained using HRL data infrastructure practices, including a machine-readable schema, geometry policy, reproducible validation and ingestion workflows, authoritative storage in PostgreSQL/PostGIS, standardized exports, and documentation for contributors and users.

### Consequences

Desirable:

- HRL has a single shared program dataset for restoration project spatial information
- Restoration project data can support program-level mapping, reporting, synthesis, and coordination
- DWR stewardship provides a clear technical owner for infrastructure, validation, storage, exports, and maintenance
- Partner contributions can be incorporated into a consistent schema and geometry policy
- The dataset can be treated as a maintained program asset rather than a one-time map product
- Standardized data can be served through maps, APIs, exports, reports, and analytical workflows
- Data quality, provenance, and update processes can be documented and improved over time
- The decision clarifies that hosting and stewardship do not imply sole DWR ownership of program meaning or governance

Undesirable:

- DWR takes on exclusive stewardship responsibilities for a dataset that serves the broader HRL program
- Partner agencies may need guidance on how to submit, review, or correct records
- Shared governance may be needed for contested records, sensitive information, public-facing fields, or interpretation
- The dataset will require ongoing maintenance as projects change stages, locations, designs, or implementation status
- DWR may need to balance program-wide expectations with its own infrastructure capacity and staffing and governance constraints
- Users may need help understanding the difference between the authoritative dataset, exported files, and map products derived from it

### Confirmation

Implementation of this decision can be confirmed by reviewing HRL restoration project data documentation, schema repositories, infrastructure workflows, and access products to determine whether the dataset is maintained as a shared program asset with DWR as technical steward.

Examples of confirmation include:

- Documentation identifies the restoration project spatial dataset as a shared HRL program dataset
- Documentation identifies DWR as the technical steward or infrastructure steward
- The dataset uses the HRL restoration schema or another approved schema
- Submitted restoration project records are validated before ingestion
- Standardized records are stored in the authoritative PostgreSQL/PostGIS database
- Standardized exports are generated from the authoritative database or documented views
- Maps, reports, dashboards, or APIs identify the dataset source and update process
- Partner contribution, correction, and review pathways are documented
- Metadata distinguish stewardship, contribution, source, update date, and publication or access status
- Public-facing products clearly indicate limitations, update frequency, and appropriate use

## Pros and cons of the options

### Administer restoration project spatial data as a shared HRL program dataset with DWR as steward

Maintain the restoration project spatial dataset as a shared HRL asset, with DWR responsible for technical stewardship.

Desirable:

- Provides a single program-level view of restoration projects
- Clarifies technical stewardship while preserving the dataset's shared program purpose
- Supports standardized schema, validation, storage, export, and access workflows
- Reduces duplication and inconsistency across project-specific or agency-specific files
- Supports program-level reporting, analysis, synthesis, and mapping
- Creates a durable foundation for future public-facing and internal products
- Allows partner agencies to contribute within a governed data structure

Neutral:

- DWR stewardship may need to be paired with HRL governance or review processes
- Some project-specific details may remain in partner systems or source documents
- Some fields may have different access rules for internal, partner, and public uses

Undesirable:

- Requires ongoing DWR stewardship capacity
- Requires clear contribution and correction workflows
- May require governance decisions for contested, sensitive, incomplete, or uncertain project records
- Could be misunderstood as DWR ownership if documentation is not clear

### Treat restoration project spatial data as a DWR-owned dataset

Administer the dataset as a DWR dataset rather than a shared HRL program dataset.

Desirable:

- Provides clear ownership and decision authority
- May simplify internal DWR administration, approval, and publication
- Aligns with DWR hosting and technical stewardship capacity

Neutral:

- DWR may still be responsible for hosting or maintaining some HRL-related products beyond this dataset

Undesirable:

- Does not accurately reflect the interagency and program-wide nature of HRL restoration data
- May reduce partner trust or willingness to contribute
- Could obscure shared governance needs
- May make the dataset appear less legitimate as an HRL-wide source of restoration information
- Blurs the distinction between technical stewardship and program ownership

### Allow each partner agency or project team to maintain its own restoration project spatial data

Do not create a shared program dataset; instead, allow each agency, project team, or implementer to maintain its own spatial records.

Desirable:

- Allows data to remain close to the people who know each project best
- Reduces immediate central stewardship burden
- Allows agency- or project-specific schemas and workflows

Neutral:

- Source project systems may still remain important and may feed the shared dataset

Undesirable:

- Produces fragmented and inconsistent restoration project information
- Makes program-level mapping, synthesis, and reporting difficult
- Increases duplication and reconciliation burden
- Makes it harder to determine which record is current or authoritative
- Does not support consistent validation, geometry policy, or access products
- Makes shared HRL communication products harder to maintain

### Treat the restoration project spatial dataset as a temporary map product rather than a maintained program dataset

Develop a spatial layer or map for a specific immediate communication need without treating the underlying data as a maintained program dataset.

Desirable:

- Lower initial governance and infrastructure burden
- Faster path to an initial map or communication product
- Useful for prototypes or exploratory planning

Neutral:

- A temporary map product may help demonstrate the value of a maintained dataset

Undesirable:

- Does not create durable data infrastructure
- Risks producing an outdated or unmaintained map
- Does not support long-term synthesis, reporting, or program tracking
- Encourages manual updates and ad hoc data handling
- Makes schema, validation, provenance, and stewardship secondary
- Could create user trust in a product that lacks a maintained data foundation

### Outsource stewardship of the restoration project spatial dataset to another agency or external organization

Assign primary stewardship of the shared dataset to another agency, consultant, academic partner, or external organization.

Desirable:

- Could reduce DWR's direct stewardship burden
- Could leverage specialized external GIS, data management, or restoration-tracking expertise
- Could be appropriate if another organization already maintains a related dataset

Neutral:

- External partners may still contribute data, review records, or support specific products

Undesirable:

- No other entity currently appears positioned to host and steward the dataset as part of the HRL data infrastructure
- May complicate integration with DWR-hosted Azure, PostgreSQL/PostGIS, validation, and export workflows
- Could create unclear long-term funding, access, maintenance, and governance dependencies
- May reduce HRL's ability to align the dataset with its schema, infrastructure, and lifecycle decisions
- Could make data stewardship dependent on contracts or temporary project arrangements

## More information

This decision should be revisited if HRL governance assigns technical stewardship to another entity, if DWR no longer has capacity to steward the dataset, if a partner agency develops a more appropriate shared stewardship platform, or if the restoration project spatial dataset no longer serves program-level HRL needs.

Related ADRs:

- [ADR-001: Adopt the HRL data lifecycle as the organizing framework](adr-001-hrl-data-lifecycle.md)
- [ADR-003: Define Data Producers, the Central Data Team, and Synthesis Teams as core governance roles](adr-003-governance-roles.md)
- [ADR-005: Allow Central Data Team-managed publication pathways for large or complex datasets](adr-005-central-data-team-managed-publication-pathways.md)
- [ADR-006: Use a DWR-hosted, PaaS-first Azure architecture for HRL data infrastructure](adr-006-paas-first-azure-architecture.md)
- [ADR-009: Use PostgreSQL/PostGIS as the authoritative operational store for standardized spatial data](adr-009-postgresql-postgis-operational-store.md)
- [ADR-010: Publish standardized export files alongside the authoritative database](adr-010-standardized-export-files.md)
- [ADR-016: Use LinkML as the source-of-truth schema language for restoration spatial data](adr-016-linkml-source-of-truth-schema.md)
- [ADR-017: Standardize restoration spatial data to EPSG:3310](adr-017-standardize-restoration-spatial-data-epsg-3310.md)
