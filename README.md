# Project Title: **Sales-Performance-Analytics-Dashboard**

An interactive **Sales Performance Analytics Dashboard built in Microsoft Power BI**. This project analyses sales revenue, profitability, customer behaviour, product performance, and regional trends to provide actionable business insights.

The dashboard transforms raw sales transaction data into an interactive business intelligence solution using **Power Query, data modelling, DAX, and Power BI visualisations**.

The project focuses on key business metrics including revenue, profit, profit margin, order volume, average order value, regional performance, product performance, and year-over-year growth.

## Preview

<img width="755" height="479" alt="Screenshot 2026-08-25 at 11 42 47 AM" src="https://github.com/user-attachments/assets/79146243-6bcf-4e48-98c1-1b46e9b92a8a" />


### Power BI Dashboard

Open the `.pbix` file from the `PowerBI` folder to explore the complete interactive dashboard.

---

## Table of Contents

* [Overview](#overview)
* [Business Questions](#business-questions)
* [Dataset](#dataset)
* [Data Preparation](#data-preparation)
* [Data Model](#data-model)
* [Technologies Used](#technologies-used)
* [DAX Measures](#dax-measures)
* [Installation](#installation)
* [Usage](#usage)
* [Analysis & Visualizations](#analysis--visualizations)
* [Key Insights](#key-insights)
* [Business Value](#business-value)
* [Conclusion](#conclusion)
* [Future Improvements](#future-improvements)
* [Credits](#credits)
* [License](#license)

---

## Overview

### Motivation

Businesses generate large volumes of sales data, but raw transaction data alone does not provide an easy way to understand performance.

This project was created to transform transactional sales data into an interactive Power BI dashboard that allows users to monitor revenue, profitability, products, customers, and regional performance.

### Objective

The main objective of this project is to analyse sales performance and identify trends that can support data-driven commercial decision-making.

The dashboard provides users with the ability to:

* Monitor overall sales performance
* Track revenue and profit trends
* Compare regional performance
* Identify high-performing products
* Analyse customer segments
* Evaluate profitability
* Compare current performance with previous years
* Identify areas requiring business attention

### Learning Outcomes

While building this project, I developed practical experience in:

* Power Query data cleaning
* Data transformation
* Data modelling
* Star-schema design
* Creating relationships between tables
* DAX calculations
* KPI development
* Time-intelligence calculations
* Interactive Power BI dashboard design
* Business-focused data analysis
* Data storytelling

---

## Business Questions

The dashboard was designed to answer the following business questions:

1. What is the company's total revenue?
2. How much profit has been generated?
3. Which regions generate the highest revenue?
4. Which regions generate the highest profit?
5. Which products generate the most revenue?
6. Which products generate the highest profit?
7. How are sales changing over time?
8. What is the year-over-year sales growth?
9. Which customer segments contribute the most revenue?
10. Which products have high sales but low profitability?
11. What is the average order value?
12. Which areas should management focus on to improve profitability?

---

## Dataset

### Dataset Information

* **Dataset Type:** Sales Transaction Dataset
* **Records:** Sales transaction records
* **Data Format:** CSV
* **Primary Business Areas:** Sales, Products, Customers, Regions, Orders

### Features Included

The dataset contains information such as:

* Order ID
* Order Date
* Customer ID
* Customer Name
* Product ID
* Product Name
* Category
* Sub-Category
* Region
* Country
* Sales
* Quantity
* Discount
* Profit

### Data Preparation

The raw dataset was cleaned and transformed before being loaded into the Power BI data model.

Key preparation steps included:

* Removing duplicate records
* Handling missing values
* Correcting data types
* Standardising categorical values
* Creating calculated columns where required
* Formatting dates
* Checking numerical values
* Creating a dedicated Date table
* Preparing data for analytical modelling

---

## Data Preparation

Data preparation was performed using **Power Query**.

### Power Query Transformations

The following transformations were applied:

1. Imported the raw CSV dataset
2. Promoted the first row as headers
3. Changed column data types
4. Removed unnecessary columns
5. Removed duplicate records
6. Handled null and missing values
7. Standardised text fields
8. Created required calculated columns
9. Validated sales and profit values
10. Loaded the cleaned data into Power BI

This process ensures that the dashboard is based on consistent and reliable data.

---

## Data Model

A **star-schema approach** was used to structure the Power BI data model.

### Fact Table

**FactSales**

Contains transactional sales information:

* Order ID
* Order Date
* Customer ID
* Product ID
* Sales
* Quantity
* Discount
* Profit

### Dimension Tables

**DimDate**

* Date
* Year
* Quarter
* Month
* Month Number
* Year-Month

**DimProduct**

* Product ID
* Product Name
* Category
* Sub-Category

**DimCustomer**

* Customer ID
* Customer Name
* Segment

**DimRegion**

* Region
* Country
* State/Province

The dimension tables connect to the central sales fact table using one-to-many relationships.

This structure improves:

* DAX performance
* Data organisation
* Filtering
* Time intelligence
* Dashboard scalability

---

## Technologies Used

### Tools & Platforms

* **Microsoft Power BI**
* **Power Query**
* **DAX**
* **Microsoft Excel / CSV**
* **Git**
* **GitHub**

### Skills Applied

* Data Cleaning
* Power Query
* Data Transformation
* Data Modelling
* Star Schema
* DAX
* KPI Development
* Time Intelligence
* Data Visualisation
* Business Intelligence
* Dashboard Design
* Business Analysis

### Technologies

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge\&logo=powerbi\&logoColor=black)

![Power Query](https://img.shields.io/badge/Power%20Query-217346?style=for-the-badge\&logo=microsoft-excel\&logoColor=white)

![DAX](https://img.shields.io/badge/DAX-Data%20Analysis-blue?style=for-the-badge)

![Excel](https://img.shields.io/badge/Microsoft%20Excel-217346?style=for-the-badge\&logo=microsoft-excel\&logoColor=white)

![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge\&logo=git\&logoColor=white)

![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge\&logo=github\&logoColor=white)

---

## DAX Measures

Several DAX measures were created to calculate the key performance indicators.

### Total Sales

```DAX
Total Sales =
SUM(FactSales[Sales])
```

### Total Profit

```DAX
Total Profit =
SUM(FactSales[Profit])
```

### Total Quantity

```DAX
Total Quantity =
SUM(FactSales[Quantity])
```

### Total Orders

```DAX
Total Orders =
DISTINCTCOUNT(FactSales[Order ID])
```

### Average Order Value

```DAX
Average Order Value =
DIVIDE(
    [Total Sales],
    [Total Orders],
    0
)
```

### Profit Margin

```DAX
Profit Margin =
DIVIDE(
    [Total Profit],
    [Total Sales],
    0
)
```

### Previous Year Sales

```DAX
Previous Year Sales =
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR(DimDate[Date])
)
```

### Year-over-Year Sales Growth

```DAX
YoY Sales Growth =
DIVIDE(
    [Total Sales] - [Previous Year Sales],
    [Previous Year Sales],
    0
)
```

### Previous Year Profit

```DAX
Previous Year Profit =
CALCULATE(
    [Total Profit],
    SAMEPERIODLASTYEAR(DimDate[Date])
)
```

### YoY Profit Growth

```DAX
YoY Profit Growth =
DIVIDE(
    [Total Profit] - [Previous Year Profit],
    [Previous Year Profit],
    0
)
```

---

## Installation

To explore this project locally:

```bash
# Clone the repository
git clone https://github.com/eldinbr/Sales-Performance-Analytics-Dashboard.git

# Navigate into the project directory
cd Sales-Performance-Analytics-Dashboard
```

Open the following file:

```text
PowerBI/Sales_Performance_Analytics.pbix
```

You will need **Microsoft Power BI Desktop** to open and interact with the `.pbix` file.

---

## Usage

Instructions for using the project:

1. Clone or download the repository
2. Open the Power BI `.pbix` file
3. Refresh the data if required
4. Navigate between dashboard pages
5. Use slicers to filter the data
6. Select charts to cross-filter other visuals
7. Analyse sales, profit, products, customers, and regions

### Interactive Filters

The dashboard includes filters for:

* Year
* Quarter
* Month
* Region
* Category
* Sub-Category
* Customer Segment

These filters allow users to explore the data from different business perspectives.

---

# Analysis & Visualizations

## Dashboard 1 — Executive Overview

The Executive Overview provides a high-level summary of business performance.

### KPI Cards

The dashboard displays:

* Total Sales
* Total Profit
* Profit Margin
* Total Orders
* Average Order Value

### Visualizations

**1. Sales & Profit Trend**

A line chart showing monthly sales and profit trends.

**2. Sales by Region**

A bar chart comparing revenue across regions.

**3. Profit by Category**

A column chart showing profitability by product category.

**4. Sales by Customer Segment**

A donut or bar chart showing revenue contribution by customer segment.

**5. Top 10 Products**

A ranked bar chart displaying the highest-revenue products.

---

## Dashboard 2 — Product Analysis

The Product Analysis page focuses on product-level performance.

### Visualizations

* Sales by Category
* Sales by Sub-Category
* Profit by Category
* Top 10 Products
* Bottom 10 Products
* Sales vs Profit
* Quantity Sold by Product

### Key Questions

This page helps identify:

* Which products generate the most revenue?
* Which products generate the most profit?
* Which products sell frequently but have low profitability?
* Which categories should receive greater attention?

---

## Dashboard 3 — Regional & Customer Analysis

This page analyses geographical and customer performance.

### Visualizations

* Sales by Region
* Profit by Region
* Sales by Country
* Sales by Customer Segment
* Top Customers
* Customer contribution to total revenue

### Key Questions

The analysis helps determine:

* Which regions drive business growth?
* Which regions are most profitable?
* Which customer segments generate the most revenue?
* Which customers contribute significantly to overall sales?

---

## Key Insights

The dashboard can be used to identify several important business patterns.

### Revenue Performance

Sales trends reveal periods of strong and weak business performance and allow management to monitor changes over time.

### Regional Performance

Regional analysis highlights geographic areas that generate the greatest contribution to revenue and profit.

### Product Performance

Product-level analysis identifies high-performing products as well as products that may require pricing, marketing, or inventory review.

### Profitability

Comparing sales against profit helps identify products and categories where high revenue does not necessarily translate into high profitability.

### Customer Segments

Customer analysis provides insight into the segments contributing most significantly to overall revenue.

### Growth

Year-over-year analysis helps determine whether the business is growing or declining compared with previous periods.

---

## Business Value

The dashboard can support business decisions in several areas:

### Sales Strategy

Identify high-performing regions, products, and customer segments.

### Profitability Management

Identify products generating strong revenue but weak profit margins.

### Product Strategy

Understand which categories and products contribute most to business performance.

### Customer Strategy

Identify valuable customer segments and high-value customers.

### Regional Planning

Compare geographical performance and identify areas with growth potential.

### Management Reporting

Provide management with an interactive alternative to manually prepared sales reports.

---

## Conclusion

The **Sales Performance Analytics Dashboard** transforms raw sales transactions into an interactive business intelligence solution using **Power BI, Power Query, DAX, and data modelling**.

The project demonstrates how data can be cleaned, transformed, modelled, analysed, and presented through an interactive dashboard.

By combining financial KPIs, sales trends, product analysis, customer segmentation, and regional performance, the dashboard provides a comprehensive view of overall business performance.

The project demonstrates practical skills relevant to **Data Analyst, BI Analyst, Reporting Analyst, and Junior Power BI Developer** roles.

---

## Future Improvements

Future versions of the dashboard could include:

* Sales forecasting
* Customer lifetime value
* Customer retention analysis
* RFM customer segmentation
* Advanced profitability analysis
* What-if pricing analysis
* Sales target tracking
* Regional sales targets
* Automated data refresh
* Power BI Service deployment
* Row-level security
* Drill-through analysis
* Mobile dashboard optimisation

---

## Credits

* **Developer:** Eldin
* **Dataset:** Sales Transaction Dataset
* **Data Preparation:** Power Query
* **Data Analysis:** DAX
* **Visualisation:** Microsoft Power BI
* **Version Control:** GitHub

---

## License

This project is licensed under the **MIT License** – feel free to use and modify it.

---


