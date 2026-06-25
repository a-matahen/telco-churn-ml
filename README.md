# Customer Churn Prediction

A machine learning project that predicts which telecom customers are likely to cancel their subscription. Built end-to-end: from raw data through cleaning, exploratory analysis, feature engineering, and model comparison — with a focus on handling real-world class imbalance.

---

## Problem statement

A telecom company loses revenue every time a customer churns. If we can predict *who* is likely to leave, the business can intervene early with a retention offer. This project answers: **can we predict churn before it happens, and which model does it best?**

---

## Dataset

[IBM Telco Customer Churn](https://github.com/IBM/telco-customer-churn-on-icp4d/blob/master/data/Telco-Customer-Churn.csv) — a publicly available dataset with:
- 7,043 customers
- 21 features (contract type, tenure, monthly charges, internet service, payment method, etc.)
- Target variable: `Churn` (Yes / No) — 26.5% of customers churned

---

## Project structure

```
customer-churn-prediction/
├── Codes/
|   ├── 01_explore_and_clean.py
|   ├── 02_visualize.py
|   └── 03_train_models.py
├── data/
│   ├── telco_churn.csv              # raw dataset
│   └── telco_churn_clean.csv        # cleaned version 
├── outputs/
│   ├── 01_churn_distribution.png
│   ├── 02_churn_by_contract.png
│   ├── 03_tenure_vs_churn.png
│   ├── 04_charges_vs_churn.png
│   └── model_comparison.csv

├── .gitignore
├── requirements.txt
└── README.md
```

---

## How to run it

**1. Clone the repo**
```bash
git clone https://github.com/a-matahen/telco-churn-ml
cd customer-churn-prediction
```

**2. Install dependencies**
```bash
pip install -r requirements.txt
```

**3. Run the pipeline in order**
```bash
python 01_explore_and_clean.py    # clean the data
python 02_visualize.py            # generate charts
python 03_train_models.py         # train and evaluate models
```

All outputs (charts, model comparison table) are saved to the `outputs/` folder.

---

## What each script does

### `01_explore_and_clean.py` — Data cleaning
- Found that `TotalCharges` was stored as a string type due to 11 hidden blank values (all new customers with zero tenure and no bill yet)
- Converted `TotalCharges` to numeric and filled blanks with `0` — the correct value for a customer with no charges yet
- Dropped the `customerID` column (label, not a feature)
- Encoded the target column: `Yes → 1`, `No → 0`

### `02_visualize.py` — Exploratory analysis
Produced 4 charts that answer: *what actually drives churn?*

Key finding: **contract type is the strongest predictor of churn**

| Contract type | Churn rate |
|---|---|
| Month-to-month | 42.7% |
| One year | 11.3% |
| Two year | 2.8% |

Customers on short contracts churn at 15x the rate of customers on long-term contracts. New customers (low tenure) also churn disproportionately — most churn happens in the first 12 months.

### `03_train_models.py` — Model training and evaluation
- Encoded all categorical features using one-hot encoding
- Scaled numeric features with `StandardScaler`
- Split data 80/20 with stratification to preserve the 73/27 class ratio
- Trained and evaluated 3 models: Logistic Regression, Decision Tree, Naive Bayes

---

## Results

| Model | Accuracy | Precision | Recall | F1 Score |
|---|---|---|---|---|
| **Logistic Regression** | 0.807 | 0.658 | 0.567 | **0.609** |
| Decision Tree | 0.794 | 0.631 | 0.540 | 0.582 |
| Naive Bayes | 0.656 | 0.427 | 0.866 | 0.572 |

**Winner: Logistic Regression** — highest F1 score, best overall balance between catching churners and avoiding false alarms.

### Why F1 score — not accuracy

The dataset is imbalanced: 73% of customers stayed, 27% churned. A model that always predicts "no churn" would achieve 73% accuracy while catching zero actual churners — useless for the business. F1 score penalizes this by combining precision (are your churn predictions correct?) and recall (are you catching all the churners?).

### The Naive Bayes tradeoff

Naive Bayes has the lowest accuracy (65.6%) but the highest recall (86.6%) — it catches the most churners, at the cost of more false alarms. In a real business context, this might still be the right choice: the cost of missing a churner (lost revenue) is often higher than the cost of a false alarm (sending an unnecessary retention email).

---

## Key takeaways

- Feature engineering matters: fixing the `TotalCharges` dtype bug was a real data quality issue, not just a formatting step
- Class imbalance changes which metric you optimize for — accuracy alone is misleading
- Logistic Regression outperformed more complex models (Decision Tree) on this dataset, which is common when features are mostly binary/categorical after encoding
- Contract type alone could power a simple business rule — customers on month-to-month contracts are the highest-risk segment

---

## Tech stack

- Python 3.x
- pandas — data cleaning and manipulation
- scikit-learn — model training and evaluation
- matplotlib / seaborn — data visualization

---

## Next steps

- [ ] Apply `class_weight='balanced'` or SMOTE to directly address class imbalance
- [ ] Add `GridSearchCV` hyperparameter tuning for the Decision Tree
- [ ] Try Random Forest or XGBoost for comparison
- [ ] Build a simple prediction API with Flask or FastAPI
- [ ] Add a feature importance chart for Logistic Regression coefficients
