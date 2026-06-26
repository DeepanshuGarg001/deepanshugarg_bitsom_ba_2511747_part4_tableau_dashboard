# Part 4: Tableau Executive Dashboard & Data Storytelling

## 1. Business Problem Summary
The retail leadership team needs a centralized executive dashboard to monitor sales performance, profitability, customer segments, category performance, shipping performance, discount impact, and return patterns. The dashboard must help leadership identify risks and opportunities and support data-driven decision-making quickly and visually.

## 2. Dataset Description
The dataset (`dashboard_sales_data.xlsx`) contains **4,200 orders** from a retail business across 2024–2025. Key fields include:
- **Date fields:** `order_date`, `ship_date`
- **Geographic fields:** `region`, `state`, `city`
- **Categorical fields:** `category`, `sub_category`, `customer_segment`, `ship_mode`, `campaign_channel`
- **Numerical measures:** `sales`, `profit`, `discount`, `quantity`, `delivery_days`, `customer_rating`
- **Binary/flag fields:** `return_flag` (1 = returned, 0 = not returned)

**Key Assumptions:** Missing values in `customer_rating` (~32 rows) and `campaign_channel` (~24 rows) were treated as unknown and excluded from aggregations involving those fields. All other fields had no missing values.

## 3. Tableau Workbook Description
The packaged workbook (`tableau/executive_dashboard.twbx`) contains 7 individual views (worksheets) and 1 executive dashboard combining the most important views:
- Sales Trend View
- Regional Performance View
- Category Profitability View
- Customer Segment View
- Shipping Performance View
- Discount vs Profit View
- Return Analysis View

## 4. Calculated Fields Created
The following calculated fields were created in Tableau to derive meaningful business metrics from the raw data:

| Calculated Field | Formula | Purpose |
|:---|:---|:---|
| `Profit Margin` | `[profit] / [sales]` | Measures profitability as a % of revenue |
| `Cost` | `[sales] - [profit]` | Derives operational cost per order |
| `Average Order Value` | `[sales] / COUNTD([order_id])` | Revenue per unique order |
| `Return Rate` | `SUM([return_flag]) / COUNT([order_id])` | Proportion of orders returned |
| `Shipping Delay Bucket` | IF/ELSEIF logic on `delivery_days` | Groups orders into Fast/Standard/Slow/Very Slow |

## 5. Dashboard Components
The Executive Dashboard includes:
- **4 KPI Cards:** Total Sales ($217M), Total Profit ($33.3M), Avg Profit Margin (13.1%), Return Rate (4.5%)
- **5 Charts/Views:** Monthly Trend, Regional Performance, Sub-Category Profitability, Customer Segment Comparison, Discount vs Profit
- **3 Interactive Filters:** Region, Customer Segment, Year (applied across all sheets)
- **1 Filter Interaction:** Region filter updates all charts on the dashboard simultaneously

## 6. Filters and Interactions Used
- **Region Filter** — Dropdown with all 4 regions (East, West, South, North). Applies to all views.
- **Customer Segment Filter** — Allows leadership to drill into Consumer, Corporate, or Home Office performance.
- **Year Filter** — Allows comparison of 2024 vs 2025 performance across all charts.

## 7. Key Business Insights
1. The South Region is the top revenue generator.
2. Technology (especially Copiers) drives the highest profit margins.
3. Discounts above 20–30% frequently result in negative profit margins.
4. Furniture has the highest return rate (7.7%), creating a logistics risk.
5. Home Office segment is the most profitable customer segment.
6. Monthly sales show consistent growth from 2024 to 2025.
7. Paper is the worst-performing sub-category by total profit.
8. ~16% of orders experience slow delivery (6+ days), linked to lower satisfaction.

*Full detail for each insight is in `outputs/business_insights.md`.*

## 8. Dashboard Story Summary
The dashboard tells the story of a growing retail business facing a profitability challenge driven by aggressive discounting and logistics inefficiencies. Key recommended actions include introducing discount governance, prioritising the Home Office segment, and resolving Furniture return issues.

*Full story is in `outputs/dashboard_story.md`.*

## 9. Assumptions and Limitations
- The dashboard is based on 4,200 transactions and may not capture seasonal patterns beyond the 2024–2025 window.
- External factors (competitor pricing, macroeconomic conditions) are not represented in the data.
- Campaign channel data has ~24 missing values, making campaign ROI analysis partial.
- The dashboard assumes a static data snapshot; live Tableau Server or Tableau Online integration would enable real-time refreshes.

## 10. Screenshots Included
All screenshots are in the `screenshots/` directory:
- `full_dashboard.png` — Complete executive dashboard
- `sales_trend_view.png` — Monthly sales & profit trend chart
- `regional_performance_view.png` — Regional sales & profit bar charts
- `category_profitability_view.png` — Sub-category profitability breakdown
- `filter_interaction_view.png` — Customer segment view with active filter panel visible
