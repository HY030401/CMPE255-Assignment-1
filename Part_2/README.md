# Part 2 — Data Science Experiment Replications

This directory contains Part 2 of my CMPE 255 Assignment 1.

The goal of Part 2 is to replicate and adapt data science experiments from the instructor's `data_science_examples` repository using an AI-assisted coding workflow.

Rather than reproducing every experiment exactly, I selected and implemented five experiments covering different areas of data science and machine learning.

## Experiments

### 1. NYC Taxi Trip Duration Prediction

**Notebook:** `01_NYC_Taxi_Trip_Prediction.ipynb`

This experiment applies supervised regression to predict NYC taxi trip duration.

The workflow includes:

- Data exploration and cleaning
- Geographic distance feature engineering
- Time-based feature engineering
- Baseline prediction
- Linear Regression
- Random Forest Regression
- Model comparison
- Feature importance analysis
- Prediction demonstration

The Random Forest model achieved the best performance:

- MAE: approximately 219 seconds
- RMSE: approximately 334 seconds
- R²: approximately 0.735

Straight-line trip distance was the most important predictive feature.

---

### 2. Customer Segmentation with K-Means

**Notebook:** `02_Customer_Segmentation_Clustering.ipynb`

This experiment demonstrates unsupervised customer segmentation using synthetic customer behavioral data.

The workflow includes:

- Customer data exploration
- Feature standardization
- Elbow Method
- Silhouette Score analysis
- K-Means clustering
- PCA visualization
- Cluster profiling
- Business interpretation

Both the Elbow Method and Silhouette Score supported selecting four customer clusters.

The final four segments were interpreted as:

1. Premium High-Value Customers
2. Conservative Affluent Customers
3. Budget / Low-Engagement Customers
4. Frequent Value Shoppers

The four-cluster solution achieved a Silhouette Score of approximately 0.577.

---

### 3. Association Pattern Mining

**Notebook:** `03_Association_Pattern_Mining.ipynb`

This experiment demonstrates market basket analysis using the Apriori algorithm.

The workflow includes:

- Synthetic retail transaction generation
- Transaction encoding
- Frequent itemset mining
- Association rule generation
- Support analysis
- Confidence analysis
- Lift analysis
- Business interpretation

Some of the strongest discovered relationships included:

- Coffee → Cookies: Lift ≈ 2.83
- Chips → Soda: Lift ≈ 2.75
- Pasta → Tomato Sauce: Lift ≈ 2.59
- Bread → Milk: Lift ≈ 2.10

These patterns demonstrate how association mining can support cross-selling, product bundling, and recommendation strategies.

---

### 4. Anomaly Detection with Isolation Forest

**Notebook:** `04_Anomaly_Detection.ipynb`

This experiment demonstrates unsupervised anomaly detection using synthetic financial transaction data.

The workflow includes:

- Transaction data generation
- Exploratory analysis
- Feature standardization
- Isolation Forest
- Anomaly scoring
- Anomaly visualization
- Evaluation against known simulated anomalies
- Business interpretation

The dataset contained 1,000 transactions, including 50 intentionally simulated anomalies.

Isolation Forest recovered all 50 simulated anomalies in the controlled experiment.

The perfect result reflects the deliberately well-separated synthetic data and known anomaly proportion and should not be interpreted as expected real-world fraud detection performance.

---

### 5. Time Series Forecasting

**Notebook:** `05_Time_Series_Forecasting.ipynb`

This experiment demonstrates daily sales forecasting using chronological model evaluation.

The workflow includes:

- Time series exploration
- Trend and seasonality analysis
- Lag feature engineering
- Chronological train/test splitting
- Naive baseline forecasting
- Linear Regression
- Random Forest Regression
- Model comparison
- Feature importance
- Recursive 30-day forecasting

Model performance:

| Model | MAE | RMSE |
|---|---:|---:|
| Naive Baseline | 13.07 | 15.86 |
| Linear Regression | 7.67 | 9.66 |
| Random Forest | 8.34 | 10.32 |

Linear Regression achieved the best test performance.

The Random Forest feature importance analysis also showed that 7-day and 14-day lag features were particularly informative, which is consistent with the weekly seasonal pattern in the synthetic time series.

---

## Methods Covered

Across the five experiments, Part 2 demonstrates several different data science techniques:

| Experiment | Main Technique |
|---|---|
| NYC Taxi Trip Prediction | Supervised Regression |
| Customer Segmentation | Unsupervised Clustering |
| Association Pattern Mining | Apriori / Association Rules |
| Anomaly Detection | Isolation Forest |
| Time Series Forecasting | Forecasting / Regression |

Together with the customer churn classification project in Part 1, the assignment covers classification, regression, clustering, association mining, anomaly detection, and time series forecasting.

## AI-Assisted Workflow

AI assistance was used throughout the experiments to support:

- Experiment planning
- Code generation
- Debugging
- Feature engineering
- Model selection
- Result interpretation
- Visualization
- Business insight development
- Documentation

The generated code was executed and evaluated in Google Colab, and the experimental results were reviewed and interpreted before being included in the final notebooks.

## Notes on Synthetic Data

Several experiments use synthetic datasets to create controlled and reproducible demonstrations.

The notebooks explicitly identify where synthetic data is used. Results from these experiments are intended to demonstrate data science methodology and should not be interpreted as evidence about real customers, transactions, or business behavior.

## YouTube Walkthrough

A video walkthrough covering both Part 1 and Part 2 will be added here after recording.

**YouTube Video:** Coming soon
