# 🏦 End-to-End Business-Constrained Fraud Detection Pipeline

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![XGBoost](https://img.shields.io/badge/XGBoost-Enabled-orange.svg)
![TensorFlow](https://img.shields.io/badge/TensorFlow-LSTM-yellow.svg)
![Optuna](https://img.shields.io/badge/Optuna-Hyperparameter%20Tuning-red.svg)

## 📌 Executive Summary
This project implements an advanced, two-stage machine learning pipeline designed to process financial transactions at scale. Instead of relying on a single model and a standard 0.5 probability threshold, this system is optimized for **strict business constraints**: minimizing False Negatives (missed fraud) while drastically reducing the Human-in-the-Loop (HITL) review queue.

The system achieved a **99.44% total automation rate** on 1.78 million transactions, safely auto-approving good customers and confidently blocking fraud, leaving less than 0.6% of traffic for manual review.

## 🏗️ System Architecture

### Stage 1: The Frontline Filter (XGBoost)
* **Goal:** High-speed processing and strict risk capping.
* **Mechanism:** An XGBoost classifier tuned to capture the vast majority of safe traffic. A custom dynamic threshold is mathematically derived to ensure the model misses no more than 175 fraudulent transactions.
* **Outcome:** Auto-approves the obvious non-fraud traffic and routes the uncertain "grey area" traffic to the Stage 2 review queue.

### Stage 2: The Deep Sequence Rescuer (LSTM)
* **Goal:** False Positive rescue and final automated rejection.
* **Mechanism:** A deep learning Long Short-Term Memory (LSTM) network that looks at the sequential history of the flagged user (N=5 lookback) and calculates the temporal gap between transactions (`id_gap_since_last_tx`).
* **Outcome:** Uses a dual-threshold optimization (found via Optuna) to "rescue" good customers who were mistakenly flagged by Stage 1, while auto-rejecting obvious fraud. Only the hardest edge cases are sent to the manual React Dashboard.

## 📊 Final Business Metrics

The pipeline was tested on **1,782,993** transactions with the following real-world routing outcomes:

| Routing Decision | Transaction Count | Percentage of Traffic |
| :--- | :--- | :--- |
| **Stage 1 Auto-Approved** | 1,755,426 | 98.45% |
| **Stage 2 Auto-Approved (Rescue)** | 14,991 | 0.84% |
| **Stage 2 Auto-Rejected (Blocked)** | 2,654 | 0.15% |
| **Routed to Manual Dashboard** | **9,922** | **0.56%** |

* **Total System Automation Rate:** `99.44%`
* **Stage 2 F1-Score (Auto-Reject):** `0.6450`

### Automated Blocking Errors (Pre-Human Review)
* **Hard False Negatives (Missed Fraud):** 318
* **Hard False Positives (Good users blocked):** 995

## 🛠️ Technologies Used
* **Data Processing:** `Pandas`, `NumPy`, `Scikit-Learn`
* **Machine Learning:** `XGBoost` (Hist-tree method on GPU)
* **Deep Learning:** `TensorFlow` / `Keras` (LSTM, Masking, Dropout)
* **Hyperparameter Optimization:** `Optuna` (Custom objective functions calculating business cost)

## 📁 Repository Structure
* `final-fraud-detection-project.ipynb`: The complete, runnable Kaggle notebook containing both Stage 1 and Stage 2 pipelines.
* `business_xgb_model.json`: The exported, production-ready XGBoost model from Stage 1.

## 🚀 Key Takeaways & Methodologies
1. **Dynamic Thresholding:** Proved that precision/recall trade-offs must be dictated by business metrics (e.g., maximum acceptable financial loss), not default probability scores.
2. **Sequential Feature Engineering:** Demonstrated that a user's transaction velocity (time since last transaction) is a critical indicator of account takeover or card testing.
3. **Dual-Threshold Optuna Search:** Built a custom loss function in Optuna that penalized the model dynamically based on the financial cost of manual review ($/ticket) vs. the cost of a missed fraud.
