# 🎯 Telecom Marketing Campaign Prediction

This project aims to predict which customers are most likely to subscribe to a telecom offer based on past campaign data and economic indicators. Using machine learning (Logistic Regression and XGBoost), we enhance targeting efficiency and campaign performance.

---

## 📁 Dataset

The dataset consists of customer and macroeconomic features collected during a series of direct marketing campaigns by a telecom company.

- **Number of samples**: ~41,000
- **Features**: 20+ including:
  - Customer profile (age, job, marital status, etc.)
  - Contact details (communication type, last contact day/month, duration)
  - Previous campaign info
  - Macroeconomic indicators (employment variation, interest rate, etc.)
  - Target variable: `y` (whether the client subscribed)

---

## 📊 Exploratory Data Analysis (EDA)

Key insights from the data:

- Highly imbalanced target: ~11% subscribed (`y = yes`)
- Contact timing and method significantly affect response rate
- Economic indicators (like employment variation and interest rate) show moderate predictive power

---

## 📉 Plots

| Plot Description                       | Purpose                                             | Example Image                                         |
| -------------------------------------- | --------------------------------------------------- | ----------------------------------------------------- |
| Class Balance Bar Plot                 | Visualize imbalance in target variable              | ![Class Balance](imbalanced-target.png)               |
| Correlation Heatmap                    | Show correlations between features                  | ![Correlation Heatmap](correlation-heat-map.png)      |
| Subscription Rate vs Contact Method    | Understand impact of contact method on subscription | ![Subscription Rate](optimal-Threshold.png)           |
| SHAP Summary Plot (XGBoost)            | Feature importance and effect direction             | ![SHAP Summary](SHAP.png)                             |
| XGBoost Feature Importance             | Tree-based feature ranking                          | ![XGBoost Importance](XGBoost-feature-importance.png) |
| Confusion Matrix (Logistic Regression) | Evaluate logistic model predictions                 | ![LR Confusion](LR-confusion-matrix.png)              |
| ROC Curve (Logistic Regression)        | Assess model discrimination                         | ![ROC Curve](LR-ROC.png)                              |

---

## ⚙️ Preprocessing & Feature Engineering

- **Encoding**: One-hot and ordinal encoding for categorical variables
- **Missing values**: Mode imputation for binary unknowns
- **Transformations**:
  - Log transformation on skewed features like `age`
  - PCA on macroeconomic indicators (e.g., employment rate, interest rate)
- **Feature bins**:
  - `pdays` binned into 3 intervals: recent, older, never contacted

---

## 🤖 Models

### Logistic Regression

- **Why?** A strong baseline model that’s interpretable and fast
- **Handling imbalance**: SMOTE (Synthetic Minority Over-sampling)
- **Evaluation**: ROC-AUC, F1-score, Precision/Recall
- **Interpretation**: z-scores and p-values from `statsmodels`

### XGBoost

- **Why?** Robust to imbalance, captures non-linear relationships, widely used in industry
- **Handling imbalance**: SMOTE + `scale_pos_weight`
- **Tuning**: Grid search over `max_depth`, `gamma`, `learning_rate`, etc.
- **Interpretability**: SHAP values for global and local explainability

---

## 📈 Results

| Metric              | Logistic Regression | XGBoost (Tuned) |
| ------------------- | ------------------- | --------------- |
| Precision (Class 1) | 0.26                | 0.39            |
| Recall (Class 1)    | 0.60 → 0.67 (opt)   | 0.64            |
| F1 Score            | 0.35                | **0.48**        |
| AUC-ROC             | 0.756               | **0.80**        |

**Top SHAP Features:**

- `pdays_bin_1`: Recent contact
- `Economic_Trend_1`: Employment, interest rates
- `contact_telephone`: Lower impact
- `default_unknown`, `has_loan`, `job`

---

## 💡 Business Insights

- Contact timing is critical: recent contacts strongly boost response
- Weekday calling and avoiding telephone channel lead to better results
- Customers with loans or unknown default status respond less
- Economic trends do influence subscription likelihood

---

## 🧰 Tech Stack

- Python (3.10)
- Pandas, NumPy
- Scikit-learn
- XGBoost
- SHAP
- Statsmodels
- Matplotlib, Seaborn

---

## 🏁 How to Run

1. Clone the repo:

```bash
git clone https://github.com/yourname/telecom-marketing-predictor.git
cd telecom-marketing-predictor
```
