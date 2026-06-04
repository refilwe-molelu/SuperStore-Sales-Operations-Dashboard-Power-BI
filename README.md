# SuperStore Sales & Operations Dashboard — Power BI

**Week 2 | Power BI · DAX · Data Modeling**

A 4-page interactive Power BI dashboard analyzing SuperStore's transactional records to identify revenue trends, evaluate category profitability, and diagnose operational inefficiencies — establishing data-backed strategies to maximize profit margins and minimize order return rates.

---

## Project Overview

| | |
|---|---|
| **Tool** | Power BI Desktop |
| **Domain** | Retail / E-Commerce |
| **Dataset** | SuperStore Transactions |
| **Operational Base** | $1.57M |
| **Dashboard Pages** | 4 (Executive, Product, Logistics, Customer) |

---

## Dashboard Pages

### 1. Executive Dashboard — Sales Performance
Top-level KPIs covering total revenue, profit, and growth trends across date ranges. Analyzes revenue expansion from 2019 to 2020, seasonal buyer segments, and period-over-period performance for leadership review.

### 2. Product & Category Analysis
Ranks top-performing and underperforming items alongside true category profit margins. Surfaces the contrast between high-volume and high-margin categories — including Furniture lines running at a net deficit despite strong revenue numbers.

### 3. Operations & Logistics
Tracks warehouse fulfillment speeds by shipping mode and measures order return rates. Powered by a custom DATEDIFF measure that calculates the actual physical delivery gap between Order Date and Ship Date.

### 4. Customer Insights
Segments customers into Consumer, Corporate, and Home Office groups. Reveals the Consumer segment driving 48.09% of aggregate sales and the Q4 holiday seasonality spike that should inform all future marketing timing.

---

## Data Model

Built on a clean star schema with a custom **Dim_Calendar** table created in DAX to eliminate chronological sorting errors and ensure all visuals group by clean monthly cycles (January–December).

```
FactSales
    └── Dim_Calendar   (DAX-generated time table)
    └── Dim_Product    (category, sub-category, product name)
    └── Dim_Customer   (segment, region)
    └── Dim_Ship       (shipping mode)
```

---

## DAX Measures

```dax
-- Core revenue aggregation
Total Revenue = SUM(Sales[Sales])

-- Safe profit margin with divide-by-zero protection
Profit Margin % = DIVIDE([Total Profit], [Total Revenue], 0)

-- Surface-level fulfillment metric
Avg Days to Ship = AVERAGE(Sales[Days to Ship])

-- Custom gap calculation between order and shipping dates
Days to Ship =
DATEDIFF(
    Sales[Order Date],
    Sales[Ship Date],
    DAY
)
```

---

## Key Findings

| Area | Finding |
|---|---|
| **Revenue** | Grew from 2019 → 2020, peaked sharply in Q4 due to holiday demand |
| **Customer** | Consumer segment = 48.09% of all sales — the dominant buying group |
| **Product** | Technology = highest profit margins; select Furniture lines = net deficit |
| **Logistics** | Avg fulfillment = 3.93 days; Standard Class is highest volume but slowest |

---

## Recommendations

**1. Logistical Tier Optimisation**
Implement warehouse pre-sorting protocols for Standard Class shipping to reduce the current ~4-day fulfillment timeline to a target KPI of **3.0 days**, improving customer retention and lowering return rates.

**2. Product Portfolio Realignment**
Restructure supplier contracts for bottom-performing deficit items or phase out low-margin sub-categories to prevent ongoing margin erosion. High revenue ≠ high profit.

**3. Targeted Consumer Campaigning**
Deploy holiday-specific marketing to the Consumer Segment starting in **August** to capture early Q4 shopping waves — maximizing ROI on the segment driving nearly half of all revenue.

---

## Challenges & Learnings

**Challenges**
- Resolving text-aggregation errors on order counts and dynamic return statuses
- Formulating DATEDIFF logic to accurately measure physical delivery gaps
- Building an independent Dim_Calendar to bypass Power BI's chronological sorting limitations

**Key Takeaways**
- Operations matter — supply chain efficiency directly impacts top-line revenue and margins
- Setting card visual interactions correctly upfront eliminates broken canvas headers
- End-to-end analytics (data model + BI dashboard + business recommendations) delivers executive clarity that neither component achieves alone

---

## Files

| File | Description |
|---|---|
| `SuperStore_Sales_Dashboard.pbix` | Power BI project file |
| `data/` | Source data files (if included) |

---

## Author

**Refilwe Molelu** — Business Intelligence Analyst

- Portfolio: [refilwe-molelu.netlify.app](https://refilwe-molelu.netlify.app)
- LinkedIn: [linkedin.com/in/refilwe-molelu-713379241](https://www.linkedin.com/in/refilwe-molelu-713379241)
