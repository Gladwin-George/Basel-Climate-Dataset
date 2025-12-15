# Task 1 – Basel Climate Dataset Clustering

This repository contains the implementation for **Task 1 of the SCC451 Machine Learning coursework**, focusing on **unsupervised clustering of climate data** from Basel, Switzerland.

The project demonstrates a complete clustering pipeline, including preprocessing, dimensionality reduction, model selection, and quantitative evaluation.

---

## 📊 Dataset
- **Name:** ClimateDataBasel.csv  
- **Source:** meteoblue (public climate data)  
- **Records:** 1763 daily observations  
- **Features:** 18 meteorological variables  
- **Period:** 2010–2019 (summer & winter)

Key variables include temperature, relative humidity, sea level pressure, precipitation, snowfall, sunshine duration, and wind statistics.

---

## ⚙️ Workflow Overview

### 1. Data Inspection
- Loaded raw CSV data without headers
- Assigned meaningful feature names
- Verified:
  - No missing values
  - No duplicate records

---

### 2. Outlier Detection
- Applied **Isolation Forest**
- Removed ~2% extreme anomalies
- Improves robustness for distance-based clustering methods

---

### 3. Feature Scaling
- Used **RobustScaler**
- Chosen due to skewed distributions and extreme climate values
- Reduces the influence of outliers compared to standard scaling

---

### 4. Feature Selection
- Removed highly correlated features (|ρ| > 0.95)
- Reduced redundancy while preserving information
- Final feature count: **15**

---

### 5. Dimensionality Reduction
- Applied **Principal Component Analysis (PCA)**
- Retained **95% cumulative variance**
- Reduced data to **6 principal components**

---

## 🔍 Clustering Methods

### K-Means
- Tested clusters: `k = 2 → 10`
- Optimal `k = 2` (highest Silhouette score)
- Strong global separation
- Sensitive to scale and cluster shape

---

### DBSCAN
- Applied on original (non–outlier-removed) data
- PCA (2D) used for distance computation
- `eps` selected using k-distance plot
- Results:
  - 2 clusters
  - ~12% noise points
- Excels at:
  - Detecting non-spherical clusters
  - Identifying anomalous climate events

---

### Gaussian Mixture Model (GMM)
- Applied in PCA-reduced feature space
- Model selection using **AIC** and **BIC**
- Best configuration:
  - 7 components
  - Spherical covariance
- Captures overlapping and gradual climate transitions

---

## 📈 Evaluation Metrics
All models were evaluated using:

- **Silhouette Score** (↑ better)
- **Davies–Bouldin Index** (↓ better)
- **Calinski–Harabasz Index** (↑ better)

Results are saved and visualised for direct comparison.

---

## 🏆 Summary of Results
- **DBSCAN**: Best compactness and separation, strong noise detection  
- **K-Means**: Clear global partitioning  
- **GMM**: Models soft boundaries but weaker separation  

Each method highlights different structural aspects of the climate data.

---

## 🧪 Requirements
```bash
python >= 3.8
numpy
pandas
scikit-learn
matplotlib
