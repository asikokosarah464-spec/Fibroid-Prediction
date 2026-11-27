# Deep Learning Based Early Prediction of Uterine Fibroids Using Clinical and Demographic Data: A Comparative Evaluation

**University of Greater Manchester | 2026**

---

## Overview

This repository contains the full source code for a postgraduate research dissertation completed at the University of Greater Manchester.

The study develops and evaluates eight machine learning and deep learning models for the early prediction of uterine fibroids (leiomyoma) using clinical and demographic data from the MIMIC-IV electronic health record database. Models are compared on discrimination performance (AUC-ROC), calibration, and fairness across racial/ethnic subgroups. Explainability is provided via TreeSHAP. A complementary primary survey (N=24 UK women) contextualises the clinical findings within patient experience.

**Best model:** XGBoost — AUC-ROC 0.7592 (95% CI: 0.7441–0.7743)

---

## Models Evaluated

| Model | Type |
|---|---|
| Logistic Regression (LR) | Baseline linear model |
| XGBoost | Gradient boosting (best performer) |
| Multi-Layer Perceptron (MLP) | Feedforward neural network |
| Support Vector Machine (SVM) | Kernel-based classifier |
| TabNet | Attention-based tabular deep learning |
| TabFCN | Tabular fully connected network |
| Temporal Convolutional Network (TCN) | Sequential convolutional model |
| Long Short-Term Memory (LSTM) | Recurrent neural network |

Hyperparameters were optimised using Optuna TPE Bayesian optimisation (20 trials per model).

---

## Dataset

This study uses the **MIMIC-IV** (Medical Information Mart for Intensive Care IV) database maintained by PhysioNet.

> ⚠️ **The MIMIC-IV dataset cannot be shared publicly.** Access requires:
> 1. Completion of the CITI "Data or Specimens Only Research" training programme
> 2. A signed PhysioNet data use agreement
> 3. Credentialed access approval at [physionet.org](https://physionet.org/content/mimiciv/)

**Cohort summary:**
- Total patients: 56,467
- Cases (ICD-10-CM D25.x — Leiomyoma of uterus): 2,991
- Controls: 53,476
- Features used: 24 clinical and demographic variables
- Train / Validation / Test split: 70% / 15% / 15% (stratified at patient level)
- Post-SMOTE training samples: 74,864

---

## Requirements

- Python 3.10
- Conda 26.7.2 (environment: `fibroid_ai_final`)
- See `requirements.txt` for full package list with pinned versions

Key dependencies:
```
python==3.10
torch==2.14.0
xgboost==3.2.0
pytorch-tabnet==4.1.0
scikit-learn==1.9.1
optuna==5.5.0
shap==0.51.0
pandas==3.0.6
numpy==2.4.6
imbalanced-learn==0.11.0
scipy==1.17.1
matplotlib==3.11.2
```

---

## Installation

```bash
# Clone the repository
git clone https://github.com/asikokosarah464-spec/fibroid-prediction.git
cd fibroid-prediction

# Install dependencies
pip install -r requirements.txt
```

---

## Usage

All code is contained in a single Jupyter notebook. Open and run it from top to bottom:

```bash
jupyter notebook 01_preprocessing.ipynb
```

The notebook covers in order:
1. Data preprocessing (imputation, normalisation, SMOTE, train/val/test split)
2. Training all eight models with Bayesian hyperparameter optimisation (Optuna TPE)
3. Model evaluation (AUC-ROC, accuracy, sensitivity, specificity, F1, Brier score)
4. TreeSHAP global feature importance and local explanations
5. Fairness analysis by racial/ethnic subgroup
6. Primary survey data analysis

> ⚠️ **Note:** MIMIC-IV data files must be placed in a `data/` folder in the same directory as the notebook before running.

---

## Repository Structure

```
MRS7015-Fibroid-Prediction/
│
├── README.md                     # This file
├── requirements.txt              # Python dependencies (pinned versions)
├── 01_preprocessing.ipynb        # All code: preprocessing, models, SHAP, fairness, survey
│
├── processed/                    # Saved model outputs and evaluation metrics (generated on run)
└── figures/                      # SHAP plots, fairness charts, confusion matrices (generated on run)
```

---

## Key Results

| Model | AUC-ROC | AUC-PRC | Accuracy | F1-Score | Sensitivity | Specificity | Precision | Brier Score |
|---|---|---|---|---|---|---|---|---|
| **XGBoost** | **0.7592** | 0.1410 | 0.8252 | 0.2314 | 0.4967 | 0.8436 | 0.1509 | 0.1238 |
| MLP | 0.7492 | 0.1670 | 0.7090 | 0.1910 | 0.6481 | 0.7124 | 0.1120 | 0.1879 |
| TCN | 0.7491 | 0.1519 | 0.6302 | 0.1701 | 0.7149 | 0.6255 | 0.0965 | 0.2165 |
| SVM | 0.7485 | 0.1619 | 0.6953 | 0.1861 | 0.6570 | 0.6975 | 0.1084 | 0.1945 |
| LSTM | 0.7484 | 0.1546 | 0.7586 | 0.2008 | 0.5723 | 0.7690 | 0.1218 | 0.1632 |
| TabFCN | 0.7396 | 0.1595 | 0.5671 | 0.1580 | 0.7661 | 0.5560 | 0.0881 | 0.2505 |
| TabNet | 0.7350 | 0.1358 | 0.6819 | 0.1746 | 0.6347 | 0.6845 | 0.1012 | 0.2090 |
| LR | 0.7189 | 0.1297 | 0.6790 | 0.1699 | 0.6192 | 0.6826 | 0.0984 | 0.2070 |

XGBoost significantly outperformed Logistic Regression (DeLong test p=0.0033).

**Top 5 features (TreeSHAP):** Age, BMI, INR, Haemoglobin, Race (White)

---

## Ethics

This research received ethics approval from the University of Greater Manchester Research Ethics Committee (Form RE1, approved September 2026). Primary survey participants provided informed consent. All responses were fully anonymised. No identifiable personal data was collected or stored.

---

## Author

**Sarah Ifeanyi Asikoko**
University of Greater Manchester | 2026

---

## Citation

If you use this code or findings in your work, please cite:

> Asikoko, S.I. (2026). *Deep Learning Based Early Prediction of Uterine Fibroids Using Clinical and Demographic Data: A Comparative Evaluation*. University of Greater Manchester.
