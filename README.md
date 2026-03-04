# Python-SQL-PowerBI Business Simulation – IT Academy

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)](https://jupyter.org/)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-blue)](https://www.mysql.com/)
[![Power BI](https://img.shields.io/badge/Power%20BI-Desktop-yellow)](https://powerbi.microsoft.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

This repository contains the complete code and analysis for a **business simulation project** developed during the **IT Academy Data Analytics Reskilling program**. The project simulates a real‑world HR analytics scenario: we combine **Python**, **SQL**, and **Power BI** to extract, clean, analyze, and visualize employee data, and finally propose data‑driven business strategies.

---

## 📌 Table of Contents

- [Project Overview](#project-overview)
- [Objectives](#objectives)
- [Dataset](#dataset)
- [Methodology](#methodology)
  - [Data Cleaning & Transformation](#data-cleaning--transformation)
  - [Employee Profile & Performance Analysis](#employee-profile--performance-analysis)
  - [Absenteeism & Well‑being Analysis](#absenteeism--well‑being-analysis)
- [Key Findings](#key-findings)
- [Business Proposals](#business-proposals)
- [Technologies Used](#technologies-used)
- [Repository Structure](#repository-structure)
- [How to Run](#how-to-run)
- [Results & Visualizations](#results--visualizations)
- [Contact](#contact)
- [License](#license)

---

## 🎯 Project Overview

This project addresses two main business questions:

1. **What personal and professional characteristics are associated with higher employee performance?**  
2. **Which factors are most strongly linked to elevated absenteeism, and how can we proactively manage them?**

We use a **multi‑technology approach**:
- **SQL** to extract the raw data from a MySQL database.
- **Python** (pandas, numpy, scipy, statsmodels, scikit‑learn) for data cleaning, transformation, exploratory analysis, and statistical modelling.
- **Power BI** (not included in this repo) to build interactive dashboards that communicate the findings.

The final output is a set of actionable business proposals aimed at improving recruitment, training, and retention strategies, as well as reducing absenteeism.

---

## 🎯 Objectives

- Identify **significant predictors** of high performance and of absenteeism.
- Build **predictive models** to estimate employee performance and absenteeism hours.
- Propose **data‑driven strategies** for:
  - Recruitment (selecting candidates with desirable traits)
  - Training and development (targeted programs)
  - Retention (improving work conditions, flexible policies)
  - Health and well‑being initiatives

---

## 📊 Dataset

The dataset comes from a MySQL database (`Equip_15.RRHH_22092025`) and contains **845 records** of employee absence episodes. Each record includes:

- **Personal attributes**: age, number of children (`Son`), weight, height, body mass index, transportation expense, distance to work, etc.
- **Work‑related attributes**: service time, average work load, hit target percentage, disciplinary failure flags, etc.
- **Absenteeism details**: reason for absence, month, day, season, and hours absent.

After cleaning and de‑duplication, **806 unique employee‑episode records** are retained for analysis.

---

## ⚙️ Methodology

### 1. Data Cleaning & Transformation  
[`DataCleaningAndTransformation_220925.ipynb`](DataCleaningAndTransformation_220925.ipynb)

- Connected to MySQL using `mysql.connector`.
- Converted numeric codes to meaningful categories (e.g., reason for absence, month names).
- Created numeric versions of categorical variables for correlation analysis (e.g., `Education_numeric`, `Month_absence_order`).
- Removed duplicate rows and handled invalid entries (e.g., month values outside 1‑12).
- Exported the cleaned dataset as Parquet and CSV for further analysis.

### 2. Employee Profile & Performance Analysis  
[`Analisis_Perfil_y_desempeno_220925.ipynb`](Analisis_Perfil_y_desempeno_220925.ipynb)

- Aggregated per‑employee metrics: average hit target, total absenteeism hours, number of unjustified absences, and disciplinary failure indicator.
- Performed **clustering** (K‑Prototypes) to group employees into four performance profiles based on these metrics.
- Characterised each cluster by personal attributes and used **chi‑square tests** to check associations with categorical variables.
- Built a **performance score** (0‑100) combining positive (hit target) and negative (absenteeism, disciplinary failure) factors, normalised via Min‑Max scaling, and modelled it using **logit‑transformed linear regression** (GLM with Gaussian family).

### 3. Absenteeism & Well‑being Analysis  
[`Analisis_Ausentismo_i_benestar_laboral_290925.ipynb`](Analisis_Ausentismo_i_benestar_laboral_290925.ipynb)

- Focused on **total absenteeism hours** as the target variable.
- Selected four predictor variables based on previous correlation analysis: `Disciplinary_failure`, `Social_drinker`, `Son`, `Transportation_expense`.
- Applied **multiple linear regression**, including robust techniques (weighted models, oversampling, Random Forest) to check stability.
- Calculated **practical impact** (change in absenteeism hours) for each variable and visualised results with **confidence intervals**.
- Compared univariate vs. multivariate effects and diagnosed potential multicollinearity (VIF < 5).
- Generated a **dashboard‑like executive summary** with key metrics and recommendations.

---

## 🔍 Key Findings

- **Disciplinary failure** has a strong **negative** association with absenteeism (employees with a disciplinary record actually show **fewer** absence hours), but this effect is diluted in multivariate models – possibly due to sample imbalance (only 5% of cases).
- **Having children** (`Son`) **increases** absenteeism: each child adds about **1.4 hours** of absence.
- **Social drinkers** tend to have **higher** absenteeism, though the effect is only marginally significant.
- **Transportation expense** showed no significant effect once other variables were controlled.
- The **performance score** is significantly influenced by **work load** and **education** (Master/Doctor degree has a strong positive effect).

---

## 💼 Business Proposals

Based on the findings, we propose the following actions:

### Recruitment
- Favour candidates who use **public transport** (lower transportation expense may indicate shorter commutes, but the variable itself was not significant; still, it correlates with other traits).
- Include behavioural questions about **values, hobbies, and problem‑solving** to identify candidates with good attendance records.

### Training & Development
- Implement **mentoring and coaching** programmes, especially for employees with lower performance scores.
- Launch **health and wellness** initiatives (e.g., gym discounts, stress management workshops) to reduce absenteeism.

### Retention & Work Conditions
- Introduce **flexible working hours** and **emergency leave banks** for employees with children.
- Establish **partnerships with local childcare services** to support working parents.
- Review the **disciplinary system** to ensure it does not inadvertently encourage presenteeism; instead, create **recognition programmes** for good attendance.

---

## 🛠️ Technologies Used

- **Python 3.8+** – core language
- **pandas, numpy** – data manipulation
- **matplotlib, seaborn** – data visualisation
- **scipy, statsmodels** – statistical tests and regression
- **scikit‑learn** – clustering (K‑Prototypes), preprocessing
- **mysql.connector** – database connection
- **Jupyter Notebook** – interactive development
- **Power BI** – dashboards (not in this repo, but referenced)

---

## 📁 Repository Structure
Python-SQL-PowerBI-Business-Simulation-IT-Academy/
├── 📜 README.md
├── 📜 LICENSE
├── 📓 DataCleaningAndTransformation_220925.ipynb
├── 📓 Analisis_Perfil_y_desempeno_220925.ipynb
├── 📓 Analisis_Ausentismo_i_benestar_laboral_290925.ipynb
├── 📊 PresentacionResultados_220925.pptx
├── 📁 data/ (not included – contains exported Parquet/CSV files)
│ └── RRHH_220925_clean.parquet
│ └── RRHH_220925_clean.csv
├── 📁 results/ (generated analysis outputs, plots, etc.)
└── 📁 scripts/ (optional helper scripts)

text

---

## 🚀 How to Run

1. **Clone the repository:**

   git clone https://github.com/oriac-gimeno/Python-SQL-PowerBI-Business-Simulation-IT-Academy.git
   cd Python-SQL-PowerBI-Business-Simulation-IT-Academy
Install dependencies (preferably in a virtual environment):

bash
pip install pandas numpy matplotlib seaborn scipy statsmodels scikit-learn mysql-connector-python jupyter
Run Jupyter Notebook:

bash
jupyter notebook
Open any of the .ipynb files and execute the cells.

Database connection (for the first notebook):
You will need access to the original MySQL database. The connection parameters are hardcoded in the notebook; adjust them or replace with your own data source.

Outputs: The notebooks generate cleaned data files and export results (CSV, plots) into the results/ folder (you may need to create it).

📊 Results & Visualizations
The analysis produces:

Correlation heatmaps of univariate associations.

Regression coefficient plots with confidence intervals.

Executive summary dashboards (within the notebook) that combine impact estimates and recommendations.

The PowerPoint presentation (PresentacionResultados_220925.pptx) summarises all insights and business proposals in a professional format.

Example visual (from the absenteeism analysis):

https://images/impacto_practico_4_variables.png

(Note: images are not included in the repo; they are generated during notebook execution.)

📬 Contact
GitHub: oriac-gimeno

LinkedIn: Oriac Gimeno

Portfolio: https://oriac-gimeno.github.io/

📄 License
This project is licensed under the MIT License – see the LICENSE file for details.

⭐ If you find this project useful, please consider giving it a star on GitHub!

