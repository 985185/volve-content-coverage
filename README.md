[![Dataset Coverage Audit](https://img.shields.io/badge/Dataset-Coverage_Audit-blue)](docs/dataset_coverage_audit.md)
[![Quickstart](https://img.shields.io/badge/Guide-Quickstart-green)](quickstart.md)
[![Input: Frozen Catalog](https://img.shields.io/badge/Input-Frozen_Metadata_Catalog-orange)](https://github.com/985185/volve-metadata-index)
[![Build Notes](https://img.shields.io/badge/Build-Databricks_Notes-lightgrey)](notebooks/databricks_build.md)
[![Wells Covered](https://img.shields.io/badge/Wells-27-lightgrey)](outputs/coverage_matrix_binary.csv)
[![Data Categories](https://img.shields.io/badge/Data_Categories-10-lightgrey)](outputs/coverage_matrix_binary.csv)

# volve-content-coverage

Petroleum-engineer-friendly coverage map for the public Equinor Volve dataset.

This repository does not crawl the Volve dataset.
It transforms a frozen filesystem catalog into data-availability tables so you can answer practical questions like:

- Which wells have logs?
- Which wells have drilling telemetry?
- Which wells have reports?
- Which wells have seismic or interpretation data?
- What data types exist per well?

## Input

Frozen catalog produced by the separate project `volve-metadata-index` (frozen and not modified):

- `volve_catalog_v1.csv` GitHub release

## Outputs

These outputs are intentionally small.
They are coverage references, not raw Volve data.

- `outputs/coverage_by_well.csv`
  - Per-well summary: total file count and number of data categories present.
- `outputs/coverage_by_tag.csv`
  - File counts per data category (after filtering system-level archives).
- `outputs/coverage_matrix_binary.csv`
  - Well x data-category matrix (1 = present, 0 = not present).
- `outputs/coverage_matrix_counts.csv`
  - Same matrix, but with file counts instead of binary presence.

## Method summary

1. Load the frozen catalog in Databricks.
2. Filter to file entries only (exclude directories).
3. Exclude system-level archive folders that dominate row counts but do not represent petroleum engineering content.
4. Extract well identifiers from file paths (field-level folders are not well-scoped).
5. Build well-level and field-level coverage tables and a well x category matrix.

Details:
- `docs/dataset_coverage_audit.md`
- `notebooks/databricks_build.md`

## Notes and limitations

- Many catalog rows are field-level (models, seismic packages, general documents) and do not contain a well identifier in the path.
- Well identifiers are derived from path patterns, so minor naming variants can create duplicates (spacing and suffix formatting). Normalize further if needed.
- Coverage is based on file presence and tags, not file content parsing.

## Suggested use

Use these tables to select wells for drilling and completion studies, justify data availability in SPE papers, and avoid ad hoc file hunting.


## Citation

If you use this coverage audit in research, please cite:

Appalla, Tejaswy (2026). Volve Content Coverage: A petroleum data availability audit of the Equinor Volve public dataset. GitHub research artifact. https://github.com/985185/volve-content-coverage


## References

Equinor. Volve Field Data Village (public dataset release).  
https://www.equinor.com/energy/volve-data-sharing

Metadata inventory used in this project:  
https://github.com/985185/volve-metadata-index
