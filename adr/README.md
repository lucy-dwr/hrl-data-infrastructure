# ADRs

An architectural decision record (ADR) is a lightweight document that captures a
specific architectural decision, the context behind it, and its consequences.
ADRs serve as persistent decision logs that help future developers and architects
understand why a system was built a certain way.

## MADR

[Markdown Architectural Decision Record (MADR)](https://adr.github.io/madr/) is
the format in which ADRs are documented in this repository. A [template](adr-template-bare.md)
sourced from the [ADR GitHub organization](https://adr.github.io) is included in
this repository to streamline the process of writing ADRs. The ADR GitHub
organization has also published an [annotated template](https://github.com/adr/madr/blob/develop/template/adr-template.md)
to provide guidance on completing ADRs.

## ADRs

| ADR | Title | Status |
|---|---|---|
| [001](adr/adr-001-hrl-data-lifecycle.md) | Adopt the HRL data lifecycle as the organizing framework | 🟢&nbsp;Accepted |
| [002](adr/adr-002-standardized-reproducible-hrl-repositories.md) | Require semi-standardized, reproducible HRL repositories with GitHub, environment management, CI/CD, and governance files | 🟡&nbsp;Proposed |
| [003](adr/adr-003-governance-roles.md) | Define Data Producers, the Central Data Team, and Synthesis Teams as core governance roles | 🟢&nbsp;Accepted |
| [004](adr/adr-004-static-publication-before-ingestion.md) | Require static publication of data before ingestion, with EDI as the default repository | 🟢&nbsp;Accepted |
| [005](adr/adr-005-central-data-team-managed-publication-pathways.md) | Allow Central Data Team-managed publication pathways for large or complex datasets | 🟢&nbsp;Accepted |
| [006](adr/adr-006-paas-first-azure-architecture.md) | Use a PaaS-first Azure architecture for HRL data infrastructure, hosted by DWR | 🟢&nbsp;Accepted |
| [007](adr/adr-007-azure-storage-adls-gen2-object-storage.md) | Use Azure Storage / ADLS Gen2 as the raw, intermediate, export, and archival object storage backbone | 🟡&nbsp;Proposed |
| [008](adr/adr-008-azure-container-apps-jobs.md) | Use Azure Container Apps Jobs for validation and transformation workflows | 🟡&nbsp;Proposed |
| [009](adr/adr-009-postgresql-postgis-operational-store.md) | Use PostgreSQL/PostGIS as the authoritative operational store for standardized spatial data | 🟢&nbsp;Accepted |
| [010](adr/adr-010-standardized-export-files.md) | Publish standardized export files alongside the authoritative database | 🟢&nbsp;Accepted |
| [011](adr/adr-011-posit-workbench-posit-connect.md) | Procure and use Posit Workbench and Posit Connect for data science and application publishing | 🟢&nbsp;Accepted |
| [012](adr/adr-012-separate-azure-data-engineering-and-posit.md) | Separate the Azure data engineering stack from the Posit data science platform | 🟢&nbsp;Accepted |
| [013](adr/adr-013-posit-iaas-exception.md) | Treat Posit as a deliberate IaaS exception to the PaaS-first principle | 🟢&nbsp;Accepted |
| [014](adr/adr-014-restoration-spatial-data-shared-dataset.md) | Administer restoration project spatial data as a shared HRL program dataset with DWR as steward | 🟢&nbsp;Accepted |
| [015](adr/adr-015-spatial-data-pipeline-multiple-repositories.md) | Split the HRL spatial data pipeline across multiple repositories rather than a monorepo | 🟢&nbsp;Accepted |
| [016](adr/adr-016-linkml-source-of-truth-schema.md) | Use LinkML as the source-of-truth schema language for restoration spatial data | 🟢&nbsp;Accepted |
| [017](adr/adr-017-standardize-restoration-spatial-data-epsg-3310.md) | Standardize restoration spatial data to EPSG:3310 | 🟢&nbsp;Accepted |

## Potential forthcoming ADRs

| Candidate ADR | Title | Status |
|---|---|---|
| ADR-018 | Define the restoration project map architecture | ⚪&nbsp;Candidate |
| ADR-019 | Define the update workflow for restoration project records | ⚪&nbsp;Candidate |
| ADR-020 | Define the metadata and catalog strategy for HRL infrastructure datasets | ⚪&nbsp;Candidate |
| ADR-021 | Define authentication, authorization, and secret-management patterns for HRL infrastructure | ⚪&nbsp;Candidate |
| ADR-022 | Define database migration and schema-change management strategies | ⚪&nbsp;Candidate |
| ADR-023 | Define backup, archival, logging, and operational retention strategy | ⚪&nbsp;Candidate |