# 🏦 Smart Fraud Detection System

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![XGBoost](https://img.shields.io/badge/XGBoost-Enabled-orange.svg)
![TensorFlow](https://img.shields.io/badge/TensorFlow-LSTM-yellow.svg)

## 📌 Project Overview
This project is an AI system built to catch financial fraud. Instead of just guessing if a transaction is fraud or not, this system is built like a real business tool: it focuses on catching bad guys while making sure good customers don't get accidentally blocked. 

Out of 1.78 million transactions, this AI **automated 99.44% of the decisions**. It left only a tiny fraction (0.56%) for humans to review manually, saving massive amounts of time and operational costs.

👉 **[Click here to view the full Code, Dataset, and trained Model on Kaggle](https://www.kaggle.com/code/karishmas24/final-fraud-detection-project)**

## 🏗️ How It Works (The Two Steps)

### Step 1: The Quick Filter (XGBoost)
* **What it does:** This is the fast frontline defense. It looks at every transaction instantly.
* **The Goal:** It auto-approves all the obvious "safe" transactions and flags anything suspicious. We set a strict mathematical rule so it never misses more than 175 frauds.

### Step 2: The Deep Checker (LSTM Neural Network)
* **What it does:** For the tricky transactions that Step 1 wasn't sure about, Step 2 steps in. It looks at the user's past behavior (like how much time passed since their last purchase).
* **The Goal:** To "rescue" good customers who were accidentally flagged, and securely block real fraudsters. Only the absolute hardest cases are sent to a human worker.

## 📊 Final Results

The system was tested on **1,782,993** real-world transactions with these amazing results:

| Action Taken | Number of Transactions | Percentage |
| :--- | :--- | :--- |
| **Step 1: Auto-Approved (Safe)** | 1,755,426 | 98.45% |
| **Step 2: Rescued (Good Users)** | 14,991 | 0.84% |
| **Step 2: Auto-Blocked (Fraud)** | 2,654 | 0.15% |
| **Sent to Humans for Review** | **9,922** | **0.56%** |

* **Total AI Automation:** `99.44%`
* **Real Fraud Missed:** Only 318
* **Good Users Accidentally Blocked:** Only 995

## 🛠️ Tools Used
* **Data Prep:** `Pandas`, `NumPy`, `Scikit-Learn`
* **Machine Learning:** `XGBoost`
* **Deep Learning:** `TensorFlow` / `Keras` (LSTM)
* **Smart Tuning:** `Optuna` (Used to train the AI based on saving money, not just basic accuracy)

## 🚀 Why This Matters
1. **Saves Money:** By reducing the manual review queue to just 9,900 tickets, a company doesn't have to hire a massive team of manual reviewers.
2. **Happy Customers:** The "Deep Checker" rescued nearly 15,000 good customers from getting their cards incorrectly declined.
3. **Real-World Logic:** The AI was trained on real business limits, making it ready for actual production environments in banking or fintech.
