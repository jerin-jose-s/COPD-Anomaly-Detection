# COPD Patient Analysis — Anomaly Detection & Dashboard

## Executive Summary
This project analyses real COPD patient data to identify patterns in lung function, physical performance and symptom burden across different severity groups. Using Python and Tableau, the project covers the full data analytics workflow — from raw data cleaning through to an interactive clinical dashboard. Out of 100 patients analysed, **13 were flagged for clinical review** and **1 identified as critical priority.** The analysis also identified survivorship bias in age and smoking history data — a clinically significant finding that has implications for how the data should be interpreted.

---

## Business Problem
Clinical teams managing COPD patients need to quickly identify:
- Which patients have unusual readings compared to others at the same severity level
- Whether any patients may be misclassified or have data recording errors
- Which clinical measures are the strongest indicators of disease severity

Without a structured analytical approach, identifying these patients requires manual review of every record — which is time consuming and inconsistent. This project automates that process using anomaly detection and presents findings in an interactive Tableau dashboard that clinical teams can use without any technical knowledge.

---

## Methodology
1. **Data quality assessment** — 5 issues identified and documented before any changes were made:
   - Unnamed index column
   - Misaligned row (row 81, values shifted across columns)
   - Invalid CAT score of 188 (valid range 0-40)
   - Missing walk test values in 2 patients
   - Redundant COPDSEVERITY column
2. **Data cleaning** — following standard order: remove duplicates → standardize data → handle missing values → remove unwanted columns
3. **Exploratory data analysis** — patterns analysed across 4 clinical measure groups and 5 key findings identified
4. **Group-based anomaly detection** — patients flagged if readings fall outside 2 standard deviations of their severity group mean
5. **Tableau dashboard** — interactive dashboard built for clinical teams showing anomaly summary, flagged patients and priority list

---

## Skills
- **Python** — pandas
- **Data cleaning** — imputation, misaligned row detection, outlier handling
- **Statistical analysis** — group-based standard deviation thresholds, survivorship bias identification
- **Exploratory data analysis** — groupby analysis across severity groups
- **Tableau** — interactive dashboard with KPI cards, filters and colour coded priority table

---

## Results & Business Recommendation

**Data Quality:**
- 5 data quality issues identified and resolved
- CAT score of 188 replaced with 16 (median of MILD patients)
- Misaligned row flagged and removed — only 1% of dataset

**EDA Findings:**
- Lung function (FEV1, FVC) and walk test distance (MWT1Best) consistently decline with COPD severity
- Symptom scores (CAT, SGRQ, HAD) consistently increase with severity
- Age and smoking history show survivorship bias — very severe patients are younger and lighter smokers, likely because older/heavier smoking patients did not survive to participate

**Anomaly Detection:**
- **13 patients flagged** for clinical review (13% of total)
- **1 critical patient** identified (ID 108 — flagged in 3 out of 4 measures)
- **MWT1Best** had the most anomalies (7) — likely influenced by musculoskeletal comorbidities affecting walk performance independently of lung function

**Recommendation:** Patient ID 108 should be reviewed immediately — their MWT1Best of 699m is the highest in the entire dataset despite being classified as SEVERE. This is inconsistent with their severity classification and may indicate misclassification or a data recording error. The survivorship bias finding also suggests caution when using age or smoking history as predictors of severity.

---

## How to Run

1. Clone this repository
2. Install required libraries
3. Place the raw dataset (COPD.csv) in the project folder
4. Run the notebook top to bottom
5. The clean dataset (copd_clean_with_anomalies.csv) will be saved automatically
6. Load copd_clean_with_anomalies.csv into Tableau Public to view the dashboard

**Tableau Dashboard:** [https://public.tableau.com/views/COPDPatientAnomalyMonitoringDashboard/COPDPatientAnomalyMonitoringDashboard?:language=en-GB&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link]

---

## Next Steps
- **Add visualisations in Python** — box plots and correlation heatmaps to strengthen the EDA section
- **Expand anomaly detection** — include HAD and SGRQ scores as additional measures
- **Trend analysis** — extend analysis to detect deterioration over time rather than point-in-time anomalies
- **Machine learning** — build a classification model to predict COPD severity from clinical measures
