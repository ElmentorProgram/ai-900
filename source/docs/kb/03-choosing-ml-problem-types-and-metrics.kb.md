# Choosing ML Problem Types and Metrics

This document explains how to choose the right ML problem type based on what you want to predict (a number, a label, or groups). It uses a simple example for each problem type to make the differences concrete. It then introduces the most common evaluation metrics for regression and classification, and covers clustering and anomaly detection at a high level so you can recognize when they apply.

## Core ML Problem Types

You can choose the ML problem type by looking at the **output** you want:

- **Regression:** predict a **number** (for example, next month’s sales).
- **Classification:** predict a **label/category** from a fixed set (for example, triage an email into Billing or Technical Issue).
- **Clustering:** group examples into **clusters** without predefined labels (for example, customer segments by purchasing habits).
- **Anomaly Detection:** flag **unusual behavior** compared to a normal baseline (for example, suspicious transactions).

### Related Problem Types You Will Also See
These are common in real projects, but they go beyond the foundational scope of this document. They are included here to give the wider picture:

- **Forecasting:** predicting future values over time (often treated as regression, but requires time-aware evaluation).
- **Recommendation and Ranking:** selecting or ordering items (often built using classification/regression ideas, but used for “top N” decisions).


## How to Choose the Problem Type (Decision Rules)

Before choosing a problem type, it helps to know whether you have **labels** in your data.

There are two common learning types:
- **Supervised learning:** you have labeled examples, meaning each row includes the input features and the correct output you want to predict.
- **Unsupervised learning:** you do not have labels, so the model looks for structure or patterns in the input features.

Now start with one question:

What is the **output** you want the model to produce?

- If the output is a **number**, treat it as **Regression** (supervised).
- If the output is one of **fixed categories (labels)**, treat it as **Classification** (supervised).
- If you do not have labels and want to discover groups, use **Clustering** (unsupervised).
- If you want to flag rare or unusual cases compared to normal, use **Anomaly Detection** (often unsupervised, but can be supervised when labels exist).
