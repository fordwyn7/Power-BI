# POWER BI HOMEWORK ASSIGNMENT
## Report Replication

---

## Objective

Replicate the structure and logic of a given reference report using the **AdventureWorksDW2019** database. You will not copy the report — you will rebuild it from scratch using equivalent data, matching the layout, visual types, slicers, drill-through, and formatting of the reference.

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

## 2. Reference Report Description

The reference report displays **hospital patient data** broken down by year, age group, and patient type. Your task is to replicate its structure using **sales data** from AdventureWorksDW2019 with the following mappings:

| Reference Report | Your Report Equivalent |
|---|---|
| Total Patients | Total Orders (count of sales transactions) |
| Adult / Child | Customer Age Group (Young / Middle-aged / Senior) |
| Case_Type | Product Category |
| Year (2018–2021) | Year (use available years in the dataset) |

---

## 3. Report Pages

Create **2 report pages** matching the reference:

- **Page 1** — Overview (main stacked bar chart + slicers)
- **Page 2** — Drill-Through Detail Page

---

## 4. Required Visuals

### Page 1 — Overview

Replicate the following from the reference report:

**Stacked Bar Chart**
- X-axis: Year
- Y-axis: Total Orders
- Legend: Customer Age Group (Young / Middle-aged / Senior)
- Data labels visible on each segment showing values in millions (e.g., 6.0M)
- Color each age group with a distinct color (match the style: dark for one group, accent for another)

**Slicer 1 — Group Type** *(replicates "Adult Or Case" slicer)*
- Field: Customer Age Group
- Style: Radio button / list slicer
- Options: Young, Middle-aged, Senior

**Slicer 2 — Category** *(replicates "Adult_Child" slicer)*
- Field: Product Category
- Style: Checkbox list slicer

### Page 2 — Drill-Through Detail

- Configure **drill-through** from the stacked bar chart using **Year** as the drill-through field
- The detail page must contain:
  - A table showing transaction-level data (Order Date, Product, Customer, Sales Amount)
  - A KPI card for Total Orders on the drilled-through year
  - A **Back button** using the built-in back navigation action
  - **Cross-report** drill-through enabled (toggle On)
  - **Keep all filters** enabled (toggle On)

---

## 5. DAX Measures

Create the following measures to power the visuals:

| Measure | DAX Logic |
|---|---|
| Total Orders | `COUNTROWS(FactInternetSales)` |
| Total Sales Amount | `SUM(FactInternetSales[SalesAmount])` |
| Customer Age Group | Calculated column using `IF` on customer birth year to classify Young / Middle-aged / Senior |

> Format large numbers using Power BI's display units (Millions) to match the reference report's 6.0M / 1.1M style.

---

## 6. Formatting Requirements

Match the reference report's visual style as closely as possible:

- Chart title: **"Total Orders by Year and Age Group"**
- Y-axis label: **"Total Orders"**
- X-axis label: **"Year"**
- Data labels: enabled, showing abbreviated values (M for millions)
- Legend: visible, positioned at top or right
- Visual background: transparent or light neutral
- Slicer headers: visible and clearly labeled

---

## 7. Drill-Through Configuration

In the drill-through setup (visible in the reference), ensure:

- **Field:** Year
- **Cross-report:** On
- **Keep all filters:** On
- Drill-through is accessible by right-clicking a bar in the stacked chart

---

## Submission Requirements

Submit the following:

- [ ] Power BI `.pbix` file
- [ ] Page 1 with stacked bar chart and both slicers working
- [ ] Correct Age Group classification (Young / Middle-aged / Senior)
- [ ] Data labels showing values in millions
- [ ] Drill-through configured on Year field
- [ ] Page 2 with transaction table, KPI card, and Back button
- [ ] Cross-report and Keep all filters toggles enabled
- [ ] All DAX measures correctly calculated

---

## Expected Outcome

The final report should demonstrate:

- Ability to **read and replicate** a report structure from a reference
- Correct **data mapping** from a different domain (patients → customers/orders)
- Proper **stacked bar chart** configuration with legends and data labels
- Working **drill-through** between pages with correct field setup
- Clean **slicer configuration** matching the reference style
- Professional formatting consistent with the reference layout