# Nordex Sales Intelligence Dashboard

Interactive Streamlit dashboard for Nordex commercial and economics analytics.

## What This App Includes
- Overall economics trends from the `Nordex Economy` sheet.
- Year-by-year, quarterly, platform, country, delivery, and correlation analytics from `OI YYYY` sheets.
- Coverage now includes `OI2024`, `OI2025`, and `OI2026`.
- Market overlays:
  - Nordex stock monthly OHLC (`NDX1.DE` data structure)
  - Steel monthly price (`HRC=F`)
  - Copper monthly price (`HG=F`)
- Latest Nordex-related news feed view and latest patent view.

## Data Files Used By The App
- `data_cache/nordex_parsed_data.pkl`
  - Parsed/cached core dataset used for app analytics.
- `data/nordex_stock_monthly.json`
  - Monthly stock history used in the Overall Economics market chart.
- `data/market_prices_monthly.json`
  - Monthly steel/copper series used for market overlays.

Optional source workbook for data refresh:
- `Nordex_data_new.xlsx`

Optional raw stock source used for conversion:
- `data/nordex_stock_2008_2026.txt`

## How Data Loading Works
- If the Excel workbook is present, the app parses it and refreshes `data_cache/nordex_parsed_data.pkl`.
- If the workbook is not present, the app runs from `data_cache/nordex_parsed_data.pkl`.
- Stock and market charts read from local JSON files in `data/`.

## Run Locally
```powershell
python -m pip install -r requirements.txt
python -m streamlit run nordex_app.py
```

If you use a local virtual environment:
```powershell
& .\.venv\Scripts\python.exe -m pip install -r requirements.txt
& .\.venv\Scripts\python.exe -m streamlit run nordex_app.py
```

## User Guide
### Sidebar
- `Dark mode`: toggle theme.
- `Order year range`: global filter for order-based analytics.
- `Continents`, `Regions`, `Countries`, `Service schemes`, `Platforms`: filter data scope.
- `Minimum order MW`: exclude smaller orders.

### Tabs
- `Overall Economics`
  - Economics KPI cards and time series.
  - Stock candlestick chart with Y2/Y3 overlays.
  - Overlay options include economics metrics plus steel/copper series.
  - Economy year range slider also controls stock/market chart range.
- `Year-by-Year Overview`
  - Announced vs unannounced MW, order counts, average size.
  - Continent accumulation and market share views.
- `Quarterly Analytics`
  - Quarterly announced/unannounced mix and correlations.
- `Across Years`
  - Country, platform, service/time, rotor/MW, and customer trends.
- `Platform Analytics`
  - Timeline, service mix/time, customer and delivery views by platform.
- `Country Analytics`
  - Single full-width map (bubble default; switchable to choropleth).
  - Country-level platform/service/delivery summaries.
- `Delivery and Capacity`
  - Installed capacity and delivery-time trends.
- `Correlations`
  - Numeric correlation matrix and delivery-vs-order scatter analysis.
- `Latest News`
  - Nordex-related news headlines with short summaries and source links.
- `Latest Patents`
  - Recent Nordex-related patent records (publication and filing details).
- `Information`
  - Source/disclaimer statements and short author section.

## Updating Data
1. Put the latest Excel workbook in the project root (recommended name: `Nordex_data_new.xlsx`).
2. Run the app once to regenerate `data_cache/nordex_parsed_data.pkl`.
3. Update market JSON files if needed:
   - `data/nordex_stock_monthly.json`
   - `data/market_prices_monthly.json`
4. Commit updated cache/data files and deploy.

## Deploy (Streamlit Community Cloud)
1. Push repository to GitHub.
2. In Streamlit Community Cloud, create a new app from this repo.
3. Set `nordex_app.py` as the main file.
4. Deploy.

## Troubleshooting
- If visuals look stale after deployment, do a hard refresh in the browser.
- If no workbook is present, ensure `data_cache/nordex_parsed_data.pkl` exists.
- If market overlays are missing, check that JSON files exist in `data/`.
- If `streamlit` command is not found, run via Python module:
  - `python -m streamlit run nordex_app.py`
