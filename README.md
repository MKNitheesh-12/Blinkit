# BlinkIT Sales Data Analysis (SQL)

A SQL-based exploratory data analysis (EDA) project on BlinkIT (grocery delivery) sales data. The project uses T-SQL (Microsoft SQL Server syntax) to calculate key business KPIs and break down sales performance across multiple dimensions — item type, fat content, outlet size, outlet location, and establishment year.

## 📊 Project Overview

This repository contains a single SQL script (`SQLQuery12.sql`) that analyzes a retail dataset called `BlinkIT_ Data`. The queries are designed to answer common business questions such as:

- What are the total and average sales?
- How does sales performance vary by item type, fat content, and outlet attributes?
- What share of total sales does each outlet size/location contribute?
- How do sales trend across outlet establishment years?

The output of these queries is typically used to power a BI dashboard (e.g., Power BI / Tableau / Excel) for visual reporting.

## 🗂️ Dataset

| Detail | Description |
|---|---|
| **Table name** | `BlinkIT_ Data` |
| **Type** | Retail / FMCG sales transactions per item-outlet combination |
| **Key columns used** | `Total_Sales`, `Rating`, `Item_Fat_Content`, `Item_Type`, `Outlet_Location_Type`, `Outlet_Size`, `Outlet_Type`, `Outlet_Establishment_Year` |

> **Note:** The table name contains a space and trailing underscore (`[BlinkIT_ Data]`), so it must be wrapped in square brackets in every query.

## 🛠️ Tools & Tech

- **SQL Server (T-SQL)** — written and tested in SQL Server Management Studio (SSMS)
- Core techniques used:
  - Aggregate functions (`SUM`, `AVG`, `COUNT`)
  - `GROUP BY` / `ORDER BY` for dimensional breakdowns
  - `CAST` for controlled decimal precision/rounding
  - Window functions (`SUM(...) OVER()`) for percentage-of-total calculations
  - `PIVOT` for cross-tabulating sales by fat content across outlet locations
  - Subqueries for pre-aggregating data before pivoting

## 📈 Key Metrics (KPIs) Calculated

| Metric | Description |
|---|---|
| **Total Sales (Millions)** | Total revenue for outlets established in 2022, scaled to millions |
| **Average Sales** | Average sales value per item record |
| **Number of Items** | Count of item records for 2022-established outlets |
| **Average Rating** | Average customer/item rating across the dataset |

## 🔍 Analysis Breakdown

The script performs the following analyses, in order:

1. **Raw data preview** — `SELECT *` to inspect the full table
2. **Overall KPIs** — total sales (2022), average sales, item count (2022), average rating
3. **Sales by Item Fat Content** — total/avg sales, item count, and rating grouped by `Low Fat` vs `Regular`
4. **Top 5 Item Types by Sales** — ranks item categories by total sales
5. **Sales by Outlet Location Type & Fat Content** — cross-dimensional breakdown
6. **Pivot Table: Fat Content by Outlet Location** — reshapes fat-content sales into columns (`Low Fat`, `Regular`) per location type
7. **Sales by Outlet Establishment Year** — trend of sales across the years outlets opened
8. **Outlet Size Contribution** — total sales and % share of overall sales by outlet size
9. **Outlet Location Type Contribution (2022)** — % share of sales by location type, filtered to outlets from 2022
10. **Sales by Outlet Type** — total sales, % share, average sales, item count, and rating per outlet type (e.g., Grocery Store, Supermarket Type1/2/3)

## 📁 Repository Structure

```
├── SQLQuery12.sql     # Main analysis script
└── README.md          # Project documentation
```

## 🚀 How to Run

1. Open the script in **SQL Server Management Studio (SSMS)** or **Azure Data Studio**.
2. Make sure a database containing the `BlinkIT_ Data` table is selected/connected.
3. Run each query block individually (they're separated by blank lines) — each one is a standalone analysis.
4. Export results to CSV/Excel, or connect the results directly to a BI tool such as **Power BI** for dashboarding.

## 💡 Sample Insight Format

Example output structure from the "Sales by Item Fat Content" query:

| Item_Fat_Content | Total_Sales_Thousands | Avg_sales | No_of_items | Avg_Rating |
|---|---|---|---|---|
| Low Fat | ... | ... | ... | ... |
| Regular | ... | ... | ... | ... |

## 📌 Notes

- All monetary aggregates are explicitly `CAST` to `DECIMAL` types to control precision (avoiding floating-point rounding noise).
- The `SUM(...) OVER()` window function is used instead of a self-join or subquery to compute "percentage of total" in a single pass.
- The `PIVOT` query uses a subquery to pre-aggregate `Total_Sales` before pivoting, since `PIVOT` requires a single aggregation source.

## 🔮 Possible Extensions

- Add a Power BI / Tableau dashboard built on top of these queries
- Parameterize the year filter (`2022`) instead of hardcoding it
- Add `Item_Visibility`, `Item_MRP`, or `Item_Weight` based analyses
- Convert script into stored procedures or views for reuse

---

*This project is for data analysis/portfolio purposes.*
