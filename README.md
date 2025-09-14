
# 🛒 Online Retail Analysis with BigQuery

This project analyzes the **Online Retail dataset** using **Google BigQuery** and SQL.  
The goal is to uncover insights into **product sales**, **customer purchase behavior**, and **monthly revenue trends**.  

---

## 📊 Dataset
- **Name**: Online Retail Dataset (UCI Machine Learning Repository)  
- **Rows**: ~500,000 transactions  
- **Features**:  
  - `InvoiceNo` – Transaction number  
  - `StockCode` – Product code  
  - `Description` – Product name  
  - `Quantity` – Number of units purchased  
  - `InvoiceDate` – Date and time of transaction  
  - `UnitPrice` – Price per unit  
  - `CustomerID` – Unique customer identifier  
  - `Country` – Customer’s country  

📌 [Dataset Source](https://archive.ics.uci.edu/ml/datasets/online+retail)   

---

## 🚀 Problems Solved

---

### 🔹 Problem 1: Best-Selling Products
**Query:** Top 10 products by total revenue.  
`SELECT Description AS product, ROUND(SUM(Quantity * UnitPrice), 2) AS total_revenue FROM your_project.your_dataset.Online_Retail WHERE Quantity > 0 GROUP BY product ORDER BY total_revenue DESC LIMIT 10;`

**Insight:** Identifies the most profitable products.  
📂 **Result:** [results/best_selling_products.csv](results/best_selling_products.csv)  

---

### 🔹 Problem 2: Customer Purchase Behavior
**Query:** Top 10 customers by total spend, with rank.  
`WITH customer_spend AS ( SELECT CustomerID, ROUND(SUM(Quantity * UnitPrice), 2) AS total_spent FROM your_project.your_dataset.Online_Retail WHERE Quantity > 0 GROUP BY CustomerID ) SELECT CustomerID, total_spent, RANK() OVER (ORDER BY total_spent DESC) AS spend_rank FROM customer_spend ORDER BY total_spent DESC LIMIT 10;`

**Insight:** Highlights high-value customers and revenue concentration.  
📂 **Result:** [results/customer_purchase_behavior.csv](results/customer_purchase_behavior.csv)  

---

### 🔹 Problem 3: Monthly Sales Trend
**Query:** Revenue trends across year/month.  
`SELECT EXTRACT(YEAR FROM InvoiceDate) AS year, EXTRACT(MONTH FROM InvoiceDate) AS month, ROUND(SUM(Quantity * UnitPrice), 2) AS monthly_revenue FROM your_project.your_dataset.Online_Retail WHERE Quantity > 0 GROUP BY year, month ORDER BY year, month;`

**Insight:** Useful for detecting seasonality and demand spikes.  
📂 **Result:** [results/monthly_sales_trend.csv](results/monthly_sales_trend.csv)  

---

## 📂 Repository Structure

online-retail-bigquery-analysis/
│
├── data/
│   └── Online Retail.csv           # original dataset 
│
├── queries/                        # BigQuery SQL queries
│   ├── best_selling_products.sql
│   ├── customer_purchase_behavior.sql
│   └── monthly_sales_trend.sql
│
├── results/                        # CSV outputs of queries
│   ├── best_selling_products.csv
│   ├── customer_purchase_behavior.csv
│   └── monthly_sales_trend.csv
│
└── README.md                       # project documentation

---

## 📂 Results

The `/results` folder contains CSV exports of BigQuery queries:  

- **best_selling_products.csv** → Top 10 products by revenue  
- **customer_purchase_behavior.csv** → Top 10 customers by spending  
- **monthly_sales_trend.csv** → Monthly revenue across years  
These CSVs are directly queryable outputs for reproducibility. 
----
