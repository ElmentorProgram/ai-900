# Choosing ML Problem Types and Metrics

This document helps you choose the right ML problem type by starting from the **output** you want the model to produce: a **Number**, a **Label**, **Groups**, or an **Unusual/Normal** signal. It uses one simple example per problem type so the differences feel concrete.

It then introduces the most common evaluation metrics for **Regression** and **Classification**. It also covers **Clustering** and **Anomaly Detection** at a high level so you can recognize when they apply and avoid mixing metric families.

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

You can choose the ML problem type by looking at the **output** you want the model to produce:

- **Regression:** Predict a **number** (for example, next month’s sales)  
- **Classification:** Predict a **label/category** from a fixed set (for example, triage an email into Billing or Technical Issue)  
- **Clustering:** Group examples into **clusters** without predefined labels (for example, customer segments by purchasing habits)  
- **Anomaly Detection:** Flag **unusual behavior** compared to a normal baseline (for example, suspicious transactions)  

> [!NOTE]
> Choose the problem type from the **output** you want the model to produce. The same input data can support different problem types depending on the output you choose.

### Related Problem Types You Will Also See
These are common in real projects, but they go beyond the foundational scope of this document. They are included here to give the wider picture:

- **Forecasting:** Predicting future values over time (often treated as Regression, but requires time-aware evaluation)  
- **Recommendation and Ranking:** Selecting or ordering items (often built using Classification/Regression ideas, but used for **top N** decisions)  

**Metric Family Chooser (Do Not Mix Families)**  
- **Classification:** Accuracy, Precision, Recall, F1, ROC AUC, PR AUC  
- **Regression:** MAE, MSE/RMSE, R²  
- **Clustering:** Silhouette (when labels are not available)  
- **Anomaly Detection:** Depends on whether you have labels (often Precision/Recall style evaluation)

## How to Choose the Problem Type (Decision Rules)

Before choosing a problem type, first decide whether you have **labels** in your data. That determines whether you are doing **supervised** learning (predict a known target) or **unsupervised** learning (discover structure from features).

A simple rule: choose from the **output** you need the model to produce. The same input can support multiple problem types depending on what you want the model to output.

There are two common learning types:
- **Supervised Learning:** You have labeled examples, meaning each row includes the input features and the correct output you want to predict  
- **Unsupervised Learning:** You do not have labels, so the model looks for structure or patterns in the input features  

> [!IMPORTANT]
> Decide in this order: Do you have labels, what output do you want, then pick Regression, Classification, Clustering, or Anomaly Detection, don’t pick based on input alone.

**Decision Question:** What is the **output** you want the model to produce?

- If the output is a **Number**, treat it as **Regression** (Supervised)  
- If the output is one of **Fixed Categories**, treat it as **Classification** (Supervised)  
- If you do not have labels and want to discover groups, use **Clustering** (Unsupervised)  
- If you want to flag rare or unusual cases compared to normal, use **Anomaly Detection** (Often Unsupervised, but can be Supervised when labels exist)  

**Quick Distinction (When You Do Not Have Labels)**
- **Clustering:** Output is **groups/segments** (discover structure)  
- **Anomaly Detection:** Output is an **unusual/normal signal** (flag rare cases)

## Regression (Predicting Numbers) and Common Metrics

Use **Regression** when the output you want is a **number** (a numeric value), such as:
- How many items will be sold next month?
- What will the house price be?

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

### How Regression Metrics Work

Regression metrics summarize how far predicted numbers are from actual numbers. They answer different questions, so you pick based on what you need to control (typical error size, big misses, or fit vs baseline).

Each common regression metric answers a different question:
- **MAE:** Typical mistake size (treats all errors evenly)  
- **RMSE:** Typical mistake size, but penalizes large misses more  
- **R²:** How much variation the model explains vs the mean baseline  

### MAE (Mean Absolute Error)

**What It Measures:**  
MAE is the average **absolute** difference between prediction and actual. Absolute means you only care about how big the mistake is, not the direction (**too low** or **too high**)

**Formula:**  
MAE = Average(|Actual − Predicted|)

**How To Calculate:**  
Calculate the absolute error for each row, then average the errors

**Example:**  
Same actual, different direction (shows absolute value):  
- Actual: 100, Predicted: 92 → Absolute error = 8 (**8 too low**)  
- Actual: 100, Predicted: 108 → Absolute error = 8 (**8 too high**)  
MAE = (8 + 8) / 2 = **8**  
Both count as **8** because MAE ignores whether you were over or under.

Compute MAE from multiple rows:  
- Actual sales: 100, Predicted sales: 92 → Absolute error = 8  
- Actual sales: 50, Predicted sales: 55 → Absolute error = 5  
MAE = (8 + 5) / 2 = **6.5**

**How To Read It:**  
If **MAE = 6.5**, your predictions are off by about **6.5 units** on average. MAE stays in the same units as the target (minutes, dollars, units sold). If MAE drops from **6.5** to **3**, your typical mistake got smaller.

**When To Use It:**  
Use MAE when you want an easy-to-explain typical mistake size that is less dominated by rare spikes. It gives a clear typical error you can compare across model versions.

**Common Pitfall:**  
MAE treats all errors linearly, so a few very large mistakes may not stand out as strongly as they would under RMSE.

### RMSE (Root Mean Squared Error)

**What It Measures:**  
RMSE measures prediction error like MAE, but it **penalizes large mistakes more** because errors are squared before averaging. Squaring **amplifies large errors**, so a single big miss can influence RMSE much more than it influences MAE.

**Formula:**  
RMSE = √(Average((Actual − Predicted)²))

**How To Calculate:**  
1) Compute the error for each row (Actual − Predicted)  
2) Square each error (this is the step that makes the big miss matter more)  
3) Average the squared errors  
4) Take the square root to return to the original units

**Example:**  
A case with one large miss (shows why squaring matters):  
- Actual values: 100, 100, 100  
- Predicted values: 100, 98, 80  
- Errors: 0, 2, 20  

MAE vs RMSE on the same errors:  
- MAE = (0 + 2 + 20) / 3 = **7.33**  
  This says: On average, we’re off by about **7.33 units**  
- RMSE = √((0² + 2² + 20²) / 3) = √((0 + 4 + 400) / 3) = √(134.67) ≈ **11.61**  
  This says: The 20-unit miss matters more, so the typical error looks closer to **11.61 units**

**How To Read It:**  
RMSE is in the same units as the target (like MAE), but it increases more when there are a few big misses. A large gap between RMSE and MAE is a signal that **some errors are much larger than the rest**.

**When To Use It:**  
Use RMSE when a rare large error is dangerous or costly, and you want the metric to punish large mistakes more than MAE does.

High-stakes examples where large errors are especially harmful:
- Healthcare risk scoring: missing a high-risk patient (a large error) can delay urgent care  
- Critical infrastructure / nuclear operations: large prediction errors in sensor-based monitoring can trigger unsafe decisions or missed alarms  
- Fraud detection loss forecasting: a few large misses can cause major financial impact  

**Common Pitfall:**  
RMSE can be dominated by outliers. If your data has occasional extreme spikes you don’t want to dominate the metric, RMSE can look worse even when typical performance is fine, in those cases MAE can be a better typical error view.

### When To Prefer MAE vs RMSE (Real-Life)

Use **MAE** when you want a stable, easy-to-explain typical mistake size. MAE is often preferred when you want a metric that is less dominated by a few rare spikes.

**Example:**  
Predicting delivery time in minutes where being off by 5 vs 10 minutes is not dramatically different  

Use **RMSE** when large mistakes are especially harmful and you want the metric to punish them more strongly than MAE.

**Example:**  
Predicting next month inventory demand where a big under-forecast causes stockouts and lost sales  

**Example:**  
Predicting energy load where big misses can cause operational risk or high cost  

When RMSE is not preferred: If your data has occasional extreme outliers you don’t want to dominate the metric, RMSE can over-focus on them. In those cases, MAE can be a better typical error view.

### R² (R-Squared)

**What It Measures:**  
R² is a fit summary that tells you how much of the variation in the **target (actual) values** your model explains compared to a simple baseline.

**Formula:**  
R² = 1 − (SS Res / SS Total)

**How To Calculate:**  
First compute two sums of squares, then plug them into the formula.

- **SS Res (Sum Of Squares Residual):** Σ(Actual − Predicted)²  
  Measures how much error your model makes overall  
- **SS Total (Sum Of Squares Total):** Σ(Actual − Mean(Actual))²  
  Measures how much the actual values vary around the mean (baseline variation)

**Example:**  
Worked Example (Sales Forecasting: Compute R² Step By Step)

**Scenario:** Predict daily sales (units sold). We have 3 days of data.  
- Actual sales: 100, 50, 150  
- Model predicted sales: 110, 60, 140  

Compute the mean of actual values (baseline prediction value):  
Mean(Actual) = (100 + 50 + 150) / 3 = 300 / 3 = **100** (Baseline Prediction Value)

Compute SS Res (model error):  
SS Res = (100 − 110)² + (50 − 60)² + (150 − 140)²  
SS Res = (−10)² + (−10)² + 10² = 100 + 100 + 100 = **300**

Compute SS Total (baseline variation):  
SS Total = (100 − 100)² + (50 − 100)² + (150 − 100)²  
SS Total = 0² + (−50)² + 50² = 0 + 2500 + 2500 = **5000**

Compute R²:  
R² = 1 − (300 / 5000) = 1 − 0.06 = **0.94**

**Extra Cases (Same Data, Different Model Behavior):**  
Baseline prediction value = **100** (same as the worked example)  
SS Total = **5000** (same as the worked example)

Case 1: Perfect model (no error)  
Predicted values: 100, 50, 150  
SS Res = (100 − 100)² + (50 − 50)² + (150 − 150)² = 0² + 0² + 0² = **0**  
R² = 1 − (SS Res / SS Total)  
R² = 1 − (0 / 5000) = **1**  
Meaning: Perfect fit (no error)

Case 2: Model behaves like the baseline  
Predicted values: 100, 100, 100  
SS Res = (100 − 100)² + (50 − 100)² + (150 − 100)²  
SS Res = 0² + (−50)² + 50² = 0 + 2500 + 2500 = **5000**  
R² = 1 − (SS Res / SS Total)  
R² = 1 − (5000 / 5000) = **0**  
Meaning: No better than predicting the mean (baseline)

Case 3: Model is worse than the baseline  
Predicted values: 200, 200, 200  
SS Res = (100 − 200)² + (50 − 200)² + (150 − 200)²  
SS Res = (−100)² + (−150)² + (−50)² = 10000 + 22500 + 2500 = **35000**  
R² = 1 − (SS Res / SS Total)  
R² = 1 − (35000 / 5000) = 1 − 7 = **−6**  
Meaning: Worse than predicting the mean (baseline would be better)

Example (simple numbers, not a rule):  
Model version 1: R² = **0.50**  
After adding a useful feature (like location for house prices), model version 2: R² = **0.70**

Another cue:  
If R² drops from **0.70** to **0.40**, the model is explaining less variation, often because you removed useful signal or the model got worse  
If R² increases from **0.40** to **0.65**, the model explains more variation (less baseline-level error remains)

**How To Read It:**  
- R² = **1** → Perfect fit: the model explains all variation in the target values (no error)  
- R² = **0** → Same as baseline: the model is no better than predicting the mean (baseline prediction value)  
- R² < **0** → Worse than baseline: predicting the mean would perform better than this model  
- R² is between **0 and 1** → Better than baseline: higher R² means the model explains more variation (closer to 1 is better)  

**When To Use It:**  
Use R² as a quick fit summary alongside MAE/RMSE when you want to know whether the model is explaining real signal beyond the predict-the-mean baseline.

**Common Pitfall:**  
R² does not tell you typical mistake size. A model can have a reasonable R² but still have errors that are too large for the business. Use MAE/RMSE alongside it.

### What You Are Trying To Achieve

Choose a metric that matches your risk and what you want to control.

- Want a clear **average error** number in the same units as the target → **MAE**  
- Want to penalize large mistakes more → **RMSE**  
- Want a quick **fit** summary alongside error → **R²**  

Improve the model by comparing metric values across versions and reducing error on unseen data.

## Classification (Predicting Labels) and Common Metrics

Use **Classification** when the output you want is a **label/category** from a fixed set.

Example (Email Triage):  
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
- **Positive Class:** What **positive** means in your scenario (for example, **Fraud**)  
- **Threshold (When Using Scores):** The cutoff that turns a score into a final yes/no label (changing it shifts Precision vs Recall)

After that, each metric is just a different way to summarize the same TP/FP/TN/FN counts.

Each common metric reads the confusion matrix differently:
- **Accuracy:** Uses **(TP + TN)** vs all predictions  
- **Precision:** Focuses on **FP** (false alarms)  
- **Recall:** Focuses on **FN** (missed positives)  
- **F1:** Balances **Precision** and **Recall**  
- **AUC / ROC / PR:** Evaluate ranking across thresholds  

### Confusion Matrix (TP, FP, TN, FN)

A confusion matrix is not a metric. It is the shared counting table that most classification metrics are built from. It compares what the model **predicted** to what was **actually true**, so you can see the types of mistakes it is making.

A confusion matrix counts:
- **True Positive (TP):** Predicted positive and actually positive  
- **False Positive (FP):** Predicted positive but actually negative  
- **True Negative (TN):** Predicted negative and actually negative  
- **False Negative (FN):** Predicted negative but actually positive  

Example (Fraud Detection, where **Positive = Fraud**):
- **True Positive (TP):** Model flags a transaction as fraud, and it really is fraud (caught it)  
- **False Positive (FP):** Model flags a transaction as fraud, but it was legitimate (false alarm)  
- **True Negative (TN):** Model says **not fraud**, and it really is legitimate (correctly allowed)  
- **False Negative (FN):** Model says **not fraud**, but it was fraud (missed it)  

### Thresholds (Scores → Labels)

A classification model often outputs a **score** for each case. A **threshold** turns that score into a final label (**positive** or **negative**). Changing the threshold shifts the tradeoff between **Precision** and **Recall**.

Example (Same Model Scores, Different Decisions):  
You are predicting whether a patient needs urgent follow-up. The model outputs a **risk score** (0 to 1) for each patient.  
For 4 patients, the model outputs: **0.90, 0.70, 0.40, 0.20**  
- If you set threshold **0.50**, you flag **0.90** and **0.70** as urgent  
- If you set threshold **0.30**, you flag **0.90**, **0.70**, and **0.40** as urgent  

Same model, same scores. Only the **threshold** changed, so the final yes/no decisions changed.

### Accuracy

**What It Measures:**  
Accuracy is the overall proportion of correct predictions. It treats **false positives** and **false negatives** as equally bad, so it can hide problems when one type of mistake matters more.

**Formula:**  
Accuracy = (TP + TN) / (TP + FP + TN + FN)

**How To Calculate:**  
1) Build the confusion matrix counts (**TP, FP, TN, FN**)  
2) Add the correct predictions: **TP + TN**  
3) Divide by total predictions: **TP + FP + TN + FN**

**Example:**  
Suppose you evaluate a model on 100 cases and you get:  
- TP = 12, FP = 8, TN = 70, FN = 10  

Compute accuracy:  
Accuracy = (TP + TN) / Total  
Accuracy = (12 + 70) / (12 + 8 + 70 + 10) = 82 / 100 = **0.82**  

This says: The model is correct **82%** of the time overall.

**How To Read It:**  
Accuracy answers: Of all predictions, how many did we get right?  
A higher value means more correct predictions overall, but it does not tell you which errors you are making (false alarms vs missed positives).

**When To Use It:**  
Use Accuracy when:
- Classes are reasonably balanced  
- False positives and false negatives have similar cost  
- You want a quick overall score as a starting point

**Common Pitfall:**  
Accuracy can mislead on imbalanced data because you can get high accuracy by always predicting the majority class.

Example (Rare Fraud):  
You have 10,000 transactions, only 100 are fraud (1%), and 9,900 are legitimate.  
A useless model that always predicts legitimate gets:  
- TP = 0, FP = 0, TN = 9,900, FN = 100  
Accuracy = (0 + 9,900) / 10,000 = **0.99**

This looks great, but the model caught **0 fraud**.

In imbalanced or high-risk scenarios, rely more on:
- **Precision** (control false alarms)  
- **Recall** (avoid missing positives)  
- **F1** (balance both)  
- The **confusion matrix** (see TP/FP/TN/FN counts)

### Precision

**What It Measures:**  
Precision answers: When the model says **positive**, how often is it right?  
It measures how clean your positive predictions are, meaning how many are true positives vs false alarms.

Precision is mainly about controlling **false positives (FP)**. If precision is low, your system raises too many alerts that turn out to be wrong.

**Formula:**  
Precision = TP / (TP + FP)

**How To Calculate:**  
1) Define the **Positive Class** (for example, **Fraud**)  
2) Count how many predicted positives were correct (**TP**)  
3) Count how many predicted positives were wrong (**FP**)  
4) Divide TP by (TP + FP)

**Example:**  
Suppose the model flags 20 transactions as fraud:  
- 8 are truly fraud → TP = 8  
- 12 are legitimate → FP = 12  

Precision = TP / (TP + FP) = 8 / (8 + 12) = 8 / 20 = **0.40**

This says: When the model alerts, it is correct **40%** of the time.

**How To Read It:**  
Higher precision means fewer false alarms.  
If Precision = **0.40**, 60% of your alerts are wrong. If Precision improves to **0.80**, only 20% of alerts are wrong (cleaner alerts).

**When To Use It:**  
Use Precision when false alarms are costly or disruptive, for example:
- Blocking legitimate payments  
- Sending too many cases to manual review  
- Triggering expensive investigations  

In these scenarios, improving Precision reduces wasted effort and customer friction.

**Common Pitfall:**  
Precision can look high if the model rarely predicts positive at all.

Example:  
If the model flags only 2 cases as fraud and both are real fraud, Precision = **1.00**.  
But if there were 100 fraud cases total, it still missed most fraud (Recall is very low).  

So Precision should be read together with Recall, especially for rare positives.

### Recall / TPR (True Positive Rate) (Sensitivity)

**What It Measures:**  
Recall answers: Of the actual positives, how many did we catch?  
It measures how well the model finds the positive cases you care about (for example, catching fraud, catching disease, catching failures).

Recall is mainly about controlling **false negatives (FN)**. If recall is low, you are missing many real positives.

**Formula:**  
Recall = TP / (TP + FN)

**How To Calculate:**  
1) Define the **Positive Class** (for example, **Fraud**)  
2) Count how many actual positives were caught (**TP**)  
3) Count how many actual positives were missed (**FN**)  
4) Divide TP by (TP + FN)

**Example:**  
Suppose there are 50 real fraud cases in your evaluation set. The model catches 30 of them:  
- TP = 30 (caught fraud)  
- FN = 20 (missed fraud)

Recall = TP / (TP + FN) = 30 / (30 + 20) = 30 / 50 = **0.60**

This says: The model catches **60%** of real fraud cases.

**How To Read It:**  
Higher recall means fewer missed positives.  
If Recall = **0.60**, you miss 40% of true positives. If Recall increases to **0.90**, you miss only 10%.

**When To Use It:**  
Use Recall when missing a positive is costly or risky, for example:
- Fraud detection (missed fraud leads to loss)  
- Medical screening (missed disease can delay treatment)  
- Safety monitoring (missed failures can cause incidents)

In these scenarios, you often accept more false alarms to avoid missing positives.

**Common Pitfall:**  
Recall can be pushed high by flagging too many cases as positive.

Example:  
If you flag almost everything as fraud, you might catch nearly all fraud (high Recall), but you also create many false alarms (low Precision).  

This is why Recall should be read together with Precision, and why thresholds are tuned to balance the tradeoff.

### F1 Score

**What It Measures:**  
F1 combines **Precision** and **Recall** into one score. It rewards models that perform well on both, and it drops quickly if either one is weak.

F1 is especially useful when:
- The positive class is rare  
- You want one summary number  
- You still care about both false alarms (**FP**) and missed positives (**FN**)

**Formula:**  
F1 = 2 × (Precision × Recall) / (Precision + Recall)

**How To Calculate:**  
1) Compute **Precision** and **Recall** from TP/FP/FN  
2) Plug them into the formula  
3) Interpret F1 as a both-must-be-good score

**Example:**  
Suppose:  
- Precision = 0.75  
- Recall = 0.60  

F1 = 2 × (0.75 × 0.60) / (0.75 + 0.60)  
F1 = 2 × 0.45 / 1.35  
F1 = 0.90 / 1.35 = **0.67**

This says: The balanced score is **0.67**, and it is pulled down by the weaker side (Recall = 0.60).

**How To Read It:**  
- F1 is high only when both Precision and Recall are high  
- F1 tends to be closer to the smaller of the two, so it exposes imbalance  

Example intuition:  
If Precision = 0.95 but Recall = 0.10, F1 will still be low because you are missing most positives.

**When To Use It:**  
Use F1 when you need one number to compare model versions and you care about both:
- False alarms (Precision)  
- Missed positives (Recall)

It is common in imbalanced classification when Accuracy is misleading.

**Common Pitfall:**  
F1 hides which side is failing.

Example:  
Two models can have the same F1 but very different tradeoffs:
- Model A: high Precision, low Recall (few false alarms, many misses)  
- Model B: low Precision, high Recall (many false alarms, few misses)

So you still check Precision and Recall directly, especially if the business cost is asymmetric.

### AUC (Area Under The ROC Curve)

**What It Measures:**  
AUC, also called **Area Under The ROC Curve**, measures how well the model **ranks positives above negatives** across all possible thresholds.

AUC focuses on ranking quality, not on one fixed cutoff. It answers: does the model tend to score true positives higher than true negatives?

**Where Do These Scores Come From:**  
A classification model often outputs a **score** for each case. You can think of it as a **fraud risk score**:
- Higher score → the model thinks the case is **more likely fraud**  
- Lower score → the model thinks the case is **more likely legitimate**  

In many models, this score is a **predicted probability** (0 to 1), but it can also be any numeric score as long as higher means more positive-like.

**How To Calculate (High Level):**  
1) Collect the model scores for positives and negatives  
2) Sweep the threshold from high to low  
3) Plot the ROC curve across thresholds  
4) AUC summarizes the ROC curve into one number (higher is better)

**Example (Scores 0 To 1):**  
Suppose you have 5 fraud cases and 5 legitimate cases. The model outputs a score for each transaction:

Fraud scores: **0.95, 0.90, 0.80, 0.70, 0.60**  
Legit scores: **0.55, 0.40, 0.30, 0.20, 0.10**

Here, fraud scores are mostly higher than legit scores, so the model separates the classes well → **High AUC**.  
If the scores overlap a lot (fraud and legit both mixed around 0.40–0.60), separation is weak → **Lower AUC**.

**How To Read It:**  
AUC is useful because it evaluates the model’s separation quality **before** you pick the threshold.  
A higher AUC means the model is better at ranking positives above negatives.

### ROC (Receiver Operating Characteristic) vs PR (Precision-Recall)

**What It Measures:**  
ROC and PR are curve views of performance across thresholds. They show how your Precision/Recall tradeoff changes as you move the threshold.

- **ROC (Receiver Operating Characteristic):** A curve view based on **TPR vs FPR** across thresholds  
- **PR (Precision-Recall):** A curve view based on **Precision vs Recall** across thresholds  
- **TPR (True Positive Rate):** The same as **Recall** = TP / (TP + FN)  
- **FPR (False Positive Rate):** The proportion of actual negatives incorrectly flagged = FP / (FP + TN)  

With rare positives, PR often shows performance more clearly than ROC.

**Example (Rare Positives With Real Counts):**  
You have **10,000** transactions, and only **100** are actually fraud (**1%**). The model flags **500** as fraud. **TP = 50**, **FP = 450**, so:  
- Total actual legitimate = 10,000 − 100 = **9,900**  
- **FN = 100 − 50 = 50**  
- **TN = 9,900 − 450 = 9,450**

So:  
- **Precision** = TP / (TP + FP) = 50 / 500 = **0.10**  
- **Recall / TPR** = TP / (TP + FN) = 50 / 100 = **0.50**  
- **FPR** = FP / (FP + TN) = 450 / 9,900 ≈ **0.045**

**ROC Point (At This Threshold):** (**FPR ≈ 0.045**, **TPR = 0.50**)  
**PR Point (At This Threshold):** (**Recall = 0.50**, **Precision = 0.10**)

**How To Read It:**  
PR makes the pain obvious (low precision), even if ROC looks acceptable because FPR can look small when true negatives are so common.

> [!IMPORTANT]
> When positives are rare, **Precision-Recall** curves often show performance more clearly than ROC. ROC can look good even when precision is low, because true negatives dominate.

## Clustering (Grouping Similar Examples Without Labels)

Use **Clustering** when you want to group examples into **clusters** based on similarity and you do not have labels (no correct category column).  
A clustering model does not learn the right answer per row. Instead, it looks for patterns in the **features (X)** and discovers groups that tend to look alike.

Clustering is **unsupervised**: it discovers grouping patterns from **X**, then humans interpret clusters and validate whether they make sense using summaries and sanity checks.  
For example, Cluster 1 might later be described as **high spenders**, but that name is an interpretation, not a label the model trained on.

**Highlights**
- Output is a **cluster ID** (a group assignment), not a known label  
- Training data needs **features (X)**, not labels (y)  
- Typical validation: usefulness, stability over time, and interpretability  

### Why Clustering Is Useful

Clustering is useful when you want a **structure-first** view of your data. It helps you discover groups that behave differently so you can tailor actions, investigate patterns, or build simpler downstream rules.

Common outcomes include:
- Finding customer segments for marketing and retention  
- Grouping similar documents or products for organization  
- Identifying device behavior groups for monitoring and operations  

### Clustering Outputs (Cluster ID vs Human Labels)

A clustering model outputs a cluster assignment, usually an ID like Cluster 0, Cluster 1, Cluster 2.  
Humans often assign names to clusters after analysis, but those names are not training labels.

Example:
- Output: Cluster 1  
- Interpretation: **discount-driven buyers**  

### What Data Clustering Needs

Because clustering is **unsupervised**, the dataset does not need a label/target column (y).  
What it must contain is:
- **Rows (Examples):** The things you want to group (customers, devices, neighborhoods)  
- **Feature Columns (X):** Numeric or encodable attributes that represent behavior or characteristics  
- Enough **variation** and **volume** for meaningful group patterns to appear  

So the essential requirement is: clustering needs **features**, not target labels.

### Preparing Features For Clustering

Clustering depends heavily on how you represent each row as features, because similarity is computed from **X**.

Typical preparation steps:
- Scale numeric features when magnitudes differ a lot (so one large-scale feature does not dominate)  
- Encode categorical fields in a machine-friendly form (so similarity is meaningful)  
- Remove obvious leakage features that act like identifiers (so clusters do not become disguised ID groups)  

A good check: if you reorder rows, clustering should not change. If you rename IDs, clustering should not change. If it does, you likely included an ID-like feature.

### Example: Similar Purchasing Habits (Customer Segmentation)

If you want to group customers by similar purchasing habits, typical feature columns could be:
- **Purchase Frequency** (orders/month)  
- **Average Order Value**  
- **Total Spend** (last 3 months / 12 months)  
- **Discount Usage Rate**  
- **Product Category Mix** (percent spend per category)  
- **Recency** (days since last purchase)  

The clustering algorithm groups customers with similar feature patterns into segments.  
After clustering, you usually validate and interpret clusters using summary statistics, business sanity checks, and stability checks.

### Example (Real Data Feel): Customer Segmentation (Clustering)

Imagine an online shop wants to create customer segments for marketing, but there is no segment column in the data.

In this scenario:
- The **rows** are customers (one row per customer)  
- The **features (X)** are numeric/encodable signals like frequency, spend, discount rate, and recency  
- The **output** is a **cluster ID** (for example, Cluster 0, Cluster 1, Cluster 2), not a known correct label  

After you get clusters, humans interpret them:
- Cluster 0 might look like **high spend, low discount**  
- Cluster 1 might look like **discount-driven, frequent buyers**  
- Cluster 2 might look like **new or inactive customers**  

Those names are interpretations based on the feature patterns, not labels the model trained on.

### How Clustering Is Evaluated (High Level)

Clustering does not usually have one simple metric like Accuracy because there is no single correct label to compare against. In practice, you check whether the clusters are:
- **Useful** for the goal (segmentation, personalization, targeting)  
- **Stable** (not changing wildly with small data changes)  
- **Interpretable** (you can explain what makes clusters different)  

In some cases you may see internal metrics like **Silhouette Score**, but you still validate usefulness and interpretability.

### Common Pitfalls

- Using ID-like fields as features, which causes clusters to become identity groups instead of behavior groups  
- Forgetting scaling and letting one large-scale feature dominate similarity  
- Over-interpreting clusters as ground truth, clusters are discovered patterns, not confirmed labels  
- Getting clusters that change too easily over time, which usually means features are noisy or the pattern is not stable  

### Practical Defaults And Rules Of Thumb

- Start with features that represent behavior, not identity  
- Use summary statistics per cluster to validate meaning (averages, distributions, top categories)  
- Check stability by re-running clustering on a later time window and comparing whether clusters remain similar  
- Treat cluster names as human labels added after the fact, not outputs the model learned  

## Anomaly Detection (Flagging Unusual Behavior)

Use **Anomaly Detection** when you want to find data points or events that are **unusual compared to normal behavior**.  
You choose it when the goal is to surface rare cases that may represent risk, failure, fraud, or important abnormal conditions.

Anomaly detection often outputs an **anomaly score** (how unusual) and/or an **anomaly flag** (normal vs abnormal).  
It is commonly unsupervised (learn normal, flag deviations), but it can also be supervised when you have reliable labels.

**Highlights**
- Output is an anomaly **score** and/or anomaly **flag**  
- Core idea is comparing behavior to a **normal baseline**  
- Thresholds control the tradeoff between false alarms and missed anomalies  
- Validation focuses on usefulness, stability, and false positive rate in practice  

### Why Anomaly Detection Is Useful

Anomaly detection is useful when the important cases are rare and you cannot rely on having enough labeled examples.  
Instead of predicting a fixed category, you detect deviations from what is typical.

Common outcomes include:
- Flagging suspicious transactions or account activity  
- Detecting equipment faults and early warning signals  
- Detecting unusual login patterns or network intrusions  
- Detecting metric spikes or drops in telemetry  

> [!IMPORTANT]
> An anomaly flag is not a diagnosis. It is a signal to investigate.

### Key Terms (Quick Definitions)

- **Anomaly:** A data point that differs significantly from the expected pattern  
- **Normal Baseline:** What typical behavior looks like for the system or population  
- **Threshold:** The cutoff that turns an anomaly score into a final flag  
- **False Positive:** Flagged as anomalous but actually normal  
- **False Negative:** Not flagged but truly anomalous  

### What Data Anomaly Detection Needs

What you need depends on whether you have labels.

If you do not have labels (common case):
- You need **features (X)** that represent behavior  
- You need enough history to learn what **normal** looks like  
- You often need time context if patterns are seasonal or time-dependent  

If you do have labels (less common, but possible):
- You can evaluate like classification by defining what counts as **positive** (anomaly)  
- You still need features that reflect behavior, not identity  

### Example (Real Data Feel): Fraud Monitoring (Anomaly Detection)

Imagine a bank monitors card transactions to flag suspicious activity.

In this scenario:
- The **rows** are transactions (one row per transaction)  
- The **features (X)** might include amount, location, time-of-day, merchant category, and frequency patterns  
- The **output** is an anomaly **score** or a **normal vs abnormal** flag, not a business label like **fraud type**  

Because anomalies are rare, you tune thresholds to balance false alarms (false positives) vs missed fraud (false negatives).

### How Anomaly Detection Works (High Level)

A typical workflow looks like this:
- Define what **normal** looks like (baseline period, typical ranges, seasonality)  
- Choose what you will detect anomalies in (transactions, sensors, logs, images)  
- Produce an anomaly **score** or anomaly **flag**  
- Tune thresholds to balance false alarms vs missed issues  

### Common Approaches (High Level)

- **Rules or statistics:** Thresholds, z-scores, moving averages (good starting point)  
- **Unsupervised ML:** Learn normal patterns without labeled anomalies (common when anomalies are rare)  
- **Supervised ML:** Train on labeled normal vs anomaly when labels exist and are reliable  

### Common Pitfalls

- **Context changes what is normal:** Seasonality, time of day, and user segments can shift baseline behavior  
- **Too many false positives:** The system becomes unusable if everything is flagged  
- **Baseline drift:** Normal behavior changes over time, so baselines must be updated  
- **Confusing anomalies with categories:** An anomaly flag means unusual, not the reason why it is unusual  

### Practical Defaults And Rules Of Thumb

- Start by defining normal in a clear time window and re-check it regularly  
- Keep features focused on behavior signals, not identifiers  
- Treat thresholding as a design choice and tune it to operational capacity  
- Validate using review samples and stability checks, not just a single metric number  


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
- Choose the right ML problem type by focusing on the **Output**  
- Identify **Regression**, **Classification**, **Clustering**, and **Anomaly Detection** scenarios  
- Use **MAE**, **RMSE**, and **R²** for regression evaluation  
- Use the confusion matrix (**TP**, **FP**, **TN**, **FN**) to reason about classification errors  
- Use **Accuracy**, **Precision**, **Recall / TPR**, **F1**, and **AUC** for classification evaluation  
- Match metrics to real error cost (false alarms vs missed positives)  
- Explain that clustering uses **Features (X)** without labels  
- Explain that anomaly detection flags unusual behavior vs a **Normal Baseline**  
- Avoid input vs output confusion when choosing a problem type  
- Avoid relying on **Accuracy** for imbalanced classification  
- Avoid mixing metric families (regression vs classification)  
- Avoid forgetting the **Positive Class** definition  
- Avoid leakage by using information not available at prediction time  

