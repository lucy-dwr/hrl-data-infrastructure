---
status: accepted
date: 2026-01-01
decision-makers: Lucy Andrews, Louise Conrad, Pascale Goertler
consulted: HRL Science Committee, Ashley Vizek
informed: HRL Science Committee
---

# Allow Central Data Team-managed publication pathways for large or complex datasets

## Context and Problem Statement

Healthy Rivers and Landscapes (HRL) data infrastructure uses static data publication as the default prerequisite for ingestion into shared program infrastructure. In most cases, datasets should be published as documented, versioned, citable releases before they are ingested, standardized, stored, served, or used in program-level synthesis.

However, some HRL-relevant datasets may not fit well into the default EDI-first publication pathway. These may include very large files, complex geospatial datasets, imagery, LiDAR, model outputs, operational reference layers, datasets requiring specialized serving infrastructure, or datasets that need program-managed access and stewardship.

If the EDI-first rule is applied too rigidly, important datasets may be delayed, forced into unsuitable publication formats, or excluded from shared infrastructure. If exceptions are handled informally, HRL risks creating inconsistent publication practices, unclear stewardship, weak metadata, and poorly documented provenance.

HRL therefore needs a defined exception pathway for large or complex datasets that should be managed through the Central Data Team and published or served through an HRL program-supplied platform rather than through the default EDI-first pathway.

## Decision Drivers

- Need to preserve the default expectation of static, citable, documented data publication
- Need to support datasets that are too large, complex, specialized, or unique for the default EDI publication pathway
- Need to avoid ad hoc exceptions that undermine HRL data governance
- Need to ensure that non-EDI datasets still have metadata, provenance, versioning (as needed), stewardship, and access expectations
- Need to support spatial datasets, model outputs, imagery, and other complex data products
- Need to clarify the Central Data Team's role in managing exceptional standardization, storage, and serving pathways
- Need to support FAIR-aligned data access even when traditional repository publication is not the best fit
- Need to ensure that exceptions are documented and reviewable

## Considered Options

- Allow Central Data Team-managed publication pathways for large or complex datasets
- Require all datasets to use the default EDI-first publication pathway without exception
- Allow Data Producers to choose alternative publication pathways independently
- Treat HRL infrastructure as the primary publication pathway for all datasets

## Decision Outcome

Chosen option: **Allow Central Data Team-managed publication pathways for large or complex datasets** because HRL needs a practical and governed way to handle datasets that do not fit the default EDI-first publication model.

Under this decision, EDI remains the default repository for static data publication when appropriate. Exceptions are allowed for datasets whose size, complexity, format, sensitivity, operational character, or serving requirements make EDI-first publication impractical or unsuitable.

When an exception applies, the dataset should be routed through the Central Data Team for review, storage, documentation, publication, and/or serving on an HRL program-supplied platform. The alternative pathway should still provide appropriate metadata, provenance, versioning, access information, and stewardship expectations.

This decision does not eliminate the requirement for documentation or publication-quality stewardship. It creates a governed alternative pathway for datasets that require a different technical or operational approach.

### Consequences

Desirable:

- HRL can support important datasets that do not fit the default EDI-first pathway
- Exceptions are handled through a governed process rather than informal workarounds
- The Central Data Team can evaluate storage, serving, metadata, and stewardship needs for complex datasets
- Large geospatial, model, imagery, and operational datasets can be integrated into HRL infrastructure when appropriate
- HRL can maintain the principle of documented, reusable, and discoverable data products without forcing all datasets into one repository model
- Data Producers have a clear escalation pathway when EDI publication is not suitable
- Program-supplied platforms can support access patterns that static repositories may not provide well

Undesirable:

- The Central Data Team may take on additional storage, publication, and stewardship responsibilities
- Exceptions may create more operational complexity than the default EDI-first pathway
- Alternative publication pathways may require additional infrastructure, documentation, and governance
- Without clear criteria, exceptions could expand too broadly and weaken the default publication rule
- Long-term preservation responsibilities may be less straightforward for program-hosted datasets than for repository-published datasets

### Confirmation

Implementation of this decision can be confirmed by reviewing whether datasets that bypass the default EDI-first pathway have documented exception rationales, Central Data Team involvement, and equivalent stewardship information.

Examples of confirmation include:

- Exception criteria are documented for large, complex, operational, sensitive, or specialized datasets
- Datasets using an exception pathway have assigned Central Data Team stewardship
- Alternative publication or serving locations are documented
- Metadata identify the dataset source, owner, steward, version, update frequency, access pathway, and known limitations
- Provenance records distinguish original submitted data, curated data, standardized data, and served/exported products
- Data inventories distinguish EDI-published datasets from Central Data Team-managed datasets
- Program-hosted datasets include landing pages, documentation, or catalog records sufficient for discovery and reuse
- Exceptions are reviewed periodically to determine whether repository publication has become appropriate

## Pros and Cons of the Options

### Allow Central Data Team-managed publication pathways for large or complex datasets

Permit exceptions to the default EDI-first pathway when datasets require program-managed storage, publication, or serving.

Desirable:

- Provides a practical pathway for datasets that do not fit EDI well
- Keeps exceptions governed and documented
- Preserves the default publication-before-ingestion principle while allowing flexibility
- Supports complex spatial data, imagery, model outputs, and operational reference layers
- Clarifies the Central Data Team's responsibility for exceptional datasets
- Allows HRL to provide fit-for-purpose access mechanisms, such as databases, APIs, maps, bulk downloads, or catalog landing pages

Neutral:

- Exception criteria will need to be refined over time
- Some datasets may use both EDI and HRL infrastructure, depending on their components and access needs
- Program-managed publication may need to evolve as HRL infrastructure matures

Undesirable:

- Requires more Central Data Team capacity
- May create additional infrastructure and maintenance obligations
- Requires careful documentation to avoid confusion about authoritative versions
- Could weaken the default EDI-first rule if exceptions are not limited and reviewed

### Require all datasets to use the default EDI-first publication pathway without exception

Require every HRL dataset to be published through EDI before ingestion, regardless of size, complexity, format, or access needs.

Desirable:

- Creates a simple and consistent rule
- Maximizes use of an established data repository
- Supports citation, versioning, metadata, and preservation through a standard pathway
- Reduces need for HRL to operate repository-like publication services

Neutral:

- This may work well for many tabular, ecological, monitoring, or analysis-ready datasets

Undesirable:

- May be impractical for very large or complex datasets
- May force some datasets into unsuitable formats or publication structures
- May delay important infrastructure and synthesis work
- May fail to support operational access patterns such as APIs, maps, query services, or frequent updates
- May discourage Data Producers from contributing complex but important datasets
- Does not provide a clear pathway for datasets that require program-managed storage or serving

### Allow Data Producers to choose alternative publication pathways independently

Permit Data Producers to decide when EDI is not appropriate and select another repository, storage location, or sharing mechanism.

Desirable:

- Gives Data Producers flexibility
- Allows dataset-specific decisions by people close to the data
- May reduce Central Data Team bottlenecks in the short term

Neutral:

- Data Producers should still provide input on appropriate publication pathways

Undesirable:

- Creates inconsistent publication and documentation practices
- Makes it harder to track provenance and authoritative versions
- Increases risk of poorly documented or inaccessible datasets
- Makes program-level discovery and synthesis harder
- May produce unmanaged dependencies on individual project folders, agency drives, or temporary platforms
- Undermines HRL-wide governance and stewardship expectations

### Treat HRL infrastructure as the primary publication pathway for all datasets

Use HRL program infrastructure as the primary location for storing, publishing, serving, and preserving all HRL datasets, rather than relying on EDI as the default.

Desirable:

- Provides a centralized HRL-branded access point
- Allows HRL to design publication and serving around program needs
- May simplify integration with databases, APIs, maps, and applications
- Gives the Central Data Team direct control over storage and access patterns

Neutral:

- HRL infrastructure should provide publication or serving pathways for some datasets

Undesirable:

- Creates substantial repository, preservation, metadata, and governance responsibilities for HRL
- Duplicates functions already provided by established repositories
- May weaken external discoverability and citation practices
- Increases infrastructure costs and operational burden
- Makes long-term preservation more dependent on HRL-specific systems
- Blurs the distinction between static data publication and operational data services

## More Information

This decision should be revisited if EDI or another repository becomes suitable for the large or complex datasets currently requiring exceptions, if DWR adopts an enterprise data publication platform that provides appropriate citation and preservation functions, or if Central Data Team capacity is insufficient to steward program-managed publication pathways.

Related ADRs:

- [ADR-001: Adopt the HRL data lifecycle as the organizing framework](adr-001-hrl-data-lifecycle.md)
- [ADR-003: Define Data Producers, the Central Data Team, and Synthesis Teams as core governance roles](adr-003-governance-roles.md)
- [ADR-004: Require static publication of data before ingestion, with EDI as the default repository](adr-004-static-publication-before-ingestion.md)
- [ADR-006: Use a PaaS-first Azure architecture for HRL data infrastructure, hosted by DWR](adr-006-paas-first-azure-architecture.md)