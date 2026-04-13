# Agent Context — hrl-data-infrastructure

## What this repo is

This repository contains planning, design, and eventually implementation
artifacts for the **HRL (Healthy Rivers and Landscapes) data infrastructure** —
the technical backbone of the HRL Science Program's data engineering and data
science enterprise.

HRL is an eight-year, multi-agency ecological restoration and monitoring program
in the Sacramento River watershed and Bay-Delta estuary. The Science Program
investigates how coordinated restoration and environmental flows affect native
fish and aquatic ecosystems. This infrastructure exists to make the program's
data open, reproducible, interoperable, and usable over that full time horizon.

## Repo owner

Lucy Andrews, Senior Environmental Scientist, California Department of Water
Resources (DWR). Primary contact: lucy.andrews@water.ca.gov.

## Companion resources

- **HRL Docs site (primary documentation hub):**
  https://lucy-dwr.github.io/hrl-docs/
- **hrl-docs repo (source for docs site):** https://github.com/lucy-dwr/hrl-docs
- **HRL program website:** https://resources.ca.gov/Initiatives/Voluntary-Agreements-Page
- **DWR:** https://water.ca.gov/

Key documents already produced and linked from the docs site:
- HRL Data Governance and Management Plan (DGMP)
- HRL Style and Development Guide (outline — will become an online book)
- HRL Data Architecture Proposal (the founding document for this repo)

## Architecture overview

The proposed infrastructure follows a **four-layer model**:

| Layer | Responsibility | Key tech |
|---|---|---|
| 1 — Source & Publication | Federated data producers publish to stable archives | EDI, EML, Zenodo |
| 2 — Ingestion & Standardization | Automated pipelines harvest, validate, and standardize | R, `targets`, Docker, GitHub Actions |
| 3 — Storage & Serving | Central store of analysis-ready products | Azure Blob Storage, Parquet, GeoPackage, COG, PostgreSQL + PostGIS |
| 4 — Access & Applications | Data reaches analysts and the public | `hrldata` R package, data catalog, Shiny, Quarto, Plumber API |

**Phase 1 deliverable (Year 1):** Functional ingestion pipelines for the first
wave of HRL datasets + a simple queryable data catalog. STAC spatial catalog and
REST API are Phase 2 targets.

## Technology choices and rationale

- **R as primary language** — the HRL science community is R-first; all
  pipelines and the analyst-facing SDK are R-based.
- **`targets` for pipeline orchestration** — dependency graph, caching,
  reproducibility, CI/CD integration.
- **EDI as primary data archive** — standard in freshwater ecology community;
  EML metadata; scriptable via `EDIutils` and `EMLassemblyline`; free DOIs.
- **Azure Blob Storage** — DWR has an existing enterprise Azure agreement;
  chosen as implementation convenience, not hard dependency. All data stored in
  open formats (Parquet, GeoPackage, COG) so storage layer is swappable.
- **STAC (Phase 2)** — SpatioTemporal Asset Catalog standard for spatial/raster
  data discovery. Target for LiDAR and EO product catalog.
- **Open formats everywhere** — Parquet (tabular), GeoPackage (vector), COG
  (raster). No proprietary formats in the serving layer.

## Coding standards

All code in this repo follows the **HRL Style and Development Guide**. Key
conventions:

- R with fully qualified function calls (`package::function()`) — no bare
  `library()` calls in scripts
- `targets`-based pipeline orchestration
- `renv` for dependency locking — always commit `renv.lock`
- `here::here()` for all paths — no absolute paths, ever
- Snake case for files, folders, functions, and objects
- Conventional commits (`feat:`, `fix:`, `docs:`, `data:`, `refactor:`)
- Docker for containerization of pipelines
- GitHub Actions for CI/CD — PRs must pass lint, style, and schema checks

Formatting: 2-space indent, 80–90 character soft line limit, 120 hard limit.
Base R pipe (`|>`) preferred over magrittr (`%>%`).

## Data principles

- **FAIR** (Findable, Accessible, Interoperable, Reusable) and **CARE**
  (Collective Benefit, Authority to Control, Responsibility, Ethics) aligned
- All HRL data producers must publish to EDI with compliant EML metadata before
  data is eligible for ingestion (the "publication contract")
- Raw data: immutable, never overwritten, checksummed
- All pipelines: scripted, deterministic, versioned, CI/CD-gated
- Tribal data: access-controlled; sensitivity classification required before
  storage or sharing
- Semantic versioning for all data products; major schema changes get a new DOI

## Current status and immediate priorities

The team is currently in **Phase 0** (foundations). Immediate priorities:

1. Schema design for the first wave of data types (in progress — needs cross-agency working group)
2. GitHub organization and repo structure setup
3. Azure Blob Storage provisioning
4. Data engineer hire (position description in development)
5. Publication contract documentation (lives in hrl-docs)

The repo is nascent. Expect to find planning documents, ADRs, schema drafts, and
early pipeline scaffolding here. Full ingestion pipelines will land in Phase 1.

## What this repo will contain (anticipated structure)

```
hrl-data-infrastructure/
├── docs/                  # Design documents, proposals, ADRs
│   ├── architecture/      # Architecture proposal and diagrams
│   └── decisions/         # Architecture Decision Records (ADRs)
├── schemas/               # Program-wide data model and schema definitions
│   ├── tabular/           # JSON Schema / YAML for tabular data types
│   └── spatial/           # Schema and CRS standards for spatial products
├── pipelines/             # Ingestion and standardization pipelines (Phase 1)
│   └── <dataset-name>/    # One folder per ingested dataset
├── infrastructure/        # Cloud infrastructure config (Phase 1+)
│   ├── azure/             # Azure Blob Storage config, access policies
│   └── postgres/          # DB schema, migration scripts
├── catalog/               # Data catalog build (Phase 1)
└── sdk/                   # hrldata R package (or link to separate repo)
```

## Key constraints and sensitivities

- **Interagency context** — avoid infrastructure choices that require partners
  to adopt DWR-specific systems or accounts. Public data must be accessible
  without authentication.
- **Small team** — currently 1–2 people. Proposals and implementations must be
  realistic for this team size. Do not over-engineer.
- **8-year horizon** — choices must be maintainable over program lifetime and
  through personnel turnover. Favor boring, well-documented technology over
  clever or novel approaches.
- **Open science commitment** — everything that can be public should be public,
  including this repo and its design decisions.
- **No lock-in** — open formats, open standards, open source tooling at every
  layer where feasible.
