# 🚗 Car Sales Data Analysis — SQL Portfolio Project

> *Transforming 23,905 rows of dealership data into actionable business intelligence using advanced PostgreSQL.*

---

## 📌 Table of Contents

1. [Project Overview](#-project-overview)
2. [Dataset Summary](#-dataset-summary)
3. [Key Business Questions](#-key-business-questions)
4. [KPI Dashboard](#-kpi-dashboard)
5. [Analysis Sections](#-analysis-sections)
6. [Key Insights & Findings](#-key-insights--findings)
7. [SQL Techniques Used](#-sql-techniques-used)
8. [How to Run](#-how-to-run)
9. [Project Structure](#-project-structure)
10. [About the Analyst](#-about-the-analyst)

---

## 🔍 Project Overview

This project performs an end-to-end SQL analysis of a US car dealership sales dataset spanning **2022–2023**. It simulates a real-world business scenario where a Data Analyst is asked to surface KPIs, uncover performance trends, and deliver regional and customer insights to support executive decision-making.

The analysis is structured across **6 thematic sections**, from high-level revenue KPIs down to rolling averages, income segmentation, and reusable BI views — built entirely in **PostgreSQL**.

```
Dataset   →   Exploration   →   KPI Design   →   SQL Queries   →   Insights
```

---

## 📂 Dataset Summary

| Attribute         | Detail                                    |
|-------------------|-------------------------------------------|
| **Source**        | Kaggle — Car Sales Data                  |
| **Records**       | 23,905 transactions                       |
| **Time Period**   | January 2022 – December 2023              |
| **Columns**       | 16                                        |
| **Database**      | PostgreSQL                                |

### 📋 Column Reference

| Column           | Type     | Description                             |
|------------------|----------|-----------------------------------------|
| `car_id`         | VARCHAR  | Unique transaction identifier           |
| `sale_date`      | DATE     | Date of sale                            |
| `customer_name`  | VARCHAR  | Buyer's name                            |
| `gender`         | VARCHAR  | Customer gender (Male / Female)         |
| `annual_income`  | NUMERIC  | Customer annual income (USD)            |
| `dealer_name`    | VARCHAR  | Name of the dealership                  |
| `company`        | VARCHAR  | Car manufacturer / brand                |
| `model`          | VARCHAR  | Specific car model                      |
| `engine`         | VARCHAR  | Engine type (OHC / DOHC)               |
| `transmission`   | VARCHAR  | Auto or Manual                          |
| `color`          | VARCHAR  | Exterior color                          |
| `price`          | NUMERIC  | Sale price in USD                       |
| `dealer_no`      | VARCHAR  | Dealer ZIP code                         |
| `body_style`     | VARCHAR  | SUV / Sedan / Hatchback etc.            |
| `phone`          | BIGINT   | Customer phone                          |
| `dealer_region`  | VARCHAR  | Geographic region of the dealership     |

---

## ❓ Key Business Questions

```
💡 1.  What is the total revenue and average selling price across the full dataset?
💡 2.  How did sales volume and revenue grow from 2022 to 2023?
💡 3.  Which car brands and models drive the most revenue?
💡 4.  Which regions are the highest-performing dealership markets?
💡 5.  How do customer income levels influence purchase decisions?
💡 6.  What are the body style and transmission preferences by gender?
💡 7.  Which months show seasonal demand peaks?
💡 8.  What does the price distribution look like across brands?
💡 9.  Who are the high-value customers (top 5% by spend)?
💡 10. Which dealer performs best nationally and within its region?
```

---

## 📊 KPI Dashboard

> Calculated from the full dataset using SQL aggregations.

| KPI                        | Value              |
|----------------------------|--------------------|
| 🏷️ Total Units Sold        | **23,905**         |
| 💰 Total Revenue           | **$671,525,465**   |
| 📈 Avg Selling Price       | **$28,090**        |
| 💎 Max Single Sale Price   | **$85,800**        |
| 📉 Min Sale Price          | **$1,200**         |
| 📅 Date Range              | Jan 2022 – Dec 2023 |
| 🏢 Unique Brands           | **30**             |
| 🚘 Unique Models           | **154**            |
| 📍 Dealer Regions          | **7**              |
| 🔑 YoY Revenue Growth      | **+23.6% (2022→2023)** |

---

## 🗂️ Analysis Sections

### 1️⃣ Overview KPIs
High-level metrics: total revenue, units sold, average and distribution of prices, Year-over-Year performance, and monthly sales trends with cumulative running totals.

### 2️⃣ Product Performance
Revenue and volume by brand and model. Body style breakdown, engine × transmission cross-analysis, and color preference trends.

### 3️⃣ Regional Performance
Revenue rankings by dealership region, top dealer locations nationally, a region × body style matrix, and NTILE-based quartile segmentation of regions.

### 4️⃣ Customer Analytics
Gender-based purchasing patterns, income segmentation (Low → High), gender × body style preference mapping, and identification of high-value customers in the top 5th percentile.

### 5️⃣ Advanced Analytics
Month-over-Month revenue growth using `LAG()`, brand performance ranked within body style segments, price quartile distribution with `PERCENTILE_CONT`, a 3-month rolling revenue average, top brand per region using CTEs + window functions, and transmission preference shifts across years.

### 6️⃣ BI Views
Two reusable `CREATE VIEW` objects: an Executive Summary View for dashboard tools (Power BI / Tableau), and a Dealer Scorecard View with both national and regional ranking.

---

## 💡 Key Insights & Findings

### 📈 Revenue Growth
- Total revenue grew **23.6% YoY** (2022: $300.3M → 2023: $371.2M), driven largely by a 24.6% increase in transaction volume.
- Average selling price remained relatively stable (~$28K), indicating growth was volume-led, not price-led.

### 🏆 Brand Performance
- **Chevrolet, Dodge, and Ford** are the volume leaders with 1,800+, 1,671, and 1,614 units respectively.
- **Cadillac** commands the highest average selling price at **$40,972**, followed by Saab ($36,516) and Lexus ($34,025) — premium positioning in a mid-tier market.

### 🌍 Regional Insights
- **Austin** leads all regions in both revenue ($117.2M) and units (4,135).
- Revenue per region is relatively balanced ($87M–$117M), suggesting healthy national distribution with Austin as the strongest market.

### 🚙 Product Preferences
- **SUVs** are the most popular body style (6,374 units), but **Sedans** generate the highest average price at $29,833.
- **Auto transmission** slightly outpaces Manual (52.6% vs 47.4%), with Auto preference increasing from 2022 to 2023.
- **Pale White** is the dominant colour choice (47.1%), followed by Black (32.9%) and Red (20%).

### 👥 Customer Demographics
- **Male customers** account for 78.6% of transactions (18,798 vs 5,108 females) — indicating either a demographic skew or a data quality consideration worth flagging.
- **Upper-Mid income segment** ($700K–$1.2M) drives the most sales volume (6,927 units), though average purchase price is nearly uniform across all income tiers (~$28K).
- Price-to-income ratios reveal that **low-income buyers** allocate a disproportionately higher share of income to vehicle purchases — a potential target segment for financing products.

### 📅 Seasonality
- January–February show notably lower sales (315–320 units/month).
- Strong demand spikes in **March–June**, suggesting a seasonal demand curve peaking in Q2.

---

## 🛠️ SQL Techniques Used

```sql
✅ CTEs (WITH clauses)              — modular, readable query architecture
✅ Window Functions                 — RANK(), NTILE(), PERCENT_RANK(), LAG()
✅ Aggregate Functions              — SUM, AVG, COUNT, MIN, MAX, STDDEV
✅ PERCENTILE_CONT                  — median and quartile price distributions
✅ PARTITION BY                     — segmented rankings within groups
✅ Rolling Averages                 — ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
✅ CASE WHEN Segmentation           — income tier classification
✅ Date Extraction                  — EXTRACT(YEAR/MONTH), TO_CHAR formatting
✅ CREATE OR REPLACE VIEW           — reusable BI dashboard views
✅ NULLIF / ROUND                   — safe division and clean formatting
```

---

## ▶️ How to Run

### Prerequisites
- PostgreSQL 13+ (or any modern SQL database with window function support)
- A SQL client: pgAdmin, DBeaver, TablePlus, or VS Code SQL extension

### Steps

```bash
# 1. Create a database
createdb car_sales_db

# 2. Connect and create the table
psql -d car_sales_db -f car_sales_analysis.sql

# 3. Load the CSV data
psql -d car_sales_db -c "\COPY car_sales FROM 'car_data.csv' CSV HEADER;"

# 4. Run individual query sections as needed
```

> 💡 **Tip:** Each query section is clearly labeled and self-contained — you can run any section independently.

---

## 📁 Project Structure

```
car-sales-analysis/
│
├── 📄 README.md                   ← You are here
├── 📄 car_sales_analysis.sql      ← All SQL queries (6 sections)
└── 📄 car_data.csv                ← Raw dataset (add your own copy)
```

---

## 🙋‍♀️ About the Analyst

**Lydia Khasoa Wafula**
*Business Analyst | Data Analyst | Certified Virtual Assistant*
📍 Nairobi, Kenya

With a B.Eng in Mechanical & Production Engineering (Moi University) and professional certifications from McKinsey Forward and ALX Africa, I blend engineering precision with data storytelling to drive operational clarity and business value.

**Core Skills:** PostgreSQL · Python (pandas) · Power BI · Excel (Advanced) · Canva · Business Analysis

🔗 [Portfolio Website](https://sites.google.com/view/lydiawafula)
🐙 [GitHub](https://github.com/lydiawafula)
💼 [LinkedIn](https://linkedin.com/in/lydiawafula)

---

> *"Data is the new oil — but analysis is the refinery."*

---

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-Analytics-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)
![Records](https://img.shields.io/badge/Records-23%2C905-orange?style=for-the-badge)
