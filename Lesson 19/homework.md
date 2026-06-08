# POWER BI HOMEWORK ASSIGNMENT
## Currency Conversion Case

---

## Objective

Build a Power BI report that dynamically converts sales figures into multiple currencies using a proper currency conversion data model, DAX measures with `ADDCOLUMNS`, `GENERATE`, and `SELECTEDVALUE`, and an interactive currency slicer.

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
- DimCurrency
- FactCurrencyRate

> All relationships must be properly configured before building visuals.

---

## 2. Data Model

Set up the following relationships in the Model view:

| From Table | From Column | To Table | To Column |
|---|---|---|---|
| FactInternetSales | OrderDateKey | DimDate | DateKey |
| FactInternetSales | CustomerKey | DimCustomer | CustomerKey |
| FactInternetSales | ProductKey | DimProduct | ProductKey |
| FactCurrencyRate | CurrencyKey | DimCurrency | CurrencyKey |
| FactCurrencyRate | TimeKey | DimDate | DateKey |

> Your model should resemble the reference: a central Sales/Facts table connected to Date, Product, Customer, Currency, and Exchange Rate tables.

---

## 3. Daily Exchange Rates Table (Calculated)

Create a **calculated table** named `Daily Exchange Rates` using `ADDCOLUMNS` and `GENERATE` to build a daily rate table with a corrected rate that adjusts for where in the month each date falls.

The table must include the following columns:
- `Date`
- `CurrencyKey`
- `Rate` (corrected daily rate)

### DAX Logic

```
Daily Exchange Rates =
VAR xRatesExtended =
    ADDCOLUMNS (
        GENERATE (
            'FactCurrencyRate',
            DATESBETWEEN ( 'DimDate'[FullDateAlternateKey], [TimeKey], EOMONTH ( [TimeKey], 0 ) )
        ),
        "CorrectedRate", IF (
            RELATED ( 'DimCurrency'[CurrencyName] ) = "US Dollar",
            'FactCurrencyRate'[AverageRate],
            VAR DaysInMonth =
                DAY ( EOMONTH ( 'DimDate'[FullDateAlternateKey], 0 ) )
            VAR CurrentDay =
                DAY ( 'DimDate'[FullDateAlternateKey] )
            VAR Factor = ( CurrentDay - 1 ) / DaysInMonth * 0.01
            VAR CorrectedRate = 'FactCurrencyRate'[AverageRate] * ( 1 - Factor )
            RETURN
                CorrectedRate
        )
    )
VAR Result =
    SELECTCOLUMNS (
        xRatesExtended,
        "Date", 'DimDate'[FullDateAlternateKey],
        "CurrencyKey", [CurrencyKey],
        "Rate", [CorrectedRate]
    )
RETURN
    Result
```

---

## 4. DAX Measures

Create the following measures in a dedicated **Measure Table**:

### Sales (Daily)
Calculates total sales converted to USD using the daily exchange rate joined by date and selected currency.

```
Sales (Daily) =
VAR TotalSalesInUSD =
    ADDCOLUMNS (
        SUMMARIZE ( Sales, 'Date'[Calendar Year Month Number] ),
        "Rate", CALCULATE ( SELECTEDVALUE ( 'Monthly Exchange Rates'[Rate] ) ),
        "USDSalesAmount", Sales[Sales (Internal)]
    )
VAR result = SUMX ( TotalSalesInUSD, [USDSalesAmount] * [Rate] )
RETURN result
```

> Adapt the column and table references to match AdventureWorksDW2019 field names. The logic and structure must remain the same.

### Additional Required Measures

| Measure | Description |
|---|---|
| Total Sales (Base) | `SUM` of `FactInternetSales[SalesAmount]` in original currency |
| Converted Sales | Sales amount multiplied by the selected currency's exchange rate |
| Selected Currency Label | `SELECTEDVALUE` of `DimCurrency[CurrencyName]` for display |

---

## 5. Report Pages

Create **1 report page**:

- **Currency Conversion Dashboard**

---

## 6. Required Visuals

### Matrix Table *(replicates the reference)*
- **Rows:** Source Currency (DimCurrency[CurrencyName])
- **Columns:** Target Currency (selected via slicer — e.g., US Dollar, EURO, Swiss Franc, Japanese Yen)
- **Values:** Converted Sales amount
- **Totals:** Row and column totals enabled
- Format values with thousand separators and 2 decimal places

### Currency Slicer
- Field: `DimCurrency[CurrencyName]`
- Style: Checkbox list
- Allow multi-select so users can choose which target currencies appear as columns

### KPI Cards
- Total Sales (base currency)
- Converted Sales (based on slicer selection)
- Selected Currency Label

---

## 7. Formatting Requirements

- Matrix column headers must show currency names clearly
- All sales values formatted with thousand separators
- Slicer header labeled **"Currency"**
- Report title: **"Sales by Currency Conversion"**
- Bold totals row and column in the matrix

---

## Submission Requirements

Submit the following:

- [ ] Power BI `.pbix` file
- [ ] Correct data model with all relationships configured
- [ ] `Daily Exchange Rates` calculated table created
- [ ] `Sales (Daily)` measure and all required measures working
- [ ] Matrix showing sales converted across multiple currencies
- [ ] Currency slicer filtering the matrix columns correctly
- [ ] KPI cards displaying correctly
- [ ] Values formatted with thousand separators and 2 decimal places

---

## Expected Outcome

The final report should demonstrate:

- A properly structured **currency conversion data model** with exchange rate tables
- A **calculated table** built using `ADDCOLUMNS` and `GENERATE` with corrected daily rates
- Dynamic **DAX measures** using `SELECTEDVALUE` to respond to the currency slicer
- A **matrix visual** displaying sales converted into multiple target currencies simultaneously
- Clean formatting consistent with a professional financial dashboard