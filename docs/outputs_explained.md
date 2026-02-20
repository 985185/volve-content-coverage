# Outputs explained (petroleum terms)

## outputs/coverage_by_well.csv

Purpose:
- Rank wells by how much information exists for each well.

Columns:
- well: Volve well or wellbore identifier.
- total_files: number of files associated with that well (after filtering).
- data_categories_present: how many distinct data categories exist for that well.

How to use:
- Select candidate wells for drilling studies by choosing wells with high data category coverage.
- Identify wells that are present but data-poor, and exclude them early.

## outputs/coverage_by_tag.csv

Purpose:
- Quantify dataset composition by petroleum data category after removing system archives.

Columns:
- tag: category label (for example DLIS, LAS, DDR_XML, SEGY).
- file_count: number of files with that tag.

How to use:
- Justify which research directions Volve supports (drilling-heavy, log-rich, etc).
- Avoid building a study on a data type that is sparsely represented.

## outputs/coverage_matrix_binary.csv

Purpose:
- Well x category availability matrix.
- Cell value 1 indicates that at least one file of that category exists for that well.

How to use:
- Quickly find wells that support a specific study design.
  - Example: drilling operations workflows need DDR_XML and XML and supporting technical docs.
  - Example: log-based studies need DLIS or LAS.

## outputs/coverage_matrix_counts.csv

Purpose:
- Same structure as the binary matrix, but cells are file counts.

How to use:
- Distinguish between wells that barely have a data type and wells that have strong coverage.
- Prioritize wells with higher counts when coverage depth matters.

## Important note on well identifiers

Some file paths do not include a well identifier (field-level content like models and seismic packages). Those files contribute to field-level coverage and tag totals but may not appear in well-level matrices.
