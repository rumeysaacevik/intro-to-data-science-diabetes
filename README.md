# 🩺 Diabetes Prediction (PIMA Dataset)

This project focuses on **early diabetes risk prediction** using the **PIMA Indians Diabetes Dataset**.  
The problem is formulated as a **binary classification task** where the goal is to predict whether a patient is diabetic (**Outcome = 1**) or not (**Outcome = 0**) based on clinical measurements.

---

## 👥 Group Members
- Rümeysa Çevik
- Ayşe Serra Gümüştakım

---

## 🎯 Project Objective
Early prediction of diabetes supports preventive healthcare decisions and reduces long-term complications.  
This project aims to build and compare multiple machine learning models under a consistent preprocessing and evaluation framework.

---

## 📦 Dataset
- **PIMA Indians Diabetes Dataset**
- **768 samples**, **8 input features**, **1 target**
- Target: **Outcome** (1 = diabetic, 0 = non-diabetic)
- All features are **numerical**, so **no categorical encoding** is required.

Features:
- Pregnancies, Glucose, BloodPressure, SkinThickness, Insulin, BMI,
  DiabetesPedigreeFunction, Age

---

## 🔍 Exploratory Data Analysis (EDA)
EDA is performed to understand:
- Class distribution (moderate imbalance)
- Feature distributions (skewness & zero-heavy columns)
- Outliers (especially in Insulin and SkinThickness)
- Feature relationships (correlation heatmap, scatterplots, pairplots)

Key observation:
- Some physiological variables include **0 values** that are not medically plausible and are treated as missing.

---

## 🧼 Data Preprocessing

### 1) Missing Value Handling
In the PIMA dataset, **0 values** in these columns are treated as missing:
- Glucose, BloodPressure, SkinThickness, Insulin, BMI

Process:
- Replace 0 → NaN
- Impute with **median** (robust to skewness & outliers)

### 2) Outlier Handling
Outliers are identified using:
- **IQR method**
- **Z-score analysis**

Instead of removing outliers (dataset is small), values are **winsorized**:
- Clip feature values to IQR bounds

### 3) Feature Scaling
Standardization is applied using **StandardScaler**, especially for:
- Logistic Regression
- SVM (RBF)
- PCA pipelines

---

## 🤖 Models Used

### Baseline Models
- Logistic Regression (interpretable baseline)
- Random Forest (nonlinear ensemble)
- SVM (RBF kernel)

### Hyperparameter Tuning
Tuning is performed using:
- **GridSearchCV**
- **StratifiedKFold** cross-validation
- Optimization metric: **ROC-AUC**

### Additional Improvements Tested
- Feature Selection:
  - SelectKBest (mutual information)
  - RFE (Logistic Regression)
- PCA:
  - retain ~95% variance + Logistic Regression

---

## 📊 Evaluation
Models are evaluated using:
- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC

Also included:
- Confusion matrices
- ROC curves

---

## ✅ Results Summary (Highlights)

- **SVM baseline** achieved the best ROC-AUC among tested configurations.
- **Random Forest baseline** achieved the highest accuracy among baseline models.
- Hyperparameter tuning gave **limited improvements** overall.
- Feature Selection and PCA **reduced interpretability/complexity** but did not improve performance on this dataset.

---

## 🧪 Statistical Test (Hypothesis Testing)
A paired t-test is used to compare ROC-AUC scores (baseline vs tuned):

- **Logistic Regression**: no statistically significant difference
- **Random Forest**: statistically significant difference (p < 0.05)
- **SVM**: no statistically significant difference

---

## 🛠 Technologies Used
- Python
- NumPy, Pandas
- Scikit-learn
- Matplotlib, Seaborn

---

## 📌 Notes / Future Work
Potential improvements:
- Threshold optimization (precision/recall trade-off)
- Cost-sensitive learning
- Calibration
- Ensemble stacking
- More robust validation strategies
