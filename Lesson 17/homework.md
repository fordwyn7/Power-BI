# POWER BI HOMEWORK ASSIGNMENT

## Power BI Service — Refresh Options

## Objective

Demonstrate understanding of Power BI Service refresh options by configuring refresh settings for a published report and documenting the process.

---

## 1. Data Source

Use the **AdventureWorksDW2019** SQL Server database.
Download the `.bak` file from the following link:
https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2019.bak

> You may reuse the `.pbix` file from a previous lesson. No need to build a new report from scratch.

---

## 2. Tasks

### Task 1 — Publish the Report

- Open your existing `.pbix` file in Power BI Desktop
- Publish it to your **Power BI Service workspace**
- Confirm the report and its dataset appear in the workspace

### Task 2 — Manual Refresh

- In Power BI Service, navigate to your **dataset**
- Perform a **manual refresh** using the refresh button
- Take a screenshot showing the refresh completed (last refresh timestamp visible)

### Task 3 — Configure Scheduled Refresh

- Open the dataset **Settings** in Power BI Service
- Navigate to the **Scheduled refresh** section
- Configure a refresh schedule:
  - Frequency: **Daily**
  - At least **1 time slot** selected
- Take a screenshot of the configured schedule before saving

### Task 4 — Gateway (if applicable)

- Check whether your dataset requires a **Data Gateway** to refresh
- If prompted, note what type of gateway is needed:
  - Personal Gateway
  - On-premises Data Gateway
- Write 2–3 sentences explaining why a gateway is needed for SQL Server data sources

---

## 3. Short Answer Questions

Answer the following questions in a few sentences each:

1. What is the difference between **manual refresh** and **scheduled refresh** in Power BI Service?
2. Why can't Power BI Service connect directly to an on-premises SQL Server database without a gateway?
3. What happens to visuals in a published report if the dataset is not refreshed regularly?

---

## Submission Requirements

Submit the following:

- [ ] Power BI `.pbix` file (existing report, republished)
- [ ] Screenshot of successful manual refresh (timestamp visible)
- [ ] Screenshot of configured scheduled refresh settings
- [ ] Short answer questions answered (in a `.txt` or `.md` file, or written in the submission notes)
- [ ] 2–3 sentence gateway explanation

---

## Expected Outcome

The submission should demonstrate:

- Ability to **publish and locate** a dataset in Power BI Service
- Ability to **trigger a manual refresh** and confirm it succeeded
- Ability to **configure a scheduled refresh** with correct settings
- Basic understanding of **why gateways are required** for on-premises data sources
