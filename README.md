# 🛍️ Retail Sales – Exploratory Data Analysis
### CS667 – Practical Data Science | Spring 2026 | Project #1

![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.x-150458?logo=pandas&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-Interactive-3F4F75?logo=plotly&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?logo=scikit-learn&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

---

## 📌 Project Overview

A full **Exploratory Data Analysis (EDA)** pipeline on a retail sales dataset sourced from Kaggle. The goal is to uncover patterns in customer behavior, sales trends, and product performance — and translate those findings into actionable business recommendations.

This project covers the complete EDA workflow:
- Data loading, cleaning & validation
- Descriptive statistics & distribution analysis
- Bivariate & multivariate visualizations
- Time-series & seasonality analysis
- Outlier detection (IQR + Z-score)
- Feature engineering (time-based, RFM, encoding, log transforms)
- Feature importance estimation

---

## 📁 Repository Structure

```
retail-sales-eda/
│
├── CS667_Project1_EDA.ipynb     # Main Jupyter Notebook (full analysis)
├── retail_sales.xlsx            # Dataset (1,000 transactions)
├── README.md                    # This file
└── requirements.txt             # Python dependencies
```

---

## 📊 Dataset

**File:** `retail_sales.xlsx`  
**Source:** Kaggle – Retail Sales Customer Shopping Dataset  
**Size:** 1,000 transactions | 9 columns | Jan 2023 – Jan 2024

| Column | Type | Description |
|---|---|---|
| `Transaction ID` | int | Unique ID per transaction |
| `Date` | datetime | Date of purchase |
| `Customer ID` | str | Unique customer identifier |
| `Gender` | str | Male / Female |
| `Age` | int | Customer age (18–64) |
| `Product Category` | str | Beauty / Clothing / Electronics |
| `Quantity` | int | Units purchased (1–4) |
| `Price per Unit` | int | Unit price ($25–$500) |
| `Total Amount` | int | Total transaction value ($25–$2,000) |

---

## 🔍 Analysis Sections

| # | Section | Key Techniques |
|---|---|---|
| 1 | Setup & Imports | Library configuration |
| 2 | Load & Inspect | Shape, dtypes, null check, duplicate check |
| 3 | Data Cleaning | Consistency validation, snake_case normalization |
| 4 | Descriptive Statistics | `.describe()`, revenue by category, value counts |
| 5 | Univariate Analysis | Histograms, KDE plots, box plots, pie charts |
| 6 | Bivariate & Multivariate | Heatmaps, grouped bar charts, scatter plots, pair plots |
| 7 | Time-Series Analysis | Monthly resampling, rolling averages, seasonality |
| 8 | Outlier Detection | IQR method, Z-score method, spike detection |
| 9 | Feature Engineering | Time features, holiday proximity, RFM, log transforms |
| 10 | Feature Importance | Correlation ranking vs. target variable |
| 11 | Business KPIs | Summary dashboard of key metrics |

---

## 💡 Key Findings

- **Electronics** generates the highest revenue per transaction (~$597 avg) despite having fewer transactions than Clothing or Beauty — driven by $300–$500 price points
- **Price per unit** has a ~0.89 correlation with total amount — it is the single strongest predictor of spend
- A measurable **Q4 holiday uplift** exists; transactions near major holidays show higher average values
- Most customers have **low purchase frequency** (1–2 transactions), pointing to a retention opportunity
- `total_amount` is **right-skewed** (skew ~1.8) — log transformation reduces this to near zero, improving model readiness
- Outliers are **legitimate** high-value Electronics bulk purchases, not data errors — retained in the dataset

---

## 🏗️ Feature Engineering Summary

| Feature | Type | Description |
|---|---|---|
| `month`, `quarter` | Time | Extracted from transaction date |
| `day_of_week_num` | Time | 0 = Monday … 6 = Sunday |
| `is_weekend` | Binary | 1 if Saturday or Sunday |
| `week_of_year` | Time | ISO week number |
| `days_to_holiday` | Numeric | Days to nearest US holiday |
| `near_holiday` | Binary | 1 if within 7 days of a holiday |
| `Recency` | RFM | Days since customer's last purchase |
| `Frequency` | RFM | Total transactions per customer |
| `Monetary` | RFM | Total spend per customer |
| `log_total_amount` | Transform | log1p of total_amount (reduces skew) |
| `log_price_per_unit` | Transform | log1p of price_per_unit |

---

## ⚙️ Setup & Installation

### 1. Clone the repository
```bash
git clone https://github.com/your-username/retail-sales-eda.git
cd retail-sales-eda
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Launch the notebook
```bash
jupyter notebook CS667_Project1_EDA.ipynb
```

> **Google Colab:** Upload both `CS667_Project1_EDA.ipynb` and `retail_sales.xlsx` to your Colab session, then run all cells.

---

## 📦 Requirements

```
pandas
numpy
matplotlib
seaborn
scipy
scikit-learn
plotly
openpyxl
jupyter
```

Install all at once:
```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn plotly openpyxl jupyter
```

> ⚠️ **Pandas version note:** This notebook uses `resample('M')` for monthly resampling. If you are on **pandas ≥ 2.2**, replace `'M'` with `'ME'` (Month End) throughout the notebook.

---

## 📈 Visualizations Included

- Distribution histograms with KDE curves for all numeric features
- Box plots for outlier visualization
- Pie chart — gender split
- Bar charts — category counts, revenue by category, revenue by age group
- Grouped bar chart — average transaction by gender × category
- Correlation heatmap
- Interactive Plotly line chart — monthly revenue trend
- Interactive Plotly multi-line chart — monthly revenue by category
- Interactive Plotly grouped bar — revenue by age group × category
- Seasonality bar charts — day of week and month averages
- Daily revenue with 30-day rolling average overlay
- Log transformation before/after histograms

---

## 🎯 Business Recommendations

| Priority | Finding | Recommended Action |
|---|---|---|
| 🔴 High | Electronics drives majority of revenue | Pre-stock inventory before Q4; protect this category |
| 🔴 High | Most customers buy only once | Launch loyalty program + post-purchase email sequences |
| 🟠 Medium | Holiday uplift is real and measurable | Run promotions starting October to capture early shoppers |
| 🟠 Medium | 36–55 age group spends the most | Focus ad spend and creatives on this demographic |
| 🟡 Low | Gender preferences differ by category | Personalize recommendations by category affinity |
| 🟡 Low | EWMA reveals demand cycles | Use rolling forecasts for smarter inventory ordering |

---

## 🔭 Future Work

- [ ] Customer segmentation using K-Means clustering on RFM features
- [ ] Demand forecasting with SARIMA or Facebook Prophet
- [ ] Sales prediction model using engineered features
- [ ] A/B test design for loyalty program impact measurement
- [ ] Dashboard deployment with Streamlit or Dash

---

## 👤 Author

**Course:** CS667 – Practical Data Science (CRN: 23102)  
**Institution:** Pace University  
**Semester:** Spring 2026  
**Professor:** Prof. Sarbanes  

---

## 📄 License

This project is for academic purposes only. Dataset sourced from [Kaggle](https://www.kaggle.com).
