---
status: proposed
date:
decision-makers: Lucy Andrews
consulted: Ashley Vizek, Jordan Hoang, Emanuel Rodriguez
informed:
---

# Use Azure Container Apps Jobs for validation and transformation workflows

## Context and Problem Statement

Healthy Rivers and Landscapes (HRL) data infrastructure must support repeatable workflows for validating, transforming, and standardizing submitted data before those data are loaded into authoritative storage, published as exports, or used in downstream applications and analyses.

These workflows may include schema validation, geometry validation, coordinate reference system checks, controlled vocabulary checks, transformation to canonical formats, generation of validation reports, and loading of standardized data into PostgreSQL/PostGIS or other serving layers.

Many HRL validation and transformation workflows will require geospatial software dependencies, including tools and libraries that are not always well suited to lightweight serverless functions. These workflows may also need to run on demand, on a schedule, or in response to new submissions, without requiring HRL to maintain long-running servers.

HRL therefore needs a compute pattern for validation and transformation workflows that supports containerized, reproducible execution while minimizing server administration. Because HRL shared infrastructure is DWR-hosted in Azure and follows a PaaS-first architecture, Azure Container Apps Jobs are the preferred compute pattern for these workflows.

## Decision Drivers

- Need to run repeatable validation and transformation workflows for HRL data infrastructure
- Need to support geospatial dependencies such as GDAL, GEOS, PROJ, R geospatial packages, Python geospatial packages, or equivalent tooling
- Need to support reproducible execution environments through containers
- Need to avoid maintaining long-running virtual machines for episodic validation and transformation jobs
- Need to integrate with Azure Storage / ADLS Gen2, PostgreSQL/PostGIS, secrets, logs, and monitoring
- Need to support workflows that can run manually, on a schedule, or in response to new data submissions
- Need to generate validation reports and preserve workflow outputs for review and provenance
- Need to align with the DWR-hosted, PaaS-first Azure architecture
- Need to keep the infrastructure understandable and maintainable for a small Central Data Team

## Considered Options

- Use Azure Container Apps Jobs for validation and transformation workflows
- Use Azure Functions for validation and transformation workflows
- Use Azure Batch or a dedicated batch-computing environment
- Use self-managed virtual machines for validation and transformation workflows
- Run validation and transformation workflows locally or manually

## Decision Outcome

Chosen option: **Use Azure Container Apps Jobs for validation and transformation workflows** because container jobs provide a practical balance of reproducibility, dependency control, Azure integration, and reduced operational burden.

Under this decision, HRL validation and transformation workflows should be packaged as containerized jobs when they need to run as part of shared infrastructure. These jobs may read raw or submitted files from Azure Storage / ADLS Gen2, apply validation and transformation logic, write validation reports and intermediate outputs back to storage, and load standardized records into PostgreSQL/PostGIS or other downstream systems.

This decision does not require every exploratory script, manual prototype, or one-time analysis to run as a Container Apps Job. It applies to shared, repeatable infrastructure workflows that need to be maintained, rerun, audited, or incorporated into production-like HRL data infrastructure.

### Consequences

Desirable:

- Validation and transformation workflows can be packaged with their software dependencies
- Geospatial libraries and command-line tools can be included in the container image
- Jobs can run without maintaining long-running virtual machines
- Workflows can be triggered manually, on a schedule, or through event-driven orchestration
- Jobs can integrate with Azure Storage / ADLS Gen2, PostgreSQL/PostGIS, secrets, logs, and monitoring
- Containerized workflows improve reproducibility across development, testing, and production environments
- Validation reports and transformed outputs can be written to defined storage locations
- The Central Data Team can maintain workflow logic as code while relying on managed Azure execution infrastructure

Undesirable:

- The Central Data Team must maintain container images and deployment configuration
- Contributors may need training in containers and Azure deployment patterns
- Some workflows may require careful resource configuration for memory, CPU, runtime, and concurrency
- Debugging cloud-executed container jobs can be more complex than running scripts locally
- Job orchestration, retries, notifications, and failure handling must be designed explicitly
- Azure Container Apps Jobs may not be the right fit for very large-scale or high-performance batch workloads

### Confirmation

Implementation of this decision can be confirmed by reviewing HRL validation and transformation workflows to determine whether shared, repeatable jobs are containerized and executed using Azure Container Apps Jobs or an approved equivalent.

Examples of confirmation include:

- Validation and transformation workflows have container definitions or container build files
- Job configuration is defined as code or documented deployment configuration
- Jobs read from and write to defined Azure Storage / ADLS Gen2 locations
- Jobs can access required secrets and database connections through approved Azure mechanisms
- Jobs generate validation reports or logs that are preserved for review
- Jobs load standardized outputs into PostgreSQL/PostGIS or another approved serving layer when appropriate
- Job failures are logged and can be reviewed by the Central Data Team
- Local development instructions explain how to run the same validation or transformation code outside Azure for testing

## Pros and Cons of the Options

### Use Azure Container Apps Jobs for validation and transformation workflows

Package validation and transformation workflows as containers and run them as managed Azure jobs.

Desirable:

- Supports reproducible execution environments
- Handles complex geospatial dependencies better than many lightweight serverless approaches
- Avoids maintaining long-running servers for episodic workloads
- Aligns with the DWR-hosted, PaaS-first Azure architecture
- Integrates with Azure Storage, databases, secrets, logs, and monitoring
- Supports scheduled, manual, and event-triggered execution patterns
- Allows workflows to be developed and tested locally in containers before deployment

Neutral:

- Requires container build, registry, and deployment practices
- Resource requirements must be configured per workflow
- Some orchestration or notification needs may require additional Azure services

Undesirable:

- Adds complexity for contributors unfamiliar with containers
- Requires maintenance of container images and deployment configuration
- Cloud debugging can be more difficult than local script execution
- May not be sufficient for very large-scale batch workloads or specialized high-performance computing needs

### Use Azure Functions for validation and transformation workflows

Implement validation and transformation logic as serverless functions.

Desirable:

- Good fit for lightweight event-driven workflows
- Can scale automatically for small tasks
- Reduces infrastructure management burden
- Integrates with Azure events, storage, and monitoring

Neutral:

- Azure Functions may still be useful for lightweight triggers, notifications, or orchestration around larger jobs

Undesirable:

- Less suitable for workflows with heavy geospatial dependencies
- Runtime, memory, packaging, and dependency constraints may create friction
- Long-running validation or transformation jobs may exceed function-oriented design assumptions
- Complex geospatial environments can be harder to maintain in function deployments
- Could split workflow logic across many small functions and reduce readability

### Use Azure Batch or a dedicated batch-computing environment

Run validation and transformation workflows using Azure Batch or another batch-oriented compute platform.

Desirable:

- Suitable for large-scale parallel or compute-intensive workloads
- Supports job queues and managed pools of compute resources
- Can handle workloads that exceed simpler job execution patterns

Neutral:

- May become appropriate for specialized workflows that require substantial parallel processing or high-performance computing

Undesirable:

- More complex than necessary for the expected first generation of HRL validation and transformation workflows
- Requires additional operational knowledge and configuration
- May increase infrastructure complexity before HRL has demonstrated need
- Could make routine validation workflows harder to understand and maintain

### Use self-managed virtual machines for validation and transformation workflows

Run validation and transformation workflows on one or more manually administered virtual machines.

Desirable:

- Provides direct control over installed software and runtime environments
- May be familiar to users accustomed to server-based execution
- Can support specialized tools that are difficult to containerize or run in managed services

Neutral:

- Some IaaS exceptions may be needed for tools that cannot run in managed container services

Undesirable:

- Conflicts with the PaaS-first architecture unless justified as an exception
- Requires operating system patching, security management, backup, monitoring, and server administration
- Increases risk of undocumented server configuration becoming part of the workflow
- Makes reproducibility harder than containerized execution
- Can create long-running infrastructure costs for episodic workloads
- Increases operational burden on the Central Data Team

### Run validation and transformation workflows locally or manually

Run validation and transformation scripts from staff computers or through manual desktop workflows.

Desirable:

- Low initial setup burden
- Familiar to many analysts and data managers
- Useful for prototyping, debugging, or exploratory data preparation

Neutral:

- Local execution may remain appropriate for development, testing, and one-time exploratory work

Undesirable:

- Does not provide a durable infrastructure execution pattern
- Makes runs dependent on local environments, file paths, and individual staff machines
- Makes provenance, logging, repeatability, and auditing harder
- Does not scale well across repeated submissions or multiple datasets
- Makes it difficult to integrate validation workflows with Azure Storage, databases, APIs, and applications
- Increases the risk that production data workflows depend on undocumented manual steps

## More Information

This decision should be revisited if Azure Container Apps Jobs do not meet HRL requirements for performance, cost, orchestration, monitoring, security, or maintainability; if DWR adopts another standard managed job-execution platform; or if HRL workloads grow to require Azure Batch, Databricks, Kubernetes, or another specialized compute environment.

Related ADRs:

- [ADR-001: Adopt the HRL data lifecycle as the organizing framework](adr-001-hrl-data-lifecycle.md)
- [ADR-002: Require standardized, reproducible HRL repositories with GitHub, environment management, CI/CD, and governance files](adr-002-standardized-reproducible-hrl-repositories.md)
- [ADR-006: Use a DWR-hosted, PaaS-first Azure architecture for HRL data infrastructure](adr-006-dwr-hosted-paas-first-azure-architecture.md)
- [ADR-007: Use Azure Storage / ADLS Gen2 as the raw, intermediate, export, and archival object storage backbone](adr-007-azure-storage-adls-gen2-object-storage-backbone.md)
- [ADR-009: Use PostgreSQL/PostGIS as the authoritative operational store for standardized spatial data](adr-009-postgresql-postgis-authoritative-operational-store.md)
- [ADR-010: Publish standardized export files alongside the authoritative database](adr-010-standardized-export-files.md)
- [ADR-017: Use LinkML as the source-of-truth schema language for restoration spatial data](adr-017-linkml-source-of-truth-schema.md)