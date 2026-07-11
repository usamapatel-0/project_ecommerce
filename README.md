# 🛒 E-Commerce Analytics | End-to-End Data Engineering Project

## 📌 Overview

This project demonstrates an end-to-end **Data Engineering pipeline** built on **Databricks Lakehouse Platform** using the **Medallion Architecture (Bronze → Silver → Gold)**.

The pipeline ingests raw e-commerce transactional data from **AWS S3**, processes it using **Apache Spark**, stores it in **Delta Lake**, and creates business-ready **Dimension** and **Fact** tables for analytics.

The project replaces traditional Python-based ETL scripts with a scalable distributed processing architecture and provides AI-powered analytics through **Databricks Genie** and interactive BI dashboards.

---

# 🏗️ Architecture

<img width="1746" height="901" alt="ChatGPT Image Jul 11, 2026, 05_21_29 PM" src="https://github.com/user-attachments/assets/d03e9f02-2423-4d68-9b79-8cd8cf0c3469" />



---

# 🚀 Tech Stack

| Technology | Purpose |
|------------|---------|
| Databricks Free Edition | Lakehouse Platform |
| Apache Spark | Distributed Data Processing |
| AWS S3 | Data Lake Storage |
| Delta Lake | ACID Transactions & Time Travel |
| Unity Catalog | Data Governance |
| Spark SQL | Analytics |
| Databricks SQL | Reporting |
| AI/BI Dashboard | Visualization |
| Genie AI | Natural Language Query |
| Databricks Jobs | Pipeline Automation |

---

# 📂 Project Structure

```
project_ecommerce/

├── 1_setup/
│   └── setup_catalog
│
├── 2_medallion_processing_dim/
│   ├── 2_dim_silver
│   └── 3_dim_gold
│
├── 3_medallion_processing_fact/
│   └── 3_fact_gold
│
├── dashboards/
│
└── README.md
```

---

# 🗂️ Catalog Structure

```
Catalog
│
└── ecommerce
      │
      ├── source_data
      │
      ├── bronze
      │
      ├── silver
      │
      └── gold
```
<img width="447" height="845" alt="image" src="https://github.com/user-attachments/assets/52ca1730-ed2c-4b64-9e4f-52918034bfd3" />


---

# 📥 Data Source

Raw CSV files are stored inside AWS S3.

```
S3
│
└── source_data
      │
      └── raw
            ├── brands
            ├── category
            ├── customers
            ├── products
            ├── orders
            ├── order_items
            └── date

```
<img width="1918" height="825" alt="Screenshot 2026-07-11 131857" src="https://github.com/user-attachments/assets/89591a6f-758d-48e3-bd36-12f5f66dca84" />

<img width="1918" height="826" alt="Screenshot 2026-07-11 134013" src="https://github.com/user-attachments/assets/a6d6c42b-b0ed-46a8-8efc-ad0611f60e4d" />

<img width="1918" height="850" alt="Screenshot 2026-07-11 131631" src="https://github.com/user-attachments/assets/61c8b71f-c5e8-474d-98fa-7a80f5dc0158" />
<img width="1917" height="867" alt="Screenshot 2026-07-11 131704" src="https://github.com/user-attachments/assets/7078e0a6-f157-43dc-a9b4-616520fc35b5" />


Databricks accesses these files using **Unity Catalog External Volumes**.

---

# 🥉 Bronze Layer

The Bronze layer stores raw source data without modifying the business data.

### Operations

- Raw CSV ingestion
- Schema enforcement
- Delta table creation
- Metadata tracking
- Source file tracking

Metadata Added

- `_source_file`
- `ingested_at`

Bronze Tables

- brz_brands
- brz_category
- brz_customers
- brz_products
- brz_orders
- brz_order_items
- brz_date

---

# 🥈 Silver Layer

The Silver layer cleans and standardizes the raw data.

### Transformations

- Remove duplicate records
- Handle NULL values
- Data type conversion
- Remove special characters
- Standardize text
- Generate business-friendly columns
- Schema validation

Silver Tables

- slv_brands
- slv_category
- slv_customers
- slv_products
- slv_orders
- slv_order_items
- slv_date

---

# 🥇 Gold Layer

The Gold layer contains analytics-ready data optimized for reporting.

---

## Dimension Tables

### Product Dimension

Contains

- Product ID
- SKU
- Brand
- Category
- Color
- Size
- Material
- Weight
- Rating

---

### Customer Dimension

Contains

- Customer Information
- Demographics
- Country
- Region

---

### Date Dimension

Contains

- Year
- Quarter
- Month
- Week
- Day
- Weekend Flag

---

## Fact Table

### fact_transactions_denorm

Denormalized transaction table containing **34 business columns**.

### Transaction Information

- transaction_id
- transaction_date
- transaction_ts
- customer_id
- product_id
- seq_no
- channel

---

### Financial Metrics

- quantity
- gross_amount
- discount_percent
- discount_amount
- tax_amount
- net_amount
- net_amount_inr

---

### Product Attributes

- sku
- category_code
- category_name
- brand_code
- brand_name
- color
- size
- rating_count

---

### Time Dimensions

- year
- quarter
- month_name
- week
- day_name
- hour_of_day
- is_weekend

---

### Promotion Details

- coupon_code
- coupon_flag

---

# 🔄 Medallion Pipeline

```
AWS S3

↓

External Volume

↓

Bronze

↓

Silver

↓

Gold

↓

Dashboards

↓

Business Users
```

---

# 📊 Dashboard KPIs

The dashboard provides insights into

- Total Revenue
- Total Sales
- Total Orders
- Monthly Sales Trend
- Revenue by Category
- Revenue by Brand
- Channel Performance
- Coupon Performance
- Customer Purchase Analysis
- Product Performance

---

https://github.com/user-attachments/assets/26f34dad-c2b0-409c-8b97-8b66fba538fb




# 📈 Business Metrics

### Total Sales

₹1.81 Billion

### Top Performing Category

Electronics

₹1.38 Billion

### Other Categories

- Home & Kitchen
- Apparel
- Sports & Outdoors
- Beauty & Personal Care
- Toys & Games
- Grocery
- Books

---

# 💰 Currency Support

Supported currencies

- INR
- USD

Automatic currency conversion to INR is implemented in the Gold layer.

---

# 📱 Sales Channels

- Website
- Mobile

---

# 🤖 Genie AI

The Gold layer is connected with **Databricks Genie** allowing business users to ask natural language questions.

Example

- Show monthly sales.
- Which category generated highest revenue?
- Top 10 selling products.
- Best customers by revenue.
- Sales trend for Electronics.

---

# 🔐 Data Governance

Implemented using Unity Catalog.

Features

- Catalog Management
- Schemas
- External Volumes
- Managed Tables
- Data Lineage
- Fine-grained Access Control

---

# ⚙️ Orchestration

Pipeline execution is automated using **Databricks Jobs**.

```
S3 Upload

↓

Bronze

↓

Silver

↓

Gold

↓

Dashboard Refresh
```

---


---

# ⭐ Key Features

- End-to-End Data Engineering Pipeline
- Medallion Architecture
- Apache Spark Processing
- AWS S3 Integration
- Delta Lake
- Unity Catalog
- Delta Tables
- Dimension & Fact Modeling
- Currency Conversion
- AI-powered Analytics
- Interactive Dashboards
- Databricks Jobs Automation

---

# 🎯 Business Use Cases

- Sales Analytics
- Customer Behavior Analysis
- Revenue Analysis
- Product Performance
- Brand Performance
- Category Analysis
- Coupon Effectiveness
- Order Analytics
- Executive Reporting

---

# 🔮 Future Enhancements

- Delta Live Tables
- Auto Loader
- Streaming Pipeline
- Customer Cohort Analysis
- Customer Lifetime Value (CLV)
- Product Recommendation Engine
- Inventory Analytics
- ML Demand Forecasting
- CI/CD with GitHub Actions
- Terraform Deployment

---

# 👨‍💻 Author

**Usama Patel**

📧 Email: usamapatel340@gmail.com

---

**Built using Databricks Lakehouse Platform, Apache Spark, AWS S3, Delta Lake and Unity Catalog.**
