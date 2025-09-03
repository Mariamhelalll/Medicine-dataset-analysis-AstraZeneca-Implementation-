# Medicine-dataset-analysis-AstraZeneca-Implementation-
# AstraZeneca Adverse Event Dataset Analysis

## 📌 Project Overview
This project analyses the AstraZeneca adverse event dataset with the goal of predicting and interpreting drug side-effects using machine learning.  
The notebook provides a complete pipeline covering **data preprocessing, feature engineering, supervised classification, unsupervised exploration, and model evaluation** — with a strong focus on **clinical interpretability** for pharmacovigilance applications.  

---

## 🔬 Objectives
- Harmonise and clean adverse event data for reliable analysis.  
- Build a **multi-label classifier** to predict drug-related side-effects.  
- Explore **unsupervised clustering** of drugs by side-effect patterns.  
- Provide **clinically interpretable evaluation** of the models.  

---

## ⚙️ Methodology

### 1. Data Preparation
- Data harmonisation: renamed and normalised AE labels.  
- Text preprocessing with **TF-IDF vectorisation** for descriptions.  
- Handling missingness and encoding categorical variables (manufacturer, formulation, etc.).  

### 2. Modelling
- **Supervised:** One-vs-Rest Logistic Regression baseline with balanced class weights.  
- **Unsupervised:** Clustering of side-effect profiles for exploratory grouping.  
- **Pipeline:** Reproducible scikit-learn `Pipeline` with preprocessing and classification stages.  

### 3. Evaluation
Originally, the model was evaluated with **ROC-AUC and PR-AUC per label**. The updated version now includes deeper, clinically focused evaluation methods (see below).  

---

## 🚀 Improvements Added

### 🔹 Heatmap-based Evaluation
- **PR-AUC Heatmap:** Compact visualisation of precision–recall trade-offs across all AE labels.  
- **F1-Score Heatmap:** Balanced accuracy across labels, highlighting strengths in common AEs and weaknesses in rare ones.  
- **Confusion Matrix Components Heatmap:** TP, FP, FN, TN counts per label for clinical interpretability (identifying missed detections vs false alarms).  

### 🔹 Threshold Tuning
- Per-label threshold optimisation to reduce false negatives, especially for rare but clinically significant AEs.  

### 🔹 Calibration Curves
- Assessed probability calibration to determine whether predicted risks (e.g., 70% chance of nausea) match real-world frequencies.  
- Added clinical interpretation of calibration for common vs rare side-effects.  

### 🔹 Clinical Commentary
- Integrated **British English clinical conclusions** for each evaluation method, linking results directly to safety implications.  
- Highlighted **long-tailed dataset imbalance**: strong detection of frequent AEs (*nausea*, *headache*) but weak performance on rare AEs (*rash*, *palpitations*).  

---

## 📊 Key Insights
- The model is **reliable for common adverse events**, achieving high PR-AUC and F1-scores.  
- **Rare AEs remain problematic** with high false negatives, limiting clinical safety without expert oversight.  
- Calibration suggests that probability estimates for frequent AEs are trustworthy, but rare AEs show over/under-confidence.  
- Heatmaps and interpretability tools make the analysis transparent and clinically relevant.  

---

## 📈 Next Steps
- Extend modelling to include **tree-based algorithms** (Random Forest, XGBoost, LightGBM) for improved non-linear feature handling.  
- Enrich feature set with **dose, demographics, and treatment duration**.  
- Apply **dimensionality reduction (UMAP/t-SNE)** for visualising drug clustering by AE profiles.  
- Develop a **dashboard-style report** for pharmacovigilance teams.  

---

## 🛠️ Tools & Libraries
- **Python 3.10**  
- **pandas, numpy, matplotlib, seaborn** – data handling and visualisation  
- **scikit-learn** – preprocessing, classification, metrics, calibration  
- **nbformat / Jupyter** – reproducible analysis notebook  

---

## 📂 Repository Structure
├── Astrazeneca_data_set_analysis.ipynb # Main analysis notebook
├── data/ # (Optional) Dataset storage
├── README.md # Project documentation


---

## ✅ Clinical Disclaimer
This project is a **data science demonstration** and not a replacement for medical or regulatory decision-making. Predictions are purely illustrative and require expert review in any real-world setting.  

---

## 📌 Author
Developed by *Maryam Mohamed* as part of an individual academic project on **Computer Science & Artificial Intelligence** with applications in **data science for healthcare** .  



