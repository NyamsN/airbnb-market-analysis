# Airbnb Pricing, Location and Listing Characteristics Investigation

**AnalystLab Africa Experience Lab · Week 1 · Track B (Data Science)** · Intern: Nelson Nyamweya

## Purpose
A statistical investigation of which listing characteristics (room type, capacity, bedrooms) are associated with higher **advertised** Airbnb prices within each of 10 cities, whether review activity relates to listing ratings, and how host responsiveness differs between cities. It supports the shared Airbnb Market Intelligence Platform.

## Folder structure
```
AnalystLab_Week1_TrackB_DataScience/
├── README.md                     this file
├── requirements.txt              Python packages
├── notebooks/
│   ├── Airbnb_TrackB_Analysis.ipynb   reproducible notebook (executed, with outputs)
│   └── Airbnb_TrackB_Analysis.html    same notebook as HTML, viewable in any browser
├── data/
│   ├── raw/                      put the 4 supplied CSVs here (not included: 400 MB)
│   └── processed/listings_clean.parquet   cleaned listing table produced by the notebook
├── outputs/
│   ├── figures/                  13 figures (F01–F13, PNG, 200 dpi)
│   └── tables/                   22 result tables (T00–T18, CSV)
├── report/
│   ├── Airbnb_TrackB_Statistical_Analysis_Report.docx
│   └── Airbnb_TrackB_Statistical_Analysis_Report.pdf
└── docs/
    ├── data_quality_summary.md
    ├── presentation_script.md    5–10 minute recorded presentation outline
    ├── feedback_and_improvements_log.md
    └── social_posts.md           LinkedIn and X drafts
```

## Deliverables map (Track B)
| Required deliverable | Where |
|---|---|
| 1. Reproducible Python notebook | `notebooks/Airbnb_TrackB_Analysis.ipynb` |
| 2. Data-quality summary | `docs/data_quality_summary.md`, notebook Sections 2, 3 and 6 |
| 3. At least five visualisations | `outputs/figures/` (13 figures) |
| 4. Statistical analysis report | `report/` (Word and PDF) |
| 5. Findings and recommendations | Report Sections 6 and 9; notebook Section 8 |
| 6. Reproduction instructions | This README |

## Tools
Python 3.13, pandas, NumPy, SciPy, statsmodels, Matplotlib, Seaborn, Jupyter. No Excel was used.

## How to reproduce
1. Install Python 3.10+ and run `pip install -r requirements.txt`.
2. Copy the four supplied files into `data/raw/`: `Listings.csv`, `Reviews.csv`, `Listings_data_dictionary(1).csv`, `Reviews_data_dictionary(1).csv` (names with or without `(1)` both work).
3. From the project folder run `jupyter notebook notebooks/Airbnb_TrackB_Analysis.ipynb`, then **Kernel → Restart & Run All**.
   Or headless: `jupyter nbconvert --to notebook --execute --inplace notebooks/Airbnb_TrackB_Analysis.ipynb`
4. Every table and figure in `outputs/` and `data/processed/listings_clean.parquet` is regenerated. Runtime is under a minute on a laptop with 8 GB RAM (Reviews.csv, 5.4M rows, is loaded with pandas).
5. Built-in `assert` checks stop the run if the record counts, duplicate-ID count or referential integrity do not match the brief.

## Methodology (summary)
- **Inspection:** keys, Listings→Reviews relationship (one-to-many, 0 orphans), duplicate `review_id` investigation, missing values, types, price checks.
- **Cleaning:** removed 113 non-positive prices (which include all 85 zero-capacity rows); kept and flagged 5,094 extreme prices outside each city's 1st–99th percentile; no imputation.
- **Currency:** no currency field, so all price tests are within city in local currency; cross-city visuals use price ÷ city median. No exchange-rate conversion was required.
- **Hypotheses:** H1 price by room type (Kruskal–Wallis, Mann–Whitney); H2 capacity and price (Spearman, OLS on log price with HC3 errors); H3 review volume and rating (Spearman, Kruskal–Wallis); H4 host responsiveness by city (Kruskal–Wallis, χ²). Effect sizes reported; Holm correction across cities; trimmed robustness re-runs.

## Key results
| | Result |
|---|---|
| H1 | Price differs by room type in 10/10 cities; entire place = 1.5–2.6× private-room median (ε² 0.05–0.43) |
| H2 | Capacity positively associated with price in 10/10 cities (ρ 0.31–0.68); +7% to +23% per extra guest holding room type and bedrooms |
| H3 | Review volume weakly negatively related to rating (ρ = −0.20), driven by noisy ratings on low-volume listings |
| H4 | Host responsiveness differs across cities, but effects are small (ε² 0.013, Cramér's V 0.16) |

## Assumptions
- City currency mapping as listed in `docs/data_quality_summary.md`.
- Prices are nightly advertised prices at the time of the snapshot (early 2021).
- Missing response/acceptance data is informative (not random) and is not imputed.

## Limitations
Advertised prices are not revenue; review counts are not occupancy; ratings are not sentiment (no review text in the data). District exists only for New York. Results are associations, not causal effects. Data covers the COVID-19 period. Full list in report Section 8.

## Privacy
Host names, host locations, listing names and host/reviewer IDs are not shown in any output.

## Attribution
Dataset: Airbnb Listings and Reviews Dataset, supplied by AnalystLab Africa. AI assistance (Claude) was used to help draft code and documentation; all figures come from the notebook outputs.
