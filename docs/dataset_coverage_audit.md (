# Dataset Coverage Audit (Volve)

## Motivation

The public Equinor Volve dataset is a field archive release rather than a curated research dataset. Data availability varies across wells and disciplines. Before engineering analysis, a systematic audit of data availability was performed to identify which wells and data types are sufficiently represented for defensible research.

The audit is designed to answer practical questions:
- Which wells contain drilling telemetry?
- Which wells contain daily drilling reports?
- Which wells contain wireline logs?
- Which wells contain reservoir modeling files?
- Which wells contain seismic or interpretation data?

## Methodology

A frozen filesystem catalog (metadata-only) was used as the source inventory. The catalog enumerates file paths and tags without modifying the Volve dataset.

The audit steps were:

1. Filter to file entries only (directories excluded).
2. Remove system-level archive folders that dominate row counts but do not represent petroleum engineering content.
3. Extract well identifiers from file paths using Volve well naming patterns (for example, 15/9-F-1 and wellbore suffixes).
4. Use the existing catalog tags to classify files into petroleum-relevant categories (for example: DDR_XML, DLIS, LAS, SEGY, WELL_TECH, DOCS, XML).

A well x data-category matrix was produced indicating presence or absence of each category per well. Category counts were also computed.

## Results summary

After excluding system-level archives, the remaining dataset is dominated by:
- Drilling telemetry and structured XML
- Well technical documents and reports
- Wireline logs (DLIS, LAS, LIS)
- Reservoir modeling files (RMS model)
- Seismic and interpretation data in smaller volumes

Well-level content was identified for a subset of wells. Data richness varies substantially between wells.

## Implications for research design

This coverage audit enables defensible well selection and reduces selection bias. Subsequent engineering studies should select wells based on documented availability of:
- continuous drilling telemetry and structured operational reporting
- supporting logs and technical documentation

Wells lacking sufficient category breadth should be excluded from operational behavior studies and time-series based analyses.
