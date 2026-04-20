# 🏥 Multi-Hospital Patient Performance Analysis
### Excel Analytics Project | Healthcare Business Intelligence Dashboard

> **Designed by:** Sami Ullah  
> **Domain:** Healthcare Analytics  
> **Tool:** Microsoft Excel (Multi-Tab Workbook)  
> **Dataset Size:** 55,500 Patient Records | 2019–2024  
> **Total Treatment Revenue Analyzed:** $1.42 Billion

---

## 📋 Table of Contents

1. [Project Overview](#project-overview)
2. [Business Problem](#business-problem)
3. [Dataset Description](#dataset-description)
4. [Workbook Structure](#workbook-structure)
5. [Data Cleaning & Preparation](#data-cleaning--preparation)
6. [Analytical Methods](#analytical-methods)
7. [Key Metrics & KPIs](#key-metrics--kpis)
8. [Dashboard Visualizations](#dashboard-visualizations)
9. [Key Findings & Insights](#key-findings--insights)
10. [Recommendations](#recommendations)
11. [Presentation Slide Outline](#presentation-slide-outline)
12. [Tools & Techniques Used](#tools--techniques-used)
13. [How to Use This File](#how-to-use-this-file)

---

## Project Overview

This project delivers a comprehensive healthcare analytics solution for a multi-hospital network across the United States. Using Microsoft Excel as the primary analytics and visualization platform, the analysis transforms 55,500 raw patient records into an executive-ready interactive dashboard — enabling data-driven decisions around patient care, hospital operations, cost management, and resource planning.

The final output is a single, multi-tab Excel workbook containing raw data, cleaned data, pivot-driven KPIs, and a fully interactive dashboard — designed for both operational managers and C-suite stakeholders.

---

## 📊 Dashboard Preview

![Healthcare Analytics Dashboard]("Healthcare Project.png")


> *Interactive dashboard built in Excel — filter all visuals dynamically using the Gender slicer.*

---

## Business Problem

The executive leadership of a large U.S. healthcare network commissioned this analysis to answer six core operational questions:

| # | Question | Business Impact |
|---|----------|----------------|
| 1 | How are patient volumes trending over time? | Capacity planning and growth strategy |
| 2 | What is driving treatment costs and length of stay? | Cost reduction and efficiency |
| 3 | Which hospitals perform best or worst? | Resource reallocation and benchmarking |
| 4 | What are the most common medications and test results? | Procurement and clinical protocols |
| 5 | How does insurance provider mix affect volumes? | Reimbursement and payer strategy |
| 6 | Are there seasonal patterns in admissions? | Staffing and scheduling optimization |

---

## Dataset Description

The raw dataset (`healthcare_dataset` sheet) contains **55,500 patient records** spanning 2019–2024 with the following fields:

| Column | Description | Type |
|--------|-------------|------|
| Name | Patient full name | Text |
| Age | Patient age in years | Numeric |
| Gender | Male / Female | Categorical |
| Blood Type | ABO/Rh blood group | Categorical |
| Medical Condition | Primary diagnosis | Categorical |
| Date of Admission | Admission date (Excel serial) | Date |
| Doctor | Attending physician name | Text |
| Hospital | Treating facility name | Text |
| Insurance Provider | Payer organization | Categorical |
| Billing Amount | Total treatment cost in USD | Currency |
| Room Number | Assigned room | Numeric |
| Admission Type | Elective / Emergency / Urgent | Categorical |
| Discharge Date | Discharge date (Excel serial) | Date |
| Medication | Primary medication administered | Categorical |
| Test Results | Abnormal / Normal / Inconclusive | Categorical |
| Age Group | Derived age band (10–20, 21–30 … 71+) | Categorical |
| Length of Stay | Derived: Discharge − Admission (days) | Numeric |
| Seasons | Derived: Season of admission | Categorical |

### Data Dimensions at a Glance

- **Time Range:** 2019–2024 (partial 2024)
- **Age Groups:** 8 bands (10–20 through 71 and Older)
- **Medical Conditions:** 6 (Arthritis, Diabetes, Hypertension, Obesity, Cancer, Asthma)
- **Insurance Providers:** 5 (Cigna, Medicare, UnitedHealthcare, Blue Cross, Aetna)
- **Medications:** 6 (Aspirin, Ibuprofen, Paracetamol, Penicillin, Lipitor, other)
- **Admission Types:** 3 (Elective, Emergency, Urgent)
- **Blood Types:** 8 (O−, O+, B−, B+, AB−, AB+, A+, A−)

---

## Workbook Structure

The Excel file is organized into **5 dedicated tabs**, each serving a distinct purpose in the analytics pipeline:

```
📁 Project.xlsx
│
├── 📄 healthcare_dataset    ← Raw source data (55,500 rows)
├── 📊 KPIs                  ← Pivot tables powering all dashboard metrics
├── 📋 Brief                 ← Project scope and executive summary
├── 💡 Insights              ← Written analytical commentary and findings
└── 📈 Report (Dashboard)    ← Interactive visual dashboard
```

### Tab Descriptions

**`healthcare_dataset`** — The foundation of the entire analysis. Contains the full, cleaned patient-level dataset with all original fields plus derived columns (Age Group, Length of Stay, Seasons) added during the data preparation phase.

**`KPIs`** — Houses all PivotTables that feed the dashboard. This tab is the calculation engine: any change to source data automatically refreshes all visuals through these pivots. Organized into logical sections: summary KPIs, trend analysis, demographic breakdowns, and provider/clinical metrics.

**`Brief`** — A concise one-page project brief outlining the business context, objectives, scope, and stakeholders. Serves as the project's "landing page" for non-technical reviewers.

**`Insights`** — Narrative analytical commentary translating chart data into plain-language findings. Written for a non-technical executive audience. Each insight links directly to a corresponding dashboard visual.

**`Report`** — The interactive dashboard. A fully visual, single-screen summary of all key metrics with slicers for dynamic filtering by Gender. Designed to match the organization's brand aesthetic using a navy and sky-blue palette.

---

## Data Cleaning & Preparation

All data preparation was performed directly in Excel. The following steps were applied before analysis:

### 1. Date Standardization
- Admission and Discharge dates were stored as Excel serial numbers
- Formatted both columns as `DD/MM/YYYY` using Excel's Format Cells dialog
- Verified no dates fell outside the 2019–2024 range

### 2. Derived Column: Length of Stay
```
= Discharge Date − Date of Admission
```
Calculated as a simple date subtraction, formatted as a whole number (days). Validated that no negative values existed (no discharge before admission).

### 3. Derived Column: Age Group
Created using a nested `IFS` formula to bin continuous age into 8 categorical bands:
```excel
=IFS(Age<=20,"10-20", Age<=30,"21-30", Age<=40,"31-40", Age<=50,"41-50",
     Age<=60,"51-60", Age<=70,"61-70", Age>70,"71 and Older")
```

### 4. Derived Column: Seasons
Extracted month from admission date and mapped to meteorological seasons:
```excel
=IFS(MONTH(AdmissionDate)<=2,"Winter", MONTH(AdmissionDate)<=5,"Spring",
     MONTH(AdmissionDate)<=8,"Summer", MONTH(AdmissionDate)<=11,"Autumn",
     TRUE,"Winter")
```

### 5. Data Validation Checks
- Checked for blank cells in critical columns (Name, Age, Gender, Billing Amount)
- Used `COUNTBLANK()` across all key columns — zero blanks found
- Verified Gender only contained "Male" / "Female" using `COUNTIF` validation
- Confirmed Billing Amount had no zero or negative values using `COUNTIF(range,"<=0")`
- Applied `TRIM()` and `PROPER()` to name and hospital fields to remove inconsistent casing

### 6. Duplicate Check
- Applied Excel's **Remove Duplicates** function on the full dataset
- Cross-validated using `COUNTIFS` on Name + Admission Date combination
- No duplicate records found in the final dataset

---

## Analytical Methods

### PivotTable Architecture
All aggregations are built using Excel PivotTables on the `KPIs` tab, connected to the source table via structured Excel Table references. This ensures:
- Automatic refresh when source data is updated (`Refresh All`)
- Consistent aggregation logic across all visuals
- Single source of truth — all dashboard charts reference KPI pivots only

### Calculations Performed

| Metric | Method |
|--------|--------|
| Total Patients | `COUNT` of patient records |
| Total Treatment Cost | `SUM` of Billing Amount |
| Average Treatment Cost | `AVERAGE` of Billing Amount |
| Average Length of Stay | `AVERAGE` of Length of Stay column |
| Yearly Admission Trend | PivotTable: Year × Patient Count |
| Patients by Condition | PivotTable: Medical Condition × Patient Count |
| Patients by Insurance | PivotTable: Insurance Provider × Patient Count |
| Top Hospitals | PivotTable: Hospital × Patient Count, sorted descending |
| Top Doctors | PivotTable: Doctor × Patient Count, sorted descending |
| Admission Type Split | PivotTable: Admission Type × Patient Count (%) |
| Age Group Distribution | PivotTable: Age Group × Patient Count |
| Blood Type Distribution | PivotTable: Blood Type × Patient Count |
| Seasonal Patterns | PivotTable: Season × Year × Patient Count |

### Slicers & Interactivity
- A **Gender slicer** is connected to all PivotTables on the dashboard
- Selecting "Female" or "Male" dynamically filters every chart and KPI card simultaneously
- The slicer is formatted to match the dashboard color theme for a polished UX

---

## Key Metrics & KPIs

| KPI | Value |
|-----|-------|
| 📊 Total Patients | **55,500** |
| 💰 Total Treatment Cost | **$1,417,432,043** |
| 💵 Average Treatment Cost | **$25,539** |
| 🛏️ Average Length of Stay | **16 days** |
| 📅 Peak Admission Year | **2020 (11,285 patients)** |
| 🏥 Top Hospital | **Llc Smith (44 patients)** |
| 👨‍⚕️ Top Doctor | **Michael Smith (27 patients)** |
| 🦠 Most Common Condition | **Arthritis (9,308 patients)** |
| 🏦 Largest Insurance Payer | **Cigna (11,249 patients)** |
| 👴 Largest Age Group | **71 and Older (12,142 patients)** |

---

## Dashboard Visualizations

The `Report` tab presents 10 visual components arranged in a structured grid layout:

| Visual | Chart Type | Key Insight Conveyed |
|--------|------------|---------------------|
| KPI Cards (×4) | Stat tiles | High-level summary metrics |
| Admission Trend Yearly | Line chart | Volume changes 2019–2024 |
| Top 5 Hospitals by Patients | Horizontal bar | Hospital performance comparison |
| Top 5 Doctors by Patients | Horizontal bar | Physician workload |
| Patients by Medical Conditions | Horizontal bar | Condition prevalence |
| Patients by Gender | Donut chart | Gender distribution (50/50) |
| Patients by Insurance Providers | Horizontal bar | Payer mix |
| Patients by Admission Type | Donut chart | Elective/Emergency/Urgent split |
| Patients by Age Group | Horizontal bar | Age-based demand |
| Patients by Blood Group | Column chart | Blood type distribution |

### Design Principles Applied
- **Consistent color palette:** Navy (#1F3864) for headers, sky-blue (#5BA3C9) for bars, with accent highlights
- **No chart junk:** Gridlines minimized, data labels on all bars for immediate readability
- **White space:** Clean card layout with adequate spacing between components
- **Accessible fonts:** Bold labels on all axes, 11pt+ font sizes throughout

---

## Key Findings & Insights

### 1. Admission Volume — Post-2020 Plateau with 2024 Drop
Patient admissions surged from 7,387 in 2019 to 11,285 in 2020, then stabilized at approximately 11,000 per year through 2023. The sharp decline to 3,854 in 2024 likely reflects a partial-year dataset rather than an actual reduction. Leadership should confirm whether 2024 data is complete before drawing year-over-year conclusions.

### 2. Aging Population Drives Demand
Patients aged **71 and older represent the single largest age cohort (12,142 patients — 22% of total volume)**, nearly three times the size of the smallest group (10–20, at 2,443). This has direct implications for bed capacity, geriatric specialist staffing, and long-term care partnerships.

### 3. Near-Perfect Parity Across Conditions and Gender
All six medical conditions show nearly identical patient counts (~9,200–9,300 each), suggesting the dataset may be synthetic or stratified. Similarly, gender is split 50/50 (Male: 27,774 / Female: 27,726). Analysts should validate whether this uniformity reflects real population data or dataset construction.

### 4. Insurance Payer Mix Is Evenly Distributed
The five insurance providers each cover roughly 20% of patients (Cigna: 11,249 — Aetna: 10,913). This balanced distribution reduces single-payer dependency risk. However, Medicare's growing patient base (11,154) warrants attention given regulatory reimbursement rate considerations.

### 5. Admission Type Split is Nearly Equal
Elective (34%), Urgent (33%), and Emergency (33%) admissions are in near-equal thirds. The high proportion of urgent and emergency cases — totaling 66% of all admissions — signals the need for robust emergency staffing protocols and bed availability planning.

### 6. Hospital Volume Concentration is Low
Top hospitals peak at only 44 patients (Llc Smith), suggesting admissions are widely distributed across a large hospital network. No single facility appears to be overburdened, which is a positive operational signal — though it may also indicate fragmentation of care.

### 7. Test Results Are Evenly Split Across Categories
Abnormal (18,627), Normal (18,517), and Inconclusive (18,356) test results are nearly identical in count — a statistically unusual distribution that may warrant data quality review or indicate that result categorization needs refinement.

---

## Recommendations

Based on the analysis, the following strategic recommendations are presented to the executive team:

### Operational Recommendations

**1. Develop a Senior Care Strategy**
With 71+ patients comprising 22% of volume, the network should invest in geriatric care units, specialized staff training, and discharge planning protocols tailored to older patients to reduce average length of stay.

**2. Investigate 2024 Data Completeness**
The significant drop in 2024 admissions (3,854 vs. ~11,000/year prior) must be validated. If data is incomplete, forecasting models and budget plans based on 2024 figures will be inaccurate.

**3. Reduce Inconclusive Test Results**
With 33% of all test results classified as "Inconclusive," the network should audit testing protocols and equipment calibration across facilities to improve diagnostic accuracy and reduce repeat testing costs.

**4. Standardize Emergency Capacity Planning**
Given that 66% of admissions are non-elective (urgent + emergency), hospitals should maintain surge capacity protocols and avoid scheduling elective procedures during historically high-volume periods.

### Financial Recommendations

**5. Benchmark Average Treatment Cost by Condition**
At an overall average of $25,539 per patient, breaking costs down by condition, admission type, and hospital will identify outliers and opportunities to standardize high-cost care pathways.

**6. Negotiate Medicare & Cigna Contracts Proactively**
As the two largest payers, Cigna and Medicare together cover ~40% of the network's patient volume. Favorable contract terms with these payers could have a material impact on reimbursement revenue.

### Strategic Recommendations

**7. Expand Data Capture for Seasonality Analysis**
Current seasonal data is available but not yet visualized in the dashboard. Adding a seasonal admissions trend chart would enable better resource forecasting and seasonal staffing models.

**8. Monitor High-Volume Physicians for Burnout Risk**
Top physicians (Michael Smith: 27 patients, John Smith & Robert Smith: 22 each) should be monitored for unsustainable caseloads, especially given that these counts likely represent recent snapshots, not full-period totals.

---

## Tools & Techniques Used

| Category | Tool / Technique |
|----------|----------------|
| Platform | Microsoft Excel (Office 365) |
| Data Storage | Excel Table (structured reference) |
| Aggregation | PivotTables with calculated fields |
| Derived Features | IF / IFS formulas for Age Group, Seasons |
| Date Engineering | DATE, MONTH, YEAR, subtraction for Length of Stay |
| Data Validation | COUNTBLANK, COUNTIF, Remove Duplicates |
| Text Cleaning | TRIM, PROPER, Find & Replace |
| Visualization | Native Excel charts (Bar, Line, Donut, Column) |
| Interactivity | Slicers connected to multiple PivotTables |
| Dashboard Design | Manual layout with shapes, icons, and color fills |
| Presentation | PowerPoint (recommended for slide deck export) |

---

## How to Use This File

### Prerequisites
- Microsoft Excel 2016 or later (Office 365 recommended)
- Macros not required — all functionality uses native Excel features

### Opening the File
1. Download `Project.xlsx` from this repository
2. Open in Microsoft Excel
3. If prompted, click **Enable Editing**
4. Navigate to the `Report` tab to view the interactive dashboard

### Refreshing the Data
If the source data in the `healthcare_dataset` tab is updated:
1. Go to the `KPIs` tab
2. Right-click any PivotTable and select **Refresh All**, or
3. Navigate to **Data → Refresh All** in the Excel ribbon
4. All dashboard charts will update automatically

### Using the Dashboard Slicer
- The **Gender slicer** on the `Report` tab filters all visuals simultaneously
- Click "Female" or "Male" to filter
- Click the clear filter icon (↙) in the slicer to reset to all patients

### Navigating the Tabs
| Tab | Purpose | Audience |
|-----|---------|----------|
| `Brief` | Project overview | All stakeholders |
| `healthcare_dataset` | Raw + cleaned data | Analysts |
| `KPIs` | Pivot calculations | Analysts |
| `Insights` | Written commentary | Executives |
| `Report` | Interactive dashboard | All stakeholders |

---

## Repository Contents

```
📁 Repository
├── 📊 Project.xlsx                          ← Main analytics workbook
├── 🖼️ Healthcare_Project.png                ← Dashboard screenshot
├── 📄 Healthcare_Business_Problem.pdf       ← Original project brief
└── 📝 README.md                             ← This documentation file
```

---

## License & Usage

This project was created for analytical and educational purposes. The dataset used is synthetic/anonymized and does not contain real patient information. All findings and recommendations are based on the provided dataset and should be validated against real-world data before operational implementation.

---

*Built with Microsoft Excel · Documented for GitHub · Designed for executive decision-making*
