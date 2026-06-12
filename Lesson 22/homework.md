# POWER BI HOMEWORK ASSIGNMENT
## Basic Static Segmentation

---

## Objective

Build a Power BI report that demonstrates **static segmentation** using a `DATATABLE` calculated table to define fixed price range buckets, then classify products and sales into those segments using DAX.

---

## 1. Data Source

Use the **AdventureWorksDW2019** SQL Server database.
Download the `.bak` file from the following link:
https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2019.bak

### Required Tables

- FactInternetSales
- DimProduct
- DimDate
- DimCustomer
- DimSalesTerritory

> All relationships must be properly configured before building visuals.

---

## 2. Step 1 — Create the Price Ranges Table

Create a new **calculated table** named `Price Ranges` using `DATATABLE`.

### DAX

```
Price Ranges =
DATATABLE(
    "PriceRangeKey", INTEGER,
    "Price Range",   STRING,
    "Min Price",     CURRENCY,
    "Max Price",     CURRENCY,
    {
        { 1, "VERY LOW",  0,    100       },
        { 2, "LOW",       100,  300       },
        { 3, "MEDIUM",    300,  600       },
        { 4, "HIGH",      600,  1500      },
        { 5, "VERY HIGH", 1500, 999999999 }
    }
)
```

### Requirements

- Table must appear in the Data panel as `Price Ranges`
- Display the table as a **Table visual** on Page 1 showing all 4 columns
- Verify all 5 rows are present with correct min/max values

---

## 3. Step 2 — Classify Products into Segments

Create a **calculated column** on `DimProduct` named `Price Segment` that assigns each product to a price range based on its `ListPrice`.

### DAX

```
Price Segment =
SWITCH(
    TRUE(),
    DimProduct[ListPrice] < 100,              "VERY LOW",
    DimProduct[ListPrice] < 300,              "LOW",
    DimProduct[ListPrice] < 600,              "MEDIUM",
    DimProduct[ListPrice] < 1500,             "HIGH",
    DimProduct[ListPrice] >= 1500,            "VERY HIGH"
)
```

---

## 4. Step 3 — DAX Measures

Create the following measures in a dedicated **Metrics** table:

| Measure | DAX |
|---|---|
| Total Sales | `SUM(FactInternetSales[SalesAmount])` |
| Total Orders | `COUNTROWS(FactInternetSales)` |
| Avg Unit Price | `AVERAGE(DimProduct[ListPrice])` |
| Sales by Segment | `CALCULATE([Total Sales], ALLEXCEPT(DimProduct, DimProduct[Price Segment]))` |

---

## 5. Report Pages

Create **2 report pages**:

- **Page 1** — Price Ranges reference table + segment distribution
- **Page 2** — Sales analysis by segment

---

## 6. Required Visuals

### Page 1

**Table visual** — Price Ranges lookup table
- Columns: `PriceRangeKey`, `Price Range`, `Min Price`, `Max Price`
- All 5 rows visible

**Bar Chart** — Product count by Price Segment
- X-axis: `Price Segment`
- Y-axis: Count of `DimProduct[ProductKey]`
- Sort by segment order (VERY LOW → VERY HIGH)
- Data labels enabled

### Page 2

**Stacked Bar Chart** — Total Sales by Price Segment and Year
- X-axis: Year
- Legend: `Price Segment`
- Y-axis: `Total Sales`

**Matrix** — Sales breakdown by Price Segment
- Rows: `Price Segment`
- Values: `Total Sales`, `Total Orders`, `Avg Unit Price`
- Grand totals enabled
- Conditional formatting on `Total Sales` column (data bars or color scale)

**Slicer** — Year slicer filtering both visuals

---

## 7. Formatting Requirements

- Sort `Price Segment` in logical order: VERY LOW → LOW → MEDIUM → HIGH → VERY HIGH
- Format all currency values with thousand separators and 2 decimal places
- Bar chart bars colored distinctly per segment
- Page titles on both pages
- Matrix rows bold for totals

---

## Submission Requirements

Submit the following:

- [ ] Power BI `.pbix` file
- [ ] `Price Ranges` calculated table created using `DATATABLE`
- [ ] Table visual on Page 1 showing all 5 price range rows
- [ ] `Price Segment` calculated column added to `DimProduct`
- [ ] All 4 DAX measures created in a Metrics table
- [ ] Bar chart showing product count per segment on Page 1
- [ ] Stacked bar chart by segment and year on Page 2
- [ ] Matrix with conditional formatting on Page 2
- [ ] Year slicer working on Page 2

---

## Expected Outcome

The final report should demonstrate:

- Correct use of **`DATATABLE`** to define a static segmentation lookup table
- Proper **`SWITCH(TRUE())`** pattern for classifying rows into segments
- A clean segment distribution visual showing how products spread across price buckets
- Sales analysis broken down by segment with **conditional formatting** highlighting top performers
- Understanding of when static segmentation is appropriate vs dynamic approaches