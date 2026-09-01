# CMPE 255 Assignment 1 — Part 1

## Telco Customer Churn Prediction

This folder contains Part 1 of my CMPE 255 Assignment 1.

The goal of this project is to complete an end-to-end data science workflow using an AI coding assistant.

The project uses the Telco Customer Churn dataset to answer the following question:

> Can customer information, service usage, contract type, and billing behavior be used to identify customers who are at risk of churn?

---

# Files

| File | Description |
|---|---|
| `CMPE255_Assignment1_Telco_Churn.ipynb` | Complete data science notebook |
| `WA_Fn-UseC_-Telco-Customer-Churn.csv` | Telco Customer Churn dataset |
| `CMPE255_Assignment1_Part1_ChatGPT_Transcript.pdf` | AI-assisted development transcript |
| `README.md` | Part 1 documentation |

---

# Dataset

The Telco Customer Churn dataset contains:

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

- `No` = customer did not leave
- `Yes` = customer left the company

The original class distribution was:

- **No Churn:** 5,174 customers — 73.46%
- **Churn:** 1,869 customers — 26.54%

Because the two classes are not balanced, model performance was evaluated using more than accuracy alone.

---

# Data Science Workflow

The notebook follows an end-to-end workflow:

1. Business and data understanding
2. Data quality checking
3. Data cleaning
4. Exploratory data analysis
5. Feature preprocessing
6. Train/test splitting
7. Logistic Regression
8. Random Forest
9. Gradient Boosting
10. Model comparison
11. Confusion matrix analysis
12. ROC-AUC analysis
13. Feature interpretation
14. Classification threshold analysis
15. Business recommendations

---

# Data Cleaning

An important issue was found in the `TotalCharges` column.

Although it represents a numerical value, the column was originally stored as text.

There were **11 blank TotalCharges values**.

All 11 customers had:

```text
tenure = 0
```

These records appeared to represent new customers who had not yet accumulated total charges.

The column was converted to numeric format and the blank values were replaced with `0`.

No customer records were removed.

The cleaned dataset still contained all **7,043 customers**.

---

# Exploratory Data Analysis

Several useful patterns were found during exploratory analysis.

## Contract Type

| Contract Type | Churn Rate |
|---|---:|
| Month-to-month | 42.71% |
| One year | 11.27% |
| Two year | 2.83% |

Month-to-month customers showed much higher churn than customers with longer contracts.

## Customer Tenure

| Customer Group | Average Tenure |
|---|---:|
| No Churn | 37.57 months |
| Churn | 17.98 months |

Customers who churned had much shorter average tenure.

## Internet Service

| Internet Service | Churn Rate |
|---|---:|
| DSL | 18.96% |
| Fiber optic | 41.89% |
| No internet service | 7.40% |

Fiber optic customers showed the highest churn rate.

## Payment Method

Electronic check customers had the highest churn rate at approximately:

**45.29%**

These findings describe relationships in the dataset and should not automatically be interpreted as cause-and-effect relationships.

---

# Machine Learning Models

Three classification models were trained:

- Logistic Regression
- Random Forest
- Gradient Boosting

The same train/test split was used for all models.

Categorical features were processed using one-hot encoding, and numerical features were standardized where appropriate.

Scikit-learn pipelines were used to keep preprocessing and modeling together and reduce the risk of data leakage.

---

# Model Comparison

| Model | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| **Logistic Regression** | **0.8055** | 0.6572 | **0.5588** | **0.6040** | 0.8421 |
| Random Forest | 0.7835 | 0.6186 | 0.4813 | 0.5414 | 0.8206 |
| Gradient Boosting | 0.8027 | **0.6655** | 0.5160 | 0.5813 | **0.8434** |

No model produced the best value for every metric.

Gradient Boosting achieved the highest ROC-AUC and precision.

Logistic Regression achieved the highest accuracy, recall, and F1 score.

For this project, **Logistic Regression was selected as the main model** because recall is important when the goal is to identify customers who may leave.

---

# Logistic Regression Results

The selected Logistic Regression model achieved:

- **Accuracy:** 80.55%
- **Precision:** 65.72%
- **Recall:** 55.88%
- **F1 Score:** 60.40%
- **ROC-AUC:** 84.21%

The confusion matrix was:

| | Predicted No Churn | Predicted Churn |
|---|---:|---:|
| **Actual No Churn** | 926 | 109 |
| **Actual Churn** | 165 | 209 |

The model correctly identified 209 customers who churned but missed 165 customers who actually churned.

For a customer retention system, these false negatives are important because those customers would not receive a retention alert.

---

# Classification Threshold Experiment

The default probability threshold of `0.50` is not always the best choice for a business problem.

Several thresholds were compared:

| Threshold | Precision | Recall | F1 Score |
|---:|---:|---:|---:|
| 0.30 | 0.5193 | **0.7540** | **0.6150** |
| 0.35 | 0.5432 | 0.7059 | 0.6140 |
| 0.40 | 0.5682 | 0.6684 | 0.6143 |
| 0.45 | 0.6021 | 0.6150 | 0.6085 |
| 0.50 | **0.6572** | 0.5588 | 0.6040 |

Reducing the threshold from `0.50` to `0.30` increased recall from:

**55.88% → 75.40%**

This allows the model to identify more customers who may churn.

However, it also lowers precision and creates more false-positive alerts.

The best threshold therefore depends on the business cost of contacting a customer compared with the cost of losing a customer.

---

# Model Interpretation

The Logistic Regression model identified several characteristics associated with higher predicted churn, including:

- Fiber optic internet
- Month-to-month contracts
- Electronic check payments
- Lack of online security
- Lack of technical support

Characteristics associated with lower predicted churn included:

- Longer customer tenure
- Two-year contracts
- DSL internet service

These relationships are useful for interpretation but should not be treated as proof of causation.

---

# Business Recommendations

Based on the analysis, several possible business actions were identified:

1. Focus retention efforts on newer customers.
2. Consider encouraging suitable customers toward longer contracts.
3. Investigate the customer experience for fiber optic users.
4. Investigate why electronic check customers show higher churn.
5. Use predicted churn probabilities to support targeted retention campaigns.
6. Consider a lower classification threshold when identifying more at-risk customers is more important than avoiding false-positive alerts.

---

# Key Lessons

This project showed that data science involves more than simply training a model.

Important lessons included:

- Check data quality before modeling.
- Understand the data before selecting algorithms.
- Avoid data leakage.
- Compare multiple models.
- Do not rely only on accuracy.
- Understand false positives and false negatives.
- Match model evaluation to the business goal.
- A more complex model does not automatically perform better.
- Classification thresholds can be adjusted for different business needs.
- AI-generated code and conclusions still need to be tested and reviewed.

---

# AI-Assisted Workflow

ChatGPT was used throughout Part 1 to help with:

- Planning the data science workflow
- Writing and explaining Python code
- Debugging problems
- Designing exploratory analysis
- Selecting evaluation metrics
- Comparing models
- Interpreting model outputs
- Testing classification thresholds
- Developing business recommendations
- Organizing documentation

The generated code was executed in Google Colab and the outputs were reviewed during the project.

The AI-assisted development process is documented in:

`CMPE255_Assignment1_Part1_ChatGPT_Transcript.pdf`

---

# Medium Article

A detailed Medium article was also published for this project:

[Predicting Customer Churn with AI-Assisted Data Science: An End-to-End Machine Learning Project](https://medium.com/@yhz1805/predicting-customer-churn-with-ai-assisted-data-science-an-end-to-end-machine-learning-project-38d42dc91b9d)

The article explains the full workflow, results, model interpretation, classification threshold experiment, and business insights.

---

# How to Run

1. Open `CMPE255_Assignment1_Telco_Churn.ipynb` in Google Colab or Jupyter Notebook.
2. Make sure `WA_Fn-UseC_-Telco-Customer-Churn.csv` is available.
3. Update the dataset file path if necessary.
4. Run the notebook cells from top to bottom.
5. Review the EDA, model results, threshold experiment, and conclusions.

---

# Status

- [x] Dataset included
- [x] Data cleaning
- [x] Exploratory data analysis
- [x] Machine learning models
- [x] Model comparison
- [x] Model interpretation
- [x] Classification threshold experiment
- [x] Business recommendations
- [x] ChatGPT transcript
- [x] Medium article

**Part 1: Completed**
