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

## Architecture overview

The proposed infrastructure follows a **four-layer model**:

| Layer | Responsibility | Key tech |
|---|---|---|
| 1 — Source & Publication | Federated data producers publish to stable archives | EDI, EML; alternative archive for complex data objects TBD |
| 2 — Ingestion & Standardization | Automated pipelines harvest, validate, and standardize | R (primary), orchestration framework TBD (`targets` / Nextflow / Snakemake), containerization TBD, GitHub Actions |
| 3 — Storage & Serving | Central store of analysis-ready products | Cloud object storage TBD (Azure Blob Storage leading candidate), Parquet, vector format TBD (GeoPackage / GeoParquet), COG, PostgreSQL + PostGIS |
| 4 — Access & Applications | Data reaches analysts and the public | `hrldata` R package, data catalog, Shiny / Streamlit / other dashboards, Quarto, REST API |

## Technology choices and rationale

- **R as primary language** — the HRL science community is R-first; all
  pipelines and the analyst-facing SDK are R-based.
- **Pipeline orchestration: TBD** — leading candidates are `targets` (R-native,
  lower learning curve), Nextflow (polyglot, strong HPC/cloud support), and
  Snakemake (Python-based, language-agnostic). Decision pending assessment of
  likely language mix and compute requirements.
- **EDI as primary data archive** — standard in freshwater ecology community;
  EML metadata; scriptable via `EDIutils`, `EMLassemblyline`, and `hrlpub`; free
  DOIs. Archive for large/complex data objects (LiDAR, EO, model outputs) TBD.
- **Cloud object storage: TBD** — Azure Blob Storage is the leading candidate
  given DWR's existing enterprise agreement, but the decision has not been made.
  All data stored in open formats so the storage layer is swappable.
- **Vector spatial format: TBD** — GeoPackage is widely used; GeoParquet is
  emerging as a more cloud-native alternative. Decision before first spatial
  pipeline.
- **Containerization: TBD** — Docker is the leading candidate; subject to DWR
  IT policy constraints on shared compute.
- **STAC** — SpatioTemporal Asset Catalog standard for spatial/raster data
  discovery. Target for LiDAR and EO product catalog.
- **Open formats everywhere** — Parquet (tabular), vector format TBD, COG
  (raster). No proprietary formats in the serving layer.

## Coding standards

All code in this repo follows the forthcoming **HRL Style and Development Guide**.
Key conventions:

- R with fully qualified function calls (`package::function()`) — no bare
  `library()` calls in scripts
- Pipeline orchestration framework TBD (see Technology choices above)
- `renv` for dependency locking — always commit `renv.lock`
- `here::here()` for all paths — no absolute paths, ever
- Snake case for files, folders, functions, and objects
- Conventional commits (`feat:`, `fix:`, `docs:`, `data:`, `refactor:`)
- Containerization tooling TBD (Docker leading candidate, pending DWR IT policy)
- GitHub Actions for CI/CD — PRs must pass lint, style, and schema checks

Formatting: 2-space indent, 80–90 character soft line limit, 120 hard limit.
Base R pipe (`|>`) preferred over magrittr (`%>%`).

## Data principles

- **FAIR** (Findable, Accessible, Interoperable, Reusable) and **CARE**
  (Collective Benefit, Authority to Control, Responsibility, Ethics) aligned
- All HRL data producers must publish to EDI with compliant EML metadata before
  data is eligible for ingestion (the "publication contract"), unless data are
  large or unusual (e.g., EO data)
- Raw data: immutable, never overwritten, checksummed
- All pipelines: scripted, deterministic, versioned, CI/CD-gated
- Tribal data: access-controlled; sensitivity classification required before
  storage or sharing
- Semantic versioning for all data products; major schema changes get a new DOI

## Current status and immediate priorities

The team is currently in a planning phase. Immediate priorities:

1. Schema design for the first wave of data types (in progress — needs cross-agency working group)
2. GitHub organization and repo structure setup
3. Cloud storage provisioning
4. Data engineer hire
5. Publication contract documentation (lives in `hrl-docs`)

The repo is nascent. Expect to find planning documents, architecture decision
records, schema drafts, and early pipeline scaffolding here.

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
