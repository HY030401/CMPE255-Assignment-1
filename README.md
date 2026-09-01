# CMPE 255 Assignment 1 — AI-Assisted Data Science

## Overview

This repository contains my work for CMPE 255 Assignment 1.

The goal of this assignment is to use an AI coding assistant or chatbot to perform data science workflows end-to-end, understand the generated outputs, and document the complete process.

The repository is organized into two parts:

- **Part 1:** End-to-end AI-assisted data science using the Telco Customer Churn dataset.
- **Part 2:** Replication and exploration of data science experiments using prompts provided in the course repository.

---

# Part 1 — Telco Customer Churn Prediction

## Project Goal

The goal of Part 1 is to build an end-to-end customer churn prediction workflow using the Telco Customer Churn dataset.

The project investigates the following question:

> Can customer characteristics, service usage, contract information, and billing behavior be used to identify customers who are at risk of churn?

The workflow was developed with AI assistance and includes data understanding, cleaning, exploratory data analysis, preprocessing, machine learning, model evaluation, model interpretation, and business recommendations.

---

## Dataset

The project uses the **Telco Customer Churn** dataset.

The dataset contains:

- **7,043 customer records**
- **21 original columns**
- Customer demographic information
- Service subscriptions
- Contract information
- Payment information
- Monthly and total charges
- Customer churn status

The target variable is:

`Churn`

where:

- `No` = customer remained with the company
- `Yes` = customer churned

The original target distribution was:

- **No Churn:** 5,174 customers (73.46%)
- **Churn:** 1,869 customers (26.54%)

This class imbalance motivated the use of evaluation metrics beyond accuracy.

---

## End-to-End Data Science Workflow

The project follows the workflow below:

1. Business and data understanding
2. Data quality assessment
3. Data cleaning
4. Exploratory data analysis
5. Feature preprocessing
6. Train/test split
7. Logistic Regression
8. Random Forest
9. Gradient Boosting
10. Multi-metric model evaluation
11. Confusion matrix analysis
12. ROC and ROC-AUC analysis
13. Feature interpretation
14. Classification threshold analysis
15. Business recommendations

---

## Data Cleaning

An important data quality issue was identified in the `TotalCharges` column.

Although `TotalCharges` represents a numerical value, it was originally stored as an object/string column.

Further investigation identified **11 blank `TotalCharges` values**. All 11 records belonged to customers with:

`tenure = 0`

These customers appear to be new customers who had not yet accumulated total charges.

The column was therefore converted to numeric format and the blank values were replaced with `0` rather than removing the customer records.

The cleaned dataset retained all **7,043 customers**.

---

# Exploratory Data Analysis

## Churn Distribution

Approximately:

- **73.46%** of customers did not churn.
- **26.54%** of customers churned.

Because the target classes are imbalanced, accuracy alone was not used to determine model quality.

---

## Contract Type

Contract type showed a strong relationship with churn.

| Contract Type | Churn Rate |
|---|---:|
| Month-to-month | 42.71% |
| One year | 11.27% |
| Two year | 2.83% |

Month-to-month customers had substantially higher churn than customers with longer contracts.

---

## Customer Tenure

Average customer tenure was:

| Customer Group | Average Tenure |
|---|---:|
| No Churn | 37.57 months |
| Churn | 17.98 months |

Customers who churned tended to have considerably shorter relationships with the company.

---

## Monthly Charges

Average monthly charges were:

| Customer Group | Average Monthly Charge |
|---|---:|
| No Churn | $61.27 |
| Churn | $74.44 |

Customers who churned tended to have higher monthly charges.

---

## Internet Service

Churn rates differed substantially across internet service types:

| Internet Service | Churn Rate |
|---|---:|
| DSL | 18.96% |
| Fiber optic | 41.89% |
| No internet service | 7.40% |

Fiber optic customers showed the highest churn rate.

---

## Payment Method

Electronic check customers showed the highest churn rate:

| Payment Method | Churn Rate |
|---|---:|
| Electronic check | 45.29% |
| Mailed check | 19.11% |
| Bank transfer (automatic) | 16.71% |
| Credit card (automatic) | 15.24% |

These relationships represent associations in the dataset and should not automatically be interpreted as causal relationships.

---

# Machine Learning

Three classification models were trained and evaluated:

- Logistic Regression
- Random Forest
- Gradient Boosting

The same train/test split was used for all three models to provide a fair comparison.

Categorical variables were processed using one-hot encoding, while numerical variables were standardized where appropriate.

Preprocessing and model training were combined using scikit-learn pipelines to reduce the risk of data leakage.

---

## Model Comparison

| Model | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| **Logistic Regression** | **0.8055** | 0.6572 | **0.5588** | **0.6040** | 0.8421 |
| Random Forest | 0.7835 | 0.6186 | 0.4813 | 0.5414 | 0.8206 |
| Gradient Boosting | 0.8027 | **0.6655** | 0.5160 | 0.5813 | **0.8434** |

No model achieved the best result on every metric.

Gradient Boosting achieved the highest ROC-AUC and precision, while Logistic Regression achieved the highest accuracy, recall, and F1-score.

For this project, **Logistic Regression was selected as the primary model** because identifying customers who actually churn is important for retention applications.

---

## Logistic Regression Results

The selected Logistic Regression model achieved:

- **Accuracy:** 80.55%
- **Precision:** 65.72%
- **Recall:** 55.88%
- **F1-score:** 60.40%
- **ROC-AUC:** 84.21%

The confusion matrix was:

| | Predicted No Churn | Predicted Churn |
|---|---:|---:|
| **Actual No Churn** | 926 | 109 |
| **Actual Churn** | 165 | 209 |

The model correctly identified 209 churned customers but missed 165 customers who actually churned.

These false negatives are particularly important in a customer retention application because the company would fail to identify those customers as being at risk.

---

# Model Interpretation

The Logistic Regression model identified several characteristics associated with higher predicted churn, including:

- Fiber optic internet service
- Month-to-month contracts
- Higher total charges
- Electronic check payments
- Lack of online security
- Lack of technical support

Characteristics associated with lower predicted churn included:

- Longer customer tenure
- Two-year contracts
- DSL internet service
- Customers without internet service

These model relationships were broadly consistent with the earlier exploratory data analysis.

The coefficients describe associations learned by the model and should not be interpreted as proof of causation.

---

# Classification Threshold Experiment

The default classification threshold of `0.50` does not necessarily provide the best operating point for every business application.

Different Logistic Regression thresholds were therefore evaluated:

| Threshold | Precision | Recall | F1 Score |
|---:|---:|---:|---:|
| 0.30 | 0.5193 | **0.7540** | **0.6150** |
| 0.35 | 0.5432 | 0.7059 | 0.6140 |
| 0.40 | 0.5682 | 0.6684 | 0.6143 |
| 0.45 | 0.6021 | 0.6150 | 0.6085 |
| 0.50 | **0.6572** | 0.5588 | 0.6040 |

Reducing the threshold from `0.50` to `0.30` increased recall from **55.88% to 75.40%**.

This means the model can identify substantially more customers who eventually churn, but at the cost of lower precision and therefore more false-positive retention alerts.

The appropriate threshold should depend on the business cost of contacting customers compared with the cost of losing customers.

---

# Business Recommendations

Based on the exploratory analysis and machine learning results, several potential actions can be considered:

1. **Focus on newer customers**  
   Customers with shorter tenure showed substantially higher churn risk.

2. **Encourage appropriate customers toward longer contracts**  
   Month-to-month customers showed much higher churn than customers with one-year or two-year contracts.

3. **Investigate the fiber optic customer experience**  
   Fiber optic customers showed relatively high churn and were also associated with higher predicted churn in the model.

4. **Investigate electronic check customers**  
   Electronic check users showed substantially higher churn than customers using other payment methods.

5. **Use predicted churn risk for retention targeting**  
   A lower classification threshold could be used when the business prefers identifying more at-risk customers even at the cost of additional false-positive alerts.

---

# Key Takeaways

This project demonstrates that end-to-end data science involves more than simply training a machine learning model.

Important decisions included:

- Understanding data quality issues before modeling
- Interpreting exploratory patterns
- Preventing data leakage
- Comparing multiple models
- Evaluating models using more than accuracy
- Understanding false positives and false negatives
- Interpreting model features carefully
- Connecting classification thresholds with business objectives

A more complex model did not automatically produce better results. Logistic Regression remained highly competitive and provided the best recall and F1-score among the three evaluated models at the default threshold.

---

# Repository Structure

```text
CMPE255-Assignment-1/
│
├── README.md
│
├── Part_1/
│   ├── README.md
│   ├── CMPE255_Assignment1_Telco_Churn.ipynb
│   ├── CMPE255_Assignment1_Part1_ChatGPT_Transcript.pdf
│   └── WA_Fn-UseC_-Telco-Customer-Churn.csv
│
└── Part_2/
    ├── README.md
    ├── 00_Dynamic_Todo_Workspace.ipynb
    ├── 01_NYC_Taxi_Trip_Prediction.ipynb
    ├── 02_NanoLlama_Small_Language_Model.ipynb
    ├── 03_Customer_Segmentation_Clustering.ipynb
    ├── 04_Association_Pattern_Mining.ipynb
    ├── 05_Data_Science_Skills_Mastery_Lab.ipynb
    ├── 06_Anomaly_Detection.ipynb
    └── 12_Time_Series_Forecasting.ipynb
```

---

# Part 1 — Customer Churn Prediction

Part 1 is an end-to-end customer churn classification project using the Telco Customer Churn dataset.

The project includes:

- Business and data understanding
- Data quality checking
- Data cleaning
- Exploratory data analysis
- Feature preprocessing
- Logistic Regression
- Random Forest
- Gradient Boosting
- Multi-metric model evaluation
- ROC-AUC analysis
- Feature interpretation
- Classification threshold analysis
- Business recommendations

Logistic Regression was selected as the final model because it provided a strong balance of performance and better recall and F1 score for the customer retention objective.

Detailed code, outputs, and documentation are available in the [`Part_1`](./Part_1) directory.

**Status: Completed**

---

# Part 2 — Data Science Experiment Replications

Part 2 contains AI-assisted replications and compact adaptations of the instructor's Projects **00–05**.

All required Projects 00–05 were completed.

| Project | Experiment | Main Method / Goal | Status |
|---|---|---|---|
| 00 | Dynamic Todo Workspace | Python + Gradio interactive application | Completed |
| 01 | NYC Taxi Trip Prediction | Regression | Completed |
| 02 | NanoLlama / Small Language Model | Small language model fine-tuning | Completed |
| 03 | Customer Segmentation | K-Means clustering | Completed |
| 04 | Association Pattern Mining | Apriori / association rules | Completed |
| 05 | Data Science Skills Mastery Lab | Complete machine learning workflow | Completed |

Two additional experiments were also completed:

| Project | Experiment | Main Method |
|---|---|---|
| 06 | Anomaly Detection | Isolation Forest |
| 12 | Time Series Forecasting | Regression with time series features |

Detailed code, results, visualizations, limitations, and documentation are available in the [`Part_2`](./Part_2) directory.

**Status: Completed**

---

# Selected Part 2 Results

Some of the main results from Part 2 include:

- **NYC Taxi Prediction:** Random Forest achieved R² ≈ 0.735 and MAE ≈ 219 seconds.
- **NanoLlama:** Training loss decreased from approximately 10.83 to 10.71, but generated text remained poor, demonstrating that lower training loss does not automatically mean useful text generation.
- **Customer Segmentation:** Four clusters were selected with a Silhouette Score of approximately 0.577.
- **Association Mining:** Coffee → Cookies produced a lift of approximately 2.83.
- **Data Science Skills Lab:** Logistic Regression achieved approximately 98.25% test accuracy and 98.02% mean cross-validation accuracy.
- **Anomaly Detection:** Isolation Forest recovered all 50 intentionally created anomalies in the controlled synthetic experiment.
- **Time Series Forecasting:** Linear Regression achieved the best MAE of 7.67.

---

# AI-Assisted Development

ChatGPT was used throughout the assignment to assist with:

- Planning data science workflows
- Writing and understanding Python code
- Debugging notebook issues
- Designing exploratory analyses
- Comparing models
- Selecting evaluation methods
- Interpreting results
- Identifying limitations
- Organizing project documentation

Generated outputs were reviewed and tested throughout the workflow.

An important lesson from the assignment was that AI-generated code and conclusions still require human review.

For example, the NanoLlama experiment showed decreasing training loss but poor generated text. This required evaluating the actual model output rather than assuming that a lower loss meant the model was useful.

---

# Medium Article

A Medium article was published for Part 1 describing the complete customer churn workflow, including data cleaning, exploratory analysis, machine learning, model interpretation, threshold analysis, and business insights.

The article link is included in this repository.

---

# Chat Transcript

The AI-assisted development transcript for Part 1 is included in the `Part_1` directory.

The transcript documents the iterative process used to plan, implement, debug, evaluate, and interpret the customer churn project.

**Status: Completed**

---

# YouTube Walkthrough

A final YouTube walkthrough will cover both Part 1 and Part 2.

The video will include:

- Repository overview
- Part 1 customer churn workflow
- Part 1 model results and business findings
- Part 2 required Projects 00–05
- Additional experiments
- Main lessons from the AI-assisted workflow

**YouTube Video: Coming soon**

---

# Final Deliverables

- [x] Part 1 end-to-end data science notebook
- [x] Part 1 dataset
- [x] Exploratory data analysis
- [x] Machine learning model comparison
- [x] Model interpretation
- [x] Classification threshold experiment
- [x] Medium article
- [x] Chat transcript
- [x] Part 2 Project 00
- [x] Part 2 Project 01
- [x] Part 2 Project 02
- [x] Part 2 Project 03
- [x] Part 2 Project 04
- [x] Part 2 Project 05
- [x] Additional Experiment 06
- [x] Additional Experiment 12
- [x] Part 2 documentation
- [ ] YouTube walkthrough

---

# Assignment Status

**Part 1: Completed**

**Part 2 Required Projects 00–05: Completed**

**Additional Experiments: Completed**

**Medium Article: Published**

**Chat Transcript: Completed**

**YouTube Walkthrough: Pending**
