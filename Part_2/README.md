# CMPE 255 Assignment 1 — Part 2

## Data Science Experiment Replications

Part 2 contains my AI-assisted replications and adaptations of Projects **00–05** from the instructor's `data_science_examples` repository.

The original projects include larger applications, user interfaces, training workflows, and data science demonstrations. For this assignment, I used the instructor prompts as the main goals and created smaller, reproducible versions that can run in Google Colab.

The goal was not to copy every project exactly, but to reproduce and understand the main idea of each project.

---

# Required Projects 00–05

| Project | Experiment | Main Goal | Status |
|---|---|---|---|
| 00 | Dynamic Todo Workspace | Build an interactive task management application | Completed |
| 01 | NYC Taxi Trip Prediction | Predict taxi trip duration using regression | Completed |
| 02 | NanoLlama / Small Language Model | Demonstrate a small language model fine-tuning workflow | Completed |
| 03 | Customer Segmentation | Discover customer groups using clustering | Completed |
| 04 | Association Pattern Mining | Discover relationships between items in transaction data | Completed |
| 05 | Data Science Skills Mastery Lab | Demonstrate multiple data science skills in one workflow | Completed |

All required Projects **00–05 are completed**.

---

# Project 00 — Dynamic Todo Workspace

**Notebook:** [`00_Dynamic_Todo_Workspace.ipynb`](./00_Dynamic_Todo_Workspace.ipynb)

This project implements a compact interactive Todo application using Python and Gradio.

### Main Features

- Add new tasks
- View current tasks
- Mark tasks as completed
- Delete tasks
- Display task status
- Interactive web interface

The application was tested through the Gradio interface to verify that the main user actions work correctly.

This is a lightweight adaptation of the original full application concept. Tasks are stored in memory rather than in a permanent database.

---

# Project 01 — NYC Taxi Trip Prediction

**Notebook:** [`01_NYC_Taxi_Trip_Prediction.ipynb`](./01_NYC_Taxi_Trip_Prediction.ipynb)

This experiment predicts NYC taxi trip duration using regression models.

### Main Steps

- Data understanding
- Data cleaning
- Time feature engineering
- Geographic distance calculation
- Baseline prediction
- Linear Regression
- Random Forest
- Model comparison
- Feature importance
- Trip duration prediction demo

### Main Results

| Model | MAE | RMSE | R² |
|---|---:|---:|---:|
| Baseline | 458.86 sec | 650.25 sec | — |
| Linear Regression | 280.58 sec | 406.37 sec | 0.609 |
| Random Forest | **218.93 sec** | **334.48 sec** | **0.735** |

Random Forest produced the best performance.

Geographic trip distance was the most important feature.

---

# Project 02 — NanoLlama / Small Language Model

**Notebook:** [`02_NanoLlama_Small_Language_Model.ipynb`](./02_NanoLlama_Small_Language_Model.ipynb)

This project demonstrates a compact language model fine-tuning workflow.

A very small GPT-style pretrained model was used so that the experiment could run quickly in Google Colab.

### Main Steps

- Create instruction-response training data
- Format text conversations
- Tokenize text
- Load a small pretrained language model
- Test before fine-tuning
- Fine-tune for 20 epochs
- Track training loss
- Test after fine-tuning
- Inspect generated text
- Create a simple text generation function

### Main Result

Training loss decreased from approximately:

**10.83 → 10.71**

However, the generated text did not become useful.

Before fine-tuning, the model repeatedly generated the word `stairs`.

After fine-tuning, the model mainly repeated the word `the`.

This experiment demonstrates an important lesson:

> Lower training loss does not automatically mean better text generation quality.

The result also shows the limitations of using an extremely small model and only 12 training examples.

---

# Project 03 — Customer Segmentation

**Notebook:** [`03_Customer_Segmentation_Clustering.ipynb`](./03_Customer_Segmentation_Clustering.ipynb)

This experiment uses K-Means clustering to discover customer groups from synthetic customer behavior data.

### Main Skills

- Data exploration
- Feature scaling
- Elbow Method
- Silhouette Score
- K-Means clustering
- PCA visualization
- Cluster profiling
- Business interpretation

### Main Result

The best clustering solution used:

**K = 4**

with a Silhouette Score of approximately:

**0.577**

The four customer groups were interpreted as:

1. Premium High-Value Customers
2. Conservative Affluent Customers
3. Budget / Low-Engagement Customers
4. Frequent Value Shoppers

PCA was used for visualization only. The clustering model used the full standardized feature set.

---

# Project 04 — Association Pattern Mining

**Notebook:** [`04_Association_Pattern_Mining.ipynb`](./04_Association_Pattern_Mining.ipynb)

This experiment uses the Apriori algorithm and association rules to discover product relationships in synthetic retail transactions.

### Main Skills

- Transaction data preparation
- Market basket encoding
- Apriori frequent itemset mining
- Support
- Confidence
- Lift
- Association rule interpretation

### Example Results

| Rule | Lift |
|---|---:|
| Coffee → Cookies | 2.83 |
| Chips → Soda | 2.75 |
| Pasta → Tomato Sauce | 2.59 |
| Bread → Milk | 2.10 |

Bread and Milk appeared together in approximately **30.7%** of transactions.

These patterns could support product recommendations, bundling, promotions, and store planning.

Association does not imply causation.

---

# Project 05 — Data Science Skills Mastery Lab

**Notebook:** [`05_Data_Science_Skills_Mastery_Lab.ipynb`](./05_Data_Science_Skills_Mastery_Lab.ipynb)

This experiment combines multiple common data science skills into one complete workflow using the Breast Cancer Wisconsin dataset.

The project is an educational demonstration and is not intended for real medical use.

### Skills Demonstrated

- Data loading
- Data quality checking
- Exploratory analysis
- Feature scaling
- Train/test splitting
- Machine learning pipelines
- Logistic Regression
- K-Nearest Neighbors
- Random Forest
- Cross-validation
- Model comparison
- Confusion matrix analysis
- Feature importance
- PCA visualization

### Model Results

| Model | Test Accuracy | F1 Score | Mean CV Accuracy |
|---|---:|---:|---:|
| Logistic Regression | **0.9825** | **0.9861** | **0.9802** |
| KNN | 0.9561 | 0.9655 | 0.9670 |
| Random Forest | 0.9561 | 0.9655 | 0.9604 |

Logistic Regression produced the best result.

Its confusion matrix was:

```text
[[41, 1],
 [ 1, 71]]
```

This means it correctly classified **112 of 114 test samples**.

Random Forest feature importance and PCA were also used to explore and interpret the data.

---

# Additional Experiments

In addition to the required Projects 00–05, I completed two additional experiments.

## Project 06 — Anomaly Detection

**Notebook:** [`06_Anomaly_Detection.ipynb`](./06_Anomaly_Detection.ipynb)

This experiment uses Isolation Forest to identify unusual financial transactions.

The dataset contains 1,000 synthetic transactions, including 50 intentionally created anomalies.

Isolation Forest recovered all 50 simulated anomalies in this controlled experiment.

The perfect result should not be interpreted as real-world fraud detection performance because the synthetic anomalies were intentionally well separated from normal transactions.

---

## Project 12 — Time Series Forecasting

**Notebook:** [`12_Time_Series_Forecasting.ipynb`](./12_Time_Series_Forecasting.ipynb)

This experiment predicts daily sales using time series features.

The workflow includes:

- Chronological train/test splitting
- Lag features
- Naive baseline
- Linear Regression
- Random Forest
- Forecast evaluation
- Future forecasting

### Main Results

| Model | MAE | RMSE |
|---|---:|---:|
| Naive Baseline | 13.07 | 15.86 |
| Linear Regression | **7.67** | **9.66** |
| Random Forest | 8.34 | 10.32 |

Linear Regression produced the best result.

The experiment also showed that 7-day and 14-day lag features were especially useful for predicting daily sales.

---

# AI-Assisted Workflow

ChatGPT was used throughout Part 2 to help with:

- Understanding the instructor project goals
- Planning smaller reproducible experiments
- Writing and explaining Python code
- Debugging problems
- Designing evaluation methods
- Interpreting outputs
- Identifying limitations
- Organizing notebook documentation

Generated code and conclusions were tested and reviewed during the workflow.

AI output was not treated as automatically correct.

---

# How to Run

The notebooks were developed in Google Colab.

To reproduce an experiment:

1. Open the selected `.ipynb` notebook in Google Colab or Jupyter Notebook.
2. Run the cells from top to bottom.
3. Install any requested package when required.
4. Review the saved outputs, visualizations, evaluation results, and conclusions.

Some experiments use synthetic data so that they can be reproduced without downloading external datasets.

---

# Limitations

These projects are compact educational adaptations.

They do not reproduce every feature of the original full applications.

Important limitations include:

- Some experiments use synthetic data.
- The Todo application uses in-memory storage.
- The language model is extremely small and does not produce useful chatbot responses.
- The experiments do not include production deployment.
- The projects focus on demonstrating the main workflow and learning goals.

These limitations are discussed directly in the individual notebooks.

---

# YouTube Walkthrough

A video walkthrough of Part 1 and Part 2 will be linked here after recording.

**[Watch the Assignment 1 Walkthrough on YouTube](https://www.youtube.com/watch?v=_sqO-ba8oYQ)**

---

# Status

**Required Projects 00–05: Completed**

**Additional Experiments 06 and 12: Completed**

**Part 2: Completed**
