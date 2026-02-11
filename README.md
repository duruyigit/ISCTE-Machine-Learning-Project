# ISCTE-Machine-Learning-Project
Final project for ISCTE Introduction to Machine Learning course (2025/2026). Analyzes Maia Municipality energy data using CRISP-DM for consumer clustering and time-series forecasting.

# Energy Consumption Clustering & Forecasting
# 📌 Project Overview
This project investigates the characterization and forecasting of electricity consumption patterns for individual CPEs (Consumption Points of Electricity) of the Municipality of Maia.
The study follows the CRISP-DM methodology, combining:
Unsupervised learning (Clustering)
Supervised learning (Forecasting)
Feature engineering
Cluster-aware modeling strategies
The main objective is to understand heterogeneous consumption behaviors and evaluate whether model complexity improves forecasting performance over a simple weekly persistence baseline.

# 📊 Dataset Description
The dataset contains high-frequency (15-minute resolution) energy measurements from January 2023 to May 2025.
Key variables include:
Active Power
Reactive Inductive Power
Reactive Capacitive Power
Timestamp
CPE identifier
Consumption column was removed as specified in project guidelines. 

# 🔎 Data Preparation & Feature Engineering
Key steps:
Missing value handling
Temporal interpolation
Removal of duplicates
Outlier detection (IQR method)
Time-window aggregation (Night, Morning, Afternoon, Evening)
Engineered features include:
Peak-to-average ratio
Load variability index
Seasonal consumption ratio
Weekday vs weekend ratio
Nighttime vs worktime load share
Power factor and reactive power indicators
Correlation analysis and feature selection were applied to ensure non-redundant, informative features.

# 🤖 Exercise 1 – Clustering
Two clustering methods were applied:
K-Means
Evaluated k ∈ [2–15]
Silhouette score, Davies–Bouldin, Calinski–Harabasz used
Final selection: k = 8
PCA visualization for dimensionality reduction
DBSCAN
Epsilon selected using k-distance plot
Effect-size based cluster interpretation
Clusters identified:
Strictly periodic consumers
Semi-regular consumers
Highly irregular / noisy consumers
Near-zero consumption consumers
Volatile profiles
Key insight:
Consumer regularity is more important than magnitude for forecasting performance.

# 📈 Exercise 2 – Forecasting Models
Goal:
One-week-ahead active power forecasting.
Models evaluated:
Weekly Persistence Baseline (Lag 168)
ARIMA
Random Forest
XGBoost
MLP

Key findings:
Hourly aggregation drastically reduced noise.
Weekly baseline consistently outperformed complex ML models.
Model performance strongly depended on cluster membership.
No single global best model exists.

# ⚙️ Experiment 3 – Cluster-Aware Modeling
Instead of applying one global pipeline, cluster-specific preprocessing was applied:
Input scalers tested:
None
StandardScaler
MinMaxScaler
RobustScaler
Target transformations:
None
Log1p
Standardized
Seasonal subtraction

Findings:
Tree-based models (RF, XGBoost) are robust to scaling.
Linear models require careful normalization.
Cluster-based normalization improves robustness.
Baseline remains dominant for strictly periodic clusters.

# 🧠 Core Conclusions
Weekly seasonality dominates consumption behavior.
Forecast accuracy depends more on behavioral regularity than model complexity.
Cluster-aware modeling significantly improves interpretability.
Highly irregular clusters require exogenous variables for meaningful improvement.
For stable consumers, simple persistence is often optimal.

# 🛠 Tech Stack
Python
Pandas
NumPy
Scikit-learn
XGBoost
Statsmodels (ARIMA)
Matplotlib / Seaborn

# 📌 Skills Demonstrated
CRISP-DM methodology
Advanced feature engineering
Clustering validation techniques
Time-series forecasting
Cluster-aware modeling
Bias–variance tradeoff analysis
Model evaluation with RMSE / NRMSE

# 🚀 Future Work
Integration of exogenous variables (weather, calendar events)
Probabilistic forecasting
Automated model selection per cluster
Production-level pipeline implementation
