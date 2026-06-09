# 🌌 Stellar Object Classification
### Capstone Project — Sloan Digital Sky Survey (SDSS)

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange?logo=scikit-learn&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)

---

## 📖 Overview

This project builds and compares multiple **machine learning classification models** to automatically identify celestial objects — **Stars**, **Galaxies**, and **Quasars (QSO)** — from photometric and spectroscopic measurements collected by the **Sloan Digital Sky Survey (SDSS)**.

Automated stellar classification is essential for modern astronomy, where surveys generate millions of observations that are impossible to label manually. This project demonstrates a complete end-to-end ML pipeline — from raw data to a deployable model.

---

## 📁 Project Structure

```
Stellar-Object-Classification/
│
├── Stellar_object_classification.ipynb   # Main Jupyter Notebook (polished, 11 sections)
├── star_classification.csv               # SDSS dataset (100,000 records, 18 features)
├── Capstone Project Stellar Object Detection.pptx  # Presentation slides
├── Capstone Project Stellar Object Detection.pbix  # Power BI dashboard
├── .gitignore
└── README.md
```

---

## 📊 Dataset

| Property | Detail |
|---|---|
| **Source** | [Sloan Digital Sky Survey (SDSS)](https://www.sdss.org/) |
| **Records** | 100,000 observations |
| **Features** | 18 (photometric + spectroscopic) |
| **Target Classes** | GALAXY (~59%), STAR (~22%), QSO/Quasar (~19%) |

### Key Features

| Feature | Description |
|---|---|
| `alpha` | Right Ascension angle (sky position) |
| `delta` | Declination angle (sky position) |
| `u`, `g`, `r`, `i`, `z` | Photometric filter intensities (ultraviolet → infrared) |
| `redshift` | Doppler shift of light — strongest discriminator for QSOs |
| `class` | Target label: GALAXY / STAR / QSO |

---

## 🔬 Methodology

### 1. Data Preprocessing
- Inspected data types, null values, duplicates — **no missing values found**
- Identified and removed **one outlier** (index 79543 with anomalous u/g readings)
- Dropped non-informative identifier columns (`obj_ID`, `spec_obj_ID`, etc.)
- Applied **StandardScaler** for feature normalisation

### 2. Exploratory Data Analysis
- Class distribution visualisation
- Univariate distribution plots (KDE) for all numeric features
- Outlier detection via box plots
- Pair plots and correlation heatmaps for photometric filters and positional features

### 3. Feature Engineering
- Label-encoded the target variable (GALAXY=0, QSO=1, STAR=2)
- 80/20 train-test split with `random_state=42`
- 5-Fold Cross-Validation for generalisation assessment

### 4. Models Trained

| Model | Key Parameter |
|---|---|
| Logistic Regression | Default (baseline) |
| Decision Tree | Default |
| K-Nearest Neighbours | k = 5 |
| Support Vector Machine | Linear kernel, C = 1 |
| AdaBoost | Default |
| **Random Forest** ⭐ | 100 estimators, random_state=42 |

---

## 📈 Results

| Model | Accuracy |
|---|---|
| Logistic Regression | ~95–97% |
| Decision Tree | ~97–98% |
| KNN (k=5) | ~97–98% |
| SVM (linear) | ~96–97% |
| AdaBoost | ~91–93% |
| **Random Forest** | **~98–99%** ✅ |

> **Winner: Random Forest** — Highest accuracy and most balanced precision/recall/F1-score across all three classes.  
> **Key insight:** The `redshift` feature is the strongest single predictor, as quasars exhibit characteristically high redshift values.

---

## 🚀 Getting Started

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scikit-learn joblib
```

### Run the Notebook
```bash
jupyter notebook Stellar_object_classification.ipynb
```

### Load the Saved Model
```python
from joblib import load
model = load('Stellar_object_detection_model.joblib')
predictions = model.predict(new_data)
```

---

## 🗺️ Notebook Structure

The notebook is organised into **11 clearly labelled sections**:

1. Project Overview
2. Importing Libraries
3. Loading the Dataset
4. Data Preprocessing & Inspection
5. Exploratory Data Analysis (EDA)
6. Multivariate Analysis
7. Feature Engineering & Data Splitting
8. Model Building & Evaluation *(6 models)*
9. Model Comparison & Selection
10. Model Deployment
11. Summary & Conclusions

---

## 🔭 Future Work

- **Hyperparameter Tuning** — GridSearchCV on Random Forest parameters
- **Feature Importance Analysis** — Identify and retain only the most predictive features
- **Class Imbalance Handling** — SMOTE oversampling for minority classes
- **Deep Learning** — Explore neural network architectures for improved accuracy
- **API Deployment** — Wrap the model in a Flask/FastAPI REST endpoint

---

## 🛠️ Tech Stack

- **Language:** Python 3.x
- **Data Manipulation:** pandas, numpy
- **Visualisation:** matplotlib, seaborn
- **Machine Learning:** scikit-learn
- **Model Persistence:** joblib
- **Notebook:** Jupyter

---

## 📄 License

This project is licensed under the MIT License.

---

*Made with ❤️ for the Stellar Object Classification Capstone Project*
