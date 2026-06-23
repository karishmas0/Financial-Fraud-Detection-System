# Financial Fraud Detection System 🚀

Ek advanced 2-stage machine learning pipeline jo financial transactions mein fraud detect karti hai.

## 🛠 Project Overview
- **Stage 1 (Filter):** XGBoost model jo safe transactions ko fast filter karta hai.
- **Stage 2 (Investigator):** LSTM network jo suspicious cases ka sequence analysis karta hai.

## 📊 Key Metrics
- **Automation Rate:** 69.15%
- **Processing Throughput:** 38,540 tx/sec

## 📂 Repository Files
- `fraud-detection-system.ipynb`: Full training & evaluation workflow.
- `stage1_xgb.json` & `stage2_lstm.keras`: Pre-trained model artifacts.
- `scaler.pkl`: Feature normalization object.

## 🚀 How to Use
1. Clone the repository.
2. Load the models (`stage1_xgb.json`, `stage2_lstm.keras`) and scaler (`scaler.pkl`).
3. Feed transaction data into the pipeline for automated fraud scoring.
