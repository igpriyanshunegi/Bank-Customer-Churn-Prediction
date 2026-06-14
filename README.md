# 🏦 Bank Customer Churn Clustering

> Unsupervised customer segmentation using **DBSCAN** and **PCA** on real-world bank churn data — identifying behavioral clusters to enable targeted retention strategies.

---

## 📌 Project Overview

Customer churn is one of the most critical challenges in the banking industry. This project takes an **unsupervised machine learning approach** to segment customers into distinct behavioral groups using **DBSCAN clustering** on the Bank Customer Churn dataset.

Rather than simply predicting *who will churn*, this project asks: **what kinds of customers exist, and which segments are most at risk?** The insights enable banks to proactively design personalized retention campaigns.

---

## 🗂️ Repository Structure

```
📦 bank-customer-churn-clustering
 ┣ 📓 Bank_Customer_Churn_Clustering.ipynb   ← Main analysis notebook
 ┣ 📊 Bank_Customer_Churn_Prediction.csv     ← Dataset (10,000 customers)
 ┗ 📄 README.md
```

---

## 📊 Dataset

| Property | Value |
|---|---|
| **Source** | Bank Customer Churn Prediction |
| **Rows** | 10,000 customers |
| **Features** | 12 columns |
| **Churn Rate** | ~20.4% |
| **Countries** | France, Spain, Germany |

### Feature Description

| Feature | Type | Description |
|---|---|---|
| `customer_id` | int | Unique customer identifier (dropped before modeling) |
| `credit_score` | int | Customer credit score |
| `country` | str | Customer's country (France / Spain / Germany) |
| `gender` | str | Customer gender (Male / Female) |
| `age` | int | Age of the customer |
| `tenure` | int | Number of years with the bank |
| `balance` | float | Account balance |
| `products_number` | int | Number of bank products held |
| `credit_card` | int | Has credit card? (1 = Yes, 0 = No) |
| `active_member` | int | Is active member? (1 = Yes, 0 = No) |
| `estimated_salary` | float | Estimated annual salary |
| `churn` | int | **Target** — Did customer leave? (1 = Yes, 0 = No) |

---

## 🔬 Methodology

### Pipeline at a Glance

```
Raw CSV
  │
  ▼
Data Cleaning
(drop customer_id, handle categoricals)
  │
  ▼
One-Hot Encoding
(country, gender → dummy variables)
  │
  ▼
Feature Scaling
(StandardScaler)
  │
  ▼
Dimensionality Reduction
(PCA — retain 90% variance)
  │
  ▼
DBSCAN Clustering
(eps=1.8, min_samples=5)
  │
  ▼
Evaluation & Visualization
(Silhouette Score, Churn Rate per Cluster)
```

### Why DBSCAN?

- Handles **arbitrary cluster shapes** (not just spherical like K-Means)
- Automatically identifies **outliers/noise** as a `-1` cluster
- Does **not require pre-specifying** the number of clusters

### Why PCA?

- Reduces dimensionality before clustering to avoid the **curse of dimensionality**
- Retaining 90% variance ensures minimal information loss
- Speeds up DBSCAN computation significantly

---

## 📈 Results

| Metric | Value |
|---|---|
| **Clusters Found** | 23 meaningful clusters + 1 noise group |
| **Silhouette Score** | ~0.17 |
| **Accuracy (cluster → churn mapping)** | ~79.6% |
| **Precision (Non-Churners, Class 0)** | High |
| **Recall (Churners, Class 1)** | Low (class imbalance) |

> **Note:** The silhouette score of ~0.17 reflects genuine behavioral overlap across customers — common in real-world financial data. It does not indicate a failed model; rather, it confirms that churn risk is a spectrum, not a clean binary split.

---

## 💡 Key Insights

- **23 distinct customer segments** were identified by DBSCAN, revealing the rich behavioral diversity within the customer base.
- **Certain clusters showed markedly higher churn rates**, making them prime targets for retention interventions.
- **Non-churners (Class 0)** are well-captured by the model; **churners (Class 1)** are harder to isolate due to their minority status (~20% of data).
- The small noise cluster (`-1`) captures edge-case customers whose behavior doesn't fit any defined group.

---

## 🏢 Business Value

| Application | Description |
|---|---|
| 🎯 **Targeted Retention** | High-churn clusters can receive personalized offers, loyalty rewards, or outreach |
| 💳 **Product Upselling** | Low-product-count clusters are opportunities to cross-sell banking products |
| 📞 **Proactive Engagement** | Identify at-risk segments before they churn, not after |
| 📐 **Credit Policy** | Segment-specific risk profiles inform better lending decisions |

---

## 🛠️ Tech Stack

| Library | Purpose |
|---|---|
| `pandas` | Data loading and manipulation |
| `numpy` | Numerical operations |
| `matplotlib` / `seaborn` | Data visualization |
| `scikit-learn` | Preprocessing, PCA, DBSCAN, metrics |
| `Google Colab` | Notebook execution environment |

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/igpriyanshunegi/Bank-Customer-Churn-Prediction.git
cd bank-customer-churn-clustering
```

### 2. Install Dependencies

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

### 3. Run the Notebook

Open `Bank_Customer_Churn_Clustering.ipynb` in **Jupyter Notebook**, **JupyterLab**, or **Google Colab**.

If using Google Colab, upload `Bank_Customer_Churn_Prediction.csv` to your Google Drive and update the `file_path` variable at the top of the notebook.

---

## 🔮 Future Improvements

- [ ] Try **HDBSCAN** for more robust cluster detection
- [ ] Experiment with **K-Means** and **Gaussian Mixture Models** for comparison
- [ ] Apply **SMOTE** or class-weighting to improve churner identification
- [ ] Build a **Streamlit dashboard** for interactive cluster exploration
- [ ] Use cluster labels as features in a downstream **supervised churn classifier**

---

## 👤 Author

**Priyanshu**

---

## 📄 License

This project is for educational and portfolio purposes. The dataset is publicly available on [Kaggle](https://www.kaggle.com/datasets/gauravtopre/bank-customer-churn-dataset).
