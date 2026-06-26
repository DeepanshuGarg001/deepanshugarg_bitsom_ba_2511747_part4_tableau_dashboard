# Chart Selection Justification

This document explains every major chart used in the Executive Dashboard, covering the business question it answers, why that chart type was chosen, the design principles applied, and what mistakes were deliberately avoided.

---

## 1. Sales & Profit Trend — Line Chart with Fill

**Business Question Answered:** How are sales and profit changing over time? Is the business growing?

**Why This Chart Type:** A line chart is the most intuitive choice for time-series data. It allows the viewer to instantly understand direction (growth vs. decline), identify peaks and troughs, and compare two time-series (Sales vs. Profit) simultaneously. A bar chart for monthly data over 18+ months would look cluttered and make it difficult to see trends.

**Fields Used:** Order Date (Month) on X-axis, Sum(Sales) and Sum(Profit) as two separate lines on Y-axis.

**Design Principle Applied:** Consistent colour coding (blue = Sales, green = Profit) is maintained across all dashboard views, creating a visual language that the user learns once and applies everywhere. The fill under each line adds visual weight without distorting the data.

**Mistake Avoided:** Using a Pie Chart for trend data — Pie charts cannot show change over time and would be completely meaningless here.

---

## 2. Regional Performance — Horizontal Bar Chart

**Business Question Answered:** Which region performs best? Where should leadership focus expansion?

**Why This Chart Type:** A horizontal bar chart is ideal for comparing discrete categories (regions) against a numerical measure (sales/profit). It is easier to read than a vertical bar chart when the category labels are long, and it allows for natural left-to-right value comparison.

**Fields Used:** Region on Y-axis, Sum(Sales) and Sum(Profit) on X-axis (two side-by-side panels).

**Design Principle Applied:** Bars are sorted from smallest to largest (ascending), so the top bar is always the best performer, making it immediately clear to the leadership audience. Each region is assigned a consistent unique colour.

**Mistake Avoided:** Using a Map chart for this view. A map can show *where*, but it cannot easily communicate the exact numerical *magnitude* of the difference between regions as clearly as a bar chart.

---

## 3. Category Profitability — Horizontal Bar Chart (Diverging)

**Business Question Answered:** Which categories and sub-categories drive profit or losses?

**Why This Chart Type:** A diverging horizontal bar chart allows positive and negative profit values to be shown naturally — bars extending right are profitable, bars extending left are losses. This immediately highlights which sub-categories are destroying value.

**Fields Used:** Sub-Category on Y-axis, Sum(Profit) on X-axis, coloured by Category.

**Design Principle Applied:** Colour is used semantically — positive bars are blue, negative bars are red, making the health of each sub-category immediately clear at a glance. The vertical zero-line acts as a visual anchor.

**Mistake Avoided:** Using a Treemap. While Treemaps look visually impressive, they make it very hard to compare values when positive and negative numbers coexist, as the size encoding breaks down for losses.

---

## 4. Customer Segment View — Grouped Bar Chart

**Business Question Answered:** Which customer segment has the highest revenue and profit? Which segment should be prioritized?

**Why This Chart Type:** A grouped bar chart allows side-by-side comparison of two measures (Sales and Profit) across three customer segments. This makes it easy to see both the absolute value and the relationship between revenue and profitability for each segment.

**Fields Used:** Customer Segment on X-axis, Sum(Sales) and Sum(Profit) as grouped bars, coloured consistently.

**Design Principle Applied:** Labels are kept to a minimum. Only axis labels and the legend are shown; no data labels are placed on top of bars to avoid clutter.

**Mistake Avoided:** Using a stacked bar chart. Stacked bars make it hard to compare the internal segments once the baseline changes. A grouped chart is cleaner and more honest.

---

## 5. Full Executive Dashboard — Combined KPI Cards + Multi-Chart Layout

**Business Question Answered:** What is the overall business health at a glance? What are the most critical metrics leadership needs to monitor?

**Why This Layout:** The dashboard opens with four KPI summary cards across the top row (Total Sales, Total Profit, Avg Margin, Return Rate). KPI cards are the most executive-friendly format — they communicate the single most important number in a metric's story in under 2 seconds. The charts below tell the underlying story that explains the KPIs.

**Fields Used:** KPI Cards use aggregated measures. The supporting charts re-use the individual views from other sheets.

**Design Principle Applied:** Dark background with high-contrast coloured text gives the dashboard a polished, professional executive feel while reducing eye strain in presentation settings. Visual hierarchy is maintained — KPIs are largest and at the top, supporting charts are smaller and below.

**Mistake Avoided:** Overloading the dashboard with more than 6-7 charts. A dashboard with 12+ charts becomes a "chart dump" and loses its ability to tell a coherent story. We deliberately chose the most impactful 5 views.
