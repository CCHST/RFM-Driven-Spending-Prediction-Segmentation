#  [Presentation Video Link](https://youtu.be/NYtbNUmiaeM?si=wv27IYVKiXjDnr9X)

# Credit Line Recommendation Using Customer Segmentation & Risk Analysis

## Project Summary

This project builds a **data-driven credit line recommendation system** using two main components:

1. **Customer Segmentation & Spending Prediction (Notebook 1)**
   - Segment customers using **RFM (Recency, Frequency, Monetary)** metrics
   - Predict future segment transitions using machine learning
   - Estimate each segment’s future spending behavior

2. **Risk Analysis & Credit Adjustment (Notebook 2)**
   - Build custom **risk flags** from multiple datasets
   - Aggregate behavior at **Q4 level**
   - Recommend personalized credit lines based on both behavior and risk

This end-to-end framework allows the organization to **better allocate credit**, **reduce risk**, and **identify growth opportunities**.

---


# 1_Customer Segmentation & Spending Prediction using RFM and Machine Learning.ipynb (Notebook 1)

## Project Overview

This project leverages **RFM (Recency, Frequency, Monetary)** analysis and machine learning models to:

1. **Segment customers** based on past behavior
2. **Predict future RFM segments**
3. **Estimate Q4 2025 spending** per customer group
4. **Visualize segment transitions** and generate actionable insights for credit line adjustments

---

## Data Period

- **Training & Observation**: July 2024 – March 2025
- **Training Target**: 2024 Q4
- **Prediction Input**: 2025 Q1
- **Prediction Target**: 2025 Q4 (estimated)

---

## Key Steps & Workflow

1. **Data Processing & Wrangling**
   - Handle missing values and drop duplicates
   - Filter transaction codes related to actual spending/purchases

2. **Data Integration**
   - Merge transaction records with customer and account datasets

3. **Historical Spending Pattern Analysis**
   - Explore trends in customer transaction behavior over time

4. **RFM Feature Engineering**
   - Convert transaction dates to datetime format
   - Filter observation period (e.g., July–September 2024)
   - Calculate RFM metrics per customer:
     - `Recency`: Days since last transaction
     - `Frequency`: Number of transactions
     - `Monetary`: Total spending amount

5. **Model Setup & Forecasting**
   - Use RFM scores from **2024 Q3** as input features (X)
   - Use **2024 Q4** RFM scores as prediction target (y)
   - Train a classifier (Random Forest) to learn customer segment transitions
   - Predict RFM segments for **Q4 2025** using Q1 2025 data

6. **Model Evaluation & Insights**
   - Evaluate model performance with accuracy and classification metrics
   - Generate a **transition matrix** to visualize customer movement across segments
   - Estimate potential **Q4 2025 spending** by predicted segment

---

# Risk Analysis & Credit Line Recommendation (Notebook 2)
## Project Purpose

This notebook performs account-level risk analysis and prepares a clean, structured dataset for credit line prediction and recommendation.
It integrates data from multiple domains, builds risk indicators, applies RFM segmentation, and outputs a Q4-level dataset ready for modeling.

---

## Main Dataset Sources

- `account_dim_20250325.csv` – Account metadata (activation status, balances, status flags)
- `statement_fact_20250325.csv` – Monthly billing cycle data (balances, return checks)
- `rams_batch_cur_20250325.csv` – RAMS features (utilization, credit line, behavior scores)
- `fraud_claim_case_20250325.csv` / `fraud_claim_tran_20250325.csv` – Reported fraud cases
- `syf_id_20250325.csv` – Customer ID cross-reference

---

## Key Steps & Workflow

### 1. Data Import and Cleaning
- Load all major datasets and convert account identifiers.
- Filter accounts: only keep **active**, **activated** accounts.
- Drop duplicates and remove negative or invalid entries.

### 2. Feature Engineering & Risk Flagging
The notebook creates **5 custom binary risk flags** per account-month:
- `external_risk_flag`
- `delinquency_flag`
- `return_check_flag`
- `overutilization_flag`
- `fraud_flag`

If any of these = 1, the account is labeled as **high risk** in that month.

### 3. Q4 Aggregation
- Keep only **October to December 2024** (Q4).
- Aggregate features to quarter level:
  - Numeric columns: average
  - Risk flags: set to 1 if triggered in any month
- Attach RFM segmentation data (`df_q4_rfm.csv`) to each account

### 4. Final Output
The output is a quarterly dataset with:
- Account ID
- RFM Score
- Risk Group (`High Risk` or `Low Risk`)
- Aggregated balances, utilization, and transaction history

## ▶️ How to Run

1. Place all raw data files in the `data/` folder.
2. Before running this notebook, make sure you have already completed
1_Customer Segmentation & Spending Prediction.ipynb
This will generate the necessary RFM segmentation results used in Step 4 of this notebook.
3. Launch Jupyter Notebook and open 2_Risk Analysis & Credit Line Recommendation.ipynb.
4. Run cells in order to:
   - Merge and clean data
   - Create risk flags
   - Aggregate to Q4
   - Join with RFM clusters