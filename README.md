# 📊 Indian E-Commerce Sales Analysis — SQL Project

## 📌 Overview
This project presents an end-to-end SQL analysis of a simulated Indian e-commerce dataset, built and executed in MySQL Workbench. It models a realistic online retail backend with customers, products, and transactional sales data connected through primary and foreign key relationships, and uses SQL to answer 25 real business questions — from basic revenue summaries to advanced customer segmentation, churn analysis, and stockout risk detection.

The dataset spans **June 2024 to June 2026** (~2 years of transactions), giving enough depth for meaningful trend, cohort, and behavioral analysis.

---

## 🗂️ Schema Summary

| Table Name | Rows | Columns |
|---|---|---|
| customers | 40,000 | Customer_ID, Customer_Name, Gender, Age, Age_Group, Date_of_Birth, Email, Phone, City, State, Pincode, Registration_Date, Customer_Tier, Total_Orders, Total_Spent |
| products | 2,000 | Product_ID, Product_Name, Category, Brand, Original_Price, Discount_Percent, Discount_Amount, Selling_Price, Stock_Quantity, Weight_kg, Avg_Rating, Total_Reviews |
| sales | 250,000 | Order_ID, Customer_ID, Product_ID, Order_Date, Order_Time, Delivery_Date, Quantity, Unit_Price, Order_Value, Shipping_Cost, Coupon_Code, Coupon_Discount, Total_Amount, Payment_Mode, Order_Status, Rating, Review_Text, City, State, Customer_Age, Customer_Age_Group |

### 🔑 Keys & Relationships
- `customers.Customer_ID` → Primary Key
- `products.Product_ID` → Primary Key
- `sales.Order_ID` → Primary Key
- `sales.Customer_ID` → Foreign Key referencing `customers`
- `sales.Product_ID` → Foreign Key referencing `products`

```
customers (1) ──< sales (many)     via Customer_ID
products  (1) ──< sales (many)     via Product_ID
```

---

## 🛠️ Tools Used
- **MySQL Workbench 8.0** — schema design, data import, query execution
- **SQL** — joins, aggregations, window functions (`RANK`, `NTILE`, `LAG`), CTEs, subqueries
- **Excel / CSV** — raw data source

---

## 🏗️ Project Structure
```
├── README.md                    # Project overview (this file)
├── questions.md                 # 25 business questions, organized by difficulty
├── ecommerce_sql_queries.sql    # All 25 SQL queries in one file
├── query_results.md             # Actual output of each query run against the dataset
└── erd_diagram.png              # Entity-relationship diagram
```

---

## ❓ Business Questions (25 total, in 3 phases)

### 🟢 Phase 1 — Easy (Q1–Q9)
Basic `SELECT`, `WHERE`, `GROUP BY` — single-table aggregations covering row counts, revenue totals, category/state breakdowns, and stock checks.

### 🟡 Phase 2 — Medium (Q10–Q18)
Multi-table joins and grouped aggregations — monthly revenue trends, top customers/products, delivery performance by state, coupon effectiveness, payment mode analysis, and category ratings.

### 🔴 Phase 3 — Hard (Q19–Q25)
Window functions, CTEs, and subqueries — churn risk detection, RFM-style customer segmentation (`NTILE`), month-over-month growth (`LAG`), stockout risk detection, top product per category (`RANK`), repeat purchase rate by tier, and order-frequency analysis.

Full question list: [`questions.md`](./questions.md)
All SQL queries: [`ecommerce_sql_queries.sql`](./ecommerce_sql_queries.sql)
Full output for every query: [`query_results.md`](./query_results.md)

---

## 📈 Key Insights

- 💰 **Total revenue from delivered orders** is approximately **₹474.16 crore (₹4.74 billion)** across the full 2-year period.
- 📅 **2025 was the peak year**, with 120,519 orders from 38,024 unique customers — more than either 2024 or 2026 (partial years in the dataset).
- 👑 **Top customer** by lifetime spend is a Platinum-tier customer with **₹10.71 lakh** spent across 10 orders — showing high-tier customers drive disproportionate revenue.
- 📦 **Top-selling product** is the *Noise Watch V1* (Electronics), generating **₹19.35 crore** in revenue from 2,308 units sold.
- 🏆 **Electronics** is both the largest category by product count (290 products) and consistently one of the highest-rated categories (avg. rating 4.4/5).
- ⭐ **Customer ratings are strong and consistent across categories** — all categories average between 4.39–4.4 out of 5, suggesting stable product/service quality platform-wide.
- 🎟️ **Coupon usage is relatively low** — only 20.07% of orders used a coupon, and interestingly, average order value was *slightly lower* (₹23,059) for coupon orders vs. non-coupon orders (₹23,889), suggesting coupons may be used more on smaller purchases rather than driving bigger baskets.
- 💳 **Credit Card users spend the most per order** on average (₹26,535), followed by UPI (₹24,724) — despite UPI being the most-used payment mode by volume (128,474 orders).
- 🔁 **Repeat purchase rates are extremely high for top-tier customers** — 99.79% of Platinum customers and 98.83% of Gold customers have ordered more than once, compared to 94.07% for Silver, showing tier status correlates strongly with loyalty.
- ⚠️ **18,906 customers (~47% of the customer base)** haven't ordered in the last 90 days — a substantial churn-risk segment worth targeting with re-engagement campaigns.
- ✅ **No products are currently out of stock** (0 products with Stock_Quantity = 0), indicating healthy inventory levels across the catalog.
- 🚚 **Delivery times are consistent nationwide**, averaging ~4.5 days across all states — no major regional delivery bottlenecks in this dataset.

*(All figures above are pulled directly from the actual query outputs in `query_results.md`.)*

---

## 🚀 How to Reproduce This Project

1. Clone this repository
2. Open MySQL Workbench and create the database schema (tables: `customers`, `products`, `sales`) with the primary/foreign keys described above
3. Import `customers.csv`, `products.csv`, and `sales.csv` into their respective tables
4. Run the queries from `ecommerce_sql_queries.sql` (organized Easy → Medium → Hard)
5. Compare your output against `query_results.md` to validate

---

## 🙋 About
This project was built as a hands-on SQL portfolio piece to demonstrate practical database design and analytical querying skills — schema design, data validation, joins, aggregations, and advanced SQL (window functions, CTEs) — applied to a realistic, large-scale e-commerce dataset (40,000 customers, 2,000 products, 250,000 transactions).
