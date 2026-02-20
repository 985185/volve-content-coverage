[![Dataset Coverage Audit](https://img.shields.io/badge/Dataset-Coverage_Audit-blue)](docs/dataset_coverage_audit.md)
[![Reproducible](https://img.shields.io/badge/Method-Reproducible-green)](quickstart.md)
[![Metadata Based](https://img.shields.io/badge/Input-Frozen_Metadata_Catalog-orange)](https://github.com/985185/volve-metadata-index)
[![Petroleum Engineering](https://img.shields.io/badge/Domain-Petroleum_Engineering-red)](#)
# volve-content-coverage

Petroleum-engineer-friendly coverage map for the public Equinor Volve dataset.

This repository does not crawl the Volve dataset.
It transforms a frozen filesystem catalog into data-availability tables so you can answer practical questions like:
- Which wells have drilling telemetry?
- Which wells have daily drilling reports?
- Which wells have wireline logs?
- Which wells have seismic or interpretation data?

## Input

Frozen catalog produced by the separate project `volve-metadata-index` (frozen, not modified):
- `volve_catalog_v1.csv` (GitHub release)

## Outputs

All outputs are small by design. They are coverage references, not raw data.

- `outputs/coverage_by_well.csv`
  - Per-well summary: total file count and number of data categories present.
- `outputs/coverage_by_tag.csv`
  - File counts per data category (after filtering out system archives).
- `outputs/coverage_matrix_binary.csv`
  - Well x data-category matrix (1 = present, 0 = not present).
- `outputs/coverage_matrix_counts.csv`
  - Same matrix, but with file counts instead of binary presence.

## Method summary

1. Load the frozen catalog into Databricks.
2. Filter to files only (exclude directories).
3. Exclude large system-level archives that distort coverage statistics (not petroleum content).
4. Extract well identifiers from file paths (since many field-level folders are not well-scoped).
5. Build well-level and field-level coverage tables and a well x category matrix.

## Notes and limitations

- Many catalog rows are field-level (models, seismic packages, general docs) and do not contain a well identifier in the path.
- Well identifiers are derived from path patterns, so minor naming variants can create duplicates (for example, spacing or suffix formatting). If needed, normalize these in a follow-up refinement.
- Coverage is based on file presence and tags, not file content parsing.

## Suggested use

Use these tables to select wells for drilling and completion studies, justify data availability in SPE papers, and avoid ad hoc file hunting.
