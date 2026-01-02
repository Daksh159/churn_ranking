
# 📉 Customer Churn Ranking Model (ROC-AUC Optimized)

## 🔍 Project Overview

This project focuses on **customer churn prediction with an emphasis on ranking churn risk rather than pure classification accuracy**.

Instead of asking:

> *“Will this customer churn or not?”*

the goal here is:

> *“Which customers are **most likely to churn**, so they can be prioritized for retention?”*

This makes the problem **more aligned with real-world business use cases**, where limited resources are used to retain **high-risk customers first**.

---

## 🎯 Problem Statement

Customer churn occurs when users stop using a service. Businesses want to:

* Identify customers at **high risk of churning**
* Rank them so retention strategies can be applied **efficiently**
* Avoid misleading models caused by **data leakage**

---

## 📊 Dataset

* Customer churn dataset (train & test split)
* Binary target variable:

  * `1` → Customer churned
  * `0` → Customer did not churn
* Dataset is **relatively balanced**, so accuracy alone is **not sufficient** to evaluate performance

---

## 🧠 Key Design Decision: Why ROC-AUC?

### Why not Accuracy?

* Accuracy assumes a **fixed probability threshold**
* Not suitable when **ranking customers by risk** is more important than exact predictions

### Why not Precision / Recall?

* Precision & Recall depend on a **chosen threshold**
* Threshold choice varies by business constraints

### ✅ Why ROC-AUC?

* Measures how well the model **ranks churners above non-churners**
* Threshold-independent
* Directly aligns with:

  > *“Prioritize customers who are most likely to churn”*

👉 **ROC-AUC is the correct metric for churn ranking problems**

---

## ⚠️ Feature Leakage Handling (Critical Insight)

During exploratory analysis, three features were identified as **leakage features**:

* Support call history
* Payment delay indicators
* Last customer interaction outcomes

These features:

* Contain **post-churn or near-churn information**
* Artificially inflate model performance
* Would **not be available at prediction time in real deployments**

### 🚫 Action Taken

* All leakage features were **removed**
* Model performance dropped significantly — **expected and correct behavior**
* Remaining features reflect **true predictive difficulty**

📌 This step ensures the model is **realistic, honest, and production-relevant**

---

## 🧪 Modeling Approach

* Supervised binary classification
* Focus on **ranking quality** rather than label prediction
* Models evaluated using:

  * ROC-AUC
  * Classification report (for diagnostic purposes only)

Even after leakage removal:

* The model struggles to **separate churners clearly**
* This indicates:

  * Limited signal in available features
  * Realistic business challenge

---

## 📈 Results Summary

* ROC-AUC drops after leakage removal
* Accuracy remains close to random
* Recall for churners is high, but precision is low

🔎 **Interpretation**:

* The model can **rank churners better than random**
* But cannot reliably predict churn labels without stronger features

This is a **valid and important outcome**, not a failure.

---

## 🧩 Key Learnings

* Feature leakage can completely invalidate ML models
* ROC-AUC is superior for **ranking problems**
* Real-world churn prediction is **hard without behavioral depth**
* Honest models are better than inflated ones

---

## 🚀 Future Improvements

* Add **time-based features** (customer trends)
* Behavioral aggregation (usage decay, engagement slope)
* Survival analysis / time-to-churn modeling
* Cost-sensitive learning for retention optimization

---

## 🛠️ Tech Stack

* Python
* Pandas, NumPy
* Scikit-learn
* Matplotlib / Seaborn
* Jupyter Notebook

---

## 📁 Repository Structure

```
📦 churn_ranking
 ┣ 📓 customer-churn.ipynb   # Data analysis, modeling, evaluation
 ┗ 📄 README.md              # Project documentation
```

---

### ⭐ Final Note

This project prioritizes **correct problem framing and honest evaluation** over inflated metrics — a crucial mindset for building real ML systems.

---

