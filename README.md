# Australian Housing: Buy vs Rent Analytics

A single-file, static HTML dashboard for comparing buy-vs-rent metrics across Australian suburbs. It ships with a fully worked Victorian sample (75 suburbs, 2020-2025) and lets you add any other state's data on top of it, live in the browser, via drag-and-drop CSVs.

Open `index.html` directly in a browser — no build step, no server.

## What's in the dashboard

- **Dashboard Summary** — KPI band plus preview panels for growth ranking, the rent/cash-rate trend, the growth-vs-yield quadrant, and cluster composition.
- **Growth vs Yield Quadrant**, **Cluster Composition**, **Suburb Detail Table** — full-page, filterable, sortable views. Click any suburb for its own detail page.
- **Before/After Policy Event Testing** — paired t-test results (rent before/after 6 rate/policy events), fixed to the original Victorian sample of 75 suburbs and cross-validated against SAS Studio's `PROC TTEST`.

Filters (search, state, region, cluster, verdict) apply across every view.

## Adding another state's data

Use the **Add a state dataset** panel in the sidebar:

1. Optionally type the state's name (e.g. `Queensland`). If you skip this, the dashboard uses a `State` column in your CSV if present, otherwise it guesses from the file name.
2. Drag a suburb-summary CSV onto the drop zone (or click it to browse). Required columns: `Suburb, Region, Price2024, WeeklyRentJun25`.
3. Optionally include a matching `Quarterly_Rent`-style CSV (`Suburb, Quarter, WeeklyRent`) in the same drop to power that state's rent trend line and detail-page chart.

Working examples are in [`data/templates/`](data/templates/) — `Suburbs_Master_TEMPLATE.csv` and `Quarterly_Rent_TEMPLATE.csv` — using three clearly-fictional suburbs ("Sample Springs" etc.) so you can see the feature work before dropping in real figures.

**Optional columns** (`GrossYieldPct`, `PriceToRentRatio`, `GrowthPAPct`, `Growth10YrPct`, `RentVolatilityCVPct`, `Verdict`, `Cluster`) are used when present. When they're missing:

- **Yield / price-to-rent ratio** are derived from price and rent.
- **Verdict** (Buy/Neutral/Rent) is estimated the same way the Victorian dataset was built: suburbs are ranked by price-to-rent ratio within the new state and split into thirds (lowest third → Buy, middle → Neutral, top third → Rent).
- **Cluster** is approximated from price and yield relative to the new state's own median (a simple rule, not full k-means — see the caveat below).

You can remove an uploaded state at any time from the chip list under the drop zone. The original Victorian dataset can't be removed this way.

### Modelling caveat

The Victorian dataset's `Verdict` and `Cluster` columns, and the six event t-tests, were originally computed offline in Python/SAS (k-means clustering, paired t-tests) — see `docs/PowerBI_Production_Build_Guide.docx` for the full methodology. Browser JavaScript can't reproduce k-means or a proper t-test on the fly, so uploaded states get the percentile/rule-based approximations described above, not a full re-run of that pipeline. If you have real cluster/verdict labels from your own analysis, put them straight in the `Verdict`/`Cluster` columns of your CSV and the dashboard will use them as-is instead of estimating.

## Project layout

```
index.html                          the dashboard (open this)
data/
  Suburbs_Master.csv                 Victorian dataset backing the dashboard
  Quarterly_Rent.csv
  Cash_Rate.csv
  Quarters_Dim.csv
  Event_Results.csv
  Event_Suburb_Pairs.csv
  templates/                         example CSVs for testing the upload feature
docs/
  PowerBI_Production_Build_Guide.docx  original data model / methodology notes
```
