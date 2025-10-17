# SDN-DDoS-Detection-XAI
# Explainable SDN DDoS Detection using XGBoost and SHAP

## Project Overview
This project develops a **machine learning-based intrusion detection model** for identifying **DoS and DDoS attacks** in a **Software Defined Networking (SDN)** environment.  
An **XGBoost classifier** is trained on the **InSDN dataset** to distinguish between **normal** and **attack** traffic, followed by the use of **Explainable AI (XAI)** through **SHAP (SHapley Additive exPlanations)** to interpret model decisions.

The goal is to build a **high-performing yet transparent** network defense model that supports trust, accountability, and operational insight in SDN security.

---

## Key Objectives
- Build a robust **binary classification model** to detect attack vs normal SDN flows.  
- Achieve near-perfect accuracy using **XGBoost**, optimized for imbalanced network data.  
- Apply **SHAP** to interpret the influence of traffic features on predictions.  
- Visualize **global and local feature importance** for model transparency.  

---

##  Dataset
**Dataset:** InSDN (SDN Intrusion Detection Dataset)  
- Collected under controlled SDN testbed conditions  
- Includes multiple attack types: DoS, DDoS, Probe, BFA, etc.  
- This project filters for **Normal, DoS, and DDoS** traffic  
- Features: 84 (after cleaning, 52 used post-correlation reduction)  
- Rows: ~123,000 after deduplication and preprocessing

**Reference:**  
Almiani, M. et al., “A Machine Learning-Based Cyber Attack Detection Model for Software Defined Networks,” *Electronics*, 2020.

---

## Workflow Overview

### 1. **Data Cleaning**
- Removed duplicates and non-predictive columns (`Flow ID`, `Src IP`, `Dst IP`, `Timestamp`)  
- Encoded `Label`: Normal → 0, DoS/DDoS → 1  
- Confirmed no missing or inconsistent entries

### 2. **Preprocessing**
- Scaled numerical features  
- Removed multicollinear features (|corr| ≥ 0.9)  
- Finalized feature matrix: 52 predictive features

### 3. **Data Partitioning**
- Stratified 80/20 train–test split  
- Maintained class ratio (≈55% Normal / 45% Attack)

### 4. **Model Training**
- **Algorithm:** XGBoost (`binary:logistic`)  
- **Metrics:** Accuracy, Precision, Recall, F1, ROC-AUC  
- **Performance:**
  | Metric | Score |
  |---------|-------|
  | Accuracy | 0.99996 |
  | Precision | 0.99991 |
  | Recall | 1.00000 |
  | F1 Score | 0.99995 |
  | ROC-AUC | 1.00000 |

### 5. **Explainability (SHAP)**
- **Global Explainability:** SHAP summary plot reveals top contributors  
  - `Bwd Pkt Len Min`, `Fwd IAT Min`, `Init Bwd Win Byts`  
- **Local Explainability:** Dependence and interaction plots visualize key feature interactions  
- **Key Insight:**  
  - Short backward packet lengths with low TCP window bytes strongly drive **attack** predictions  
  - Larger, stable packet flows align with **normal** behavior

---

## Key Visuals
| Visualization | Description |
|----------------|-------------|
| **Feature Importance (XGBoost)** | Highlights top 20 contributing features |
| **SHAP Summary Plot** | Displays global feature influence on predictions |
| **Dependence Plot** | Shows how `Bwd Pkt Len Min` interacts with `Init Bwd Win Byts` |
| **Interaction Heatmap** | Visualizes top feature–feature interactions |

*(Figures available in the `/figures` directory)*

---

## Tools and Libraries
- **Language:** Python 3.11  
- **Core Libraries:** pandas, numpy, scikit-learn, xgboost  
- **XAI Framework:** SHAP  
- **Visualization:** seaborn, matplotlib  
- **Development Environment:** VS Code, Conda virtual environment

---

##  Folder Structure

```
SDN-DDoS-DoS-Detection-XAI/ 
│
├── data/                  # InSDN dataset CSVs (excluded or linked)
├── notebooks/             # Jupyter notebooks for EDA, preprocessing, training, SHAP
├── figures/               # Exported figures for poster and report
├── models/                # Saved trained models (.json, .pkl)
├── src/                   # Python scripts (data_cleaning.py, preprocess.py, model_train.py)
├── README.md              # Project documentation
└── requirements.txt       # Library dependencies
```
---

##  Future Work
- Extend classification to multiclass (Probe, BFA, etc.)
- Compare XGBoost vs LightGBM vs Deep Learning approaches
- Integrate SHAP in real-time SDN controller decision loop

---

## Author
**Alex Silas Butler-Demeo**  
Master of Engineering (Network Engineering & Telecommunications)  
RMIT University, Melbourne  
Supervisor: *Dr. Shuo Li*

---

## Repository Access
[View Full Codebase on GitHub](https://github.com/yourusername/Explainable-SDN-DDoS-Detection)  
 

