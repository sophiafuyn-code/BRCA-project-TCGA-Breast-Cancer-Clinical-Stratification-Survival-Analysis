# TCGA-Breast-Cancer-Clinical-Stratification-Survival-Analysis

This project is an analysis of clincial and genomic data from 1,108 breast cancer patients in the TCGA  BRCA cohort.The goal of this analysis is to classify patients by molecular subtype ( HE+/ HER2-, triple -negative , HR+/HER2+, HER2+ HR-) and their associations to overall survival (OS) and disease free survival using standard oncology statistical analysis on R.This project was conducted independently to investigate clinical stratification of breast cancer patients by molecular subtype and its association with survival outcomes, using standard oncology statistical methods in R.

## Dataset 

| Property | Detail                                |
|----------|---------------------------------------|
| Source   |cBioPortal — TCGA BRCA Firehose Legacy |
| Patient  |1,108                                  |
| Variables|141 clinicial and genomic features     |
| File     |brca_tcga_clinical_data.tsv            |

<details>
<summary><b>Key variables used</b></summary>

* Diagnosis age, tumour stage (AJCC)
* ER / PR / HER2 receptor status (IHC + FISH)
* Overall survival (months + vital status)
* Disease-free survival (months + recurrence status)
* Menopause status, race category
* Tumour mutation burden (TMB, nonsynonymous)

</details>

## Analysis 

| Analysis                        | Key package       |
|---------------------------------|-------------------|
| Data cleaning                   |readr, dplyr       |
| Patient characteristics         |tableor            |
| Molecular subtype classification|dplyr              |
| Kaplan-Meier(KM) survival curve |survival, survminer|   
| Cox porportional hazard model   |survival, survminer|  

<details>
<summary><b>Methodology details</b></summary>
  
* Table 1
   * seperation by ER status (ER + and ER)
   * Continous variables as mean ± SD
   * Categorical variables reported as count(%)
   * standised mean difference (SMD) inculded
     
* Molecular subtypes
   * HR+/HER2− · HR+/HER2+ · HER2+ (HR−) · Triple-negative
   * #Derived from raw ER, PR, HER2 IHC/FISH columns using case_when()
     
* KM
   * OS and DFS curves stratified by subtype
   * Log-rank p-values and at-risk tables shown
   * Pairwise comparisons with Benjamini–Hochberg correction
   * Median survival extracted per group with surv_median()

* Cox model
   * Univariable and multivariable models
   * Adjusted for age and AJCC stage
   * Proportional hazards assumption tested via cox.zph() and Schoenfeld residuals
   * Results visualised as forest plot with ggforest()
   
*  Molecular subtypes
   * Distribution on Log scale 
   * TMB- high defined as ≥10 mut/Mb (standard immunotherapy threshold)
   * OS compared by TMB group
</details>

## How to Run 

1. Clone the repositoy
git clone
(https://github.com/me50/sophiafuyn-code/brca-tcga-survival.git) ( place holder) 

2. install.packages(c("tidyverse", "survival", "survminer", "tableone"))

3. Add the data file
Place brca_tcga_clinical_data.tsv in the data/ folder.
Download from cBioPortal TCGA BRCA.

4. Run scripts in order
rsource("R/01_load_clean.R")
source("R/02_table1.R")
source("R/03_subtypes.R")
source("R/04_survival_km.R")
source("R/05_cox_model.R")
source("R/06_tmb_analysis.R")

   * #### 01_load_clean.R must be run first — all other scripts depend on the brca_clean object it creates.
  * ### Requirement
   
      | Package  | Version | Purpose                          |
      |----------|---------|----------------------------------|
      | tidyverse| 2.0.0   | data wrangling and visualisation |
      | survival | 3.5     | KM curve and Cox modelling       |
      | survminer| 0.4.9   | survival plot visualisation      |
      | tableone | 0.13.2  | patient characteristics table    | 

