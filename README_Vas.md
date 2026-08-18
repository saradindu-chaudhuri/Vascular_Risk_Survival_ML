# Vascular and Metabolic Drivers of Survival: Interpretable Machine Learning Pipeline

An end-to-end clinical data science and survival analysis pipeline evaluating cardiovascular and renal risk factors, non-linear feature interactions, and time-to-event outcomes using the UCI Heart Failure cohort dataset.

---

## 📌 Project Overview

Cardiovascular and metabolic comorbidities—such as hypertension, renal impairment, and reduced ejection fraction—are critical drivers of survival and systemic cognitive/vascular health. This project models follow-up survival trajectories and identifies key risk factors using:

1. **Stratified Kaplan-Meier Analysis & Log-Rank Testing:** Evaluating survival function differences across hypertensive vs. non-hypertensive patient cohorts.
2. **Multivariable Cox Proportional Hazards:** Quantifying statistical hazard ratios ($\text{HR}$) across clinical parameters.
3. **Tuned Random Survival Forest (RSF):** Capturing non-linear predictor interactions using 5-fold cross-validation via `GridSearchCV`.
4. **SHAP (SHapley Additive exPlanations):** Interrogating global feature attributions and risk factor interactions.

---

## 🛠️ Tech Stack & Dependencies

* **Language:** Python 3.x
* **Environment:** Google Colab / Jupyter Notebook
* **Key Libraries:**
  * `ucimlrepo` – Direct API access to the UCI Machine Learning Repository
  * `pandas`, `numpy` – Data manipulation & structured array formatting
  * `lifelines` – Kaplan-Meier survival curves & Cox Proportional Hazards
  * `scikit-survival` – Non-linear Random Survival Forests
  * `scikit-learn` – Cross-validation (`GridSearchCV`, `KFold`)
  * `shap` – Model interpretability & feature dependence plotting
  * `matplotlib`, `seaborn` – Visualizations

---

## 📊 Key Findings & Methodology

### 1. Statistical Survival Modeling (Cox PH)
* **`serum_creatinine` ($\text{HR} = 1.38, p < 0.005$):** Every $1 \text{ mg/dL}$ increase in serum creatinine elevates hazard risk by **38%**, highlighting renal clearance as a primary metabolic predictor.
* **`ejection_fraction` ($\text{HR} = 0.95, p < 0.005$):** Every $1\%$ increase in ejection fraction reduces event hazard by **5%**.
* **`high_blood_pressure` ($\text{HR} = 1.61, p = 0.03$):** Hypertensive status increases relative hazard by **61%**.

### 2. Ensemble Survival ML & Interpretability

| Model Architecture | Validation Strategy | Concordance Index (C-Index) | Key Takeaway |
| :--- | :--- | :---: | :--- |
| **Cox Proportional Hazards** | Baseline Cohort | **0.740** | Linear baseline; identifies significant clinical HRs ($p < 0.05$). |
| **Tuned Random Survival Forest** | 5-Fold Cross-Validation | **0.742** | Captures non-linear comorbidity interactions (`max_depth: 8`, `min_samples_leaf: 5`). |

* **SHAP Interpretability:** Confirmed `serum_creatinine`, `ejection_fraction`, and `age` as the dominant global risk factors.
* **Feature Interaction:** SHAP dependence plots demonstrated that when `ejection_fraction` drops below ~35%, co-occurring hypertension significantly exacerbates risk predictions compared to non-hypertensive cases.

---

## 🚀 How to Run

1. **Clone the Repository:**
   ```bash
   git clone [https://github.com/YOUR_USERNAME/Vascular_Risk_Survival_Analysis.git](https://github.com/YOUR_USERNAME/Vascular_Risk_Survival_Analysis.git)
   cd Vascular_Risk_Survival_Analysis
