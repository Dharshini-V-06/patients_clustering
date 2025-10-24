#  Patient Health Clustering Analysis

This project performs **unsupervised learning** on a healthcare dataset containing patient information to identify potential patterns or groups using **K-Means**, **Hierarchical Clustering**, and **DBSCAN**.
It includes complete **data preprocessing**, **dimensionality reduction (PCA)**, **outlier handling**, and **cluster evaluation**.

---

##  Project Overview

The goal of this project is to analyze and cluster patients based on health metrics such as blood pressure, cholesterol, glucose levels, and other physiological and lifestyle indicators.
By applying multiple clustering algorithms and comparing their performance, we aim to identify meaningful patient segments for potential medical insights or risk grouping.

---

##  Dataset Information

**File:** `patient_dataset.csv`
**Shape:** (6000, 16)

| Column            | Description                   | Type            |
| :---------------- | :---------------------------- | :-------------- |
| age               | Age of patient                | Numeric         |
| gender            | Gender (0 = Female, 1 = Male) | Numeric     |
| chest_pain_type   | Type of chest pain            | Numeric     |
| blood_pressure    | Resting blood pressure        | Numeric         |
| cholesterol       | Serum cholesterol level       | Numeric         |
| max_heart_rate    | Maximum heart rate achieved   | Numeric         |
| exercise_angina   | Exercise-induced angina (0/1) | Binary          |
| plasma_glucose    | Plasma glucose level          | Numeric         |
| skin_thickness    | Skin fold thickness           | Numeric         |
| insulin           | Insulin level                 | Numeric         |
| bmi               | Body Mass Index               | Numeric         |
| diabetes_pedigree | Family diabetes likelihood    | Numeric         |
| hypertension      | Hypertension presence         | Binary          |
| heart_disease     | Heart disease status          | Binary (Target) |
| residence_type    | Urban/Rural                   | Categorical     |
| smoking_status    | Smoker / Non-Smoker / Unknown | Categorical     |

---

##  Data Preprocessing Steps

1. **Handled Missing Values**

   * Numerical columns (`plasma_glucose`, `skin_thickness`, `insulin`) → filled with **mean**.
   * Categorical columns (`gender`, `residence_type`) → filled with **mode**.

2. **Encoded Categorical Features**

   * Used `LabelEncoder` for binary and categorical columns (`gender`, `residence_type`, etc.).

3. **Outlier Treatment**

   * Applied **IQR (Interquartile Range)** method and **capped** outliers beyond 1.5×IQR.

4. **Feature Scaling**

   * Standardized features using **`StandardScaler`**.

5. **Dimensionality Reduction**

   * Applied **PCA** (2 components) for better visualization and clustering performance.

---

##  Clustering Algorithms Used

### 1. **K-Means Clustering**

* Optimal `k` determined using the **Elbow Method**.
* Final clusters: **2**
* Silhouette Score: **0.309**

### 2. **Hierarchical Clustering**

* Performed using **Ward linkage**.
* Number of clusters: **2**
* Silhouette Score: **0.255**

### 3. **DBSCAN (Density-Based Spatial Clustering)**

* Parameters: `eps=0.3`, `min_samples=3`
* Identified **2 clusters + 29 noise points**
* Silhouette Score: **0.406**

---

##  Model Comparison

| Algorithm        | Silhouette Score |
| ---------------- | ---------------- |
| **K-Means**      | 0.309            |
| **Hierarchical** | 0.255            |
| **DBSCAN**       | **0.406**        |

 **DBSCAN** performed best, forming the most natural clusters with the highest silhouette score.

---

##  Insights

* The dataset was nearly symmetric (no significant skewness), meaning scaling and PCA were highly effective.
* DBSCAN handled noisy data better than K-Means and Hierarchical methods.
* Potential for deeper analysis using more features or supervised learning (predicting `heart_disease`).

---

##  Libraries Used

```python
pandas
numpy
matplotlib
seaborn
scikit-learn
scipy
```

---

##  Visualizations

* **Boxplots** for outlier detection (before and after treatment)
* **Elbow curve** for optimal K selection
* **Dendrogram** for hierarchical clustering
* **k-distance plot** for DBSCAN parameter tuning

---
