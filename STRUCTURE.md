# 📁 Project Structure Guide

This document explains the purpose of every folder and file in this repository.
Read this before adding any new file so it lands in the right place.

---

## Repository Layout

```
malaria-outbreak-prediction-environmental-risk-analysis/
│
├── data/
│   ├── raw/
│   │   └── Malaria_outbrea_Dataset_IoT_generated_and_Epidem.csv
│   └── processed/
│
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_eda.ipynb
│   ├── 03_feature_engineering.ipynb
│   └── 04_predictive_model.ipynb
│
├── sql/
│   ├── 01_outbreak_patterns.sql
│   ├── 02_environmental_analysis.sql
│   ├── 03_regional_comparison.sql
│   └── 04_risk_indicators.sql
│
├── powerbi/
│
├── reports/
│
├── images/
│
├── docs/
│
├── README.md
├── STRUCTURE.md          ← you are here
├── requirements.txt
└── .gitignore
```

---

## Folder & File Reference

### `data/`
Holds all dataset files. Never commit sensitive or personally identifiable data.

| Subfolder | What goes here |
|---|---|
| `raw/` | The original, untouched dataset exactly as downloaded from Kaggle. **Never edit files here.** This project uses a single CSV file containing both IoT environmental readings and epidemiological records. |
| `processed/` | Cleaned and transformed datasets produced by the notebooks. The main output will be `malaria_cleaned.csv`. Feature-engineered versions (e.g. with lag variables or risk scores) also live here. |

---

### `notebooks/`
All Jupyter notebooks for Python-based analysis. Numbered to show the order they must be run in — each notebook depends on the output of the one before it.

| File | Purpose |
|---|---|
| `01_data_cleaning.ipynb` | Load the raw CSV, inspect structure, handle missing values, fix data types (especially date/time columns from IoT readings), and save the cleaned file to `data/processed/`. Run this **first**. |
| `02_eda.ipynb` | Exploratory Data Analysis — environmental trend charts, outbreak frequency over time, regional comparisons, and correlation analysis between environmental variables and malaria cases. |
| `03_feature_engineering.ipynb` | Prepare features for modelling — create lag variables (e.g. rainfall 2 weeks prior), encode categorical variables, build a binary outbreak target column, and save the model-ready dataset to `data/processed/`. |
| `04_predictive_model.ipynb` | Train and evaluate a classification model to predict outbreak risk. Compare at least two algorithms (e.g. Logistic Regression vs Random Forest). Report accuracy, precision, recall, and feature importance. |

> **Tip:** Keep markdown cells in every notebook explaining what you are doing and why.
> This turns your notebook into a story, not just code — which is exactly what a
> portfolio reviewer wants to see.

---

### `sql/`
SQL query files organized by analysis theme. Each file should have a comment block at the top stating its purpose, and a comment above each query explaining the business question it answers.

| File | Covers |
|---|---|
| `01_outbreak_patterns.sql` | Outbreak frequency over time, monthly and seasonal trends, outbreak duration |
| `02_environmental_analysis.sql` | Average environmental readings (temperature, humidity, rainfall) by period, correlation flags |
| `03_regional_comparison.sql` | Outbreak counts by region, highest-risk areas, region-level environmental averages |
| `04_risk_indicators.sql` | Define high-risk environmental thresholds, flag high-risk records, outbreak rate under different conditions |

---

### `powerbi/`
Power BI dashboard files (`.pbix`). Each dashboard is a separate file targeting a different audience or analysis angle.

| File (planned) | Covers |
|---|---|
| `01_malaria_outbreak_overview.pbix` | Outbreak frequency over time, regional outbreak map, case trends |
| `02_environmental_monitoring.pbix` | Temperature, humidity, and rainfall trends; environmental readings vs outbreak events |
| `03_risk_assessment.pbix` | Predicted risk scores by region and period, high-risk zone highlights, intervention priority areas |

> **Note:** `.pbix` files cannot be previewed on GitHub. Always export a PDF snapshot
> of each finished dashboard and save it to `reports/` so reviewers can see the
> work without opening Power BI.

---

### `reports/`
Written outputs and exported visuals — anything that summarises or presents findings.

| File (planned) | Description |
|---|---|
| `final_report.md` | Full project write-up: background, methodology, EDA findings, model results, and public health recommendations |
| `executive_summary.md` | One-page plain-English summary for a public health or non-technical audience |
| `dashboard_01_snapshot.pdf` | PDF export of the Outbreak Overview dashboard |
| `dashboard_02_snapshot.pdf` | PDF export of the Environmental Monitoring dashboard |
| `dashboard_03_snapshot.pdf` | PDF export of the Risk Assessment dashboard |

---

### `images/`
Screenshots and charts used inside the `README.md` or other documentation files.

| What goes here |
|---|
| Dashboard screenshots embedded in the README |
| Key EDA charts (e.g. rainfall vs outbreak frequency) worth highlighting at a glance |
| Model performance visuals (e.g. confusion matrix, feature importance chart) |

> **Naming tip:** Use descriptive names like `eda_rainfall_vs_cases.png` or
> `model_feature_importance.png` rather than `chart1.png`.

---

### `docs/`
Supporting documents that provide context for the project.

| File (planned) | Description |
|---|---|
| `linkedin_post_draft.md` | Draft of the LinkedIn portfolio post for this project |
| `data_dictionary.md` | Definitions for each column in the dataset — especially important here since the dataset mixes IoT sensor fields with epidemiological fields |

> **Priority note:** Write the `data_dictionary.md` early in this project. The dataset
> combines two very different data sources (IoT sensors + health records) and column
> names may not be self-explanatory. Documenting them upfront will save confusion later.

---

### Root-level Files

| File | Purpose |
|---|---|
| `README.md` | Main project page visible on GitHub. Should include project overview, tools used, key findings, and links to notebooks and dashboards. Update this last once the project is complete. |
| `STRUCTURE.md` | This file. Explains the repo layout so any collaborator or reviewer understands where things live. |
| `requirements.txt` | Lists all Python packages needed to run the notebooks. Run `pip install -r requirements.txt` to install them. Includes `scikit-learn` for predictive modelling. |
| `.gitignore` | Tells Git which files to ignore (checkpoint files, system files, etc.). Do not delete this. |
| `.gitkeep` | Empty placeholder files used to track empty folders in Git. Delete them once real files are added to that folder. |

---

## Rules to Follow

1. **Never edit files in `data/raw/`** — treat the original dataset as read-only.
2. **Run notebooks in order** — each notebook builds on the output of the previous one. Start with `01`, then `02`, and so on.
3. **Write the data dictionary early** — this dataset combines IoT and epidemiological fields; document column meanings in `docs/data_dictionary.md` as you explore.
4. **Comment your SQL** — every query needs a comment explaining the business question it answers.
5. **Save the model** — in `04_predictive_model.ipynb`, export the trained model using `joblib` and save it to `data/processed/` so it can be reloaded without retraining.
6. **Export dashboard PDFs** — always save a PDF snapshot of Power BI dashboards to `reports/` before closing.
7. **Update the README last** — once the project is done, add screenshots, model results, and findings.
8. **Delete `.gitkeep` files** once real files have been added to that folder.