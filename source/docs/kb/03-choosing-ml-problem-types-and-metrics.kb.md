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

## Regression (Predicting Numbers) and Common Metrics

Use **Regression** when the output you want is a **number** (a numeric value), such as:
- “How many items will be sold next month?”
- “What will the house price be?”

### Why Metrics Matter
A **metric** is a number that tells you **how well your model is performing**.  
In regression, that means: **how far your predicted numbers are from the real numbers**.

Metrics matter because they let you:
- measure **how close** predictions are to actual values,
- compare **model A vs model B** fairly,
- check whether a change you made **helped or hurt**.

Also: metrics depend on the **ML problem type**.  
- **Regression** predicts a **number** → metrics like **MAE, RMSE, R²** (this section).  
- **Classification** predicts a **label/category** → uses different metrics (not these).

In practice you improve a regression model using this loop:
- Measure metrics on the **current model** (baseline).
- Change something (add/remove a feature, change algorithm, tune hyperparameters, clean data).
- Measure metrics again (same data split / same test set).
- Compare:
  - If **MAE/RMSE go down** (or **R² goes up**), the change likely **improved** the model.
  - If they move the opposite way, the change likely **made it worse**.

So it’s literally: **before change vs after change**.

### MAE (Mean Absolute Error)
**MAE** is the average absolute difference between prediction and actual.

How to read it:
- If **MAE = 5**, your predictions are off by about **5 units** on average.
- If you improve the model and **MAE drops from 5 to 3**, your “average mistake size” got smaller.

Example:
- Actual sales: 100, Predicted sales: 92 → error = 8  
- Actual sales: 50, Predicted sales: 55 → error = 5  
MAE averages these absolute errors.

Why it’s useful:
- MAE is easy to explain and compare across model versions.

### RMSE (Root Mean Squared Error)
**RMSE** measures error like MAE, but it **penalizes large mistakes more**.

A small worked example:
- Actual values: 100, 100, 100  
- Model predictions: 100, 98, 80  
- Errors: 0, 2, 20  

How the two metrics react:
- **MAE** averages the absolute errors: (0 + 2 + 20) / 3 = **7.33**  
  This says: “On average, we’re off by about 7.33 units.”
- **RMSE** squares errors before averaging, so the big miss matters more:  
  sqrt((0² + 2² + 20²) / 3) = sqrt((0 + 4 + 400) / 3) = sqrt(134.67) ≈ **11.61**

Interpretation:
- Both metrics notice the 20-unit miss, but RMSE reacts more strongly because squaring amplifies large errors.

RMSE penalizes big mistakes more, which matters when a rare large error is dangerous.

High-stakes examples where large errors are especially harmful:
- Healthcare risk scoring: missing a high-risk patient (a large error) can delay urgent care.
- Critical infrastructure / nuclear operations: large prediction errors in sensor-based monitoring can trigger unsafe decisions or missed alarms.
- Fraud detection loss forecasting: a few large misses can cause major financial impact.

### When to Prefer MAE vs RMSE (Real-Life)
Use **MAE** when you want a stable, easy-to-explain “typical mistake size”:
- Example: predicting delivery time in minutes where being off by 5 vs 10 minutes is not dramatically different.
- MAE is often preferred when you want a metric that is less dominated by a few rare spikes.

Use **RMSE** when large mistakes are especially harmful and you want the metric to punish them:
- Example: predicting next month inventory demand where a big under-forecast causes stockouts and lost sales.
- Example: predicting energy load where big misses can cause operational risk or high cost.

When RMSE is not preferred:
- If your data has occasional extreme outliers you don’t want to dominate the metric, RMSE can over-focus on them. In those cases, MAE can be a better “typical error” view.

### R² (R-squared)
**R²** is a “fit” summary: how much of the variation in the target your model explains compared to a simple baseline.

A concrete intuition:
- If **R² is higher**, the model explains more of the ups and downs in the real values.
- If **R² is low**, the model is not capturing much signal (it may behave close to a baseline).

Think of R² as: “How much better is the model than a simple baseline at explaining why values vary?”

Example (simple numbers, not a rule):
- Model version 1: **R² = 0.50**  
  Meaning: it explains about 50% of why the target values vary in your dataset.
- After adding a useful feature (like location for house prices), model version 2: **R² = 0.70**  
  Meaning: it now explains about 70% of the variation, so it’s capturing more real signal.

Another cue:
- If R² drops from **0.70** to **0.40**, the model is explaining less variation, often because you removed useful signal or the model got worse.

Important note:
- R² does not tell you the typical “mistake size”, so you still use **MAE/RMSE** alongside it.

How to read it (high level):
- **Higher R²** means the model explains more variation than a simple baseline.
- **Lower R²** means the model explains little (or performs close to a baseline).
- R² is helpful as a summary, but it does not tell you the typical “mistake size”, so you still need MAE or RMSE.

### What You Are Trying to Achieve
- Choose a metric that matches your risk:
  - Want a clear “average error” number → **MAE**
  - Want to penalize large mistakes more → **RMSE**
  - Want a quick “fit” summary alongside error → **R²**
- Improve the model by comparing metric values across versions and reducing error on unseen data.

