# Multi-Modal Prediction of Breast Cancer Recurrence Using Clinical and Radiomic Features from DCE-MRI

## 📌 Overview
This repository contains the implementation of a multi-modal machine learning framework for predicting breast cancer recurrence by integrating clinical variables and radiomic features derived from dynamic contrast-enhanced (DCE) MRI.

The framework evaluates three experimental settings:
1. Clinical-only models  
2. Radiomics-only models  
3. Multi-modal fusion models  

---

## 🎯 Objectives
- Predict breast cancer recurrence using multi-modal data  
- Evaluate the contribution of clinical and radiomic features  
- Address class imbalance using cost-sensitive learning  
- Improve classification performance using threshold optimization  

---

## 📊 Dataset

This study uses the **Duke Breast Cancer MRI dataset**, publicly available via The Cancer Imaging Archive (TCIA).

- Total patients: **920**  
- Recurrence cases: **87 (9.45%)**  
- Non-recurrence: **833 (90.55%)**  

Radiomic features were **pre-extracted** and provided with the dataset following Saha et al.

### Feature Types:
- Shape features  
- First-order statistics  
- Texture features  
- Kinetic features (DCE-MRI)  

📥 Dataset access:  
[https://www.cancerimagingarchive.net/](https://www.cancerimagingarchive.net/collection/duke-breast-cancer-mri/)

---

## ⚙️ Methodology

### 1️⃣ Clinical Model
- 19 clinical variables  
- Includes pre-treatment and post-treatment features  

---

### 2️⃣ Radiomic Model
- Initial features: **530**  
- Feature selection:
  - Bootstrap AUC estimation (1000 iterations)  
  - Correlation filtering (|r| > 0.8)  
- Final signature: **20 features**  

---

### 3️⃣ Fusion Model (Multi-Modal)
- Early fusion (clinical + radiomic features)  
- Evaluated configurations:
  - Trial A: 39 features  
  - Trial B: 34 features ✅ (best)  
  - Trial C: 25 features  

---

## 🤖 Models

### Logistic Regression (LR)
- max_iter = 1000  
- C = 1.0  
- solver = liblinear  
- class_weight = balanced  

### Random Forest (RF)
- n_estimators = 300  
- class_weight = balanced  

### XGBoost
- n_estimators = 300  
- eval_metric = logloss  
- scale_pos_weight ≈ 9.5  

---

## 🔁 Evaluation Strategy

- Train/Test split: **80% / 20%**  
- Cross-validation: **5-fold stratified (training set)**  

### Metrics:
- AUC (ROC)  
- Accuracy  
- F1-score  
- Precision  
- Sensitivity (Recall)  
- Specificity  

All results are reported as:  
**mean ± std (min–max)**  

---

## 🎯 Threshold Optimization

- Applied after model prediction  
- Threshold range: **0.05 → 0.60 (step = 0.025)**  
- Objective: **maximize F1-score**  

---

## 📈 Results Summary

| Model              | AUC  | F1-score |
|-------------------|------|----------|
| Clinical          | 0.705 | 0.286 |
| Radiomics         | 0.746 | 0.310 |
| Fusion (Trial B)  | **0.750** | **0.390** |

---

## 🧪 Reproducibility

- Fixed random seed used across all experiments  
- Consistent preprocessing and feature selection pipeline  
- Explicit hyperparameter configuration  
- Full implementation provided  

---

## 💻 Requirements

- Python 3.12  
- scikit-learn  
- xgboost  
- numpy  
- pandas  
- jupyter  

## 📄 Citation

### 📌 Paper
If you use this work, please cite:

Alabdah, M., Jakubíček, R.  
Multi-Modal Prediction of Breast Cancer Recurrence Using Clinical and Radiomic Features from DCE-MRI.

---

### 📊 Radiomics Study

Saha, A., Harowicz, M. R., Grimm, L. J., Kim, C. E., Ghate, S. V., Walsh, R., & Mazurowski, M. A.  
A machine learning approach to radiogenomics of breast cancer: A study of 922 subjects and 529 DCE-MRI features.  
British Journal of Cancer, 119, 508–516 (2018).

---

### 📦 Dataset (TCIA)

Saha, A. et al.  
Dynamic contrast-enhanced magnetic resonance images of breast cancer patients with tumor locations.  
The Cancer Imaging Archive, 2021.  
https://doi.org/10.7937/TCIA.e3sv-re93

## ⚠️ Notes

- Dataset is **not included** due to TCIA restrictions  
- Users must download data manually from TCIA

  ## 📬 Contact

Madeleine Alabdah  
Brno University of Technology  
Email: 273027@vutbr.cz  

## 📜 License

This project is licensed under the MIT License.
