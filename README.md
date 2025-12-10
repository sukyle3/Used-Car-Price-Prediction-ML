# Market Valuation Engine: Used-Car Price Prediction


## Overview
Used-car pricing depends on a mix of numerical and categorical factors such as mileage, vehicle age, brand, fuel type, transmission, and condition. In this project, my friends and I tried to evaluate which supervised regression approach best captures these relationships and how unsupervised structure can support interpretability.

---

## Methods

### 1) Data Cleaning & Feature Engineering
- Handled missing values and standardized inconsistent categories  
  (e.g., imputing missing fuel types for Tesla/Rivian as **electric**, consolidating hybrid labels).
- Created **Age** from model year.
- Applied **frequency encoding** for high-cardinality categorical variables to strengthen model performance.

### 2) Unsupervised Learning (Interpretability)
- Applied **K-Means**, **Spectral Clustering**, and **K-Prototypes** to explore latent pricing structure.
- Identified **8 clusters** using the Elbow Method (TSS) and Silhouette analysis.
- Cluster patterns showed meaningful separation in **log(price)**, mileage, and age, helping contextualize downstream supervised results.

### 3) Supervised Model Benchmarking
- Benchmarked five models using an **80/20 train-test split** with **grid search + cross-validation**:
  - Elastic Net, KNN, SVR, Random Forest, CatBoost
- Evaluated performance using **RMSE** and **R²**.

---

## Results (Test Set)

| Model | Test RMSE | Test R² | Key Techniques Demonstrated |
|------|-----------:|--------:|-----------------------------|
| **CatBoost Regressor** | **21,524.72** | **0.74** | Native handling of categorical features, optimized gradient boosting |
| Random Forest | 29,279.34 | 0.52 | Ensemble learning, tuning of tree-based hyperparameters |
| KNN Regression | 36,928.77 | 0.24 | Feature scaling, distance-based prediction, K selection |
| Support Vector Regression (SVR) | 36,011.11 | 0.28 | Kernel methods (RBF), tuning **C** and **gamma** |
| Elastic Net | 42,569.08 | 0.24 | Regularization (L1/L2), outlier sensitivity awareness |

---

<p align="center"><b>CatBoost: Predicted vs Actual</b></p>
<p align="center">
  <img width="650" alt="CatBoost predicted vs actual" src="https://github.com/user-attachments/assets/d11ef4fd-c63a-412f-ae06-c32dbbcde65a" />
</p>

<p align="center"><b>CatBoost: Feature Importance</b></p>
<p align="center">
  <img width="650" alt="CatBoost feature importance" src="https://github.com/user-attachments/assets/ec072b1e-556e-4814-922a-615c2dc11201" />
</p>

<p align="center"><b>K-Means: Elbow + Silhouette</b></p>
<p align="center">
  <img width="650" alt="K-Means elbow and silhouette" src="https://github.com/user-attachments/assets/394b653c-d935-4073-b221-dcde5332b3cd" />
</p>



## Key Findings
- **Best model:** CatBoost achieved the strongest performance by a clear margin (**RMSE ≈ 21.5K**, **R² ≈ 0.74**).
- **Primary pricing drivers:** **Mileage**, **Vehicle Age**, and **Brand** were the most influential predictors in CatBoost feature importance analysis.
- **Interpretability value-add:** Clustering revealed intuitive pricing segments that aligned with age/mileage trends, supporting more business-friendly explanations of model outputs.

---

## Limitations
The project also examined why a depreciation-trained model may **overestimate** prices when extrapolated toward near-new vehicle conditions, since external market forces (macro trends, manufacturing costs, demand shocks) are not explicitly captured.

---

## Languages / Libraries
- **Languages:** Python, R  
- **Libraries:** pandas, NumPy, scikit-learn, CatBoost, Matplotlib, Seaborn  

