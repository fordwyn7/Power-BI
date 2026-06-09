# POWER BI HOMEWORK ASSIGNMENT
## Visual Calculations, Mapping Tables & New Visuals

---

## Objective

Build a Power BI report demonstrating **Visual Level Calculations** (running sum, moving average, percent of parent), a **Fuzzy Matching Mapping Table** in Power Query, and a **Gauge visual** with configured min, max, and target values.

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

## 2. Report Pages

Create **2 report pages**:

- **Page 1** — Visual Calculations Dashboard
- **Page 2** — Mapping Table & Gauge

---

## 3. Visual Level Calculations

Use the **New visual calculation** feature (Insert → New visual calculation) on a Matrix visual.

### Matrix Setup

- Rows: Year → Quarter → Month (calendar hierarchy)
- Values: `Sales Actuals Total` (SUM of SalesAmount)

### Required Visual Calculations

Add the following as visual-level calculations on the matrix:

**1. Rolling Average**
```
Rolling Average = FORMAT(MOVINGAVERAGE([Sales Actuals Total], 2), "#,##0.00")
```

**2. Running Sum**
```
Running Sum = RUNNINGSUM([Sales Actuals Total])
```

**3. Percent of Parent**
```
Percent of Parent = DIVIDE([Sales Actuals Total], COLLAPSE([Sales Actuals Total], ROWS))
```

### Requirements

- All 3 calculations must appear as separate columns in the matrix
- Matrix must show Year/Quarter/Month hierarchy with expand/collapse working
- Format `Rolling Average` as `#,##0.00`
- Format `Percent of Parent` as a decimal (e.g., 0.43)
- Row totals must be enabled

### Line Chart

Add a line chart on the same page showing:
- X-axis: Calendar Year + Month
- Y-axis: `Sales Actuals Total`
- Add `Running Sum` as a second Y-axis value (secondary axis)

---

## 4. Mapping Table (Fuzzy Matching)

Use **Power Query** to create a mapping table that matches territory names using fuzzy logic.

### Setup

1. Create a simple reference table manually in Power Query named `RegionMap` with two columns:
   - `InputRegion` — containing some slightly inconsistent region name variations (e.g., "Unted States", "Untied Kingdom", "Franc", "Australa")
   - `CorrectRegion` — the correct names (e.g., "United States", "United Kingdom", "France", "Australia")

2. Load the `DimSalesTerritory` table which contains the `SalesTerritoryCountry` column

3. Use **Merge Queries → Fuzzy match** to join `DimSalesTerritory[SalesTerritoryCountry]` with `RegionMap[InputRegion]`
   - Join Kind: Left Anti or Left Outer
   - Enable: `IgnoreCase = true`, `IgnoreSpace = true`, `Threshold = 0.55`

4. Add a new column `MappedRegion` that shows the matched `CorrectRegion` value

### Requirements

- The merge must use `Table.FuzzyNestedJoin` (applied via the Merge Queries UI)
- Show the resulting table in the report as a plain **Table visual** on Page 2
- Table must display: `SalesTerritoryCountry`, `MappedRegion`

---

## 5. Gauge Visual

Add a **Gauge visual** on Page 2 showing average product review score or sales performance.

### Configuration

| Field | Value |
|---|---|
| Value | Average of `SalesAmount` (or `OrderQuantity`) |
| Minimum | 0 |
| Maximum | MAX of `SalesAmount` |
| Target | A fixed DAX measure representing a sales target |

### DAX Measures Required

```
Average Sales = AVERAGE(FactInternetSales[SalesAmount])
Max Sales = MAX(FactInternetSales[SalesAmount])
Sales Target = [Average Sales] * 1.1
```

### Requirements

- Gauge must show the **callout value** (center number)
- **Target label** must be enabled
- **Data labels** must be enabled
- Title: `"Average Sales vs Target"`

---

## 6. Formatting Requirements

- Matrix column headers clearly labeled
- All sales values formatted with thousand separators
- Gauge colors: blue fill, gray background arc
- Line chart has axis titles and a legend
- Page titles on both pages

---

## Submission Requirements

Submit the following:

- [ ] Power BI `.pbix` file
- [ ] Matrix with all 3 visual calculations (Rolling Average, Running Sum, Percent of Parent)
- [ ] Line chart with Sales and Running Sum
- [ ] `RegionMap` table created in Power Query
- [ ] Fuzzy merge applied using `Table.FuzzyNestedJoin`
- [ ] Table visual showing mapped regions on Page 2
- [ ] Gauge visual with Value, Min, Max, and Target configured
- [ ] All 3 DAX measures for the gauge created
- [ ] Both pages properly titled and formatted

---

## Expected Outcome

The final report should demonstrate:

- Correct use of **Visual Level Calculations** (`MOVINGAVERAGE`, `RUNNINGSUM`, `DIVIDE`+`COLLAPSE`) directly inside a matrix
- Understanding of how visual calculations differ from regular DAX measures
- Ability to build a **fuzzy matching mapping table** in Power Query using `Table.FuzzyNestedJoin`
- Proper configuration of a **Gauge visual** with min, max, target, and callout value
- Clean formatting across both report pages