
# Prism-Insurance-Analytics-Dashboard

## Problem Statement

This dashboard helps **Prism Insurance Pvt. Ltd.** understand their business performance better. It gives the insurance team a clear view of how their policies are distributed, how claims are being processed, and where operational gaps exist. Through key metrics and visual breakdowns, the team can identify which policy types generate the most premium, which age groups file the highest claims, and how active vs. inactive policies are trending.

Since the majority of claims fall under the **Rejected** category (4.4K) compared to Settled (3.4K) and Pending (2.3K), there is a clear need to investigate rejection reasons and improve the claims processing pipeline. Additionally, **Young Adults** record significantly lower claim amounts (1.7M) compared to Adults (8.8M) and Elders (6.4M), suggesting different risk profiles that can be used to refine underwriting strategies.

With **93.86% active policies** out of 10,000+ policyholders and a total coverage of **600.55M**, this dashboard equips decision-makers with the insights needed to optimize premium collection, reduce claim rejections, and improve overall portfolio health.

---

## Steps Followed

- **Step 1 :** Load data into Power BI Desktop; the dataset is a CSV file containing policyholder, premium, coverage, and claims data for Prism Insurance Pvt. Ltd.

- **Step 2 :** Open the Power Query Editor. Under the **View** tab, in the **Data Preview** section, enable **"Column Distribution"**, **"Column Quality"**, and **"Column Profile"** options to thoroughly inspect the dataset.

- **Step 3 :** Change column profiling from the default 1,000 rows to **"Column profiling based on entire dataset"** to ensure data quality checks are accurate across all records.

- **Step 4 :** Inspect all columns for errors, nulls, and empty values. Data was found to be largely clean; any null values in monetary columns (Premium Amount, Coverage Amount, Claim Amount) were excluded from aggregate calculations.

- **Step 5 :** In the **Report View**, under the View tab, a **dark theme** was applied to the canvas. A custom dark background with teal and orange accent colors was chosen to reflect a professional, corporate insurance brand identity.

- **Step 6 :** The company name **"PRISM INSURANCE PVT. LTD."** was added to the report canvas using a styled text box with a bold italic orange font, positioned prominently in the top-left corner as a brand header.

- **Step 7 :** Three **Slicer visuals** (dropdown style) were added to the top of the canvas for the following fields:
  - Policy Number
  - Claim Number
  - Customer ID

  These slicers allow stakeholders to drill into individual policy or claim records instantly.

- **Step 8 :** Three **KPI Card visuals** were added to the canvas representing the three core business metrics:

  (a) **Premium Amount** --> 5.98M

  (b) **Coverage Amount** --> 600.55M

  (c) **Claim Amount** --> 16.91M

  Cards were styled with a rounded rectangular border and teal accent color to make them visually prominent.

- **Step 9 :** Two **single-value card visuals** were added to display total customer count segmented by gender:

  - **Female** --> 5,001
  - **Male** --> 5,003

  These cards were styled with golden/amber text labels against a dark card background for clear differentiation.

- **Step 10 :** A **horizontal bar chart** was added to represent **Premium Amount by Policy Type**, covering the following five policy categories:

  (a) Travel - **2.5M**

  (b) Health - **1.2M**

  (c) Auto - **1.0M**

  (d) Life - **0.7M**

  (e) Home - **0.6M**

  Teal-colored bars were used consistent with the dashboard's color theme.

- **Step 11 :** A **Donut Chart** was added to represent the **Count of Active vs. Inactive Policies**:

  - Active --> **9.39K (93.86%)**
  - Inactive --> **0.61K (6.14%)**

  Active policies were represented in teal and inactive in blue-grey, with percentage labels displayed directly on the chart.

- **Step 12 :** A **Waterfall / Stream Area Chart** was added to display the **Number of Claims by Claim Status**:

  - Rejected --> **4.4K**
  - Settled --> **3.4K**
  - Pending --> **2.3K**

  This visual helps the claims team quickly identify the volume of unresolved and rejected cases.

- **Step 13 :** A **Line Chart** was added to represent **Claim Amount by Age Group**, showing a declining trend:

  - Adult --> **8.8M**
  - Elder --> **6.4M**
  - Young Adult --> **1.7M**

  Data points were highlighted with circular markers for clarity.

- **Step 14 :** A **Matrix Table** was added to provide granular claim breakdowns by Policy Type across three claim statuses (Pending, Rejected, Settled):

  | Policy Type | Pending | Rejected | Settled |
  |---|---|---|---|
  | Auto | 2,08,10,615.30 | 4,06,71,711.59 | 3,29,84,558 |
  | Health | 2,76,82,791.20 | 5,24,01,928.42 | 4,00,17,100 |
  | Home | 1,30,01,816.73 | 2,74,06,202.63 | 2,06,45,568 |
  | Life | 1,72,59,587.93 | 3,37,22,751.49 | 2,31,21,204 |
  | Travel | 5,72,47,694.90 | 10,73,95,611.51 | 8,61,82,353 |
  | **Total** | **13,60,02,506.05** | **26,15,98,205.64** | **20,29,50,786** |

- **Step 15 :** A new **calculated column** was created to group customers into age segments for the Claim Amount by Age Group visual:

  ```DAX
  Age Group =
  IF(insurance_data[Age] <= 30, "Young Adult",
  IF(insurance_data[Age] <= 60, "Adult",
  "Elder"))
  ```

- **Step 16 :** New **DAX measures** were created for the three core KPI cards:

  ```DAX
  Total Premium Amount = SUM(insurance_data[PremiumAmount])

  Total Coverage Amount = SUM(insurance_data[CoverageAmount])

  Total Claim Amount = SUM(insurance_data[ClaimAmount])
  ```

- **Step 17 :** A measure was created to calculate the **Count of Active and Inactive Policies**:

  ```DAX
  Active Policies = COUNTROWS(FILTER(insurance_data, insurance_data[PolicyStatus] = "Active"))

  Inactive Policies = COUNTROWS(FILTER(insurance_data, insurance_data[PolicyStatus] = "Inactive"))
  ```

- **Step 18 :** The report was then published to **Power BI Service** for sharing and stakeholder access.

---

## Snapshot of Dashboard (Power BI Desktop)

![image arg](https://github.com/user-attachments/assets/d312f33b-acb8-45c2-9ffe-0a2dbc005423)

---

## Insights

A single page report was created on Power BI Desktop and published to Power BI Service.

The following inferences can be drawn from the dashboard:

---

### [1] Total Policyholders = 10,004

- Female Policyholders --> **5,001**
- Male Policyholders --> **5,003**

  → Gender distribution is nearly equal, with a negligible difference of 2 policyholders.

---

### [2] Core KPIs

- **Total Premium Amount** --> 5.98M
- **Total Coverage Amount** --> 600.55M
- **Total Claim Amount** --> 16.91M

  → The coverage-to-claim ratio indicates a healthy portfolio with claims representing only ~2.8% of total coverage.

---

### [3] Premium Amount by Policy Type

- Travel --> **2.5M** (highest)
- Health --> **1.2M**
- Auto --> **1.0M**
- Life --> **0.7M**
- Home --> **0.6M** (lowest)

  → Travel policies contribute the highest premium revenue, nearly double that of the next category (Health), making it the most commercially significant product line.

---

### [4] Active vs. Inactive Policies

- Active --> **9.39K (93.86%)**
- Inactive --> **0.61K (6.14%)**

  → An overwhelming majority of policies are active, indicating strong customer retention. However, the 6.14% inactive segment should be analyzed to understand lapse reasons and reduce churn.

---

### [5] Number of Claims by Claim Status

- Rejected --> **4.4K** (highest)
- Settled --> **3.4K**
- Pending --> **2.3K** (lowest)

  → The high rejection count is a red flag. More claims are being rejected than settled, which could signal issues in the claims documentation process, eligibility criteria, or customer awareness. This requires immediate operational attention.

---

### [6] Claim Amount by Age Group

- Adult --> **8.8M** (highest)
- Elder --> **6.4M**
- Young Adult --> **1.7M** (lowest)

  → Adults (mid-age group) file the highest claim amounts, followed by Elders. Young Adults represent the lowest risk segment by claim volume, which can be leveraged in premium pricing strategies.

---

### [7] Claim Breakdown by Policy Type

- **Travel** records the highest total rejected claims  **10,73,95,611.51**
- **Home** records the lowest total pending claims  **1,30,01,816.73**
- Across all policy types, **Rejected claims consistently exceed Settled claims**, pointing to a systemic issue in the claims approval pipeline.

  → Travel and Health policy claims need the most attention from the claims management team given their high rejection values.

---

## Tools & Technologies Used

| Tool | Purpose |
|---|---|
| Power BI Desktop | Dashboard development & DAX measures |
| Power Query Editor | Data cleaning & transformation |
| DAX | KPI measures, calculated columns, filtering |
| Power BI Service | Publishing & stakeholder sharing |
| CSV Dataset | Source data — Prism Insurance Pvt. Ltd. |


