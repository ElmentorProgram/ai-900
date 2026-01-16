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
