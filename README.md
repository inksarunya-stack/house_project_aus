# Australian Housing: Buy vs Rent Analytics

A single-file, static HTML dashboard comparing buy-vs-rent metrics across 75 Victorian suburbs (2020-2025).

Open `index.html` directly in a browser — no build step, no server.

## What's in the dashboard

- **Dashboard Summary** — KPI band plus preview panels for growth ranking, the rent/cash-rate trend, the growth-vs-yield quadrant, and cluster composition.
- **Growth vs Yield Quadrant**, **Cluster Composition**, **Suburb Detail Table** — full-page, filterable, sortable views. Click any suburb for its own detail page. The table can be exported as a CSV via the Download CSV button (respects the current filters and sort order).
- **Before/After Policy Event Testing** — paired t-test results (rent before/after 5 rate/policy events, computed in Python), fixed to the Victorian sample of 75 suburbs.
- **Rent vs Buy Advisor** — a standalone financial calculator. Prefill from any suburb in the dataset (or enter your own numbers) and it computes:
  1. A year-by-year net-cost comparison of buying vs renting (mortgage amortisation, VIC stamp duty, ongoing ownership costs, and the investment return a renter forgoes on the deposit) with a break-even year and cost chart.
  2. A scenario table that flexes interest rate, purchase price, rent inflation, and holding period one at a time, each with its own verdict, plus a set of auto-generated insights comparing the scenarios.
  3. An estimated travel time to Melbourne's CBD (car/train/tram, peak vs off-peak) with a simple schematic distance/direction map — all computed from suburb coordinates and rule-of-thumb speeds, not a live routing API.

  Everything here is illustrative and computed client-side — there's no backend, no API keys, and no live traffic/timetable data. It's explicitly not financial advice.

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
