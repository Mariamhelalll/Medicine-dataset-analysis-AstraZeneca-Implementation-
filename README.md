# Medicine-dataset-analysis-AstraZeneca-Implementation-
# Drug Side-Effect Prediction and Clustering

## Project Overview
This project demonstrates how structured drug information and patient feedback can be combined to **predict** and **cluster** drug side-effects. The work mirrors real-world pharmaceutical challenges in **post-marketing surveillance** and **drug safety monitoring**, where organisations such as AstraZeneca need to monitor known risks and detect unexpected adverse reactions.

The dataset includes:
- **Drug characteristics**: composition, intended uses, manufacturer.
- **Patient feedback**: reviews, ratings, and sentiment.
- **Reported side-effects**: free-text adverse events mapped into a multi-label target matrix.

The aim of the project is to build a pipeline that:
1. Predicts the likelihood of each drug being associated with specific side-effects.
2. Clusters drugs by their side-effect profiles to surface hidden patterns.

---

## Methodology

### 1. Data Preparation
- Harmonised multiple tables into a single, clean dataset.
- Standardised column names and normalised text features.
- Encoded side-effects into a **multi-label binary target matrix (Y)**.
- Combined drug composition, uses, and patient review features into **X**.

### 2. Exploratory Data Analysis
- Plotted distributions of side-effects: identified a **long-tail distribution** (a small number of very common adverse events such as nausea, headache, dizziness, and many rare ones).
- Analysed review sentiment: drugs with poor reviews often aligned with higher side-effect frequencies.

### 3. Feature Engineering
- Used a **ColumnTransformer**:
  - TF-IDF for text features (`composition`, `uses`, reviews).
  - One-hot encoding for categorical features (manufacturer).
  - Scaling for numerical features (review counts/ratings).

### 4. Modelling
- **Baseline Model**: One-Vs-Rest Logistic Regression for multi-label prediction.
- **Evaluation**:
  - ROC-AUC (overall separability).
  - PR-AUC (preferred for imbalanced classes).
- **Interpretability**: Examined feature coefficients to identify influential words or attributes.

### 5. Clustering
- Aggregated data into a *drug × side-effect* matrix.
- Applied clustering (Agglomerative Clustering, KMeans) to group drugs by side-effect patterns.
- Observed grouping by therapeutic classes (e.g., antibiotics, antidepressants).

---

## Results

### Predictive Model
- **ROC-AUC**: Consistently strong (>0.80) across most side-effects, showing the model distinguishes positives from negatives.
- **PR-AUC**:
  - Common side-effects (nausea, dizziness): moderate to strong performance (~0.65–0.75).
  - Rare side-effects: lower performance (<0.50), reflecting class imbalance.
- **Interpretability**: Clinically relevant features surfaced (e.g., “stomach”-related terms predicting gastrointestinal adverse events).

### Clustering
- Grouped drugs into meaningful sets:
  - Painkillers clustered around gastrointestinal side-effects.
  - Antidepressants clustered around neurological side-effects.
- Revealed **therapeutic-class level patterns** consistent with pharmacological knowledge.

### Insights from Patient Feedback
- Negative reviews strongly correlated with higher side-effect reporting.
- Patient text added complementary signal to structured drug attributes.

---

## Conclusions

- The dataset supports both **prediction of side-effects** and **clustering of drugs** based on adverse event profiles.  
- The supervised model performed well for common side-effects but struggled with rare events due to limited examples.  
- Clustering added value by surfacing **unexpected patterns** and class-level structures.  
- Interpretability analysis confirmed the model aligned with plausible clinical reasoning, enhancing trust for pharmacovigilance use.  

**Final Takeaway**:  
This pipeline illustrates how machine learning can replicate a pharmacovigilance workflow — predicting **known risks** and detecting **emerging signals** from real-world evidence. It provides a solid foundation for developing a **signal detection tool** to support safety scientists in monitoring drug risks.

---

## Next Steps

For practical application by a client such as AstraZeneca:
1. **Validation** with safety scientists on the Top-6 predicted side-effects and drug clusters.
2. **Standardisation** of side-effect labels (e.g., mapping to MedDRA terminology).
3. **Address class imbalance** to improve recall for rare adverse events (class weighting, oversampling).
4. **Enhanced text modelling** using modern NLP embeddings (e.g., BERT).
5. **Operationalisation** of the pipeline into a dashboard for routine monitoring.
6. **Dataset expansion** to include dosage, demographics, and temporal data for richer analysis of risk.
7. **Drift monitoring** to detect changes in side-effect reporting patterns over time.

---

## Repository Structure
├── data/ # Raw and cleaned datasets
├── notebooks/
│ └── Astazeneca_data_set_analysis.ipynb # Main notebook with full pipeline
├── models/ # Saved models and transformers
├── results/ # Evaluation metrics, plots, and clustering outputs
└── README.md # Project documentation


---

## How to Run
1. Clone this repository.
2. Install the requirements:
   ```bash
   pip install -r requirements.txt
jupyter notebook notebooks/Astazeneca_data_set_analysis.ipynb


