# Logistics Performance and Profitability Analysis (Power BI)

![Executive Overview Dashboard](dashboard.jpeg)

## Table of Contents
1. [Project Title](#logistics-performance-and-profitability-analysis-power-bi)
2. [Project Overview](#project-overview)
3. [Business Objectives](#business-objectives)
4. [Business Questions](#business-questions)
5. [Dataset Description](#dataset-description)
6. [DAX Measures Used](#dax-measures-used)
7. [Tools Used](#tools-used)
8. [Data Cleaning Process](#data-cleaning-process)
9. [KPIs](#kpis)
10. [Visualizations Created](#visualizations-created)
11. [Key Findings](#key-findings)
12. [Business Insights](#business-insights)
13. [Recommendations](#recommendations)
14. [Skills Demonstrated](#skills-demonstrated)
15. [Conclusion](#conclusion)
16. [Author](#author)

---

## Project Overview
This capstone project analyzes the operations of a trucking and logistics company. I built a multi-table data model in Power BI covering trips, loads, customers, routes, drivers, trucks, trailers, fuel, maintenance and safety data, then created an Executive Overview dashboard that tracks revenue, profit, fuel cost, delivery reliability and fleet efficiency.

## Business Objectives
- Measure overall financial performance (revenue, profit and fuel cost).
- Identify the highest-value customers.
- Track monthly revenue and profit trends to find weak periods.
- Find the routes with the highest fuel cost.
- Understand where trip activity is concentrated by state.
- Assess delivery reliability (on-time rate) and fuel efficiency (MPG).

## Business Questions
1. Who are the top customers by revenue?
2. How do revenue and profit change month by month, and which months are weakest?
3. Which routes have the highest fuel cost?
4. Which states generate the most trips?
5. How reliable is delivery performance, and how efficient is the fleet's fuel use?

## Dataset Description
The data model contains **14 related tables** plus a dedicated measures table (`_Measure`).

| Area | Tables |
|---|---|
| Operations | Trips, Loads, Routes, Delivery events |
| Customers and facilities | Customers, Facilities |
| Fleet | Trucks, Trailers, Truck utilization metrics |
| People | Drivers, Driver monthly metrics |
| Costs and safety | Fuel purchases, Maintenance records, Safety incidents |

Tables are linked through ID columns (for example trip id, customer, route id, driver id), and `Load date` is used for time analysis (month and year).

## DAX Measures Used
The report uses a dedicated `_Measure` table. Main measures (column names below are illustrative; adjust them to match your model):

```DAX
Total Revenue      = SUM(Loads[revenue])
Total Fuel Cost    = SUM('Fuel purchases'[total_cost])
Total Profit       = [Total Revenue] - [Total Operating Cost]
Total Trips        = DISTINCTCOUNT(Trips[trip id])
On-Time Rate %     = DIVIDE(COUNTROWS(FILTER('Delivery events', 'Delivery events'[on time flag] = TRUE())), COUNTROWS('Delivery events'))
Avg MPG            = AVERAGE(Trips[mpg])
Profit Margin %    = DIVIDE([Total Profit], [Total Revenue])
Fuel Cost Ratio    = DIVIDE([Total Fuel Cost], [Total Revenue])
Revenue per Miles  = DIVIDE([Total Revenue], [Total Miles])
```

Other measures in the report: Total Loads, Total Customers, Total drivers, Total truck, Active Trucks, Total Miles, Total Operating Cost, Total Maintenance Cost, Total Incidents, Preventable incident Rate, Total claim amount and Avg Fleet Utilization.

## Tools Used
- **Power BI Desktop**: data modeling, DAX, Power Query and dashboard design
- **GitHub**: documentation and version control

## Data Cleaning Process

| Step | Action |
|---|---|
| Data types | Set correct types for IDs, dates, numeric and Boolean fields |
| Missing values and duplicates | Checked key columns and removed or handled problem records |
| Data modeling | Connected the 14 tables with one-to-many relationships on ID columns |
| Date handling | Used `Load date` with a date hierarchy for month and year analysis |
| Measures organization | Moved all DAX into a dedicated `_Measure` table |
| Slicers | Added filters for fuel purchase, trip, on-time flag, trailer type, facility type, year, customer type and driver |

## KPIs

| Total Revenue | Total Profit | Total Fuel Cost | On-Time Rate % | Total Trips | Avg MPG |
|:---:|:---:|:---:|:---:|:---:|:---:|
| **$262.53M** | **$161.20M** | **$95.59M** | **55.67%** | **85K** | **6.50** |

Derived ratios: profit margin of about **61%**, and fuel cost equal to about **36%** of revenue.

## Visualizations Created
- **KPI cards**: Revenue, Profit, Fuel Cost, On-Time Rate, Trips and Avg MPG
- **Bar chart**: Top 5 Customers by Revenue
- **Line chart**: Monthly Revenue
- **Line chart**: Monthly Profit
- **Column chart**: Top 5 Routes by Fuel Cost
- **Bar chart**: Total Trips by State
- **Slicers**: Fuel purchase id, Trip id, On time flag, Trailer type, Facility type, Year, Customer type, Driver id
- **Detail page**: Additional KPIs on fleet utilization, incidents, claims, maintenance cost and revenue per mile

## Key Findings
Answers to the business questions:

1. **Top customers:** First Group leads with **$9.1M**, followed by First Logistics ($6.4M), Metro Wholesale ($5.4M), XYZ Wholesale ($5.3M) and Continental Suppl. ($5.2M). Together they bring in about $31.4M, or roughly 12% of revenue.
2. **Monthly trend:** Revenue stays steady at about $21M to $22M a month. **February is the weakest month**, with the lowest revenue ($20.2M) and profit ($7.1M). September is the next weakest ($21.3M revenue, $7.7M profit).
3. **Fuel cost by route:** **RTE00047 and RTE00015** are the most expensive at about $1.8M each, followed by RTE00005, RTE00046 and RTE00052 at about $1.7M.
4. **Trips by state:** **Texas leads with 10.3K trips**, then Missouri (8.7K) and Ohio (7.6K). Colorado and Michigan are lowest at 1.5K each.
5. **Reliability and efficiency:** Only **55.67%** of deliveries are on time, so nearly 45% are late. Average fuel efficiency is **6.50 MPG**.

## Business Insights
- Revenue is spread across many customers. The top customer is only about 3.5% of the total, so the company is not overly dependent on one account.
- The business is highly profitable at about 61% margin, but fuel takes about 36 cents of every revenue dollar.
- Monthly performance is stable, so February's dip is the main seasonal weakness.
- Three states (Texas, Missouri, Ohio) account for about 31% of trips, so activity is concentrated in a few markets.
- The 55.67% on-time rate is the biggest operational weakness and can put customer retention at risk.
- Fuel costs are similar across the top routes, so savings will come from fleet-wide efficiency as well as route-specific fixes.

## Recommendations
1. **Improve on-time delivery** by analyzing late deliveries by route, driver and facility, and adjusting scheduling and dispatch.
2. **Cut fuel costs** with route optimization, driver coaching on idling and speed, and fuel purchasing agreements, starting with RTE00047 and RTE00015.
3. **Raise fuel efficiency** above 6.50 MPG through maintenance and fleet upgrades.
4. **Protect top accounts**, especially First Group and First Logistics, with service-level agreements and regular reviews.
5. **Plan for February** with targeted sales or load-booking campaigns to lift the weakest month.
6. **Grow in low-volume states** such as Colorado and Michigan, and strengthen capacity in Texas, Missouri and Ohio.

## Skills Demonstrated
- Data modeling across multiple related tables
- DAX measures and KPI design
- Data cleaning and preparation (Power Query)
- Interactive dashboard design with slicers
- Data storytelling and business insight generation
- Logistics and operations analytics
- Documentation (GitHub README)

## Conclusion
The company generated **$262.53M in revenue and $161.20M in profit** across 85K trips. Financial performance is strong and diversified across customers, but delivery reliability (55.67% on time) and fuel costs ($95.59M) are the two areas with the most room to improve. Fixing these, while planning for February and growing in low-volume states, offers the clearest path to better performance.

## Author
**Udeme Jackson**
Data Analyst (Entry Level)
[LinkedIn](#) | [GitHub](#) | [Email](#)

## How to run/view the project
1.Dashboard: Open the dashboard file in Logistics-Performance-and-Profitability-Analysis folder to interact with the visualization
