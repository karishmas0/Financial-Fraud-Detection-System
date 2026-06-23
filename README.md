# 🚨 Smart Fraud Detection AI (The 2-Step System)

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![XGBoost](https://img.shields.io/badge/XGBoost-GPU--Accelerated-orange)
![TensorFlow/Keras](https://img.shields.io/badge/TensorFlow-Deep%20Learning-FF6F00)

## 📌 The Problem We Are Solving
Banks face a big problem: If their security is too weak, thieves steal money. If their security is too strict, good customers get their cards blocked for no reason (which makes them angry!). Single AI models struggle to balance this.

**Our Solution:** Instead of one AI, we built a team of **Two AIs** working together to keep the bank safe without annoying the customers.

---

## 🧠 How It Works (The 2 Steps)

### 🛡️ Step 1: The "Strict Bouncer" (XGBoost AI)
* **What it does:** It quickly checks every single transaction that comes to the bank. 
* **The Rule:** "Do not let any fraud escape."
* **How it decides:** If your transaction looks 100% safe, it approves your payment instantly. But if it has even a 1% doubt, it does **not** fail your payment. Instead, it holds it and sends it to Step 2. 

### 🕵️ Step 2: The "Smart Detective" (Deep LSTM AI)
* **What it does:** This AI is highly advanced. It only checks the "doubtful" cases sent by the Bouncer. 
* **The Rule:** "Do not block a good customer."
* **How it decides:** Instead of just looking at your current payment, it looks at your **last 5 transactions** like a short movie. It understands your spending habits. It realizes, *"Oh, this isn't a fraudster, this is just a good customer buying a new iPhone."* It clears the good customers and only blocks the actual thieves.

---

## 📊 The Results (Tested on 1.7 Million Payments)

We tested this system on **1,782,993** real transactions. The results were amazing:

* **Frauds Caught:** 2,640
* **Frauds Missed:** Only 26 (The Bouncer successfully stopped 99% of the attacks!)
* **Happy Customers:** Over **1.5 Million** good customers had their payments approved instantly without any friction or delay.
* **Team Workload Saved:** The system automatically handled over 92% of the traffic, saving the bank's human team thousands of hours of manual checking.

---

## 📁 What's in the Box? (Files)

I have exported the "brains" of these trained AIs so anyone can use them:
* `stage1_xgb.json` 👉 The saved rules of the XGBoost Bouncer.
* `stage2_lstm.keras` 👉 The saved neural network brain of the LSTM Detective.
* `scaler.pkl` 👉 The math tool that scales new data so the AI can read it.

---

## 🚀 How to Use My Code

You can easily load my AI models into your own Python project using this code:

```python
import joblib
from tensorflow.keras.models import load_model

# 1. Wake up the AIs!
bouncer_model = joblib.load('stage1_xgb.json')  
detective_model = load_model('stage2_lstm.keras')
data_scaler = joblib.load('scaler.pkl')

# 2. Check your new data
# (Write your code here to pass new transactions through the Bouncer and Detective)
