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
## 📌 Project Overview

Adverse drug reactions (ADRs) remain a critical concern in both clinical trials and post-marketing surveillance. The AstraZeneca dataset used in this project contains reports of side-effects linked to different drugs, alongside structured information such as formulation, manufacturer, and drug description. A major challenge of such data is its **long-tailed distribution**: a small number of adverse events (e.g., nausea, headache, dizziness) appear frequently, while many others (e.g., rash, chest pain, palpitations) occur only rarely.  

This project applies **machine learning techniques** to predict and analyse adverse events in this dataset, with an emphasis on **clinical interpretability**. The workflow covers:

1. **Data Preparation and Harmonisation**  
   - Cleaning and renaming labels to ensure consistency.  
   - Handling missing values and categorical variables.  
   - Vectorising text fields with **TF-IDF** and scaling numerical features.  

2. **Supervised Learning**  
   - Framed as a **multi-label classification** problem.  
   - Implemented **One-vs-Rest Logistic Regression** with class balancing to manage skewed label distributions.  
   - Evaluated with clinically relevant metrics (Precision–Recall AUC, F1-score, calibration).  

3. **Unsupervised Exploration**  
   - Grouping drugs by their adverse event profiles to uncover patterns.  
   - Highlighting potential drug clusters that share safety signals.  

4. **Interpretability Enhancements**  
   - Added **heatmaps** for PR-AUC, F1-score, and confusion matrix components to provide an accessible visual overview.  
   - Introduced **threshold tuning** to reduce false negatives for rare but serious adverse events.  
   - Assessed **calibration curves** to determine whether predicted risks align with observed outcomes.  
   - Wrote detailed **clinical conclusions** for each evaluation, ensuring findings can be understood in a healthcare context.  

By combining strong technical modelling with a clinical interpretability layer, this project bridges the gap between raw machine learning outputs and meaningful pharmacovigilance insights.

---

## 🧾 Conclusions

The expanded evaluation provides a clear picture of both the strengths and limitations of the current approach:

### Performance on Frequent Adverse Events
- For common side-effects such as **nausea**, **headache**, and **dizziness**, the model achieves **high PR-AUC and F1-scores**.  
- Calibration curves for these labels are close to the ideal diagonal, meaning probability estimates (e.g., a 70% predicted risk of nausea) align with observed frequencies.  
- Clinically, this indicates that the model is reliable for screening frequent adverse events and could support early signal detection in pharmacovigilance workflows.  

### Performance on Rare Adverse Events
- Rare conditions such as **rash**, **palpitations**, and **chest pain** show **low PR-AUC and F1-scores**, reflecting the difficulty of learning from sparse data.  
- False negatives are disproportionately high for these labels, representing a critical clinical risk as genuine safety signals could be missed.  
- Calibration is weaker, with the model often over- or under-estimating risks due to limited examples.  
- Clinically, these findings confirm that rare but potentially serious adverse events must remain under expert review and cannot yet be delegated to the model alone.  

### Error Analysis and Interpretability
- **Confusion matrix component heatmaps** reveal the types of errors made across labels:  
  - High **False Positives (FPs):** Lead to unnecessary noise in safety monitoring, but are less dangerous.  
  - High **False Negatives (FNs):** Indicate blind spots, the most significant issue for patient safety.  
- The combination of **heatmaps** and **clinical commentary** provides a transparent and interpretable evaluation framework, suitable for both technical and medical audiences.  

### Overall Clinical Implications
- The model demonstrates strong potential for automating the detection of **frequent side-effects**, making pharmacovigilance processes more scalable.  
- However, it underlines the importance of **human-in-the-loop oversight** for **rare and serious adverse events**.  
- Improvements such as **per-label threshold tuning, richer clinical features (dose, demographics, treatment duration), and more advanced classifiers** (e.g., tree-based models or neural networks) are necessary before deployment in a regulatory setting.  

---

**In summary:**  
The analysis shows that while machine learning can meaningfully enhance pharmacovigilance by reliably identifying common adverse events, it is not yet robust enough to replace expert oversight for rare and high-risk conditions. The improvements added — heatmaps, threshold tuning, calibration curves, and detailed clinical interpretation — make this project both **technically rigorous** and **clinically relevant**, ensuring that the results can inform real-world safety monitoring in a transparent and trustworthy manner.


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



