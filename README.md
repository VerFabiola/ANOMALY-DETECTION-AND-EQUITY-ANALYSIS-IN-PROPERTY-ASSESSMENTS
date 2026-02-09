# Outliers Detection and Equity Analysis in Property Assessments
## 📌 Project Overview
This project analyzes residential property assessment data from the City of Edmonton’s Open Data Portal to evaluate the reliability and equity of assessed values. The primary objective is to identify anomalous property assessments that deviate significantly from expected values based on observable property attributes.
## 🎯 Objectives
- Evaluate whether detected anomalies are randomly distributed or concentrated across specific neighborhoods or socioeconomic groupings.
- Detect atypical assessments using a combination of regression diagnostics, unsupervised anomaly detection, and ensemble-based machine learning methods
- Compare anomaly detection results across multiple methods to improve robustness and interpretability.
- Conduct equity analysis to identify potential spatial or socioeconomic disparities in assessment outcomes.
## 📊 Data Cleaning & Preparation
- **Dataset**: Property Assessment Data dataset from the City of Edmonton’s Open Data Portal, containing **5.07 million properties, 21 variables**, and assessment values from 2012–2024.
- Removed irrelevant variables and records by dropping non-analytical identifiers and columns with >70% missing values to preserve data quality.
- Filtered the dataset to residential properties assessed between 2021–2024, excluding properties without garages to reduce heterogeneity.
- Performed feature engineering.
- Restricted the analysis to low-density residential zoning categories to ensure a homogeneous and comparable property set.
- **Final Dataset: 13 variables for 682,000 residential properties spanning 268 Edmonton neighbourhoods**.
## 🔎 Anomaly Detection
### Statistical diagnostics with Cooks Distance: Cook’s Distance is a classical regression diagnostic measure that identifies observations with a disproportionately large influence on a fitted regression model.
- Log assessed values are predicted using property characteristics, **6,821 properties** were identified as regression-based outliers, model achieves **R² = 0.796**; 
### Unsupervised ML: Isolation Forest an unsupervised algorithm designed to detect anomalies by isolating them rather than profiling normal data
- Trained multiple models using different feature subsets (e.g., all continuous variables, spatial + value, structural + value, dependent + strongest predictors) ensuring robust detection across varied data perspectives.
- Results:  **12,000** properties were consistently flagged as anomalies, representing 39% of all Isolation Forest detected outliers.
### Ensemble ML: Random Forest, Gradient Boosting
- Trained ensemble ML to predict log-assessed property values. Data was split 80% training / 20% testing with 3-fold cross-validation.
- Hyperparameter Tuning: Key model parameters were optimized using grid search.
- Performance: Random Forest R² ≈ 0.844; Gradient Boosting R² ≈ 0.759, flagging **26,491–28,007** anomalous properties. Top predictive features included Neighbourhood, Property Age, and Log Lot Size.
## 📈 Key Insights
- Spatial clustering of agreed anomalies is observed in Edmonton’s central corridor and west side, particularly along the river valley.
- Neighborhoods with the highest anomaly rates(12%) tend to contain significantly larger than average residential lot
- Over-assessed properties are typically newer homes on large lots with the highest assessed values,
- Under-assessed properties are more often smaller, newer constructions with lower assessed values relative to comparable properties
## ⚠️ Limitations 
- Limited to low density residential properties and excludes important market features (e.g., renovations, interior quality, and other structural attributes).
- Cook’s Distance is sensitive to threshold selection, future research could combine threshold based methods with studentized residuals.
