# Fintech Company Risk Profiling – Data Scientist Take-Home Assignment

## Project Overview

This project builds a **company financial risk profiling model** for a fintech credit decisioning system.
The goal is to estimate the **probability of distress (default proxy)** for SMEs, assign a **risk tier**, and implement a **decision policy** based on expected credit loss.

The solution follows a realistic fintech workflow:

**Data → Model → Probability of Default (PD) → Risk Tier → Decision Policy**

---

## Objective

* Predict financial distress using company financial ratios
* Build a company-level **risk profile**
* Create an **ECL-based approval policy**
* Provide explainable decision logic

---

## Dataset

**Taiwanese Bankruptcy Prediction Dataset (UCI)**

* Binary target: `Bankrupt?`
* Financial ratios of companies
* Highly imbalanced dataset (few bankrupt companies)

---

## Project Workflow

### 1. Data Understanding

* Checked dataset shape and data types
* Analyzed target class imbalance
* Performed stratified train-test split

---

### 2. Exploratory Data Analysis (EDA)

Created three business-focused visualizations:

* Class imbalance distribution
* Feature distribution comparison
* Correlation heatmap

**Key insights:**

* Dataset is highly imbalanced with very few bankrupt firms
* Profitability-related ratios strongly relate to bankruptcy
* Some financial ratios show strong correlations with risk

---

### 3. Modeling

Two models were trained:

#### Baseline Model

* Logistic Regression

#### Improved Model

* XGBoost (best performing model)

---

### Model Performance (Test Set)

| Model               | ROC-AUC   | PR-AUC |
| ------------------- | --------- | ------ |
| Logistic Regression | 0.917     | 0.319  |
| XGBoost             | **0.967** | 0.500  |

**Selected final model:** XGBoost

---

### Threshold Selection

A probability threshold of **0.20** was chosen.

Reason:

* Bankruptcy events are rare
* Missing a risky company is more costly than rejecting a safe one
* Lower threshold helps reduce expected losses

---

## 4. Company Risk Profile

Each company receives:

| Field       | Description                       |
| ----------- | --------------------------------- |
| PD          | Predicted probability of distress |
| Risk Tier   | A (low risk) to D (high risk)     |
| Top Reasons | Top 3 important features          |

### Risk Tier Logic

| Tier | PD Range    | Risk Meaning  |
| ---- | ----------- | ------------- |
| A    | < 0.05      | Very low risk |
| B    | 0.05 – 0.15 | Low risk      |
| C    | 0.15 – 0.30 | Medium risk   |
| D    | > 0.30      | High risk     |

---

## 5. Decision Policy (ECL Based)

### Assumptions

* **EAD (Exposure at Default):** $10,000
* **LGD (Loss Given Default):** 60%
* **ECL Formula:**
  `ECL = PD × LGD × EAD`

### Decision Rule

* Approve if **ECL < $1,200**
* Decline otherwise

This keeps expected loss per company within a conservative threshold.

---

## Portfolio Results (Test Set)

*(Values will depend on your notebook output)*

* Approval rate: **0.97%**
* Total expected loss: **$25195.56**
* Expected defaults: **4.2**

---

## Tech Stack

* Python
* pandas
* numpy
* scikit-learn
* XGBoost
* matplotlib

---

## Project Structure

```
── fintech_risk_assignment.ipynb
── requirements.txt
── README.md
```

---

## How to Run

1. Clone the repository:

```bash
git clone <repo-link>
cd fintech-risk-assignment
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Open the notebook:

```bash
jupyter notebook
```

4. Run all cells in:

```
fintech_risk_assignment.ipynb
```

---

## Key Takeaways

* XGBoost significantly improved risk prediction over logistic regression
* PD-based risk tiers provide clear business interpretation
* ECL-based decision rule enables practical credit policy

---

## Project Demo
Watch the Loom video here:
https://www.loom.com/share/ca940a1f1ab144019fe9a5aa4c7d1207

## Author

**Sahil Jahagirdar**
Data Science Graduate
Skills: Python, SQL, Machine Learning, Data Analysis
