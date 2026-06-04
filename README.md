# ElectroHub Retail Sales & Profitability Analytics Dashboard

## Overview

ElectroHub is a multi category retail company operating across Electronics, Clothing, Footwear, Home Appliances, Accessories, Kitchenware, Bags, and Personal Care products.

This project focuses on building an end-to-end Business Intelligence solution using SQL Server and Power BI to analyze sales performance, profitability, discounts, product performance, and regional sales trends. The dashboard transforms raw transactional data into actionable business insights that support data-driven decision-making.

---

## Business Problem

As ElectroHub expanded across multiple product categories and regions, tracking business performance through traditional reporting became increasingly difficult.

The business required a centralized analytics solution to:

- Monitor sales and profitability trends
- Identify top and underperforming products
- Analyze discount effectiveness
- Compare business performance across different time periods
- Track regional sales distribution
- Enable interactive reporting for stakeholders

---

## Project Objectives

- Build an interactive retail analytics dashboard
- Analyze sales trends across multiple time periods
- Track product-level performance
- Evaluate promotional discount impact
- Monitor regional sales performance
- Enable comparative period analysis using DAX
- Support data-driven business decisions

---

## Technology Stack

| Category | Technology |
|-----------|------------|
| Database | SQL Server |
| Data Transformation | Power Query |
| Data Modeling | Star Schema |
| Visualization | Power BI Desktop |
| Calculations | DAX |
| Reporting | Power BI |

---

## Dataset Overview

The project uses four interconnected datasets.

### Customer Table

| Field |
|---------|
| Customer ID |
| Customer Name |
| City |
| State |
| Pincode |
| Email ID |
| Phone Number |

### Product Table

| Field |
|---------|
| Product ID |
| Product Name |
| Product Line |
| Price (INR) |

### Promotion Table

| Field |
|---------|
| Promotion ID |
| Promotion Name |
| Ad Type |
| Coupon Code |
| Price Reduction Type |

### Sales Transactions Table

| Field |
|---------|
| Date |
| Customer ID |
| Promotion ID |
| Product ID |
| Units Sold |
| Price Per Unit |
| Total Sales |
| Discount Percentage |
| Discount Value |
| Net Sales |

---

## Project Workflow

```text
CSV Files
    ↓
SQL Server
    ↓
ElectroHub_Test Environment (300 Records)
    ↓
Power Query Transformations
    ↓
Star Schema Data Modeling
    ↓
DAX Measures
    ↓
Dashboard Development
    ↓
Validation & Testing
    ↓
ElectroHub_Prod Environment (3000+ Records)
    ↓
Final Business Dashboard
```

---

## Test-to-Production Workflow

To simulate a real-world BI implementation workflow, a separate testing environment was created before deploying the final dashboard.

### ElectroHub_Test
- Approximately 300 transaction records
- Relationship validation
- KPI verification
- DAX testing
- Dashboard interaction testing

### ElectroHub_Prod
- 3000+ transaction records
- Final reporting environment
- Business analysis and dashboard deployment

This approach helped validate calculations and dashboard functionality before working with the complete dataset.

---

## Data Cleaning & Transformation

The following transformations were performed using Power Query:

### Data Type Validation
- Verified and corrected data types across all tables.

### Discount Standardization
- Extracted discount percentages from text-based promotion descriptions.
- Created a structured Discount Percentage column.

### Data Enrichment
- Merged Product and Sales tables using Product ID.
- Populated Price Per Unit values.

### Missing Value Handling
- Replaced null discount values with 0.

### Calculated Columns

**Total Sales**

```text
Total Sales = Units Sold × Price Per Unit
```

**Discount Value**

```text
Discount Value = Total Sales × Discount Percentage / 100
```

**Net Sales**

```text
Net Sales = Total Sales − Discount Value
```

**Profit**

```text
Profit = 10% × Net Sales
```

---

## Data Modeling

A Star Schema model was implemented for efficient reporting and analysis.

### Fact Table
- Sales Transactions

### Dimension Tables
- Customer
- Product
- Promotion

### Relationships

| Dimension Table | Fact Table | Key | Cardinality |
|---------------|------------|-----|-------------|
| Customer | Sales Transactions | Customer ID | One-to-Many |
| Product | Sales Transactions | Product ID | One-to-Many |
| Promotion | Sales Transactions | Promotion ID | One-to-Many |

---

## DAX Implementation

### Comparative Period Analysis

A secondary date table and inactive relationship were used to compare Net Sales across two user-selected time periods.

```DAX
Sum of Net Sales =
CALCULATE(
    SUM(Sales_transaction_test[Net Sales]),
    ALL('Date Table 1'),
    USERELATIONSHIP(
        'Date Table 2'[Date],
        Sales_transaction_test[Date_dd_mm_yyyy]
    )
)
```

This enables dynamic period-over-period comparison without affecting the primary reporting period.

---

## Dashboard Features

### Executive KPIs

- Total Sales
- Net Sales
- Total Profit
- Total Orders
- Quantity Sold
- Average Discount

### Product Performance Analysis

- Top 5 Products by Sales
- Bottom 5 Products by Sales
- Top 5 Products by Profit
- Bottom 5 Products by Profit
- Top 5 Products by Quantity Sold
- Bottom 5 Products by Quantity Sold

### Sales Trend Analysis

- Daily Sales Trends
- Monthly Sales Trends
- Quarterly Sales Trends
- Yearly Sales Trends

### Profitability Analysis

- Sales vs Profit Scatter Plot

### Discount Analysis

- Average Discount by Promotion

### Geographic Analysis

- Net Sales by City

---

## Dashboard Preview

### Executive Dashboard
(Add Screenshot)

### Product Performance Dashboard
(Add Screenshot)

### Sales Trend Dashboard
(Add Screenshot)

---

## Project Outcome

Developed a centralized retail analytics solution capable of analyzing 3,000+ sales transactions across multiple product categories. The dashboard provides visibility into sales performance, profitability, promotional effectiveness, and regional trends, enabling more informed business decision-making.
