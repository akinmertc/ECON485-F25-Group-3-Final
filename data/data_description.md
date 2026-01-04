# Data Description
## ECON485 Project: Tourism Statistics Exports

**Team:** ECON485 Project Group  
**Last Updated:** 2026-01-04

---

## Overview

This folder contains three UTF-8, comma-delimited CSV exports derived from official Excel tables (TUIK and Ministry of Culture/Tourism sources). Turkish characters and any in-cell line breaks are preserved; the table layout closely follows the originals for traceability.

---

## Data Files

| File Name | Rows | Description | Date Range |
|-----------|------|-------------|------------|
| `data/csv_income_and_expenses_data.csv` | 36 | Tourism income/expense series with inbound/outbound visitor counts and average spend (1000 $ and $). Includes header/explanatory rows and footnotes. | 2004-2025 (Jan-Sep 2025) |
| `data/csv_Number_of_trips_and_nights_by_age_group_of_travelers_data.csv` | 44 | Domestic trips and overnights by age group; average overnights; bilingual headers (TR/EN); Quarter III. | 2017-2018 Q3 |
| `data/csv_2022_data.csv` | 824 | Certified accommodation stats by province/district: arrivals, overnights, average stay, occupancy (%), split by foreign/local/total. | 2022 |

Row counts include header/comment/blank lines as preserved in the source spreadsheets.

---

## Dataset Details

### `csv_income_and_expenses_data.csv`
- Structure: Multiple header/comment rows describing units, followed by yearly metrics; ends with source and footnote lines.
- Metrics (data rows): Year, incoming visitors, departing visitors, tourism income (1000 $), transfer passenger tourism income (1000 $), average expenditure ($), tourism expenditure (1000 $), citizen expenditure ($). Some separator columns are intentionally blank.
- Notes: Dot (.) is the decimal separator; "-" marks missing or not applicable fields; final lines provide source and explanatory notes.

### `csv_Number_of_trips_and_nights_by_age_group_of_travelers_data.csv`
- Structure: Bilingual headers (TR/EN), then age-group rows: 0-14, 15-24, 25-44, 45-64, 65+, Total.
- Metrics per year (2017, 2018): Number of trips (thousand), number of overnights (thousand), average overnights. Empty cells separate the two years' blocks.
- Notes: Header rows are retained for bilingual context; data rows start after the age-group header line.

### `csv_2022_data.csv`
- Structure: First line is a long dataset description; second line holds column headers; subsequent lines list districts with a "Total" row for each province.
- Metrics: Arrivals (foreign/local/total), overnights (foreign/local/total), average length of stay (days), occupancy rate (%) — each reported for foreign, local, and total.
- Notes: Decimal separator is dot (.); district rows often leave the province cell blank to imply "same as above," so forward-fill when grouping by province.

---

## Loading and Processing Guidance

- Encoding: UTF-8; delimiter `,`; line ending `\n`. Empty cells are preserved.
- Multi-header files: Use `skiprows` or pattern matching to drop descriptive lines until the first numeric data row (for example, the first year or the first province/district row).
- Numeric parsing: Read as string first if you need to control decimal parsing or handle "-" as missing.
- Python example:
  ```python
  import pandas as pd

  df_income = pd.read_csv("data/csv_income_and_expenses_data.csv", header=None)
  df_age = pd.read_csv("data/csv_Number_of_trips_and_nights_by_age_group_of_travelers_data.csv", header=None)
  df_2022 = pd.read_csv("data/csv_2022_data.csv", header=None)

  # Example: isolate data rows for the income series
  income_data = df_income[df_income[1].astype(str).str.match(r"^\d{4}")]
  ```

---

## Known Limitations

- Header and footnote rows are retained; consumers must skip them for numeric analysis.
- `csv_2022_data.csv` uses blank province cells to imply "same as above"; grouping may require forward-filling province names.
- "-" represents missing or not applicable values in some columns; treat as nulls when aggregating.

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 2.4 | 2026-01-04 | Updated for new `_data` CSV filenames, revised row counts, and clarified parsing guidance. |
