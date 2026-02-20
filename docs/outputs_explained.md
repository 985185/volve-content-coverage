# Outputs explained (petroleum terms)

## outputs/coverage_by_well.csv

Purpose:
Rank wells by how much information exists for each well.

Columns:

- well: Volve well or wellbore identifier
- total_files: number of files associated with that well (after filtering)
- data_categories_present: how many distinct data categories exist for that well

How to use:

- Select candidate wells for drilling studies by choosing wells with many categories present.
- Identify wells that are present but data-poor, and exclude them early.
- Use as a defensible well-selection basis in research writing.

## outputs/coverage_by_tag.csv

Purpose:
Quantify dataset composition by petroleum data category after removing system-level archives.

Columns:

- tag: category label (for example DLIS, LAS, DDR_XML, SEGY)
- file_count: number of files with that tag

How to use:

- Justify which research directions Volve supports (drilling-heavy, log-rich).
- Avoid building a study on a data type that is sparsely represented.

## outputs/coverage_matrix_binary.csv

Purpose:
Well x category availability matrix.

Rows are wells.
Columns are categories.
Cell value:

- 1 indicates at least one file exists for that category and well
- 0 indicates the category is absent for that well

How to use:

- Quickly identify wells that support a specific study design.
- Example: drilling operations workflows typically require DDR_XML and telemetry (WITSML or XML) plus supporting WELL_TECH or DOCS.
- Example: log-based studies require DLIS and/or LAS.

## outputs/coverage_matrix_counts.csv

Purpose:
Same structure as the binary matrix, but cells are file counts.

How to use:

- Distinguish between wells that barely have a data type and wells that have deeper coverage.
- Prioritize wells with higher counts when depth matters.

## Note on field-level content

Some file paths do not include a well identifier (field-level content like models, seismic packages, general documents). Those files contribute to tag totals but may not appear in well-level matrices.
