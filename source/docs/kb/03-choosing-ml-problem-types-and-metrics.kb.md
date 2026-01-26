# Choosing ML Problem Types and Metrics

This document explains how to choose the right ML problem type based on what you want to predict (a number, a label, or groups). It uses a simple example for each problem type to make the differences concrete. It then introduces the most common evaluation metrics for regression and classification, and covers clustering and anomaly detection at a high level so you can recognize when they apply.

**This Document Covers**
- Core ML Problem Types  
- How to Choose the Problem Type (Decision Rules)  
- Regression (Predicting Numbers) and Common Metrics  
- Classification (Predicting Labels) and Common Metrics  
- Clustering (Grouping Similar Examples Without Labels)  
- Anomaly Detection (Flagging Unusual Behavior)  
- Common Pitfalls (Problem Type and Metric Mistakes)  
- Summary

## Core ML Problem Types

You can choose the ML problem type by looking at the **output** you want:

- **Regression:** predict a **number** (for example, next month’s sales)  
- **Classification:** predict a **label/category** from a fixed set (for example, triage an email into Billing or Technical Issue)  
- **Clustering:** group examples into **clusters** without predefined labels (for example, customer segments by purchasing habits)  
- **Anomaly Detection:** flag **unusual behavior** compared to a normal baseline (for example, suspicious transactions)  

> [!NOTE]
> Choose the problem type from the **output** you want the model to produce. The same input data can support different problem types depending on the output you choose.

### Related Problem Types You Will Also See
These are common in real projects, but they go beyond the foundational scope of this document. They are included here to give the wider picture:

- **Forecasting:** predicting future values over time (often treated as regression, but requires time-aware evaluation)  
- **Recommendation and Ranking:** selecting or ordering items (often built using classification/regression ideas, but used for “top N” decisions)  

**Metric Family Chooser (Do Not Mix Families)**  
- **Classification**: Accuracy, Precision, Recall, F1, ROC AUC, PR AUC  
- **Regression**: MAE, MSE/RMSE, R²  
- **Clustering**: Silhouette (when labels are not available)  
- **Anomaly Detection**: depends on whether you have labels (often Precision/Recall style evaluation)  

## How to Choose the Problem Type (Decision Rules)

Before choosing a problem type, it helps to know whether you have **labels** in your data.

There are two common learning types:
- **Supervised learning:** you have labeled examples, meaning each row includes the input features and the correct output you want to predict  
- **Unsupervised learning:** you do not have labels, so the model looks for structure or patterns in the input features  

> [!IMPORTANT]
> Decide in this order, do you have labels, what output do you want, then pick Regression, Classification, Clustering, or Anomaly Detection, don’t pick based on input alone.

**Decision question:** What is the **output** you want the model to produce?

> [!NOTE]
> The same input type can support different problem types, choose from the **output** you need.

- If the output is a **number**, treat it as **Regression** (supervised)  
- If the output is one of **fixed categories (labels)**, treat it as **Classification** (supervised)  
- If you do not have labels and want to discover groups, use **Clustering** (unsupervised)  
- If you want to flag rare or unusual cases compared to normal, use **Anomaly Detection** (often unsupervised, but can be supervised when labels exist)  

**Quick Distinction (When You Do Not Have Labels)**
- **Clustering:** the output is **groups/segments** (discover structure)  
- **Anomaly Detection:** the output is an **unusual/normal signal** (flag rare cases)  

## Regression (Predicting Numbers) and Common Metrics

Use **Regression** when the output you want is a **number** (a numeric value), such as:
- “How many items will be sold next month?”
- “What will the house price be?”

> [!IMPORTANT]
> Compare model versions on the same split using unseen data, MAE or RMSE should go down, R² should go up, otherwise the change likely didn’t help.

### Why Metrics Matter
A **metric** is a number that tells you **how well your model is performing**.  
In regression, that means: **how far your predicted numbers are from the real numbers**.

Metrics matter because they let you:
- Measure **how close** predictions are to actual values
- Compare **model A vs model B** fairly
- Check whether a change you made **helped or hurt**

Also: metrics depend on the **ML problem type**.  
- **Regression** predicts a **number** → metrics like **MAE, RMSE, R²** (this section)
- **Classification** predicts a **label/category** → uses different metrics (not these)

In practice you improve a regression model using this loop:
- Measure metrics on the **current model** (baseline)
- Change something (add/remove a feature, change algorithm, tune hyperparameters, clean data)
- Measure metrics again (same data split / same test set)
- Compare:
  - If **MAE/RMSE go down** (or **R² goes up**), the change likely **improved** the model
  - If they move the opposite way, the change likely **made it worse**

So it’s literally: **before change vs after change**.

### MAE (Mean Absolute Error)
**MAE** is the average **absolute** difference between prediction and actual.

What “absolute” means:
- You only care about **how big** the mistake is, not the direction (**too low** or **too high**)

Example:
- Actual: 100, Predicted: 92 → **absolute error = 8** (8 too low)  
- Actual: 100, Predicted: 108 → **absolute error = 8** (8 too high)  
Both count as **8** because MAE ignores whether you were over or under.

How to calculate and read it:
- Using the sales example:
  - Actual sales: 100, Predicted sales: 92 → absolute error = 8  
  - Actual sales: 50, Predicted sales: 55 → absolute error = 5  
- MAE averages these absolute errors: (8 + 5) / 2 = **6.5**
- If **MAE = 6.5**, your predictions are off by about **6.5 units** on average.
- If MAE drops from **6.5** to **3**, your typical mistake got smaller.

Why it’s useful:
- MAE is easy to explain because it stays in the **same units as the target** (minutes, dollars, units sold)
- It gives a clear “typical mistake size” you can compare across model versions

### RMSE (Root Mean Squared Error)
**RMSE** measures error like MAE, but it **penalizes large mistakes more**.

Why it penalizes large mistakes more:
- RMSE **squares** each error before averaging
- Squaring makes big errors grow a lot (for example, 20² is much larger than 2²)

A small worked example:
- Actual values: 100, 100, 100  
- Model predictions: 100, 98, 80  
- Errors: 0, 2, 20  

How MAE vs RMSE react:
- **MAE** averages the absolute errors: (0 + 2 + 20) / 3 = **7.33**  
  This says: “On average, we’re off by about 7.33 units.”
- **RMSE** squares errors before averaging, so the big miss matters more:  
  sqrt((0² + 2² + 20²) / 3) = sqrt((0 + 4 + 400) / 3) = sqrt(134.67) ≈ **11.61**

Interpretation:
- Both metrics notice the 20-unit miss, but RMSE reacts more strongly because squaring amplifies large errors.

When RMSE is useful:
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
**R²** is a “fit” summary: it tells you how much of the **variation** in the **target (actual) values** your model explains compared to a simple **baseline**.

What “target” means:
- The **target** is the real number you want to predict (so **target = actual**).

What the baseline is:
- A simple reference model that always predicts the **average** target value (it does not learn patterns).

## R² Formula (How to Calculate It)
R² = 1 − (SS Res / SS Total)

Sum of Squares (SS) means we add up squared differences.

- **Sum of Squares Residual (SS Res):**  
  Measures how much error your model makes overall.  
  SS Res = Σ(Actual − Predicted)²

- **Sum of Squares Total (SS Total):**  
  Measures how much the actual values vary around the average (baseline variation).  
  SS Total = Σ(Actual − Average(All Actual))²

### Worked Example (Sales Forecasting: Compute R² Step by Step)

**Scenario:** Predict daily sales (units sold).  
We have 3 days of data:

**Actual sales:** 100 (**Actual₁**), 50 (**Actual₂**), 150 (**Actual₃**)  
**Model predicted sales:** 110, 60, 140  

**Average (also called Mean) of all actual values:**  
Average(All Actual) = (sum of all actual values) / (number of values)  
Average(All Actual) = (100 + 50 + 150) / 3 = 300 / 3 = **100**

**Baseline = Average(All Actual)** (predict this same value for every row).  
Baseline prediction (always predict the average): **100, 100, 100**

**SS Total (baseline variation):** measures how much the actual values vary around the average (baseline).  
SS Total = (Actual₁ − Average(All Actual))² + (Actual₂ − Average(All Actual))² + (Actual₃ − Average(All Actual))²  
SS Total = (100 − 100)² + (50 − 100)² + (150 − 100)²  
SS Total = 0² + (−50)² + 50² = 0 + 2500 + 2500 = **5000**

**Advanced notation:**  
SS Total = Σ(Actual − Mean(Actual))²

**SS Res (model error):** measures how much error the model makes overall.  
SS Res = (Actual₁ − Predicted₁)² + (Actual₂ − Predicted₂)² + (Actual₃ − Predicted₃)²  
SS Res = (100 − 110)² + (50 − 60)² + (150 − 140)²  
SS Res = (−10)² + (−10)² + 10² = 100 + 100 + 100 = **300**

**Advanced notation:**  
SS Res = Σ(Actual − Predicted)²

### Compute R² (Final Step)

R² = 1 − (SS Res / SS Total)  
R² = 1 − (300 / 5000) = 1 − 0.06 = **0.94**

**Interpretation (easy version):**  
R² = **0.94** means the model removed about **94%** of the “predict-the-average” baseline error (only about **6%** remains).

### Two Quick Extra Cases (Same Data, Different Model Behavior)

We keep the same actual sales values, so **SS Total stays the same**:  
SS Total = **5000**

#### Case 1: Model behaves like the baseline → R² = 0
If the model predicts the average every time (same as baseline):  
Predicted values: **100, 100, 100**

SS Res = (100 − 100)² + (50 − 100)² + (150 − 100)²  
SS Res = 0² + (−50)² + 50² = 0 + 2500 + 2500 = **5000**

R² = 1 − (SS Res / SS Total)  
R² = 1 − (5000 / 5000) = 1 − 1 = **0**

**Meaning:** the model is no better than predicting the average.

#### Case 2: Model is worse than the baseline → R² can be negative
If the model predicts poorly, the squared errors can be bigger than the baseline errors.  
Example predicted values: **200, 200, 200**

SS Res = (100 − 200)² + (50 − 200)² + (150 − 200)²  
SS Res = (−100)² + (−150)² + (−50)² = 10000 + 22500 + 2500 = **35000**

R² = 1 − (SS Res / SS Total)  
R² = 1 − (35000 / 5000) = 1 − 7 = **−6**

**Meaning:** worse than predicting the average (the baseline is a safer model than this one).

### A Concrete Intuition
- If **R² is higher**, the model explains more of the variation in the real values (it reduces more of the baseline error).  
- If **R² is low** (near 0), the model is not capturing much signal (it behaves close to the baseline).  
- If **R² is negative**, the model is worse than the baseline (predicting the average would be better).

Example (simple numbers, not a rule):  
- Model version 1: **R² = 0.50**  
  Meaning: it explains about 50% of why the target values vary in your dataset.  
- After adding a useful feature (like location for house prices), model version 2: **R² = 0.70**  
  Meaning: it now explains about 70% of the variation, so it’s capturing more real signal.

Another cue:  
- If **R² drops from 0.70 to 0.40**, the model is explaining less variation, often because you removed useful signal or the model got worse.

This is why if **R² goes up**, the change (**any update you try during model development**) likely improved the model: it means the model is reducing more of the “predict-the-average” baseline error than before.  
Example: if **R² increases from 0.40 to 0.65**, the model explains more of the variation in the target values (less baseline-level error remains).

Important note:
- R² does **not** tell you typical “mistake size”, so you still use **MAE/RMSE** alongside it.

### What You Are Trying to Achieve
- Choose a metric that matches your risk:
  - Want a clear “average error” number → **MAE**
  - Want to penalize large mistakes more → **RMSE**
  - Want a quick “fit” summary alongside error → **R²**
- Improve the model by comparing metric values across versions and reducing error on unseen data.

## Classification (Predicting Labels) and Common Metrics

Use **Classification** when the output you want is a **label/category** from a fixed set.

Example (email triage):  
A support team receives many customer emails every day. They want a model that reads a new email and assigns it to one predefined ticket type so it can be routed to the right team, for example:
- **Billing**
- **Technical Issue**
- **Account Access**
- **Feature Request**

In this scenario:
- The **input** is the email text (and possibly metadata like subject line)  
- The **output** is one label from the predefined list, so it’s **Classification**

> [!IMPORTANT]
> Define the positive class first, then read Precision and Recall, otherwise you can optimize the wrong outcome.

### How Classification Metrics Work

Classification metrics are built from **confusion matrix counts**:

- **TP, FP, TN, FN** (what the model predicted vs what was actually true)

Before reading metrics, make two things explicit:
- **Positive class:** what “positive” means in your scenario (for example, **Fraud**)  
- **Threshold (when using scores):** the cutoff that turns a score into a final yes/no label (changing it shifts Precision vs recall)

After that, each metric is just a different way to summarize the same TP/FP/TN/FN counts.

Each common metric reads the confusion matrix differently:
- **Accuracy:** uses **(TP + TN)** vs all predictions  
- **Precision:** focuses on **FP** (false alarms)  
- **Recall:** focuses on **FN** (missed positives)  
- **F1:** balances **precision and recall**  
- **AUC / ROC / PR:** evaluate ranking across thresholds  

Let’s see them in detail in the next sections.

### Confusion Matrix (TP, FP, TN, FN)

A confusion matrix counts:
- **True Positive (TP):** predicted positive and actually positive  
- **False Positive (FP):** predicted positive but actually negative  
- **True Negative (TN):** predicted negative and actually negative  
- **False Negative (FN):** predicted negative but actually positive  

Example (Fraud Detection, where **Positive = Fraud**):
- **True Positive (TP):** model flags a transaction as fraud, and it really is fraud (caught it)  
- **False Positive (FP):** model flags a transaction as fraud, but it was legitimate (false alarm)  
- **True Negative (TN):** model says **not fraud**, and it really is legitimate (correctly allowed)  
- **False Negative (FN):** model says **not fraud**, but it was fraud (missed it)  

This is why “positive” should be defined clearly before reading metrics.

### Accuracy
Accuracy is the overall proportion correct.  
Example: If you have 100 predictions and 90 are correct, **accuracy = 90%**.  
Real-life: useful when classes are reasonably balanced and false positives vs false negatives have similar cost.

### Precision
Precision is: **When the model says positive, how often is it right?**  
Example: model predicts “fraud” 40 times, but only 30 are truly fraud: Precision = 30/40 = **75%**.  
Real-life: you care about Precision when false alarms are costly (for example, blocking legitimate customer payments).

### Recall / TPR (True Positive Rate) (Sensitivity)
Recall, also called **TPR (True Positive Rate)** or **Sensitivity**, is: **Of the actual positives, how many did we catch?**  
Example: there are 50 real fraud cases, model catches 30: Recall = 30/50 = **60%**.  
Real-life: you care about Recall when missing a positive is costly (for example, catching disease in medical screening).

### Precision vs Recall (Fraud Alerts)
Numeric example:  
You have **1000** transactions, and **10** are actually fraud. The model flags **20** transactions as fraud. **TP = 8** (truly fraud) and **FP = 12** (not fraud), So:  
**Precision** = 8 / 20 = **0.40** (when we alert, how often we are right).   
**Recall** = 8 / 10 = **0.80** (how many of the real fraud cases we caught).

### ROC vs PR (Rare Positives)
- **ROC (Receiver Operating Characteristic):** a curve view based on TPR vs FPR across thresholds  
- **PR (Precision-Recall):** a curve view based on precision vs Recall across thresholds  

With rare positives, PR often shows performance more clearly than ROC.

Numeric example:   
You have **10,000** transactions, and only **100** are actually fraud (**1%**). The model flags **500** as fraud. **TP = 50**, **FP = 450**, So:   
**Precision** = 50 / 500 = **0.10**.    
**Recall** = 50 / 100 = **0.50**.    
With rare positives, PR makes this pain obvious (low precision), even if ROC looks acceptable.

### AUC (Area Under ROC Curve)
AUC, also called **Area Under the ROC Curve**, measures how well the model **ranks positives above negatives** across all possible thresholds.

**Where do these scores come from?**  
A classification model often outputs a **score** for each case. You can think of it as a **fraud risk score**:
- Higher score → the model thinks the case is **more likely fraud**.
- Lower score → the model thinks the case is **more likely legitimate**.

In many models, this score is a **predicted probability** (0 to 1), but it can also be any numeric score as long as **higher = more fraud-like**.   
AUC uses these scores to evaluate ranking quality.

**Numeric example (scores 0 to 1)**  
Suppose you have 5 fraud cases and 5 legitimate cases. The model outputs a score for each transaction:

Fraud scores: **0.95, 0.90, 0.80, 0.70, 0.60**  
Legit scores: **0.55, 0.40, 0.30, 0.20, 0.10**

Here, fraud scores are mostly higher than legit scores, so the model separates the classes well → **High AUC**.  
If the scores overlap a lot (fraud and legit both mixed around 0.4–0.6), separation is weak → **Lower AUC**.

**Threshold example (why AUC helps)**  
If you choose threshold **0.80**, you only flag scores ≥ 0.80 as fraud (stricter, fewer false alarms).  
If you choose threshold **0.50**, you flag more transactions (catch more fraud, but more false alarms).  
AUC is useful because it evaluates the model’s separation quality **before** you pick the threshold.

### F1 Score
F1, also called the **Harmonic Mean of Precision and Recall**, balances precision and Recall into one number and tends to be closer to the smaller one.  
**Where does F1 come from?**  
F1 is calculated from precision and Recall using this formula:  
F1 = 2 × (Precision × Recall) / (Precision + Recall)

This formula makes F1 behave like a “both-must-be-good” score:
- If **Precision** is low, F1 drops.
- If **Recall** is low, F1 drops.
- F1 is high only when **both** are high.

**Worked example**  
If Precision is 75% and Recall is 60%, F1 is a single combined score that will be between them (closer to the smaller one).  
Precision = **0.75**  
Recall = **0.60**

F1 = 2 × (0.75 × 0.60) / (0.75 + 0.60)  
F1 = 2 × 0.45 / 1.35  
F1 = 0.90 / 1.35 = **0.67**

So here, F1 is **0.67 (67%)**, which is between 0.60 and 0.75 and closer to the smaller one.  
Real-life: useful when you need both precision and Recall and want one summary number.

> [!IMPORTANT]
> **ROC vs PR:**
> When positives are rare, **Precision-Recall** curves often show performance more clearly than ROC.
> ROC can look “good” even when precision is low, because true negatives dominate.

### Threshold Example (Same Model Scores, Different Decisions)
Example: You are predicting whether a patient needs urgent follow-up. The model outputs a **risk score** (0 to 1) for each patient.  
For 4 patients, the model outputs: **0.90, 0.70, 0.40, 0.20** (these are the model’s outputs).  
- If you set threshold **0.50**, you flag **0.90** and **0.70** as urgent.  
- If you set threshold **0.30**, you flag **0.90**, **0.70**, and **0.40** as urgent.  
Same model, same scores. Only the **threshold** changed, so the final yes/no decisions changed.

### Accuracy: When It Misleads

Accuracy can be misleading when the dataset is **imbalanced** (most examples are from one class). A model can look high accuracy by mostly predicting the majority class, while doing a poor job on the rare class you actually care about.

Example:
- If 99 out of 100 transactions are legitimate, a model that always predicts legitimate gets **99% accuracy**, but it catches **0 fraud**.

In imbalanced or high-risk scenarios, rely more on:
- **Precision** (control false alarms)
- **Recall** (avoid missing positives)
- **F1** (balance both)
- Confusion matrix (see TP/FP/TN/FN counts)  

## Clustering (Grouping Similar Examples Without Labels)

Use **Clustering** when you want to group examples into **clusters** based on similarity, and you **do not have labels** (no “correct category” column).

A clustering model does not learn “the right answer” per row. Instead, it looks at patterns in the **features (X)** and discovers groups that tend to look alike.

> [!NOTE]
> Clustering is unsupervised that discovered first grouping pattern from X, then humans often interpret them or validate whether the clusters make sense using summaries and business sanity checks. For example, “Cluster 1” might later be described as “high spenders”, but that name is an interpretation, not a label the model trained on.

### What Data Clustering Needs

Because clustering is **unsupervised**, the dataset does **not** need a label/target column (`y`).  
What it must contain is:

- **Rows (examples):** the things you want to group (customers, devices, neighborhoods, etc.)
- **Feature columns (X):** attributes that represent each example’s behavior or characteristics
- Enough **variation** and **volume** for meaningful group patterns to appear

So the essential requirement is: clustering needs **features**, not target labels.

### Example: “Similar Purchasing Habits” (Customer Segmentation)

If you want to group customers by similar purchasing habits, typical feature columns could be:

- **Purchase frequency** (orders/month)
- **Average order value**
- **Total spend** (last 3 months / 12 months)
- **Discount usage rate**
- **Product category mix** (percent spend per category)
- **Recency** (days since last purchase)

The clustering algorithm groups customers with similar feature patterns into segments.  
After clustering, you usually validate and interpret clusters by checking:

- Summary statistics by cluster
- Business sanity checks (do clusters make sense?)
- Stability checks (do segments persist over time?)

### How Clustering Is “Evaluated” (High Level)

Clustering does not usually have one simple metric like accuracy, because there is no single “correct label” to compare against. In practice, you check whether the clusters are:

- **Useful** for the goal (segmentation, personalization, targeting, monitoring)
- **Stable** (not changing wildly with small data changes)
- **Interpretable** (you can explain what makes clusters different)

## Anomaly Detection (Flagging Unusual Behavior)

Use **Anomaly Detection** when you want to find data points or events that are **unusual compared to normal behavior**. The goal is to surface “outliers” that may represent risk, failure, fraud, or important rare conditions.

### What It Is Trying to Achieve

Anomaly detection is used to detect rare or abnormal cases that are important to act on, such as:
- Fraud or suspicious transactions  
- Equipment faults and predictive maintenance alerts  
- Network intrusions or unusual login behavior  
- Defective products on a production line  
- Unusual spikes or drops in metrics (usage, revenue, sensor readings)

> [!IMPORTANT]
> An anomaly flag is not a diagnosis. It is a signal to investigate.

### How It Works (High Level)

A typical anomaly detection workflow looks like this:
- Define what “normal” looks like (baseline period, typical ranges, seasonality).  
- Choose what you will detect anomalies in (transactions, sensors, logs, images).  
- Produce an **anomaly score** or a “normal vs abnormal” flag.  
- Tune thresholds to balance false alarms vs missed issues.

### Common Approaches (High Level)

Anomaly detection can be implemented in different ways depending on what data you have:

- **Rules/statistics:** thresholds, z-scores, moving averages (good starting point).  
- **Unsupervised ML:** learn patterns of normal behavior without labeled anomalies (common when anomalies are rare).  
- **Supervised ML:** train on labeled examples of normal vs anomaly (useful when labels exist and are reliable).

### Common Pitfalls and Confusion Points

- “Unusual” depends on context. Seasonality, time of day, and user segments can make normal behavior look abnormal.  
- Anomalies are rare, so too many false positives can make the system unusable.  
- What is “normal” can change over time (data drift), so baselines must be updated.

## Common Pitfalls (Problem Type and Metric Mistakes)

This section highlights common mistakes that make model results look better than they are, or make you choose the wrong problem type or metric.

### Mixing Up the Problem Type

A fast way to choose the problem type is to focus on the output:
- If the output is a **number**, it is **Regression**.  
- If the output is one of **fixed categories**, it is **Classification**.  
- If you have **no labels** and want to discover groups, it is **Clustering**.  
- If you want to flag **rare or unusual cases**, it is **Anomaly Detection**.

A common mistake is to choose based on the input only.  
For example, “sales data” could lead to regression (predict a number), classification (predict high/low category), clustering (segment customers), or anomaly detection (flag unusual activity), depending on the output you want.

### Treating Accuracy as “Good Enough” for Classification

Accuracy is useful when classes are reasonably balanced and error costs are similar, but it can hide poor performance on the rare class you care about.

Example:
- If 99 out of 100 transactions are legitimate, a model that always predicts “legitimate” gets **99% accuracy**, but it catches **0 fraud**.

In imbalanced or high-risk scenarios, rely more on:
- Confusion matrix (TP/FP/TN/FN counts)  
- **Precision** (control false alarms)  
- **Recall** (avoid missing positives)  
- **F1** (balance Precision and Recall)

### Using Regression Metrics for Classification (and Vice Versa)

Regression metrics like **MAE, RMSE, and R²** measure numeric prediction error.  
They do not describe label prediction behavior.

Classification metrics like **Accuracy, Precision, Recall, F1, and AUC** measure label performance.  
They do not measure numeric error.

> [!WARNING]
> If you pick the wrong metric family for the problem type, you can believe a model is “good” while measuring the wrong thing.

### Forgetting the “Positive Class” Definition

Many classification metrics depend on what you define as “positive.”  
Precision and Recall are always about the positive class.

If you do not define the positive class clearly, you can misinterpret the metrics.

Example:
- In fraud detection, “positive” is usually **fraud** (the rare, high-risk class).
- In medical screening, “positive” is usually **disease present**.

## Summary

You should now be able to:
- Choose the right ML problem type by focusing on the **output** (Regression, Classification, Clustering, Anomaly Detection).
- Explain why metrics matter and how they help you compare model versions on unseen data.
- Use **MAE, RMSE, and R²** to evaluate regression models and understand what each one emphasizes.
- Use the confusion matrix (**TP, FP, TN, FN**) to reason about classification errors.
- Use **Accuracy, Precision, Recall/TPR, F1, and AUC** to evaluate classification models and match metrics to error costs.
- Recognize clustering scenarios and explain that clustering uses **features (X)** without labels.
- Recognize anomaly detection scenarios and explain that it flags unusual behavior compared to a **normal baseline**.
- Avoid common mistakes like choosing the wrong problem type, relying on accuracy for imbalanced data, mixing metric families, forgetting the positive class, and introducing leakage through unsafe features.
