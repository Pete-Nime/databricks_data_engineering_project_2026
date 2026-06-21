# Areca FreshMart Retail Data Warehouse

## End-to-End Data Engineering Project Using Databricks

---

## Project Overview

This project demonstrates the design and implementation of a modern cloud-based Data Warehouse using Databricks, Apache Spark, Delta Lake, and the Kimball Data Warehouse Methodology.

The project was built using a custom retail dataset called **Areca FreshMart**, developed to simulate a real-world retail environment containing both CRM and ERP business data.

The objective was to transform raw operational data into clean, validated, and analytics-ready datasets that support business reporting, dashboarding, and decision-making.

---

# Business Problem

FreshMart operates multiple retail stores and collects data from different business systems.

These systems generate:

### CRM Data

Customer relationship information:

* Customer profiles
* Gender
* Marital status
* Customer registration dates

### ERP Data

Operational business data:

* Product information
* Product categories
* Sales transactions
* Order processing
* Pricing data

The challenge is that raw operational data is often inconsistent, incomplete, and unsuitable for direct business reporting.

This project solves that problem by building a modern Medallion Architecture Data Warehouse.

---

# Technologies Used

| Technology          | Purpose                   |
| ------------------- | ------------------------- |
| Databricks          | Data Engineering Platform |
| Apache Spark        | Distributed Processing    |
| PySpark             | Data Transformation       |
| Delta Lake          | Data Storage Layer        |
| SQL                 | Validation & Analysis     |
| GitHub              | Version Control           |
| Databricks Jobs     | Workflow Automation       |
| Kimball Methodology | Data Warehouse Design     |

---

# Data Architecture

The project follows the Medallion Architecture pattern.

Raw Data
↓
Bronze Layer
↓
Silver Layer
↓
Gold Layer
↓
Analytics & Reporting

---

# Kimball Methodology

This project follows Kimball's dimensional modelling approach.

The goal is to transform operational data into trusted analytical assets.

---

## Bronze Layer

Purpose:

Store source data exactly as received.

Tables:

* crm_cust_info
* crm_prd_info
* crm_sales_details

Characteristics:

* Raw data
* No transformations
* Historical preservation
* Source-of-truth storage

Example:

```python
df = spark.read.csv(
    file_path,
    header=True
)
```

```python
df.write.mode("overwrite") \
.saveAsTable(
"workspace.bronze.crm_cust_info"
)
```

---

## Silver Layer

Purpose:

Clean, standardise, and validate source data.

Transformations performed:

### Data Cleaning

```python
trim(col(column_name))
```

### Date Standardisation

```python
cast(DateType())
```

### Null Validation

```python
col("customer_id").isNotNull()
```

### Product Line Normalisation

```python
R → Road
M → Mountain
T → Touring
S → Other Sales
```

### Gender Standardisation

```python
M → Male
F → Female
```

### Marital Status Standardisation

```python
S → Single
M → Married
```

### Price Corrections

```python
sales_amount / quantity
```

---

## Data Quality Checks

Validation checks performed:

### Null Checks

```sql
SELECT
COUNT(*)
FROM table
WHERE column IS NULL;
```

### Duplicate Checks

```sql
SELECT
column_name,
COUNT(*)
FROM table
GROUP BY column_name
HAVING COUNT(*) > 1;
```

### Date Validation

```sql
SELECT *
FROM table
WHERE end_date < start_date;
```

### Record Counts

```sql
SELECT COUNT(*)
FROM table;
```

---

# Databricks Workflow

The project was built using Databricks notebooks.

Workflow:

### Step 1

Load CRM and ERP source data into Bronze.

### Step 2

Create Silver Customer Table.

### Step 3

Create Silver Product Table.

### Step 4

Create Silver Sales Table.

### Step 5

Perform data quality validation.

### Step 6

Write Delta tables.

### Step 7

Verify transformed outputs.

### Step 8

Schedule automated execution using Databricks Jobs.

<img width="1788" height="998" alt="Screenshot 2026-06-21 at 7 16 48 PM" src="https://github.com/user-attachments/assets/01fd875f-93e0-4b5d-b9cb-5c799f59ebd9" />
<img width="1784" height="998" alt="Screenshot 2026-06-21 at 7 17 09 PM" src="https://github.com/user-attachments/assets/ea9f031f-db77-49b1-b921-6e66dfebbe4c" />



---

# Databricks Job Automation

To simulate a production environment, a Databricks Job was created.

Features:

* Automated execution
* Scheduled refreshes
* Pipeline monitoring
* Run history tracking
* Success / Failure notifications

Benefits:

* Reduces manual work
* Supports daily refreshes
* Improves reliability
* Mimics enterprise production workflows

---

# Business Users

The final datasets can be used by:

### Data Analysts

* KPI Reporting
* Business Analysis

### Business Managers

* Sales Monitoring
* Customer Insights

### Executives

* Strategic Decision Making

### Data Scientists

* Predictive Analytics
* Machine Learning

### BI Developers

* Power BI Dashboards
* Tableau Reporting

---

# Key Skills Demonstrated

* Data Engineering
* Databricks
* Apache Spark
* PySpark
* Delta Lake
* SQL
* Data Cleansing
* Data Validation
* Data Warehousing
* Kimball Methodology
* Medallion Architecture
* Workflow Automation
* ETL / ELT Development

---

# Future Enhancements

* Gold Layer Fact & Dimension Models
* Slowly Changing Dimensions (SCD)
* Incremental Loads
* CI/CD Pipelines
* Power BI Integration
* Data Quality Monitoring
* Unity Catalog Governance

---

# Author

Peter Nime

Founder — Areca Tech Limited

AI Engineer | Data Engineer | Data Analyst

Auckland, New Zealand

