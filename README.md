# Australian Housing: Buy vs Rent Analytics

A single-file, static HTML dashboard comparing buy-vs-rent metrics across 75 Victorian suburbs (2020-2025).

Open `index.html` directly in a browser — no build step, no server.

## What's in the dashboard

- **Dashboard Summary** — KPI band plus preview panels for growth ranking, the rent/cash-rate trend, the growth-vs-yield quadrant, and cluster composition.
- **Growth vs Yield Quadrant**, **Cluster Composition**, **Suburb Detail Table** — full-page, filterable, sortable views. Click any suburb for its own detail page. The table can be exported as a CSV via the Download CSV button (respects the current filters and sort order).
- **Before/After Policy Event Testing** — paired t-test results (rent before/after 5 rate/policy events, computed in Python), fixed to the Victorian sample of 75 suburbs.

Filters (search, region, cluster, verdict) apply across every view.

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
docs/
  PowerBI_Production_Build_Guide.docx  original data model / methodology notes
```
