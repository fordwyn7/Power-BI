# POWER BI HOMEWORK ASSIGNMENT


## Objective

Build a professional regional sales report in Power BI Desktop featuring a fully functional **Day/Night mode toggle** using bookmarks and button states. Then **publish the report to Power BI Service** and demonstrate basic Service features including workspaces, dashboards, and sharing.

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

Create at least **2 report pages**:

- Regional Sales Dashboard
- Product Performance Page

- Each page must support both **Day Mode** and **Night Mode**
- Each page must have a **PowerPoint-designed background** applied for each mode
- Use the **Selection Pane** to organize and name all objects on every page

---

## 3. Day & Night Mode Implementation

Create a complete Day/Night theme switch using bookmarks and buttons.

### Mode Requirements

**Day Mode (Light Theme):**
- White or light gray background
- Dark-colored text and axis labels
- Light-colored visual backgrounds
- Soft border colors on cards and shapes

**Night Mode (Dark Theme):**
- Dark (black or deep navy) background
- White or light text and axis labels
- Dark-themed visual backgrounds
- Bright accent colors for contrast

### Bookmark Requirements

- Create **2 bookmarks** per page:
  - `DayMode` — captures the full light theme state
  - `NightMode` — captures the full dark theme state
- Place both in a **Bookmark Group** named `View Mode`
- Bookmarks must capture: background, visual colors, text formatting

### Toggle Button Requirements

- Add a **Day/Night toggle button** visible on every page
- Button must use **Button States**:
  - **Default** — shows current active mode label (e.g., "🌙 Night Mode")
  - **On Hover** — changes color or border to indicate it is clickable
  - **On Press** — brief visual feedback on click
- Clicking the button switches between Day and Night bookmark

---

## 4. KPI Cards

Create the following KPI cards using DAX measures:

| KPI | DAX Requirement |
|-----|-----------------|
| Total Sales Amount | `SUM` of sales |
| Total Profit | `SUM` of profit |
| Total Orders | `COUNTROWS` of sales fact |
| Average Sales (Last 30 Days) | `AVERAGEX` with date filter |
| Month-over-Month Sales Change (%) | `CALCULATE` + `DATEADD` |

- All KPI cards must adapt visually to Day and Night mode
- All measures must respond dynamically to slicers and filters

---

## 5. Required Visuals

Include the following visuals on the **Regional Sales Dashboard**:

- **KPI Cards** — Sales Amount, Profit, Orders (top of page)
- **Bar Chart** — Sum of Profit by Region
- **Clustered Bar Chart** — Sum of Profit and Sum of Marketing Spend by Region
- **Area/Line Chart** — Sum of Sales Amount and Sum of Target Sales by Date
- **Date Range Slicer** — allowing users to filter by date period
- **Dark/Light Mode Toggle Button** — top right area of the page

> All visuals must have titles, proper axis labels, and legend where applicable.

---

## 6. Selection Pane — Object Management

Use the Selection Pane on every report page.

### Requirements

- Rename **ALL** objects using clear, descriptive names
  - Examples: `KPI_TotalSales`, `Chart_ProfitByRegion`, `Button_ModeToggle`, `Shape_Header`
- Group related objects (e.g., all KPI cards in one group, all charts in another)
- Control **z-order** for any overlapping elements
- Day and Night background images must be stacked and toggled via the Selection Pane

---

## 7. Slicers & Filters

Add the following slicers:

- Date Range Slicer (between start and end date)
- Sales Territory / Region
- Product Category

### Requirements

- Add a **"Reset Filters"** button that restores default slicer state using a bookmark
- Slicers must work correctly in both Day and Night mode
- Slicer panel should be clearly separated from the main visual area

---

## 8. Power BI Service — Publishing & Setup

After completing the report in Power BI Desktop, publish it to Power BI Service.

### Step 1 — Publish the Report

- Sign in to Power BI Service at https://app.powerbi.com
- From Power BI Desktop, click **Home → Publish**
- Select your **personal workspace** or a shared workspace
- Confirm the report appears in Power BI Service

### Step 2 — Explore the Report in Service

- Open the published report in Power BI Service
- Verify that all visuals, bookmarks, and the Day/Night toggle work correctly in the browser
- Take a screenshot showing the report open in Power BI Service

### Step 3 — Create a Dashboard

- **Pin at least 2 visuals** from the report to a new dashboard
- Name the dashboard: `Regional Sales Dashboard`
- Arrange the pinned tiles neatly on the dashboard canvas

### Step 4 — Share the Report

- Use the **Share** button in Power BI Service
- Share the report with at least one email address (can be a classmate or test account)
- Take a screenshot of the Share dialog showing the email entered

---

## 9. Buttons & Navigation

Add clearly labeled buttons for:

- Day/Night mode toggle (on every page)
- Page navigation between report pages
- Reset filters

### Requirements

- All buttons must have **Default + Hover + Press** states configured
- Buttons must have assigned actions (bookmark or page navigation)
- Button labels must clearly describe their action

---

## 10. Text Boxes & Shapes

### Text Boxes

- Report title on each page
- Section headers for KPI area, chart area
- Mode label indicating current active theme (Day / Night)

### Shapes

- Background panels behind KPI card groups
- Section dividers
- Header bar shape at top of each page
- All shapes must be named in the Selection Pane

---

## Submission Requirements

Submit the following:

- [ ] Power BI `.pbix` file
- [ ] Working Day Mode and Night Mode with toggle button
- [ ] Button States configured on the toggle and navigation buttons
- [ ] All Selection Pane objects renamed and grouped
- [ ] All 5 KPI measures correctly calculated in DAX
- [ ] Date range slicer and filter slicers working
- [ ] Reset Filters button working via bookmark
- [ ] Report published to Power BI Service
- [ ] Dashboard created with at least 2 pinned visuals
- [ ] Screenshot of report open in Power BI Service
- [ ] Screenshot of Share dialog

---

## Expected Outcome

The final submission should demonstrate:

- A professional regional sales dashboard with **clean Day and Night themes**
- Smooth **one-click mode switching** using bookmarks and button states
- Correctly organized **Selection Pane** with named and grouped objects
- Accurate **DAX measures** responding to filters and slicers
- A successfully **published report on Power BI Service**
- A **dashboard** with pinned visuals in Power BI Service
- Understanding of how to **share reports** in the cloud
