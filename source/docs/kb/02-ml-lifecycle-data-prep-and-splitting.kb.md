# ML Lifecycle: Data Preparation and Splitting

This document explains where data ingestion and data preparation fit in the ML lifecycle. In machine learning, you need data because the model learns patterns from examples (data) so it can make predictions on new data you haven’t seen yet. It then explains why training, validation, and testing require careful splitting. It focuses on how to split data correctly to estimate real-world performance and avoid common mistakes like leakage and “peeking.”

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

These stages focus on building a reliable dataset for learning, not on measuring model performance. Training, scoring, and evaluation happen later in the lifecycle.
