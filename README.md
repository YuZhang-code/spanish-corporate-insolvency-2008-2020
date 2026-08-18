# Spanish Corporate Insolvency Data, 2008–2020

## Data-only deposit

This repository provides the original source files and the final dataset used in the study of corporate insolvency across Spanish autonomous communities and economic sectors from 2008 through 2020.

The deposit is intentionally limited to data. It does **not** contain analysis code, notebooks, figures, regression output, or intermediate result tables.

## Final dataset

The final analysis dataset is:

```text
data/final/corrected_panel_2008_2020.csv
```

It is a balanced autonomous-community–sector–year panel containing:

- 18 analytical geographies;
- 11 economic-sector groups;
- 13 years, from 2008 through 2020;
- 2,574 unique observations; and
- 33 variables.

The first seven variables identify each panel cell and its insolvency measure:

| Variable | Definition |
|---|---|
| `ccaa` | Analytical autonomous-community geography |
| `year` | Calendar year |
| `n_bankrupt` | Non-overlapping corporate insolvency count |
| `n_active` | Non-overlapping active-firm count |
| `rate` | `n_bankrupt / n_active` |
| `rate_per_10k` | Corporate insolvencies per 10,000 active firms |
| `sector` | Analytical economic-sector group |

The remaining variables are annual market and macroeconomic controls used in the empirical analysis.

The final panel contains no duplicate `ccaa`–`sector`–`year` keys and no missing values. It supersedes the earlier historical construction that summed overlapping source categories.

## Measurement definition

For autonomous community \(r\), sector \(s\), and year \(t\), the corrected rate is defined as

\[
\text{rate}_{rst} =
\frac{\text{corporate insolvencies}_{rst}}
     {\text{active firms}_{rst}},
\qquad
\text{rate per 10,000}_{rst} = 10{,}000 \times \text{rate}_{rst}.
\]

The numerator uses one autonomous-community aggregate and one analytical activity aggregate for each panel cell. It does not combine national totals with regional observations or add parent and child geography rows.

The denominator uses only the first employee-size block labelled `Total` and exact two-digit CNAE activity rows. Three-digit CNAE descendants and employee-size component bands are excluded. This prevents double counting across activity hierarchies and firm-size categories.

Ceuta and Melilla are combined into one analytical geography. Agriculture is outside the analytical sample.

## Sector aggregation

| Panel label | CNAE-2009 divisions |
|---|---|
| Actividades administrativas y servicios auxiliares | 77–82 |
| Actividades profesionales, científicas y técnicas | 69–75 |
| Comercio al por menor y vehículos | 45–47 |
| Construcción | 41–43 |
| Hostelería | 55–56 |
| Industria y energía | 05–33 |
| Información y comunicaciones | 58–63 |
| Inmobiliarias financieras y seguros | 64–66, 68 |
| Resto de servicios | 84–88, 90–96 |
| Suministro de energía eléctrica y agua, saneamiento y gestión de residuos | 35–39 |
| Transporte y almacenamiento | 49–53 |

The historical label `Comercio al por menor y vehículos` is retained for compatibility. Its data cover the full broad trade group, CNAE divisions 45–47, including wholesale trade.

## Original source files

All original files used to construct the final panel are deposited under `data/raw/`.

### Instituto Nacional de Estadística (INE)

- `data/raw/ine/active_firms_by_ccaa_cnae_employee_band_2008_2024.xlsx`
- `data/raw/ine/corporate_insolvencies_by_geography_activity_2004_2020.xlsx`
- `data/raw/ine/cpi_monthly_variation_rates.xlsx`
- `data/raw/ine/unemployment_rate_quarterly_2007_2024.xlsx`

The active-firms workbook extends through 2024, although only 2008–2020 is used in the deposited panel.

### Financial-market series

- `data/raw/market/ibex35_daily_2000_2024.csv`
- `data/raw/market/vix_daily_2000_2024.csv`
- `data/raw/market/stoxx50e_daily_2007_2024.csv`
- `data/raw/market/eurusd_daily_2003_2024.csv`
- `data/raw/market/bbva_daily_2000_2024.csv`
- `data/raw/market/caixabank_daily_2007_2024.csv`
- `data/raw/market/santander_daily_2000_2024.csv`

### Non-performing-loan series

- `data/raw/fred_world_bank/npl_to_gross_loans_annual_spain.xlsx`
- `data/raw/banco_de_espana/npl_ratio_quarterly_2014_2024.csv`

## Directory structure

```text
.
├── README.md
├── CHECKSUMS.sha256
└── data/
    ├── final/
    │   └── corrected_panel_2008_2020.csv
    └── raw/
        ├── banco_de_espana/
        ├── fred_world_bank/
        ├── ine/
        └── market/
```

## Data integrity

`CHECKSUMS.sha256` records the SHA-256 digest of every distributed file other than the checksum file itself. These hashes allow users to verify that the original source files, final dataset, and README have not changed after packaging.

The source workbooks and source CSV files are preserved as deposited; the final panel is supplied separately under `data/final/`.
