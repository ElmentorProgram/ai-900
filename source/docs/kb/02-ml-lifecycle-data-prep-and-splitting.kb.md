# ML Lifecycle: Data Preparation and Splitting

This document explains where data ingestion and data preparation fit in the ML lifecycle. In machine learning, you need data because the model learns patterns from examples (data) so it can make predictions on new data you haven’t seen yet. It then explains why training, validation, and testing require careful splitting. It focuses on how to split data correctly to estimate real-world performance and avoid common mistakes like leakage and “peeking.”

**This Document Covers**
- ML Lifecycle Overview  
- ML Lifecycle Context (Where Data Prep Fits)  
- Features, Labels, and IDs (Choosing Inputs Safely)  
- Why We Split Data (Training vs Validation vs Test)  
- How Splitting Works (Rows vs Columns)  
- Split Patterns and When Random Split Fails (Time-Based and Group-Based)  
- Common Pitfalls (Leakage, Peeking, Ordering Bias, and Overfitting)  
- Summary  

## ML Lifecycle Overview

When you build an ML model, you want it to make good predictions on **new data you haven’t seen yet** (real life). To get there, you move through a lifecycle that starts with building a reliable dataset and ends with running the model in production.

A typical end-to-end lifecycle looks like:

- **Prepare Data** (**Data ingestion** & **Data preparation**)
- **Split Data:** **Training / Validation / Test**
- **Train:** fit the model on the **training set**
- **Evaluate & Tune:** compare versions and tune choices using the **validation set**
- **Final Test:** run one last check on the **test set** (unseen “final check”)
- **Package:** confirm the **input/output schema** and how the model will be called
- **Deploy & Monitor:** deploy as an **endpoint/service**, then monitor **errors**, **data drift**, and **performance drift**

This document focuses on the early parts of that lifecycle: **Data ingestion**, **Data preparation**, and **splitting**.

## ML Lifecycle Context (Where Data Prep Fits)

When you build an ML model, you need data before training.

- **Data ingestion:** getting raw data from where it lives (files, databases, logs) into your ML workspace as a dataset you can work with.  
- **Data preparation:** cleaning and transforming that dataset so it’s usable for training (fix types, handle missing values, remove duplicates, encode categories).

These are part of building the model.  
Using the model happens later (deployment & sending new input data for predictions).

> [!NOTE]
> Data ingestion and preparation build a trainable dataset, they don’t prove the model is good, evaluation happens after training using held-out data.

These stages focus on building a reliable dataset for learning, not on measuring model performance. Training, scoring, and evaluation happen later in the lifecycle.


## Features, Labels, and IDs (Choosing Inputs Safely)

Before you can train a model, you need a dataset that represents the problem you are trying to solve. In supervised learning, each example contains inputs the model can use and an outcome you want the model to predict. The goal is to choose inputs that will still be available when you use the model in real life.

Example (mapping the terms):
- Imagine you want to predict **house sale price**.
- One **row (example/record)** could represent **one house sale**.
- The **columns** are the fields in that row.
- The **features (inputs, X)** could include living area, number of bedrooms/bathrooms, neighborhood, and property age.
- The **label (target, y)** is the sale price.

A dataset is typically organized as:
- **Rows = examples/records** (each row is one case)
- **Columns = fields/features** (inputs) plus the **label/target** (what you predict)

Each row typically includes:
- **Features (X):** the input fields the model uses
- **Label (y):** the outcome/target you want to predict

When you build a model, each row should contain:
- **Features (inputs):** information available at prediction time (what you know before the outcome happens)
- **Label (target):** the value you want the model to predict

Things to avoid:
- **Using the target as an input**
- **Using IDs as features**
- **Using dataset-level totals** when predicting a per-row outcome

## Why We Split Data (Training vs Validation vs Test)

When you build an AI model, you want it to make good predictions on **new data you haven’t seen yet** (real life). So you separate **the data** (by splitting it) to support two activities:

- **Learning (Training):** give the model many examples so it can learn patterns that connect the inputs to the outcome you care about.
- **Checking (Evaluation/Testing):** test whether it learned a general rule, or if it just memorized the training examples, by evaluating it on different examples it did not learn from.

If you test the model on the same examples it learned from, the score isn’t trustworthy.

> [!IMPORTANT]
> Splitting is how you simulate real life, train on one set of rows, evaluate on different unseen rows, if you evaluate on training rows, the score is not trustworthy.

A proper split holds out **examples (rows)** so evaluation reflects performance on **new cases**, while keeping the same set of input fields available in both training and evaluation.

### Why There Are Multiple Sets
Even though there are two activities (learning and checking), the “checking” activity is commonly split into two sets:

- **Validation set:** used during development to compare model versions and tune settings.
- **Test set:** a final “unbiased” check on unseen examples after decisions are made.

Key sets:
- **Training set:** examples used to learn patterns.
- **Validation set:** examples used during development to compare model versions and tune settings.
- **Test set:** a final “unbiased” check on unseen examples after decisions are made.

> [!WARNING]
> Do not use the test set during tuning, if you keep “checking” the test set and making decisions, it stops being an unbiased final check.


## How Splitting Works (Rows vs Columns)

Splitting is how you simulate “real life” before deployment. You want the model to learn from one set of examples, then prove it can handle **new examples** it has never seen before.

### Split by Rows (What You Usually Want)
To simulate “new data,” you hold out entire **examples (rows)** that the model never sees during training.

- If you split by **rows**, evaluation reflects performance on **new cases**.
- You keep the **same columns** (same feature inputs) so training and evaluation are solving the same task.

### Split by Columns (Why It Is Usually Wrong for Evaluation)
If you split by **columns**, you are not holding out new examples. Instead, you are removing some input fields.

That changes the problem into: “Can the model work with less information?”  
It does not answer the evaluation question: “Will this model generalize to new cases?”

> [!WARNING]
> Split by rows for evaluation, splitting by columns changes the problem into “less information”, it does not measure generalization to new examples.


### Key Rule
- Split by **rows** so evaluation uses unseen examples.
- Keep the **same feature columns** in both training and evaluation so the task stays consistent.

## Split Patterns and When Random Split Fails (Time-Based and Group-Based)

Randomly splitting rows is a common default when each row is an independent example. It helps create training and evaluation subsets that are similar in distribution, so evaluation reflects the same kind of data the model will see in real life.

However, random splitting is not always the best choice.

### Time-Based Split
If data is **time-ordered**, you usually want to train on the past and evaluate on the future. This better matches real deployment, especially for “next month” style predictions.

> [!IMPORTANT]
> Random split is fine only when rows are independent, use time-based split for time-ordered data, use group-based split when multiple rows belong to the same user, patient, or device.

### Group-Based Split
If rows are **grouped/related** (for example, multiple rows from the same user/patient/device), you usually want each group to stay in only one subset. This avoids the model seeing the same group in training and evaluation.

## Common Pitfalls (Leakage, Peeking, Ordering Bias, and Overfitting)

This section highlights common mistakes that make evaluation unreliable, and how those mistakes can hide problems like overfitting or underfitting.

> [!WARNING]
> Leakage and peeking make metrics look better than real life, you must keep anything that reveals the answer out of training, and keep the test set untouched until the end.

### Data Leakage
Data leakage happens when evaluation information accidentally influences training. A common example is using the **target** as an input feature, which makes performance look unrealistically strong.

### Peeking at the Test Set
The **test set** is a final “unbiased” check. If you repeatedly check the test set during tuning, you turn it into part of your development loop and reduce trust in the final score.

### Ordering Bias (Non-Random Splits on Ordered Data)
If data is time-ordered and you do a non-random split without thinking, early rows can differ from later rows (seasonality, collection changes), which can bias evaluation.

### Overfitting and Underfitting (What Splits Help You See)
Splitting data helps you detect whether the model is learning general patterns or not:

- **Overfitting:** performance looks strong on the **training set** but drops on **validation/test** (the model memorized training examples instead of generalizing).  
- **Underfitting:** performance is weak on both the **training set** and **validation/test** (the model did not learn useful patterns).

## Summary

You should now be able to:
- Understand the end-to-end ML lifecycle and where **data** fits.
- Explain how data flows from **ingestion** and **preparation** through **splitting**, **training**, and **deployment**.
- Explain where **Data ingestion** and **Data preparation** fit in the ML lifecycle.
- Describe **features**, **labels**, and why **IDs** and **targets** are not safe inputs.
- Explain why we split data into **training**, **validation**, and **test** sets.
- Split correctly by **rows** (not columns) to simulate performance on unseen examples.
- Choose **time-based** and **group-based** splits when random splitting is not appropriate.
- Recognize pitfalls like **leakage**, **peeking**, **ordering bias**, and how splits reveal **overfitting** and **underfitting**.
