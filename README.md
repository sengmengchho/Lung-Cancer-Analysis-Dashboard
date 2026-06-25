# Lung Cancer Analysis Dashboard

[![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=power-bi&logoColor=black)](https://powerbi.microsoft.com/)
[![Excel](https://img.shields.io/badge/Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)](https://www.microsoft.com/en-us/microsoft-365/excel)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

## Abstract

This report presents a comprehensive data visualization analysis of global lung cancer patterns using a publicly available dataset comprising 220,632 patient records across 25 countries and 24 variables. The primary objectives were to explore the distribution and determinants of lung cancer diagnoses, design an interactive six-page Power BI dashboard, and derive actionable public health insights. The dashboard was structured into six analytical pages: Overview, Smoking and Risk Factors, Treatment and Survival, Risk and Correlation Analysis, Healthcare and Environment, and an Executive Summary. Key findings indicate that smoking is the dominant risk factor, with smokers diagnosed at a rate of 7.07% compared to 2.05% for non-smokers (a 3.4x difference). Developing countries account for 75.5% of all diagnosed cases; however, per-capita diagnosis rates are nearly equal across developed and developing nations, suggesting that population size, rather than individual risk, drives the disparity. Healthcare access emerged as the most critical systemic factor: patients with good access achieved a 60% early detection rate versus 20% for those with poor access. Environmental factors, including air pollution, indoor pollution, and occupational exposure, were found to be statistically weak predictors of diagnosis in isolation. These findings inform targeted public health interventions, including anti-smoking programs, expanded cancer screening in developing countries, and prioritization of high-risk demographic groups.

---

## Table of Contents

- [Overview](#overview)
- [Dataset](#dataset)
- [Dashboard Design](#dashboard-design)
- [Key Findings](#key-findings)
- [Recommendations](#recommendations)
- [DAX Measures](#dax-measures)
- [UN Sustainable Development Goals](#un-sustainable-development-goals)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Authors](#authors)
- [Citation](#citation)
- [License](#license)

---

## Overview

### Background and Motivation

Lung cancer is one of the leading causes of cancer-related mortality worldwide, contributing significantly to global cancer deaths each year. Despite advances in medical treatments and early detection technologies, disparities in diagnosis and survival persist across countries, demographic groups, and levels of healthcare access. Understanding the patterns, risk factors, and systemic influences that drive lung cancer outcomes is critical for designing effective public health interventions.

Data visualization offers a powerful tool for making large, complex health datasets accessible to researchers, clinicians, and policymakers. By transforming raw patient data into interactive dashboards, stakeholders can quickly identify trends, compare risk factors, and evaluate the effectiveness of healthcare systems across different populations and geographies.

### Problem Statement

Despite the availability of large-scale lung cancer datasets, the relationships between individual risk factors (such as smoking, pollution, and occupational exposure), healthcare system quality, and patient outcomes remain poorly visualized and communicated. This project addresses the following core analytical questions:

- Which risk factors most significantly increase the likelihood of lung cancer diagnosis?
- Does healthcare access influence early detection rates and survival outcomes?
- How do developed and developing countries differ in terms of cancer burden, early detection, and mortality?
- Are environmental factors independent predictors of lung cancer risk, or do they interact with behavioral factors such as smoking?

### Objectives

- Explore and understand the structure, content, and distribution of the global lung cancer dataset
- Design an interactive six-page Power BI dashboard that effectively communicates key trends, patterns, and correlations in the data
- Identify and rank the most significant behavioral and environmental risk factors associated with lung cancer diagnosis
- Analyze the relationship between healthcare access, early detection rates, and patient survival outcomes
- Derive actionable public health recommendations based on data-driven insights

### Scope and Limitations

The analysis utilizes 220,632 patient records across 25 countries (6 developed and 19 developing) including variables such as demographics, smoking behavior, environmental exposures, cancer stage, treatment type, survival years, healthcare access, and annual mortality statistics. The scope is limited to the variables available in the dataset and does not include longitudinal tracking of individual patients over time. The dataset does not specify a particular collection year, and country-level attributes such as development status are fixed classifications within the dataset. Findings are descriptive and correlational; no causal inferences are drawn.

---

## Dataset

### Source

The dataset used in this project is the Lung Cancer Data Analysis dataset, sourced from GitHub at [https://github.com/vsumitwork/Lung-Cancer-Data-Analysis/tree/main](https://github.com/vsumitwork/Lung-Cancer-Data-Analysis/tree/main). It is provided in Microsoft Excel (.xlsx) format and contains 220,632 rows and 24 columns.

The dataset includes patients from 25 countries across 5 continents, classified into 6 developed and 19 developing nations. Variables cover demographic information, behavioral risk factors (e.g., smoking, passive smoking), environmental exposures (e.g., air pollution, indoor pollution, occupational exposure), clinical outcomes (e.g., cancer stage, treatment type, survival years), and country-level health statistics (e.g., annual lung cancer deaths, mortality rate).

### Dataset Specifications

| Attribute | Description |
|-----------|-------------|
| Total Records | 220,632 |
| Countries | 25 |
| Developed Countries | 6 |
| Developing Countries | 19 |
| Variables | 24 |
| Format | Microsoft Excel (.xlsx) |
| Source | GitHub |

### Data Dictionary

| Variable Name | Data Type | Unit | Description |
|---------------|-----------|------|-------------|
| ID | Text | - | Unique patient identifier |
| Country | Text | - | Country of the patient |
| Population_Size | Numeric | Millions | Population size of the country |
| Age | Numeric | Years | Age of the patient (20-85) |
| Gender | Text | - | Male or Female |
| Smoker | Text | - | Active smoker (Yes/No) |
| Years_of_Smoking | Numeric | Years | Number of years the patient has smoked |
| Cigarettes_per_Day | Numeric | Count | Average cigarettes smoked per day |
| Passive_Smoker | Text | - | Secondhand smoke exposure (Yes/No) |
| Family_History | Text | - | Family history of lung cancer (Yes/No) |
| Lung_Cancer_Diagnosis | Text | - | Confirmed diagnosis (Yes/No) |
| Cancer_Stage | Text | - | Stage 1-4; blank for non-diagnosed |
| Survival_Years | Numeric | Years | Survival years post-diagnosis |
| Adenocarcinoma_Type | Text | - | Adenocarcinoma type (Yes/No) |
| Air_Pollution_Exposure | Text | - | Outdoor air pollution (Low/Medium/High) |
| Occupational_Exposure | Text | - | Workplace chemical/dust exposure (Yes/No) |
| Indoor_Pollution | Text | - | Indoor pollution (Yes/No) |
| Healthcare_Access | Text | - | Healthcare access quality (Good/Poor) |
| Early_Detection | Text | - | Early detection (Yes/No) |
| Treatment_Type | Text | - | Chemotherapy/Radiotherapy/Surgery |
| Developed_or_Developing | Text | - | Country classification |
| Annual_Lung_Cancer_Deaths | Numeric | Count | Annual lung cancer deaths |
| Lung_Cancer_Prevalence_Rate | Numeric | % | Prevalence rate |
| Mortality_Rate | Numeric | per 100K | Mortality rate |

### Data Preprocessing

The following preprocessing and transformation steps were applied before and during visualization in Power BI:

- **Handling missing values**: Cancer_Stage and Treatment_Type columns contain blank values for non-diagnosed patients (211,671 records). These are expected nulls, not data quality issues. Visual-level filters were applied to exclude blanks where appropriate.

- **Data type conversions**: All numeric columns (Age, Cigarettes_per_Day, Years_of_Smoking, Survival_Years, Mortality_Rate) were confirmed as Whole Number or Decimal Number types in Power Query.

- **Calculated columns**: Age_Group was created using DAX SWITCH statements and categorized patients into Young Adult (18-35), Middle Age (36-60), and Senior (61+). These groups were used to stratify analysis of risk and survival outcomes.

- **DAX measures**: All key performance indicators were created as explicit measures including Total Patients, Cancer Cases, Diagnosis Rate %, Early Detection Rate %, Avg Survival Years, Avg Mortality Rate, and scenario-based risk measures.

- **Filtering**: Pages 3 (Treatment and Survival) and portions of Page 5 (Healthcare and Environment) use visual-level or page-level filters restricting data to Lung_Cancer_Diagnosis = "Yes" (8,961 records).

---

## Dashboard Design

### Design Principles

The dashboard was designed following core data visualization principles of clarity, consistency, and analytical hierarchy. Each page addresses a specific set of analytical questions, progressing logically from a high-level overview to detailed correlation analysis, and culminating in a comprehensive executive summary.

A consistent light blue card background was applied across all pages. KPI cards were positioned at the top of each page to provide immediate context before the viewer engages with detailed charts.

Chart types were selected based on the nature of the data relationships:

| Data Relationship | Chart Type |
|-------------------|------------|
| Proportional Data | Donut Charts |
| Ranked Comparisons | Horizontal Bar Charts |
| Cross-Factor Relationships | Matrix Visuals with Conditional Formatting |
| Distributions | Column Charts |

### Dashboard Structure

| Page | Visualizations | Slicers |
|------|----------------|---------|
| **Overview** | KPI cards, LC Cases by Continent (column), LC Cases by Gender (pie), LC Cases by Country (bar), Annual Deaths (bar), LC Cases by Age Group (column) | Country |
| **Smoking & Risk Factors** | KPI cards, Smokers by Continent/Country/Gender, LC Cases by Smoker x Passive Smoker, LC Cases by Occupational/Air Pollution Exposure | Age Group |
| **Treatment & Survival** | KPI cards, Cancer Stage Distribution (100% stacked bar), Survival by Treatment/Early Detection/Stage, LC Cases by Adenocarcinoma Type | Cancer Stage |
| **Risk & Correlation** | KPI cards, Diagnosis Rate by Risk Factor (ranked), Diagnosis Rate by Scenario, Cross-factor matrices | None |
| **Healthcare & Environment** | KPI cards, Early Detection Donut, Developed vs Developing comparisons, Indoor Pollution analysis | None |
| **Executive Summary** | KPI cards, Top 5 Findings, 3 Recommendations, Risk Conclusion | None |

### Dashboard Screenshots

#### Overview Page
*Global lung cancer distribution, demographics, and key KPI summary*

![Overview Page](2026-06-25%2013.46.58.jpg)

#### Smoking and Risk Factors Page
*Behavioral and environmental risk factor distributions and analysis*

![Smoking Page]()

#### Treatment and Survival Page
*Patient survival outcomes by treatment type, cancer stage, and early detection*

![Treatment Page]()

#### Risk and Correlation Analysis Page
*Ranked risk factor diagnosis rates and cross-factor interaction matrices*

![Risk Page]()

#### Healthcare and Environment Page
*Healthcare access impact on early detection, survival, and country-level comparisons*

![Healthcare Page]()

#### Executive Summary Page
*Key findings, recommendations, and risk conclusions overview*

![Executive Page]()

---

## Key Findings

### Finding 1: Smoking is the Dominant and Disproportionate Risk Factor

Active smokers in the dataset are diagnosed with lung cancer at a rate of 7.07%, compared to only 2.05% for non-smokers, a 3.4x higher rate that establishes smoking as the single most powerful predictor of lung cancer diagnosis in this global dataset. This gap widens dramatically when analyzed by intensity: smokers with more than 20 pack-years show a diagnosis rate of 8.9%, while light smokers (under 10 pack-years) sit at just 4.8%, revealing a clear dose-response relationship.

All other risk factors cluster tightly around 4%, barely exceeding the overall population average of 4.06%. The combined risk scenario analysis delivers the most striking finding: adding high air pollution and occupational exposure on top of smoking only raises the diagnosis rate from 7.12% (smoking alone) to 7.21% (all three factors combined), a marginal increase of just 0.09 percentage points.

### Finding 2: Healthcare Access Determines Early Detection, Not Cancer Prevention

Patients with good healthcare access achieve an early detection rate of 60.0% compared to only 20.0% for patients with poor access, a 3x gap. However, the overall diagnosis rates for the two groups are nearly identical (Good Access: 4.13% vs Poor Access: 4.04%), confirming that healthcare access does not prevent lung cancer, but significantly influences how early it is detected.

This distinction has major clinical significance: early-stage diagnosis (Stages 1 and 2) typically offers better treatment options and improved survival outcomes compared to late-stage diagnosis. Patients with good access and early detection achieve the highest average survival (5.58 years) compared to poor access without early detection (5.48 years).

### Finding 3: Developing Countries Carry the Majority of the Cancer Burden

Developing countries account for 75.5% of all diagnosed cases (6,766 out of 8,961), compared to 24.5% in developed countries (2,195 cases). However, per-capita diagnosis rates are nearly equal: 4.03% in developing countries versus 4.15% in developed countries. This demonstrates that the raw case gap is primarily driven by population size.

A more critical disparity is in early detection: only 20.0% of patients in developing countries are detected early, compared to 54.08% in developed nations. This gap in early detection, rather than in underlying individual risk, represents the most actionable healthcare inequality in the dataset.

### Finding 4: Stage 4 is the Most Common Diagnosis Stage

Among the 8,961 diagnosed patients, Stage 4 accounts for the largest proportion at 26.64%, followed by Stage 2 (24.53%), Stage 1 (24.45%), and Stage 3 (24.38%). The near-equal distribution across stages, combined with the finding that 72% of all patients (including non-diagnosed) were not detected early, suggests that late-stage presentation is the norm in this dataset rather than the exception.

Survival years across stages show limited variation: Stage 2 averages 5.60 years, Stage 4 5.45 years, a difference of only 0.18 years.

### Finding 5: Environmental Factors are Statistically Weak Predictors in Isolation

Diagnosis rates for environmental factors are closely clustered near the population average (4.06%):

| Factor | Diagnosis Rate |
|--------|----------------|
| Air Pollution - Low | 4.02% |
| Air Pollution - Medium | 4.08% |
| Air Pollution - High | 4.06% |
| Indoor Pollution - No | 4.09% |
| Indoor Pollution - Yes | 3.98% |
| Occupational Exposure - No | 4.06% |
| Occupational Exposure - Yes | 4.16% |

The cross-factor matrix analysis confirms that these factors do not stack additively. The highest-risk environmental combination yields a diagnosis rate of only 4.24%, still far below the smoking rate of 7.07%.

### Additional Observations

- **Gender disparity**: Males account for 59.5% of diagnosed cases, despite representing only 49.9% of the total patient population.
- **Family history does not amplify smoking risk**: Smokers with family history (7.04%) have nearly identical diagnosis rates to smokers without family history (7.08%).
- **Treatment type has minimal impact on survival**: Average survival years are very similar across treatment types: Radiotherapy (5.48 yrs), Surgery (5.47 yrs), and Chemotherapy (5.42 yrs).

---

## Recommendations

### 1. Prioritize Anti-Smoking Programs Globally

Smoking accounts for the vast majority of elevated lung cancer risk, and additional risk factors barely increase diagnosis rates beyond smoking alone. Public health investment in smoking cessation education, nicotine replacement programs, and tobacco taxation is likely to have the greatest single impact on reducing lung cancer cases.

### 2. Expand Early Cancer Screening in Developing Countries

With only 20% early detection in developing nations versus 54.1% in developed nations, structured lung cancer screening programs, particularly low-dose CT screening for high-risk smokers, should be implemented in low- and middle-income countries. This could shift diagnoses from late-stage to early-stage, significantly improving survival outcomes.

### 3. Target High-Risk Demographic Groups for Priority Screening

Male patients aged 61-70 who are active smokers represent the highest-risk demographic in this dataset. Prioritizing screening and intervention resources toward this group would maximize the impact of limited healthcare budgets and improve early detection rates.

---

## DAX Measures

| Measure | DAX Formula | Description |
|---------|-------------|-------------|
| Total Patients | `COUNTROWS(lung_cancer_Dataset)` | Total number of patient records in the dataset |
| Cancer Cases | `COUNTROWS(FILTER(lung_cancer_Dataset, lung_cancer_Dataset[Lung_Cancer_Diagnosis] = "Yes"))` | Total confirmed lung cancer diagnoses |
| Diagnosis Rate % | `DIVIDE([Cancer Cases], [Total Patients]) * 100` | Percentage of all patients with a confirmed diagnosis |
| Total Smokers | `CALCULATE(COUNTROWS(lung_cancer_Dataset), lung_cancer_Dataset[Smoker] = "Yes")` | Total number of active smokers |
| Total Passive Smokers | `CALCULATE(COUNTROWS(lung_cancer_Dataset), lung_cancer_Dataset[Passive_Smoker] = "Yes")` | Total number of passive smokers |
| Smoker Diagnosis Rate | `DIVIDE(CALCULATE([Cancer Cases], lung_cancer_Dataset[Smoker] = "Yes"), CALCULATE([Total Patients], lung_cancer_Dataset[Smoker] = "Yes")) * 100` | Diagnosis rate among active smokers only |
| Avg Survival Years | `AVERAGE(lung_cancer_Dataset[Survival_Years])` | Average survival years (applied with Lung_Cancer_Diagnosis = Yes filter) |
| Avg Mortality Rate (LC) | `CALCULATE(AVERAGE(lung_cancer_Dataset[Mortality_Rate]), lung_cancer_Dataset[Lung_Cancer_Diagnosis] = "Yes")` | Average mortality rate for diagnosed patients |
| Early Detection Rate % | `DIVIDE(CALCULATE(COUNTROWS(lung_cancer_Dataset), lung_cancer_Dataset[Early_Detection] = "Yes"), COUNTROWS(lung_cancer_Dataset)) * 100` | Percentage of patients detected early |
| Early Detection Rate - Good Access | `DIVIDE(CALCULATE(COUNTROWS(lung_cancer_Dataset), lung_cancer_Dataset[Healthcare_Access] = "Good", lung_cancer_Dataset[Early_Detection] = "Yes"), CALCULATE(COUNTROWS(lung_cancer_Dataset), lung_cancer_Dataset[Healthcare_Access] = "Good")) * 100` | Early detection rate for patients with good healthcare access |
| Early Detection Rate - Poor Access | `DIVIDE(CALCULATE(COUNTROWS(lung_cancer_Dataset), lung_cancer_Dataset[Healthcare_Access] = "Poor", lung_cancer_Dataset[Early_Detection] = "Yes"), CALCULATE(COUNTROWS(lung_cancer_Dataset), lung_cancer_Dataset[Healthcare_Access] = "Poor")) * 100` | Early detection rate for patients with poor healthcare access |

---

## UN Sustainable Development Goals Alignment

| SDG Goal | Relevant Target(s) | Contribution |
|----------|-------------------|--------------|
| **SDG 3** Good Health and Well-Being | Target 3.4 (reduce premature mortality from NCDs) / Target 3.8 (universal health coverage) | By identifying smoking as the dominant risk factor and healthcare access as the primary driver of early detection, this dashboard provides the evidence base for interventions that directly reduce premature lung cancer mortality and advance universal health coverage goals. |
| **SDG 10** Reduced Inequalities | Target 10.2 (empower and promote social and economic inclusion) | The analysis reveals a 3x early detection gap between developed and developing countries (54.08% vs 20%), quantifying a health equity disparity that this dashboard makes visible and actionable for policymakers working to reduce global health inequalities. |
| **SDG 17** Partnerships for the Goals | Target 17.18 (data availability and quality for developing countries) | By developing an accessible, interactive visualization of cross-country health data, this project supports the data literacy and evidence infrastructure needed for international health partnerships and data-driven cooperation between nations. |

---

## Project Structure

```
Lung-Cancer-Analysis-Dashboard/
│
├── Lung Cancer.pbix                     # Power BI dashboard file
├── lung_cancer_Dataset.xlsx             # Raw dataset (220,632 records)
├── README.md                            # Project documentation
├── 2026-06-25 13.46.58.jpg              # Dashboard preview image
└── LICENSE                              # MIT License
```

---

## Getting Started

### Prerequisites

- Microsoft Power BI Desktop
- Microsoft Excel (for data viewing)

### Open the Dashboard

1. Download `Lung Cancer.pbix` from this repository
2. Open in Power BI Desktop
3. Explore the six interactive pages
4. Use page-level slicers to filter by country, age group, and cancer stage

---

## Authors

| Name | Role | Student ID |
|------|------|------------|
| CHHO Sengmeng | Project Lead and Overview Dashboard Designer | e20220296 |
| CHOUB Botumraksa | Team Member | e20221709 |
| DOEUN Bunheng | Team Member | e20221528 |
| CHHENG Sotheane | Team Member | e20220686 |
| DIN Reaksa | Team Member | e20221070 |

**Course**: Data Visualization and Dashboard Design  
**Institution**: Institute of Technology of Cambodia  
**Semester**: Semester 2, 2025-2026  
**Submission Date**: June 18, 2026

---

## Citation

If you use this work in your research, please cite:

```bibtex
@report{doeun2026lungcancer,
  title={Lung Cancer Analysis Dashboard},
  author={DOEUN, Bunheng and CHOUB, Botumraksa and CHHO, Sengmeng and CHHENG, Sotheane and DIN, Reaksa},
  institution={Institute of Technology of Cambodia},
  year={2026},
  type={Course Project Report}
}
```

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgments

- Dataset source: [GitHub - Lung Cancer Data Analysis](https://github.com/vsumitwork/Lung-Cancer-Data-Analysis/tree/main)
- Course instructor for guidance and feedback
- Institute of Technology of Cambodia for academic support

---

## Contact

For questions or collaboration opportunities, please contact:

**CHHO, Sengmeng** (Project Lead)
- Email: sengmengchho@gmail.com
- Institution: Institute of Technology of Cambodia

**CHOUB Botumraksa** (Team Member)
- Email: botum.raksa@gmail.com
- Institution: Institute of Technology of Cambodia 
