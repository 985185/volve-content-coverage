# Databricks build notes

This repository is generated from a frozen filesystem catalog and does not crawl the Volve dataset.

## Input

Frozen catalog CSV:

- `volve_catalog_v1.csv` from the `volve-metadata-index` GitHub release

## Environment constraints

Some Databricks environments block `/dbfs` writes and `file:/` to DBFS copying. The reliable approach used here was:

- download to `/tmp`
- process with pandas
- copy final CSV outputs into a Unity Catalog volume (e.g., `/Volumes/workspace/default/exports`)
- download from the volume via the Databricks UI

## Steps performed

### 1) Download catalog

Downloaded the catalog CSV directly inside Databricks to driver storage:

- `/tmp/volve_catalog_v1.csv`

### 2) Load catalog and normalize tags

Loaded the CSV and split the `tags` field into a list using `|` as separator.

### 3) Filter to petroleum-relevant file inventory

- Keep `type == file`
- Exclude the dominant system archive folder:
  - `top_folder == "PI System Manager Sleipner"`

This prevents system exports from distorting coverage statistics.

### 4) Extract well identifiers from path

Because many rows are field-level content and do not include the `well` column, well identifiers were extracted from `path` using Volve naming patterns (e.g., `15/9-F-1` and suffixes).

A derived column (commonly referred to as `well_x`) was used for well-level aggregation.

### 5) Produce coverage tables

Generated:

- `coverage_by_tag.csv`
  - tag counts on the filtered dataset
- `coverage_matrix_counts.csv`
  - well x tag file counts
- `coverage_matrix_binary.csv`
  - well x tag presence (1/0)
- `coverage_by_well.csv`
  - per-well totals and number of categories present

### 6) Export outputs

Saved outputs to a Unity Catalog volume for download and then uploaded to GitHub:

- `outputs/coverage_by_tag.csv`
- `outputs/coverage_matrix_counts.csv`
- `outputs/coverage_matrix_binary.csv`
- `outputs/coverage_by_well.csv`

## Notes

- Field-level content (models, seismic packages, general documents) may not map to a specific well and therefore may not appear in well-level matrices.
- Coverage is based on file presence and tags, not content parsing.
