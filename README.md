# Customer-Behavior-Analysis


# 🛍️ Customer Shopping Behavior Analysis — End-to-End Data Analytics Project

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-336791?logo=postgresql&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi&logoColor=black)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Wrangling-150458?logo=pandas&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-Advanced%20Queries-orange?logo=sqlite&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

---

## 📌 Project Overview

This is a **full-stack data analytics project** that analyzes transactional data from **3,900 customer purchases** across multiple product categories. The project covers the complete analytics pipeline — from raw data cleaning in Python, to structured SQL analysis in PostgreSQL, to an interactive Power BI dashboard — delivering actionable insights on spending patterns, customer segmentation, product performance, and subscription behavior.

> **Goal:** Understand *who* the customers are, *how* they shop, and *what drives revenue* — using real data.

---

## 📊 Dashboard Preview

![Customer Behavior Dashboard](https://github.com/haritha090/Customer-Behavior-Analysis/blob/main/Screenshot%20(197).png?raw=true)

> **Key Metrics at a Glance:**
> - 👥 **3.9K** Total Customers
> - 💰 **$59.76** Average Purchase Amount
> - ⭐ **3.75** Average Review Rating
> - 🔔 **27%** Subscribed | **73%** Non-Subscribed

---

## 🗂️ Repository Structure

    📦 customer-shopping-behavior-analysis
    ├── 📓 Customer_Behavior.ipynb                  # EDA, cleaning, feature engineering & DB load
    ├── 🗄️ customer_queries.sql                     # 10 business-driven SQL queries with results
    ├── 📊 Customer_Behaviour_Dashboard.pbix         # Interactive Power BI dashboard
    ├── 📄 Customer_Shopping_Behavior_Analysis.pdf   # Full project report
    ├── 🗃️ customer_shopping_behavior.csv            # Raw dataset (3,900 rows × 18 columns)
    └── 📄 README.md

---

## 🔧 Tech Stack

| Layer | Tool / Technology |
|---|---|
| Data Wrangling & EDA | Python · Pandas |
| Database | PostgreSQL · SQLAlchemy · psycopg2 |
| Analytics | SQL — Window Functions, CTEs, Subqueries, Aggregations |
| Visualization | Microsoft Power BI |
| Environment | Jupyter Notebook |

---

## 🔄 Project Workflow

    Raw CSV (3,900 rows × 18 cols)
              │
              ▼
    ┌──────────────────────────────┐
    │   Python — Jupyter Notebook  │  → EDA · Cleaning · Feature Engineering
    │   Pandas + SQLAlchemy        │  → Load cleaned data into PostgreSQL
    └──────────────────────────────┘
              │
              ▼
    ┌──────────────────────────────┐
    │   PostgreSQL Database        │  → Structured storage in `customer` table
    └──────────────────────────────┘
              │
              ▼
    ┌──────────────────────────────┐
    │   SQL Analysis               │  → 10 business questions answered
    └──────────────────────────────┘
              │
              ▼
    ┌──────────────────────────────┐
    │   Power BI Dashboard         │  → Interactive visual insights
    └──────────────────────────────┘

---

## 🧹 Phase 1 — Data Cleaning & Feature Engineering (Python)

**File:** `Customer_Behavior.ipynb`

### Dataset at a Glance
- **Rows:** 3,900 | **Columns:** 18
- **Missing Data:** 37 null values in `Review Rating` column
- **Key columns:** Customer ID, Age, Gender, Location, Item Purchased, Category, Purchase Amount (USD), Season, Review Rating, Subscription Status, Shipping Type, Discount Applied, Previous Purchases, Frequency of Purchases

### Steps Performed

**🔍 Exploratory Data Analysis**
- Used `df.info()` and `df.describe()` to understand structure and summary statistics
- Identified 37 missing values in the `Review Rating` column

**🧼 Data Cleaning**
- Imputed missing `Review Rating` values using **category-wise median** — preserving category-level rating patterns rather than using a global average
- Standardized all column names to `snake_case` (e.g., `Purchase Amount (USD)` → `purchase_amount`)

**⚙️ Feature Engineering**
- Created `age_group` column using **quartile-based binning** (`pd.qcut`) with labels: `Young Adult`, `Adult`, `Middle-aged`, `Senior`
- Created `purchase_frequency_days` by mapping frequency text to numeric values:
  - Weekly → 7 | Fortnightly/Bi-Weekly → 14 | Monthly → 30 | Quarterly → 90 | Annually → 365
- Verified that `discount_applied` and `promo_code_used` were **100% identical** → dropped `promo_code_used`

**🗄️ Database Integration**
- Connected to PostgreSQL using `SQLAlchemy` + `psycopg2`
- Loaded the cleaned DataFrame into a `customer` table using `df.to_sql(if_exists='replace')`

---

## 🗄️ Phase 2 — SQL Business Analysis

**File:** `customer_queries.sql`

| # | Business Question | Key Result | SQL Concepts |
|---|---|---|---|
| Q1 | Revenue by gender | Male: $157,890 · Female: $75,191 | `GROUP BY`, `SUM` |
| Q2 | Discount users spending above average | 839 customers qualify | Subquery, `WHERE` |
| Q3 | Top 5 products by review rating | Gloves (3.86) · Sandals (3.84) · Boots (3.82) | `AVG`, `ROUND`, `ORDER BY` |
| Q4 | Avg spend: Standard vs Express shipping | Standard: $58.46 · Express: $60.48 | Conditional `WHERE`, aggregation |
| Q5 | Subscribers vs Non-Subscribers | Subscribed avg: $59.49 · Non-sub avg: $59.87 | `COUNT`, `AVG`, `SUM` |
| Q6 | Products with highest discount rate | Hat (50%) · Sneakers (49.66%) · Coat (49.07%) | `CASE WHEN`, percentage calc |
| Q7 | Customer segmentation | Loyal: 3,116 · Returning: 701 · New: 83 | `CTE`, `CASE WHEN` |
| Q8 | Top 3 products per category | Jewelry, Blouse, Sandals, Jacket lead categories | `CTE`, `ROW_NUMBER()`, Window Function |
| Q9 | Repeat buyers vs subscription | Not subscribed: 2,518 · Subscribed: 958 | Filtered `GROUP BY` |
| Q10 | Revenue by age group | Young Adult: $62,143 · Middle-aged: $59,197 | `GROUP BY`, derived column |

---

## 📊 Phase 3 — Power BI Dashboard

**File:** `Customer_Behaviour_Dashboard.pbix`

Interactive dashboard with slicers for **Subscription Status**, **Gender**, **Category**, and **Shipping Type**.

**Visuals included:**
- 🍩 **% of Customers by Subscription Status** — 27% subscribed vs 73% non-subscribed
- 📊 **Revenue by Category** — Clothing leads, followed by Accessories, Footwear, Outerwear
- 📊 **Sales by Category** — Units sold across all four categories
- 📊 **Sales by Age Group** — Young Adults and Middle-aged are top buyers
- 📊 **Revenue by Age Group** — Young Adults generate the highest revenue at $62,143

---

## 💡 Key Business Insights

| # | Insight |
|---|---|
| 💰 | Male customers generated **2x more revenue** ($157,890) than female customers ($75,191) |
| 🏷️ | **839 discount users** still spent above average — discounts attract quality buyers, not just bargain hunters |
| ⭐ | **Gloves, Sandals, and Boots** are the top-rated products with ratings above 3.82 |
| 🚚 | Express shipping users spend **$2 more on average** than Standard shipping users |
| 🔔 | Only **27% are subscribed** — a significant untapped growth opportunity |
| 👥 | **3,116 customers (80%)** fall in the Loyal segment — strong base for retention programs |
| 🧒 | **Young Adults** are the highest revenue-generating age group at $62,143 |
| 🎩 | **Hat, Sneakers, and Coat** have ~50% discount dependency — margin review needed |

---

## 💼 Business Recommendations

1. **Boost Subscriptions** — Only 27% are subscribed. Launch exclusive subscriber benefits to convert the 73% non-subscriber base.
2. **Customer Loyalty Programs** — Reward the 701 Returning customers to move them into the Loyal segment.
3. **Review Discount Policy** — Hat and Sneakers have ~50% discount rates. Audit margins to ensure profitability.
4. **Product Positioning** — Highlight Gloves, Sandals, and Boots (top-rated) in marketing campaigns.
5. **Targeted Marketing** — Focus on Young Adults and Express-shipping users who show higher spend and engagement.

---

## 🚀 How to Run This Project

**1. Clone the repository**
```bash
git clone https://github.com/your-username/customer-shopping-behavior-analysis.git
cd customer-shopping-behavior-analysis
```

**2. Install Python dependencies**
```bash
pip install pandas sqlalchemy psycopg2-binary jupyter
```

**3. Run the notebook**
Open `Customer_Behavior.ipynb`, update your PostgreSQL credentials, and run all cells.

**4. Run SQL queries**
Open `customer_queries.sql` in pgAdmin or any PostgreSQL client and execute.

**5. Open the dashboard**
Open `Customer_Behaviour_Dashboard.pbix` in Power BI Desktop and refresh the data source.

---

## 📁 Dataset

`customer_shopping_behavior.csv` — 3,900 rows × 18 columns covering customer demographics, purchase history, product categories, review ratings, shipping preferences, and subscription status.

---

## 🙋‍♀️ About

Built as an end-to-end data analytics portfolio project demonstrating skills across the full analytics stack — data wrangling, relational databases, advanced SQL, and business intelligence dashboarding.

---

## 📬 Connect

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/kaki-haritha-93a3a8292/)


---
⭐ *If you found this project helpful, consider giving it a star!*
