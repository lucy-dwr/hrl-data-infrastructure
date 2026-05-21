# ADRs

An architectural decision record (ADR) is a lightweight document that captures a
specific architectural decision, the context behind it, and its consequences.
ADRs serve as persistent decision logs that helps future developers and 
architects understand why a system was built a certain way.

This file can be a place to identify ADRs that have already been made in the
HRL program and that need to be written up. It can also evolve into an ADR table
of contents that links to ADR docs.

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
| ADR-001 | Adopt the HRL data lifecycle as the organizing framework | Accepted |
| ADR-002 | Require standardized, reproducible HRL repositories with GitHub, environment management, CI/CD, and governance files | Proposed |
| ADR-003 | Define Data Producers, the Central Data Team, and Synthesis Teams as core governance roles | Accepted |
| ADR-004 | Require static publication of data before ingestion, with EDI as the default repository | Accepted |
| ADR-005 | Allow Central Data Team-managed publication pathways for large or complex datasets | Accepted |
| ADR-006 | Use a PaaS-first Azure architecture for HRL data infrastructure, hosted by DWR | Accepted |
| ADR-007 | Use Azure Storage / ADLS Gen2 as the raw, intermediate, export, and archival object storage backbone | Proposed |
| ADR-008 | Use Azure Container Apps Jobs for validation and transformation workflows | Proposed |
| ADR-009 | Use PostgreSQL/PostGIS as the authoritative operational store for standardized spatial data | Accepted |
| ADR-010 | Publish standardized export files alongside the authoritative database | Proposed |
| ADR-011 | Procure and use Posit Workbench and Posit Connect for data science and application publishing | Accepted |
| ADR-012 | Separate the Azure data engineering stack from the Posit data science platform | Accepted |
| ADR-013 | Treat Posit as a deliberate IaaS exception to the PaaS-first principle | Accepted |
| ADR-014 | Administer restoration project spatial data as a shared HRL program dataset with DWR as steward | Accepted |
| ADR-015 | Split the HRL spatial data pipeline across multiple repositories rather than a monorepo | Accepted |
| ADR-016 | Use LinkML as the source-of-truth schema language for restoration spatial data | Accepted |
| ADR-017 | Standardize restoration spatial data to EPSG:3310 | Accepted |
