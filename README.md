# Credit Card Fraud Detection  
## Risk-Focused Exploratory Analysis & Baseline Modeling

📊 **Dataset:** European cardholders credit card transactions  
🔗 **Source:** https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud  


## Project Overview

This project explores credit card transaction data with the goal of **understanding fraud risk patterns** and building **baseline, interpretable machine learning models** for fraud detection.

Rather than focusing on raw prediction accuracy, the analysis emphasizes:

- Risk identification  
- Class imbalance awareness  
- Business-aligned evaluation metrics  
- Transparent and explainable modeling  

The work is structured into three notebooks:

1. **Exploratory Data Analysis (EDA) & Risk Insights**  
2. **Data Preprocessing & Logistic Regression**  
3. **Random Forest Modeling & Threshold Tuning**


## Dataset Summary

- **Total transactions:** 284,807  
- **Fraud cases:** 492  
- **Fraud rate:** ~0.17%  
- **Features:**
  - `V1–V28`: anonymized PCA components  
  - `Time`: seconds since first transaction  
  - `Amount`: transaction value  
  - `Class`: fraud label (1 = fraud, 0 = normal)

⚠️ The dataset is **extremely imbalanced**, making accuracy an unreliable metric.


## Notebook 1: Exploratory Data Analysis (EDA)

### Objective

Understand **where and when fraud risk concentrates**, and extract insights relevant to **risk controls and mitigation**.

### Key Analyses

- Transaction amount distributions (linear & log scale)  
- Fraud vs normal transaction comparison (density-based)  
- Time-based behavior (`Time` → `Hour`)  
- Fraud rate by hour of day  
- Amount-based risk segmentation  

### Key Findings

- Fraud is **not uniformly distributed**
- Fraud risk:
  - Concentrates in **low-value transactions**
  - Spikes during **early morning hours (≈2–4 AM)**
- High-value transactions are rare but represent **high financial exposure**

**Business Insight:**  
Fraudsters prioritize **stealth over value**, exploiting off-peak hours and small amounts to avoid detection.


## Notebook 2 and 3: Data Preprocessing & Logistic Regression

### Objective

Prepare a **model-ready dataset** and build an **interpretable baseline model**.

### Feature Engineering

- Standardized `Amount` and `Time`
- Cyclical encoding of transaction hour (`sin` / `cos`)
- High-amount risk flag (top 1% of transaction values)
- Optional amount banding for risk analysis

Processed datasets saved as:

- `X_preprocessed.csv`
- `Y_preprocessed.csv`


### Logistic Regression Model

- Class-weighted to handle imbalance
- Evaluated using **Precision–Recall AUC (PR-AUC)**

#### Results

- **PR-AUC:** ~0.72  
- Strong predictors include:
  - Transaction `Amount`
  - PCA components such as `V14`, `V12`, `V10`


### Threshold Tuning

- Threshold selected to achieve **~80% recall**
- Explicit trade-off between:
  - Fraud capture rate  
  - False positive cost  

**Interpretation:**  
Logistic Regression provides **clear directional insights** and serves as a transparent baseline for risk explanation.


## Notebook 4: Random Forest Modeling & Threshold Tuning

### Objective

Compare performance against a more flexible, non-linear model.

### Random Forest Model

- Class-weighted
- Evaluated using PR-AUC
- Same train/test split as Logistic Regression

#### Results

- **PR-AUC:** ~0.87  
- At ~80% recall:
  - **Precision:** ~95%
  - Significantly fewer false positives than Logistic Regression


### Key Observation

The Precision–Recall curve remains near **100% precision** for much higher recall values compared to Logistic Regression, indicating superior separation of fraud vs normal transactions.

**Trade-off:**

- Higher performance  
- Reduced interpretability compared to Logistic Regression  


## Model Comparison Summary

| Model               | PR-AUC |
|--------------------|--------|
| Logistic Regression | ~0.72  |
| Random Forest       | ~0.87  |


## Key Takeaways (Risk & Business Perspective)

- Fraud detection is a **risk management problem**, not a pure classification task
- Evaluation must prioritize:
  - Recall (fraud capture)
  - Precision (operational cost)
  - PR-AUC (performance under imbalance)
- Thresholds should be chosen based on **business tolerance for false positives**
- Interpretable models remain critical for trust and governance


## Tools & Libraries Used

- Python  
- Pandas, NumPy  
- Scikit-learn  
- Matplotlib, Seaborn  
- Jupyter Notebook  


## Transparency & AI Usage Disclosure

This project were developed with the assistance of **AI tools (ChatGPT)** 
All modeling decisions, interpretations, and final outputs were **reviewed, executed, and validated by the author**.  
AI was used as a **learning and productivity aid**, not a replacement for understanding.

