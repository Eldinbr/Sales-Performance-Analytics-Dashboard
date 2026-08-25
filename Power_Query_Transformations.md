# Exact Power Query Transformation Plan

1. Get Data → Text/CSV → `Dataset/sales_data.csv`
2. Promote first row as headers.
3. Set data types:
   - Order ID, Customer ID, Customer Name, Segment, Product ID, Product Name, Category, Sub-Category, Region, Country, City → Text
   - Order Date → Date
   - Quantity → Whole Number
   - Discount → Percentage
   - Sales, Profit → Fixed Decimal Number/Currency
4. Transform → Format → Trim all text columns.
5. Remove blank Order IDs.
6. Remove duplicates using Order ID.
7. Filter invalid/negative Sales rows for review.
8. Create reference queries for DimProduct, DimCustomer and DimRegion.
9. Remove duplicates from each dimension.
10. Create DimDate in DAX and mark it as the Date table.

Use this M query in Advanced Editor:

```powerquery
let
    Source = Csv.Document(
        File.Contents("Dataset/sales_data.csv"),
        [Delimiter=",", Columns=16, Encoding=65001, QuoteStyle=QuoteStyle.Csv]
    ),
    PromotedHeaders = Table.PromoteHeaders(Source, [PromoteAllScalars=true]),
    ChangedTypes = Table.TransformColumnTypes(PromotedHeaders,{
        {"Order ID", type text},{"Order Date", type date},{"Customer ID", type text},
        {"Customer Name", type text},{"Segment", type text},{"Product ID", type text},
        {"Product Name", type text},{"Category", type text},{"Sub-Category", type text},
        {"Region", type text},{"Country", type text},{"City", type text},
        {"Quantity", Int64.Type},{"Discount", Percentage.Type},
        {"Sales", Currency.Type},{"Profit", Currency.Type}}),
    Trimmed = Table.TransformColumns(ChangedTypes,{
        {"Order ID", Text.Trim, type text},{"Customer ID", Text.Trim, type text},
        {"Customer Name", Text.Trim, type text},{"Segment", Text.Trim, type text},
        {"Product ID", Text.Trim, type text},{"Product Name", Text.Trim, type text},
        {"Category", Text.Trim, type text},{"Sub-Category", Text.Trim, type text},
        {"Region", Text.Trim, type text},{"Country", Text.Trim, type text},
        {"City", Text.Trim, type text}}),
    NonBlank = Table.SelectRows(Trimmed, each [Order ID] <> null and [Order ID] <> ""),
    Deduplicated = Table.Distinct(NonBlank, {"Order ID"}),
    ValidSales = Table.SelectRows(Deduplicated, each [Sales] >= 0)
in
    ValidSales
```
