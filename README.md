# 🚨 Two-Stage Cascaded Fraud Detection Pipeline (XGBoost + Deep LSTM)

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![XGBoost](https://img.shields.io/badge/XGBoost-GPU--Accelerated-orange)
![TensorFlow/Keras](https://img.shields.io/badge/TensorFlow-Deep%20Learning-FF6F00)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Cascade%20Architecture-success)

## 📌 Project Overview
Financial fraud detection systems often struggle with a critical trade-off: catching frauds (High Recall) vs. not blocking genuine customers (High Precision). Single-model systems either let frauds slip through or cause massive customer friction by blocking legitimate transactions.

This project implements an enterprise-grade **2-Stage Cascaded Machine Learning Architecture** to solve this. It processes over 1.7 Million transactions using a fast tree-based model for initial filtering, followed by a Deep Learning sequence model to analyze temporal behavioral patterns.

---

## 🧠 System Architecture

### 🛡️ Stage 1: The "High-Recall" Filter (XGBoost)
* **Goal:** Catch ~99% of all frauds, zero tolerance for false negatives.
* **Mechanism:** A GPU-accelerated XGBoost Classifier acts as the first line of defense. It processes 100% of the traffic.
* **Logic:** If a transaction is extremely safe, it is **Auto-Approved**. If there is even a slight doubt (based on an AI-optimized threshold), it is tagged as "Doubtful" and routed to Stage 2.
* **Trade-off:** Deliberately accepts a low precision (~1%) to guarantee a 99%+ recall. 

### 🕵️ Stage 2: The "High-Precision" Sequence Analyzer (Deep LSTM)
* **Goal:** Eliminate False Positives and clear genuine customers blocked by Stage 1.
* **Mechanism:** A multi-layered Deep LSTM Neural Network.
* **Logic:** Instead of looking at a single transaction, the LSTM converts the data into **Sliding Windows (Lookback = 5)**. It evaluates the user's sequential behavior over their last 5 transactions to find deep temporal patterns.
* **Result:** It accurately separates genuine users with heavy spending habits from actual fraudsters, minimizing customer friction.

---

## 📊 Key Business Metrics & Impact

The system was evaluated on a test dataset of **1,782,993** transactions. 

### Stage 1 (XGBoost) Performance:
* **True Positives (Frauds Caught):** 2,640
* **False Negatives (Missed Frauds):** Only 26
* **True Negatives (Auto-Approved):** 1,534,825
* **Recall:** 99.02%
* **Precision:** 1.06% (By design, passed to Stage 2)

### System-Level Impact:
* **High Automation Rate:** Successfully automates decision-making for the vast majority of traffic without human intervention.
* **Minimal Customer Friction:** Safe transactions are cleared in milliseconds.
* **Reduced Manual Review Workload:** Only highly complex cases are routed to the human React Dashboard.

---

## 📁 Model Artifacts & Deployment Files

The repository includes the exported, production-ready model weights:
* `stage1_xgb.json`: The trained XGBoost decision trees and threshold rules.
* `stage2_lstm.keras`: The Deep Learning architecture, weights, and biases for temporal sequence processing.
* `scaler.pkl`: The StandardScaler object to normalize real-time incoming streaming data before LSTM inference.

---

## 🛠️ Tech Stack
* **Data Processing:** Pandas, NumPy, Scikit-Learn
* **Machine Learning:** XGBoost (`tree_method="hist"`, `device="cuda"`)
* **Deep Learning:** TensorFlow / Keras (Sequential, LSTM, BatchNormalization, Dropout)
* **Evaluation:** Precision-Recall Curves, Confusion Matrix, Classification Report

---

## 🚀 How to Run (Inference)

To use these models on new data:

```python
import joblib
import pandas as pd
from tensorflow.keras.models import load_model

# 1. Load the Artifacts
xgb_model = joblib.load('stage1_xgb.json')  # Or use xgb.Booster
scaler = joblib.load('scaler.pkl')
lstm_model = load_model('stage2_lstm.keras')

# 2. Stage 1 Prediction (Replace X_new with your data)
# Apply your Stage 1 threshold logic here...

# 3. Stage 2 Processing
# Scale doubtful data, create sequences (lookback=5), and predict using lstm_model
