# 🏦 Smart Fraud Detection System

![Python](https://img.shields.io/badge/Python-3.8+-blue)
![XGBoost](https://img.shields.io/badge/XGBoost-Enabled-orange)
![TensorFlow](https://img.shields.io/badge/TensorFlow-LSTM-yellow)
![License](https://img.shields.io/badge/License-MIT-green)

## 📌 Project Overview

This project is an AI system built to catch financial fraud. Instead of just guessing if a transaction is fraud or not, this system is built like a real business tool: it focuses on catching bad guys while making sure good customers don't get accidentally blocked.

Out of 1.78 million transactions, this AI **automated 99.44% of the decisions**. It left only a tiny fraction (0.56%) for humans to review manually, saving massive amounts of time and operational costs.

## 🧠 How It Works — Two-Stage Pipeline

**Stage 1 — Fast Filter (XGBoost)**
A tuned XGBoost model scans every transaction and makes a quick call: auto-approve the safe ones, and send only the suspicious ones (~1.4% of traffic) forward for deeper inspection. The decision threshold isn't arbitrary — it's mathematically calculated to guarantee a maximum number of missed frauds, based on business risk tolerance.

**Stage 2 — Deep Inspection (LSTM)**
Transactions flagged by Stage 1 go through an LSTM model that looks at each customer's last 5 transactions as a sequence — catching fraud patterns that only show up over time (e.g. unusual spending bursts), not just in a single transaction. This stage makes the final call: auto-approve, auto-reject, or send to a human review dashboard.

**Baseline Comparison**
Logistic Regression and Random Forest models were also trained under the same business constraints to benchmark XGBoost's performance. XGBoost significantly outperformed both, requiring the smallest review queue to hit the same fraud-recall target.

## 📊 Key Results

| Metric | Value |
|---|---|
| Total transactions processed | 1,782,993 |
| Overall automation rate | 99.44% |
| Sent to human review | 0.56% |
| Stage 1 review queue | 1.40% of traffic |
| Fraud caught | ~93% of all fraud |

## 🗂️ Repository Structure
├── fraud-detection-project.ipynb   # Main notebook (full pipeline)

├── __notebook_source__.ipynb       # Kaggle-exported source

├── business_xgb_model.json         # Trained Stage 1 XGBoost model

├── business_lr_model.pkl           # Baseline Logistic Regression model

├── business_rf_model.pkl           # Baseline Random Forest model

├── requirements.txt                # Python dependencies

└── README.md


## ⚙️ Setup & Usage

1. Clone the repo:
```bash
   git clone https://github.com/karishmas0/Financial-Fraud-Detection-System.git
   cd Financial-Fraud-Detection-System
```

2. Install dependencies:
```bash
   pip install -r requirements.txt
```

3. Open and run `fraud-detection-project.ipynb` (update `DATA_DIR` path to point to your dataset).

## 🔗 Links

👉 [View the full Code, Dataset, and trained Model on Kaggle](https://www.kaggle.com/code/karishmas24/fraud-detection-project/edit)

## 🛠️ Tech Stack

- **Python 3.8+**
- **XGBoost** — Stage 1 fast filtering
- **TensorFlow / Keras (LSTM)** — Stage 2 sequence-based detection
- **Optuna** — hyperparameter and threshold tuning
- **scikit-learn** — Logistic Regression & Random Forest baselines

## 👤 Contributor

**Karishma Singh** ([@karishmas0](https://github.com/karishmas0))
