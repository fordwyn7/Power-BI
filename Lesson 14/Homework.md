# POWER BI HOMEWORK ASSIGNMENT
## Selection Pane & Bookmark Mastery

---

## Objective

Create an advanced interactive Power BI report that deeply demonstrates the use of the Selection Pane, Bookmark Groups, Spotlight & Focus Mode, Button States, and dynamic visual management.

---

## 1. Data Source

You will use the **AdventureWorksDW2019** SQL Server database.
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

Create at least **3 report pages**:

- Main Dashboard
- Regional Sales Deep Dive
- Custom Tooltip Page *(hidden)*

- Each page must have a PowerPoint-designed background applied.
- Each page must use the Selection Pane to organize and name all objects.

---

## 3. Selection Pane — Object Management

Use the Selection Pane on every report page.

### Requirements

- Rename **ALL** objects in the Selection Pane using clear, descriptive names
  - Examples: `KPI_TotalSales`, `Chart_Monthly`, `Shape_Header`, `Button_DayMode`
- Group related objects together using Selection Pane groups
- Use the Selection Pane to control **layer order (z-order)** of overlapping visuals and shapes
- At least **2 visuals** must be intentionally stacked/overlapping and managed via the Selection Pane

---

## 4. Bookmark Groups

Organize all bookmarks into named Bookmark Groups.

### Required Bookmark Groups

**Group 1 — View Mode**
- Default View
- Day Mode
- Night Mode

**Group 2 — Visual State**
- Show Chart View
- Show Table View
- Show KPI-Only View

**Group 3 — Filter States**
- No Filter Applied
- Filtered by Region
- Filtered by Product Category

### Requirements

- Each group must contain at least 2 bookmarks
- Bookmarks within each group must be navigable using assigned buttons
- Use **"Selected Visuals"** option when capturing bookmarks to avoid unintended state changes

---

## 5. Dynamic Visual Switching

Create a section where the same data is displayed in 3 different visual formats, and the user can switch between them using bookmarks.

### Visuals to Switch Between

- Bar Chart
- Line Chart
- Data Table

### Requirements

- All 3 visuals must occupy the **exact same position** on the canvas
- Use Selection Pane to show/hide each visual per bookmark
- Only one visual is visible at a time
- Switching buttons must use bookmark actions from **Bookmark Group 2**

---

## 6. Day Mode & Night Mode

Implement a full Day/Night mode switch using bookmarks.

### Requirements

**Day Mode:**
- Light background
- Dark text
- Light-colored visuals

**Night Mode:**
- Dark background
- Light/white text
- Dark-themed visuals

- Use bookmarks to capture each mode's full canvas state
- Both modes must be placed in **Bookmark Group 1** (View Mode)
- Add a toggle button that switches between Day and Night Mode
- Button must use Button States to show different icons/labels per mode

---

## 7. Button States

Apply Button States to interactive buttons.

### Required Button States

For each navigation or bookmark button, configure:
- **Default** — normal appearance
- **On Hover** — highlight on mouseover
- **On Press** — visual feedback on click

### Minimum Requirements

- At least **3 buttons** must have all 3 states configured
- States must visually differ (e.g., color change, border, font weight)
- Day/Night toggle button must reflect the current active mode in its Default state

---

## 8. Spotlight & Focus Mode

Use Spotlight and Focus Mode features in the report design.

### Spotlight

- Configure at least 1 visual that clearly benefits from Spotlight usage
- Include a written instruction label near that visual telling users they can right-click to use Spotlight

### Focus Mode

- Add a text box or label near at least 1 complex visual (e.g., a matrix or detailed table) indicating Focus Mode is available for expanded viewing

---

## 9. KPI Section with DAX Measures

Create KPI cards using DAX measures.

### Required KPIs

| KPI | Description |
|-----|-------------|
| Total Sales Amount | Sum of all sales |
| Total Quantity Sold | Sum of quantities |
| Total Orders | Count of orders |
| Average Sales Per Customer | Using AVERAGEX |
| Month-over-Month Sales Change (%) | Using CALCULATE + DATEADD |

### DAX Requirements

- **Average Sales Per Customer** must use `AVERAGEX` over the `DimCustomer` table
- **Month-over-Month %** must use `CALCULATE` with `DATEADD`
- All measures must respond to slicer and filter selections

---

## 10. Slicers & Filter Interaction

Add slicers for:
- Year
- Product Category
- Sales Territory Country

### Requirements

- Add a **"Reset Filters"** button that clears all slicers using a bookmark from Bookmark Group 3
- Slicer panel must be **toggleable** (show/hide) using Selection Pane + bookmarks
- When hidden, a **"Show Filters"** button must be visible

---

## 11. Drill Down & Drill Through

### Drill Down

- Implement in at least 1 visual using **Year → Quarter → Month** hierarchy

### Drill Through

- Create a drill through page for Product-level detail
- Page must contain:
  - Transaction-level table
  - Product KPIs
  - A **"Back"** button using the built-in back action

---

## 12. Custom Tooltip Page

Create a hidden tooltip page.

### Requirements

- Page type must be set to **"Tooltip"**
- Must contain:
  - At least 2 mini KPI cards
  - 1 small supporting visual
- Assign the tooltip page to at least 1 visual on the Main Dashboard

---

## 13. Navigation & Buttons

Add clearly labeled buttons for:

- Page navigation (between all pages)
- Bookmark group navigation
- Day/Night mode toggle
- Reset filters
- Show/hide slicer panel
- Visual format switcher (Chart / Table / KPI view)

> All buttons must have assigned actions. All buttons must have at least Default + Hover states configured.

---

## 14. Text Boxes & Shapes

### Text Boxes

- Report title on each page
- Section headers for each content area
- Usage instruction labels near Spotlight and Focus Mode visuals

### Shapes

- KPI card containers
- Section dividers
- Background panels for visual groups
- All shapes must be named in the Selection Pane

---

## Submission Requirements

Submit the following:

- [ ] Power BI `.pbix` file
- [ ] All Selection Pane objects renamed
- [ ] Bookmark Groups properly organized
- [ ] Working Day/Night mode toggle
- [ ] Visual switching (Chart / Table / KPI)
- [ ] Button States configured on 3+ buttons
- [ ] Spotlight & Focus Mode labels added
- [ ] Working drill down and drill through
- [ ] Custom tooltip page assigned
- [ ] Reset filters and slicer toggle working
- [ ] All DAX measures correctly calculated

---

## Expected Outcome

The final report should demonstrate:

- Full mastery of the **Selection Pane** for object naming, grouping, and layer control
- Organized **Bookmark Groups** with clear logical separation
- Smooth **visual switching** using stacked visuals + bookmarks
- Professional **Day/Night mode** implementation
- Polished **button states** for a production-quality UX
- Correct use of **Spotlight** and **Focus Mode** awareness
- Dynamic **DAX measures** responding to filters
- Clean, professional dashboard design across all pages