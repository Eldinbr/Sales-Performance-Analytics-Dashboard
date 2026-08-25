# Power BI Data Model

Use a star schema.

**FactSales**
Order ID, Order Date, Customer ID, Product ID, Quantity, Discount, Sales, Profit

**DimDate**
Date, Year, Quarter, Month, Month Number, Year-Month

**DimProduct**
Product ID, Product Name, Category, Sub-Category

**DimCustomer**
Customer ID, Customer Name, Segment

**DimRegion**
Region, Country, City

Relationships:
- DimDate[Date] 1 → * FactSales[Order Date]
- DimProduct[Product ID] 1 → * FactSales[Product ID]
- DimCustomer[Customer ID] 1 → * FactSales[Customer ID]
- DimRegion[Region] 1 → * FactSales[Region]

Use single-direction filtering from dimensions to FactSales.

DimDate:
```DAX
DimDate =
ADDCOLUMNS(
    CALENDAR(DATE(2023,1,1),DATE(2025,12,31)),
    "Year",YEAR([Date]),
    "Quarter","Q"&FORMAT([Date],"Q"),
    "Month",FORMAT([Date],"MMMM"),
    "Month Number",MONTH([Date]),
    "Year-Month",FORMAT([Date],"YYYY-MM")
)
```
