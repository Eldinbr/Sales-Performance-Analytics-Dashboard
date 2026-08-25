# DAX Measures

```DAX
Total Sales = SUM(FactSales[Sales])

Total Profit = SUM(FactSales[Profit])

Total Quantity = SUM(FactSales[Quantity])

Total Orders = DISTINCTCOUNT(FactSales[Order ID])

Average Order Value = DIVIDE([Total Sales], [Total Orders], 0)

Profit Margin = DIVIDE([Total Profit], [Total Sales], 0)

Previous Year Sales =
CALCULATE([Total Sales], SAMEPERIODLASTYEAR(DimDate[Date]))

YoY Sales Growth =
DIVIDE([Total Sales] - [Previous Year Sales], [Previous Year Sales], 0)

Previous Year Profit =
CALCULATE([Total Profit], SAMEPERIODLASTYEAR(DimDate[Date]))

YoY Profit Growth =
DIVIDE([Total Profit] - [Previous Year Profit], [Previous Year Profit], 0)

Sales YTD = TOTALYTD([Total Sales], DimDate[Date])

Profit YTD = TOTALYTD([Total Profit], DimDate[Date])

Orders YTD = TOTALYTD([Total Orders], DimDate[Date])

Average Discount = AVERAGE(FactSales[Discount])

Sales per Unit = DIVIDE([Total Sales], [Total Quantity], 0)

Profit per Order = DIVIDE([Total Profit], [Total Orders], 0)
```
