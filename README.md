# Hotel Booking Data Analysis (SQL + Power BI)

Analysis of 3 years of hotel reservation data (2018–2020) using SQL Server for data prep and Power BI for visualization. The goal was to turn raw, split-up booking records into a dashboard that actually answers business questions — where's revenue coming from, how do hotel types compare, and what's driving demand over time.

![Dashboard Preview](screenshots/dashboard.png)

## What's in here

- `sql/` — the SQL script used to consolidate and join the data
- `screenshots/` — dashboard views and key visuals
- `hotel_booking_dashboard.pbix` — the Power BI file (if shared)

## The data

The raw data came split across three separate yearly tables (`2018`, `2019`, `2020`), plus two lookup tables: `market_segment` and `meal_cost`.

## What I did

1. **SQL** — Used `UNION` to combine the three yearly tables into one, then `LEFT JOIN`ed in market segment and meal cost details to enrich each reservation record.
2. **Power BI** — Built an interactive dashboard on top of the cleaned dataset, with filters by hotel type, country, and date range.

```sql
with hotels as (
    select * from dbo.[2018]
    union
    select * from dbo.[2019]
    union
    select * from dbo.[2020]
)

select * from hotels
left join dbo.market_segment
    on hotels.market_segment = market_segment.market_segment
left join dbo.meal_cost
    on meal_cost.meal = hotels.meal
```

## Key numbers

| Metric | Value |
|---|---|
| Total Revenue | $10.23M |
| Average ADR | $104.48 |
| Total Nights | 368K |
| Average Discount | 25.81% |
| Car Parking Spaces Used | 9K |

- Resort Hotels made up **53.6%** of total revenue ($5.48M) vs. City Hotels ($4.74M)
- Clear seasonal spike in revenue around mid-2019
- 2019 was the strongest year overall, with $5.49M in revenue

## Tools used

- SQL Server (T-SQL)
- Power BI (DAX, interactive dashboards)

## Notes

This was a portfolio project — the SQL part took longer than expected since the joins weren't as clean as they looked at first glance. That's usually where the real learning happens.
