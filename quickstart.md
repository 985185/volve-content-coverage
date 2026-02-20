# Quickstart

This repository provides a petroleum-engineer-friendly coverage map of the public Equinor Volve dataset.

It does not crawl the dataset.
It uses a frozen metadata catalog and produces structured data-availability tables.

## What problem does this solve?

The Volve dataset is a field archive release, not a curated research dataset.

Before starting any study, you should know:

- Which wells actually have drilling telemetry?
- Which wells have structured daily drilling reports?
- Which wells have wireline logs?
- Which wells have reservoir models or seismic data?

This repo answers those questions.

## Step 1 — Start with the well matrix

Open:

- `outputs/coverage_matrix_binary.csv`

Rows are wells.
Columns are petroleum data categories.
Value is 1 (present) or 0 (not present).

Use this to:

- Select wells for drilling studies (look for DDR_XML, WITSML or XML, and WELL_TECH or DOCS).
- Select wells for log-based studies (look for DLIS and/or LAS).
- Avoid data-poor wells.

## Step 2 — Rank wells by data richness

Open:

- `outputs/coverage_by_well.csv`

Columns:

- well
- total_files
- data_categories_present

Use this to identify high-coverage wells and avoid wells with narrow scope.

## Step 3 — Understand dataset composition

Open:

- `outputs/coverage_by_tag.csv`

This tells you how the dataset is distributed across disciplines.

Examples:

- High WITSML count suggests drilling telemetry is abundant.
- DLIS and LAS indicate wireline logs exist.
- SEGY indicates seismic is present.

## Important notes

- System-level archive folders were excluded to prevent distortion of coverage statistics.
- Well identifiers were extracted from file paths.
- Field-level data (models, seismic packages, general documents) may not appear in well-level tables.

## Recommended use in papers

You may cite this coverage audit methodology as:

“Prior to analysis, a filesystem coverage audit of the Volve dataset was performed to identify wells with sufficient operational and logging data.”

See:
- `docs/dataset_coverage_audit.md`
