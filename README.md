# Telco Customer Churn Prediction

## Overview

This project develops a machine learning solution to predict customer churn for a telecommunications company. The objective is to identify customers who are likely to leave the service, allowing the business to take proactive retention actions.

The project follows a complete machine learning workflow, including:

* Data preprocessing
* Exploratory Data Analysis (EDA)
* Feature engineering
* Model training
* Model evaluation
* Power BI dashboard visualization

---

## Dataset

**Dataset:** Telco Customer Churn

The dataset contains customer demographic information, account details, subscribed services, and whether the customer has churned.

### Target Variable

* **Churn**

  * 0 → Customer Stayed
  * 1 → Customer Churned

---

## Project Structure

```text
ML-PROJECTT/
│
├── Codes/
│   ├── pipeline.ipynb
│   ├── train_models.ipynb
│   └── visuals.ipynb
│
├── dashboard/
│   ├── model_comparison_visuals.pbix
│   └── dashboard.pdf
│
├── data/
│   ├── Telco-Customer-Churn.csv
│   ├── telco_churn_clean.csv
│   └── model_comparison.csv
│
├── outputs/
│   ├── 02_churn.png
│   ├── 03_churn.png
│   ├── 04_charges_vs_churn.png
│   ├── 05_charges_vs_churn.png
│   └── 05_tenure_vs_churn.png
│
├── requirements.txt
└── README.md
|__ .gitignore
ه Ii
```

---

## Machine Learning Pipeline

### 1. Data Preprocessing

* Missing value handling
* Duplicate removal
* Data cleaning
* Feature encoding using One-Hot Encoding
* Feature scaling using StandardScaler

---

### 2. Exploratory Data Analysis

Visualizations include:

* Churn Distribution
* Monthly Charges vs Churn
* Total Charges Analysis
* Customer Tenure Analysis
* Correlation Analysis

---

### 3. Models

The following classification algorithms were trained and compared:

* Logistic Regression
* Decision Tree Classifier
* Gaussian Naive Bayes

---

## Evaluation Metrics

Models were evaluated using:

* Accuracy
* Precision
* Recall
* F1 Score
* Confusion Matrix
* Classification Report

Because the dataset is imbalanced, **F1 Score** was used as the primary metric for comparing model performance.

---

## Power BI Dashboard

The project includes an interactive Power BI dashboard for comparing model performance.

Dashboard features include:

* Model Performance Comparison
* Accuracy Comparison
* Precision Comparison
* Recall Comparison
* F1 Score Comparison
* Model Ranking

Power BI file:

```text
dashboard/model_comparison_visuals.pbix
```

Dashboard PDF:

```text
dashboard/dashboard.pdf
```

---

## Technologies Used

### Programming

* Python 3

### Libraries

* pandas
* NumPy
* matplotlib
* seaborn
* scikit-learn

### Visualization

* Power BI

---

## Installation

Clone the repository

```bash
git clone https://github.com/a-matahen/ML-PROJECTT.git
```

Move into the project

```bash
cd ML-PROJECTT
```

Install dependencies

```bash
pip install -r requirements.txt
```

---

## How to Run

1. Open **pipeline.ipynb**
2. Execute data preprocessing.
3. Open **train_models.ipynb**
4. Train and evaluate the machine learning models.
5. Open **visuals.ipynb**
6. Generate visualizations.
7. Open the Power BI dashboard to explore model performance.

---

## Results

The trained models were compared using multiple evaluation metrics to determine the best-performing classifier.

The comparison includes:

* Accuracy
* Precision
* Recall
* F1 Score

Results are exported as:

```text
data/model_comparison.csv
```

---

## Future Improvements

* Random Forest
* XGBoost
* LightGBM
* Hyperparameter tuning using GridSearchCV
* Cross-validation
* Model deployment using Flask or FastAPI
* Interactive web application using Streamlit

---

## Author

**Abdalrahman Matahen**

AI & Data Science Student

GitHub:
https://github.com/a-matahen
