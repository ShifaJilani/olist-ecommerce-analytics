# 🛒 Olist Brazilian E-Commerce Analytics Case Study

## Overview

An end-to-end e-commerce analytics case study built using the **real-world Olist Brazilian E-Commerce public dataset**.

Rather than working with a clean, simplified demo dataset, this project focuses on the messy realities of working with multiple related datasets: understanding the data, identifying quality issues, transforming and modeling it, analyzing business problems using SQL, and communicating actionable recommendations through Power BI.

The project is structured as a **continuous business storyline across four analytical investigations**, all using the same Olist data ecosystem.

### Business Context

Olist is a Brazilian e-commerce marketplace connecting sellers with customers across Brazil.

The objective of this project is to investigate different aspects of the business — from customer conversion and revenue performance to retention, customer value, and pricing — and turn the analysis into practical business recommendations.

---

# 📌 Project Roadmap

### 1. [Funnel Analysis](./01_funnel_analysis/)

**Business Question:** Where are Marketing Qualified Leads dropping off before becoming closed deals, and which acquisition sources and landing pages represent the largest opportunities for improvement?

**Focus areas:**

- Marketing funnel analysis
- MQL-to-closed-deal conversion
- Funnel drop-off
- Conversion rates
- Acquisition source and landing-page segmentation
- SQL analysis
- Joining MQL and closed-deal data

---

### 2. [Revenue Drop Diagnostic](./02_revenue_drop_diagnostic/)


**Business Question:**
Revenue has declined. Is this a genuine business problem or could the decline be caused by data quality or reporting issues?

**Focus areas:**

* Revenue trends
* Order volume
* Average order value
* Customer behavior
* Product/category performance
* Seller performance
* Geographic analysis
* Data-quality investigation
* Root-cause analysis

The objective is not simply to identify that revenue changed, but to determine **why** it changed and what the business should do next.

---

### 3. [Churn & Customer Lifetime Value](./03_churn_clv/)

**Business Question:**
Which customers are being lost, how should churn be defined for this business, and what is the financial impact of customer loss?

**Focus areas:**

* Customer purchase history
* Churn definition
* Cohort analysis
* Retention
* Customer segmentation
* Recency and purchase frequency
* Historical Customer Lifetime Value (CLV)
* Financial impact of churn

The churn definition will be explicitly justified rather than relying on a predefined churn flag.

---

### 4. [Pricing Capstone](./04_pricing_capstone/) 

**Business Question:**
Is Olist potentially underpricing products or categories, and where might pricing changes create additional revenue opportunities?

**Focus areas:**

* Product pricing
* Category-level pricing
* Seller-level pricing
* Sales volume
* Revenue
* Price bands
* Customer behavior
* Freight considerations
* Price vs. demand relationships
* Business recommendation

Because the underlying data is observational, conclusions about pricing will be framed carefully and will not claim causal price elasticity without appropriate experimental evidence.

---

# 🧰 Tools & Technologies

* **Microsoft Fabric**

  * OneLake
  * Lakehouse
  * Data ingestion
  * Data transformation
  * SQL analytics

* **SQL**

  * Joins
  * CTEs
  * Window functions
  * Aggregations
  * Subqueries
  * Data cleaning
  * Analytical queries

* **Power BI**

  * Data modeling
  * DAX measures
  * KPI development
  * Interactive dashboards
  * Business storytelling

* **GitHub**

  * Project documentation
  * SQL scripts
  * Data transformation logic
  * Analysis outputs

---

# 🗂️ Dataset

### Olist Brazilian E-Commerce Public Dataset

The project uses the publicly available **Olist Brazilian E-Commerce Public Dataset**, containing approximately 100,000 orders from the Brazilian e-commerce marketplace between 2016 and 2018.

The dataset contains multiple interconnected tables covering areas such as:

* Customers
* Orders
* Order Items
* Products
* Sellers
* Payments
* Reviews
* Geolocation

The **Olist Marketing Funnel by Olist** dataset is also used where appropriate for the funnel analysis and can be connected to the transactional dataset.

**Source:** Olist Brazilian E-Commerce Public Dataset, publicly available through Kaggle.

> All original data remains attributed to its original source. Any transformations, derived tables, metrics, assumptions, and analyses in this repository are part of this project.

---

# 🔄 Analytical Workflow

The project follows a realistic analytics workflow rather than jumping directly into visualization.

```text
Raw Public Dataset
        ↓
Data Exploration
        ↓
Data Quality Assessment
        ↓
Cleaning & Transformation
        ↓
Data Modeling
        ↓
SQL Analysis
        ↓
Business Investigation
        ↓
Power BI / DAX
        ↓
Insights
        ↓
Business Recommendation
```

---

# 🎯 What This Project Demonstrates

This project is designed to demonstrate practical experience with:

* Working with **messy, real-world datasets**
* Understanding unfamiliar schemas
* Identifying and handling data-quality issues
* Transforming raw data into analytical datasets
* Working with multiple related tables
* Writing analytical SQL beyond basic joins
* Using **CTEs and window functions**
* Building reusable DAX measures
* Designing meaningful business KPIs
* Investigating problems rather than simply reporting numbers
* Translating analytical findings into business recommendations
* Communicating results clearly to non-technical stakeholders

---

## 📁 Repository Structure

The repository will evolve as each stage of the project is completed.

```text
olist-ecommerce-analytics/
│
├── README.md
│
|
├── 01_funnel_analysis/
│   ├── data_discovery.md
│   └── funnel_analysis.md
│
|
├── 02_revenue_drop_diagnostic/
│   └── data_discovery.md
│
|
├── 03_churn_clv/
│   └── data_discovery.md
│
|
├── 04_pricing_capstone/
│   └── data_discovery.md
│
└── ...


```

---

# 📈 Final Deliverables

The completed project will include:

* Data-quality assessment
* Data-cleaning and transformation logic
* SQL analysis
* CTE and window-function examples
* Analytical data model
* Power BI dashboard(s)
* DAX measures
* Key findings
* Business recommendations
* Supporting documentation

Each investigation will document not only **what the data shows**, but also **how the conclusion was reached**.

---

## ⚠️ Data & Analysis Disclaimer

This project is an independent analytical case study using publicly available Olist data.

Business scenarios such as revenue declines or pricing decisions may be constructed as analytical scenarios where the original dataset does not explicitly contain the stated business event.

Any assumptions, derived metrics, simulated scenarios, or analytical definitions will be clearly documented and distinguished from observations directly present in the source data.

The purpose of the project is to demonstrate a realistic **data analyst workflow**, including data preparation, analytical reasoning, SQL, visualization, and business communication.
