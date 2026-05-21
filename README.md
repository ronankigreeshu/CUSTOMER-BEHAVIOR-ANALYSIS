
# Customer Shopping Behavior Analysis

End-to-end data analytics pipeline — from raw Excel data to SQL queries,
Power BI dashboard, and stakeholder presentation.

Tools: Python · pandas · SQL · PostgreSQL · Power BI · Gamma (PPT)

---

## Overview

This project explores customer shopping patterns using a retail dataset of
~3,900 records. The goal was to build a complete analytics workflow: clean
and transform raw data in Python, store and query it in PostgreSQL, visualize
findings in Power BI, and communicate results through a professional
presentation.

- ~3,900 records
- 12 SQL queries
- 6 tools used
- 10+ business insights

---

## Dataset

File: customer_shopping_behavior.xlsx

| Column                   | Type  | Description                                      |
|--------------------------|-------|--------------------------------------------------|
| customer_id              | int   | Unique customer identifier                       |
| age                      | int   | Customer age in years                            |
| gender                   | str   | Male / Female                                    |
| category                 | str   | Product category (Clothing, Footwear, etc.)      |
| item_purchased           | str   | Specific product name                            |
| purchase_amount          | float | Transaction value in USD                         |
| review_rating            | float | Product rating 1–5 (nulls imputed)               |
| subscription_status      | str   | Yes / No                                         |
| shipping_type            | str   | Standard, Express, Next Day Air, etc.            |
| discount_applied         | str   | Yes / No                                         |
| frequency_of_purchases   | str   | Weekly, Monthly, Annually, etc.                  |
| previous_purchases       | int   | Count of prior transactions                      |
| age_group *              | str   | Young Adult / Adult / Middle-aged / Senior       |
| purchase_frequency_days *| int   | Purchase cycle in days                           |

* Engineered features added during preprocessing.

---

## Tools & Technologies

| Tool            | Purpose                                                        |
|-----------------|----------------------------------------------------------------|
| Python (Colab)  | Data loading, EDA, cleaning, database ingestion               |
| pandas          | Null imputation, feature engineering, column transformation   |
| PostgreSQL      | Relational database — structured storage and querying         |
| SQL             | 12 queries: aggregations, subqueries, CTEs, window functions  |
| Power BI        | Interactive dashboard — revenue, segments, product views      |
| Gamma           | Stakeholder presentation — findings and recommendations       |

---

## Project Steps

1. Load Dataset
   Read customer_shopping_behavior.xlsx into a pandas DataFrame in Google
   Colab. Inspected shape, data types, and null counts using df.head(),
   df.info(), df.describe(), and df.isnull().sum().

2. Exploratory Data Analysis (EDA)
   Identified missing values in Review Rating. Detected that promo_code_used
   was 100% identical to discount_applied across all rows and flagged it for
   removal.

3. Data Cleaning & Feature Engineering
   - Imputed missing review ratings using the median per product category.
   - Standardized all column names to snake_case.
   - Renamed purchase_amount_(usd) to purchase_amount.
   - Dropped the redundant promo_code_used column.
   - Created age_group using pd.qcut() with 4 quartile bins.
   - Created purchase_frequency_days by mapping frequency text to integers.

4. PostgreSQL Setup & Data Loading
   Installed and started PostgreSQL inside Colab. Created the
   customer_behavior database and loaded the cleaned DataFrame into the
   customer table using SQLAlchemy and df.to_sql().

5. SQL Analysis — 12 Queries
   Covered: revenue by gender, discount users above average spend, top-rated
   products, shipping type comparison, subscription impact, discount usage
   rates, customer segmentation (New / Returning / Loyal), top 3 products
   per category (CTE + ROW_NUMBER), subscription among repeat buyers, and
   revenue by age group.

6. Power BI Dashboard
   Built an interactive dashboard with revenue breakdowns, customer segment
   charts, product performance tables, and shipping comparisons. Connected
   directly to the PostgreSQL data source.

7. Report & Presentation
   Compiled all findings into a structured Word report with query code and
   results. Created a stakeholder slide deck in Gamma covering methodology,
   insights, and business recommendations.

---

## Dashboard Results

Revenue by Gender
  Male      $157,890  (68%)
  Female     $74,510  (32%)

Revenue by Age Group
  Middle-aged   $65,430
  Adult         $61,870
  Senior        $58,940
  Young Adult   $46,160

Customer Segments
  Returning Customer   2,847  (73%)
  Loyal Customer         812  (21%)
  New Customer           241   (6%)

Subscription Impact
  Subscribed avg spend      $60.44   |   Total revenue $135,268
  Unsubscribed avg spend    $58.91   |   Total revenue  $97,132

Top Rated Products
  1. Hoodie    4.01
  2. Dress     3.98
  3. Jeans     3.95
  4. Sneakers  3.93
  5. Jacket    3.91

Key takeaway: Subscribers generate 58% more total revenue. Middle-aged
customers are the top revenue segment. 45% of repeat buyers are unsubscribed
— the highest-ROI conversion opportunity in the dataset.

---

## How to Run

1. Upload customer_shopping_behavior.xlsx to Google Colab under /content/.

2. Install dependencies:
      pip install psycopg2-binary sqlalchemy

3. Run the PostgreSQL setup cells — they install the server, start the
   service, and create the customer_behavior database automatically.

4. Run all notebook cells top to bottom:
      Load Excel → EDA → Clean → Engineer features
      → Connect PostgreSQL → df.to_sql() → Run queries

5. Open dashboard.pbix in Power BI Desktop. Refresh the data source
   connection if needed.

6. Open the Gamma presentation link from the project folder — no
   installation required, runs in browser.

---

## File Structure

customer-shopping-behavior/
│
├── customer_shopping_behavior.xlsx   # raw dataset
├── untitled0.ipynb                   # main Colab notebook
├── dashboard.pbix                    # Power BI dashboard
├── report.docx                       # full project report
├── presentation/                     # Gamma PPT export
└── README.md                         # this file

---
```
