# Does Wealth Make Countries Happy?

## Project Overview

This application was built as part of the F21DV group project. It tells a data-driven story asking: **Does wealth make countries happy?** Five interactive visualisations guide the audience - general public and policy enthusiasts - through macro-economic data, regional happiness comparisons, long-term trends, and multi-dimensional country profiles, all connected through bidirectional cross-chart interactions.

## Quick Start

No build step or package installation is required. The application runs entirely in the browser using ES6 modules.

```bash
# Serve locally with Python (recommended)
python -m http.server 8080

# Then open in any modern browser:
# http://localhost:8080
```

> **Note:** The app uses ES6 `import`/`export` modules and must be served over HTTP (not opened directly as a `file://` URL) due to browser CORS restrictions.

## Repository Structure

```
/
├── index.html                          ← Single-page application entry point
│
├── styles/
│   └── main.css                        ← Dark theme, CSS variables, full layout
│
├── scripts/
│   ├── DataManager.js                  ← Centralised CSV loading, parsing & queries
│   ├── ScatterChart.js                 ← GDP vs Happiness scatter (log scale)
│   ├── ChoroplethMap.js                ← World map with metric selector & zoom
│   ├── BarChart.js                     ← Regional happiness comparison (horizontal)
│   ├── LineChart.js                    ← Long-range trend lines (1990–2023)
│   ├── RadarChart.js                   ← Multi-axis country profile (spider chart)
│   └── main.js                         ← App bootstrap, state, all wiring
│
├── data/                               ← Cleaned, processed datasets (CSV)
│   ├── merged_wb_happiness_2015_2019.csv   (751 rows — main dataset)
│   ├── merged_all_2015.csv                 (145 rows — full snapshot for radar)
│   ├── wb_trends_1990_2023.csv             (9,292 rows — long-range trends)
│   └── happiness_2015_2019.csv             (782 rows — happiness-only series)
│
├── raw_data/                           ← Original unmodified source files
│   ├── happiness/                      ← World Happiness Report 2015–2019 (CSV per year)
│   ├── who/                            ← WHO Life Expectancy dataset
│   └── world_bank/                     ← World Bank Development Indicators
│
├── eda/
│   └── EDA_notebook.ipynb              ← Jupyter notebook: cleaning, merging, EDA
│
├── libs/
│   ├── d3/                             ← D3.js v7 (local copy + licence)
│   └── topojson/                       ← TopoJSON Client v3 (local copy)
│
├── .gitignore
├── .gitlab-ci.yml
└── README.md                           ← This file
```

## Data Sources

| Dataset | Source | Licence |
|---|---|---|
| World Happiness Report (2015–2019) | Kaggle / Sustainable Development Solutions Network | CC BY 4.0 |
| World Bank Development Indicators | Kaggle / World Bank | CC BY 4.0 |
| WHO Life Expectancy Data | Kaggle / WHO | CC BY-NC-SA 3.0 IGO |

Raw files live in `raw_data/`. Cleaned, merged outputs live in `data/`. See `eda/EDA_notebook.ipynb` for the full data-pipeline description.

## Visualisations

| # | Chart | Type | Dataset Used | Key Interactions |
|---|---|---|---|---|
| 1 | Scatter | GDP per Capita vs Happiness | `merged_wb_happiness` | Click country → highlights on map; region legend filters |
| 2 | Choropleth Map | World happiness / GDP / life expectancy | `merged_wb_happiness` | Click country → highlights scatter; metric dropdown; zoom/pan |
| 3 | Bar Chart | Regional happiness comparison | `happiness` (aggregated) | Click region → filters scatter to that region |
| 4 | Line Chart | World Bank trends 1990–2023 | `wb_trends` | Click line → highlight country across scatter & map |
| 5 | Radar Chart | Multi-axis country well-being profile | `merged_all_2015` | Up to 3 countries; auto-populated from other chart clicks |

## Cross-Chart Interactions

- **Scatter ↔ Map** - Bidirectional country highlighting (clicking either chart updates the other)
- **Bar → Scatter** - Clicking a region bar filters the scatter plot to that region only
- **Line → Scatter / Map** - Clicking a trend line highlights the country across all charts
- **Any chart → Radar** - Clicking a country anywhere auto-populates a radar slot
- **Year buttons** - Update scatter, map, and bar charts simultaneously (2015–2019)
- **Metric dropdowns** - Switch displayed indicator on map, bar, and line charts independently
- **Reset button / double-click scatter** - Clears all filters and returns to full view
- **Scroll progress bar + nav highlighting** - IntersectionObserver tracks active story section

## Tech Stack

| Concern | Solution |
|---|---|
| Visualisation | D3.js v7 |
| Geography | TopoJSON Client v3 |
| Modules | ES6 `import` / `export` |
| Styling | Pure CSS with CSS custom properties |
| Runtime | Any modern browser (Chrome, Firefox, Edge, Safari) |
| Dev server | `python -m http.server` |

No React, Vue, Angular, jQuery, Chart.js, or Bootstrap — D3.js only, as required by the project brief.

## Folder-Level READMEs

Each major directory contains its own README with more detail:

| Folder | README |
|---|---|
| `data/` | [data/README.md](data/README.md) - processed dataset descriptions |
| `raw_data/` | [raw_data/README.md](raw_data/README.md) - original source file descriptions |
| `eda/` | [eda/README.md](eda/README.md) - EDA notebook guide |
| `libs/` | [libs/README.md](libs/README.md) - third-party library inventory |
| `scripts/` | [scripts/README.md](scripts/README.md) - JavaScript module descriptions |
| `styles/` | [styles/README.md](styles/README.md) - CSS architecture guide |
