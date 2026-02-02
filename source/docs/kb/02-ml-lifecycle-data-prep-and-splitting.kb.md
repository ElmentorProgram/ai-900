# ML Lifecycle: Data Preparation and Splitting

This document focuses on the ML lifecycle steps that happen **before and around training**: getting data into your pipeline (**Data Ingestion**), making it usable (**Data Preparation**), and splitting it into **training/validation/test** so you can measure performance on **unseen examples**.

These steps determine whether your evaluation is trustworthy. If you prepare or split data incorrectly, you can get metrics that look great but fail in production (common causes are **leakage** and **peeking**). The sections that follow explain where data prep fits in the lifecycle, how to choose safe inputs (Features vs Labels vs IDs), and how to split correctly for reliable evaluation.

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

When you build an ML model to support a real decision (for example: estimate risk, classify requests, forecast demand, detect anomalies), start by defining what you’re building and how it will be used in real life. That means clearly stating: the **target output**, the **inputs available at prediction time**, and what **good** looks like (the success metric & its target).

The goal is to perform well on **new, unseen data**, not just the data you trained on. After that, you move through the ML lifecycle: build a reliable dataset, prepare and train the model, evaluate it, and finally deploy it to production.

A typical end-to-end lifecycle looks like:
- **Prepare Data** (**Data Ingestion** & **Data Preparation**)  
- **Split Data:** **Training / Validation / Test**  
- **Train:** Fit the model on the **training set**  
- **Evaluate & Tune:** Compare versions and tune choices using the **validation set**  
- **Final Test:** Run one last check on the **test set** (unseen **final check**)  
- **Package:** Confirm the **input/output schema** and how the model will be called  
- **Deploy & Monitor:** Deploy as an **endpoint/service**, then monitor **errors**, **data drift**, and **performance drift**

> [!NOTE]
> **Data Ingestion** means collecting/loading data into your pipeline. **Inference (Scoring)** means using a trained model to make predictions.

### Metrics Targets and Iteration (How It Works)

Defining a success metric is not just picking a metric name. In practice, you also set a **target value** (what is **good enough**), evaluate the model on **held-out data**, and iterate until you meet the target. Iteration can mean improving data and features, changing the model, adjusting thresholds, or tuning settings.

The **test set** is the final unbiased check after you stop making changes.

### Training vs Inference Compute (Why It Matters)

Model size is not just **qualitative**, it affects the resources you need to build and run the model.

- **Training Compute (Building The Model):** More parameters means more weights to update during learning → more GPU hours, memory, data, and time  
- **Inference Compute (Using The Model):** More parameters means more work per prediction → higher latency, lower throughput, and higher cost per request (or per token for language models)  

**Rule of thumb:** Larger models usually cost more to train and to use. Inference cost also depends on context length, output length, and the serving setup (hardware and optimization like quantization).

## ML Lifecycle Context (Where Data Prep Fits)

When you build an ML model, you need data before training. This stage is about building a clean, usable dataset so training and evaluation are meaningful. It is not where you prove the model is good.

- **Data Ingestion:** Getting raw data from where it lives (files, databases, logs) into your ML workspace as a dataset you can work with  
- **Data Preparation:** Cleaning and transforming that dataset so it’s usable for training (fix types, handle Missing Values, remove duplicates, encode categories)  
- **Missing Values:** Fields that are blank/unknown (nulls) that can break training or reduce model quality  

These are part of building the model.  
Using the model happens later (deployment & sending new input data for predictions).

> [!NOTE]
> Data Ingestion and Data Preparation build a trainable dataset, they don’t prove the model is good, evaluation happens after training using held-out data

These stages focus on building a reliable dataset for learning, not on measuring model performance. Training, inference (scoring), and evaluation happen later in the lifecycle.

### What This Stage Is Trying To Achieve
- Make data usable, consistent, and accurate enough for training  
- Ensure the dataset represents the problem well and reduces noise that would confuse the model  
- Prevent downstream failures (training errors, incorrect evaluation, unstable predictions)  

### Common Actions In Data Ingestion And Preparation
Typical tasks include:
- Combine multiple datasets (merge/join/append) so all needed fields are in one dataset  
- Handle Missing Values using a scenario-appropriate choice  
  - Remove records with missing critical fields  
  - Impute Missing Values (fill with a reasonable value) when removal would bias the dataset  
- Remove duplicates, fix data types, standardize formats, and deal with outliers  
- Select relevant columns and encode categorical values when needed  

> [!IMPORTANT]
> Avoid leakage in preparation: fit cleaning/transform steps on the training set, then apply the same steps to validation/test.

### Feature Engineering vs Feature Selection

- **Feature Engineering:** Creating or transforming input fields to make patterns easier for a model to learn  
- **Feature Selection:** Choosing which input fields to keep and dropping the rest  

**Feature Engineering Reasons**
- Make patterns easier to learn  
- Improve generalization by turning raw data into useful signals  

**Feature Engineering Examples**
- Convert a date into `day_of_week`, `month`, `holiday_flag`  
- Convert transactions into aggregates like `orders_last_30_days`, `avg_basket_size`, `spend_trend`  
- Convert text into numeric signals (TF-IDF, embeddings, sentiment score)

#### Example (Real Data Feel): Predicting House Sale Price (Regression)

Imagine a dataset where each row is one house sale.

**Label (Target)**
- Use `SalePrice` as the label, the actual sale price (a number)

**Raw Fields (Possible Features)**
- Use `LivingAreaSqFt`, `Bedrooms`, `Bathrooms`, `Neighborhood` as starting features  
- Use `YearBuilt`, `SaleDate`, `RenovationDate` as additional raw fields (renovation can be missing)

**Feature Engineering Examples (You Create New Inputs)**
- Create `HouseAge` from `SaleYear - YearBuilt`  
- Create `YearsSinceRenovation` from `SaleYear - RenovationYear` (when renovation exists)  
- Convert `SaleDate` into `SaleMonth` or `Season` (to capture seasonality)  
- Encode `Neighborhood` into a machine-friendly form (for example, indicator columns)  
- Create `PricePerSqFt` is **not** a feature here, because it uses the label (`SalePrice`) and would leak the answer  

**Feature Selection Reasons**
- Remove irrelevant/noisy features  
- Reduce overfitting risk  
- Simplify the model (interpretability)  
- Reduce cost (fewer inputs to collect/compute)

**Feature Selection Examples (High Level)**
- Filter methods: correlation, mutual information, statistical tests  
- Wrapper methods: evaluate model performance with different subsets  
- Embedded methods: feature selection happens during training (for example, regularization)

**Common Pitfalls**
- Engineering features using information that is not available at prediction time (leakage)  
- Dropping a feature that looks weak globally but is crucial for a subset of cases  

> [!IMPORTANT]
> A common pitfall is engineering a feature using information you would not know at prediction time. That creates leakage, even if the feature looks **helpful**.

### What Does Not Belong To This Stage
Some actions happen after preparation:
- **Training:** fitting the model on training data  
- **Inference (Scoring):** using the model to predict on new/test data  
- **Evaluation:** calculating metrics such as accuracy, precision/recall, RMSE, etc

### Common Pitfalls And Confusion Points
- Mixing evaluation tasks (like calculating accuracy) into data prep can lead to unclear workflows  
- Cleaning the full dataset before splitting can cause leakage (prep should be fit on training data, then applied to validation/test)  
- Removing too many records due to missing values can bias the dataset; sometimes imputation is better

### Practical Defaults And Rules Of Thumb
- Start by profiling data (missingness, duplicates, outliers) before deciding cleaning actions  
- Treat missing target labels differently from missing feature values (missing labels usually can’t be used for supervised training)  
- Keep a repeatable pipeline so the same preparation is applied in production

## Features, Labels, and IDs (Choosing Inputs Safely)

Before you can train a model, you need a dataset that represents the problem you are trying to solve. In supervised learning, each example contains inputs the model can use and an outcome you want the model to predict. The goal is to choose inputs that will still be available when you use the model in real life.

A simple rule: **If you won’t know it at prediction time, it is not a safe feature** (even if it makes metrics look better).

### Example (Mapping The Terms)
- Imagine you want to predict **house sale price**
- One **row (example/record)** could represent **one house sale**
- The **columns** are the fields in that row
- The **features (inputs, X)** could include living area, number of bedrooms/bathrooms, neighborhood, and property age
- The **label (target, y)** is the sale price

A dataset is typically organized as:
- **Rows:** Examples/records (each row is one case)  
- **Columns:** Fields/features (inputs) plus the **label/target** (what you predict)  

When you build a model, each row should contain:
- **Features (Inputs):** Information available at prediction time (what you know before the outcome happens)  
- **Label (Target):** The value you want the model to predict  

A good feature:
- Has a meaningful relationship to the target  
- Is available at the time you will make the prediction  
- Helps the model generalize to new data  
- If a field is only known **after** the outcome happens, it is not a safe feature for training or evaluation  

### Supervised vs Unsupervised (Why This Matters)
- **Supervised Learning:** You have a label column (y) and you learn to predict it from features (X)  
- **Unsupervised Learning (Clustering):** You do **not** have labels, clustering still needs **rows & feature columns**, but there is no target label to learn  

**Key idea:** Clustering needs **features**, not target labels. Clusters are discovered, then humans interpret and name them later.

### Feature vs Label Decision Rule (Population Example)
A field like **population of an area** is not automatically **a feature** or **a label**. It depends on what you are trying to predict.

- If population is something you **know at prediction time** (for example, to predict store demand), treat it as a **feature**  
- If population is what you **want to predict**, it becomes the **label** and the task is often **regression** (predict a number)  

### Things To Avoid
- **Using the target as an input**  
- **Using IDs as features**  
- **Using dataset-level totals** when predicting a per-row outcome  

Examples:
- **IDs as features:** `CustomerID`, `OrderID`, `DeviceID`, `TicketID` can let the model memorize identity patterns instead of learning general rules  
- **Dataset-level totals:** using **total monthly revenue** to predict **this row’s sale price** mixes global information into each row and can inflate evaluation  

> [!NOTE]
> **Features go in; label comes out.** Example (Loan Approval): **Features** (credit_score=720, income=£55k, debt_to_income=0.28, missed_payments_12m=0) → **Label** (**Approve** | **Reject** | **Review**)

## Why We Split Data (Training vs Validation vs Test)

When you build an ML model, you want it to make good predictions on **new data you haven’t seen yet** (real life). Splitting is how you simulate that reality before deployment.

You split the data to support two different activities:
- **Learning (Training):** Give the model many examples so it can learn patterns that connect inputs to the outcome you care about  
- **Checking (Evaluation):** Test whether it learned a general rule, or if it just memorized training examples, by evaluating it on different examples it did not learn from  

If you test the model on the same examples it learned from, the score isn’t trustworthy.

**Example:** Training is like studying from practice questions; evaluation is like taking a mock exam with different questions. If you reuse the same questions, the score isn’t trustworthy.

> [!IMPORTANT]
> Splitting is how you simulate real life, train on one set of rows, evaluate on different unseen rows, if you evaluate on training rows, the score is not trustworthy.

A proper split holds out **examples (rows)** so evaluation reflects performance on **new cases**, while keeping the same set of input fields available in both training and evaluation.

### Why There Are Multiple Sets

Even though there are two activities (learning and checking), the **checking** activity is commonly split into two sets:
- **Validation Set:** Used during development to compare model versions and tune settings  
- **Test Set:** A final **unbiased** check on unseen examples after decisions are made  

Key sets:
- **Training Set:** Examples used to learn patterns  
- **Validation Set:** Examples used during development to compare model versions and tune settings  
- **Test Set:** A final **unbiased** check on unseen examples after decisions are made  

> [!WARNING]
> Do not use the test set during tuning, if you keep checking the test set and making decisions, it stops being an unbiased final check.

A simple mental mapping: **Train = learn**, **Validation = tune**, **Test = final check**.

### Example (Fraud Detection: Metric Targets → Evaluate → Iterate)

- Goal: detect fraud transactions  
- Metric targets: **recall ≥ 0.80** (catch most fraud) and **precision ≥ 0.20** (limit false alarms)  

Step 1: Train a model on the **training set**  
Step 2: Evaluate on the **validation set**. Suppose the model flags 500 transactions as fraud, but only 50 are truly fraud, and there are 100 real fraud cases total  
- Precision = 50 / 500 = **0.10**  
- Recall = 50 / 100 = **0.50**  

Step 3: You missed both targets, so you iterate using the **validation set**: adjust the threshold, engineer better features, try a different model, or tune hyperparameters  
Step 4: After iteration, suppose validation results improve and you reach **precision = 0.22** and **recall = 0.82** (targets met)  
Step 5: Run one final check on the **test set** to confirm the model meets targets on unseen data

### Tuning vs Fine-Tuning (Wording)

This improvement loop is usually called **iteration** or **tuning**. It means any change you make to improve metrics during development, for example changing the decision threshold, adding or transforming features, fixing leakage, handling class imbalance (rebalancing), trying a different algorithm, or tuning hyperparameters.

Do not mix this with **fine-tuning**. **Fine-tuning** is more specific: you take a **pre-trained model** (often an LLM or another pre-trained neural network) and train it further on your task data to adapt it. In classic ML (logistic regression, random forests, gradient boosting/XGBoost), you typically say **train/tune** rather than **fine-tune**.

So in the fraud example: if you miss a target (like precision), you **iterate/tune** using the validation set. You would call it **fine-tuning** only if you are adapting a **pre-trained model** by additional training on your fraud dataset.

## How Splitting Works (Rows vs Columns)

Splitting is how you simulate **real life** before deployment. The core idea is to train on some examples, then prove the model can handle **new examples** it has never seen before.

### Split By Rows (What You Usually Want)

To simulate new data, you hold out entire **examples (rows)** that the model never sees during training.

- If you split by **rows**, evaluation reflects performance on **new cases**  
- You keep the **same columns** (same feature inputs) so training and evaluation are solving the same task  

### Split By Columns (Why It Is Usually Wrong For Evaluation)

If you split by **columns**, you are not holding out new examples. Instead, you are removing some input fields.

That changes the problem into: **Can the model work with less information?**  
It does not answer the evaluation question: **Will this model generalize to new cases?**

> [!WARNING]
> Split by rows for evaluation, splitting by columns changes the problem into **less information**, it does not measure generalization to new examples.

### Key Rule
- Split by **rows** so evaluation uses unseen examples  
- Keep the **same feature columns** in both training and evaluation so the task stays consistent


## Split Patterns and When Random Split Fails (Time-Based and Group-Based)

### Random Split

Randomly splitting rows is a common default when each row is an **independent** example. It usually keeps training and evaluation sets similar in distribution, so evaluation reflects the same kind of data the model will see in real life.

However, random splitting is not always the best choice.

> [!IMPORTANT]
> Random split is fine only when rows are independent, use time-based split for time-ordered data, use group-based split when multiple rows belong to the same user, patient, or device.

**Special Splitting Cases (When Random Split Fails)**  
- **Random Split:** Shuffle and split when rows are independent  
- **Time-Based Split:** Train on past data, test on future data  
- **Group-Based Split:** Keep the same user/patient/device in only one split  

Typical starting splits:
- **80/20** (train/test) for quick experiments  
- **70/15/15** (train/validation/test) for disciplined tuning  
- **60/20/20** when data is large and you want a stronger evaluation signal  

**Stratified Split (When Classes Are Imbalanced)**  
For classification with imbalanced classes, use a **stratified** split so each subset keeps a similar class ratio.

### Time-Based Split

If data is **time-ordered**, you usually want to train on the past and evaluate on the future. This better matches real deployment, especially for **next month** style predictions.

> [!WARNING]
> **Time-based split rule:** when data has time order, do not shuffle.
> Train on **past** data and evaluate on **future** data, or your metric can look unrealistically good.

**Time-Based Split Example**  
Train on data from **Jan–Sep**, validate on **Oct**, and test on **Nov–Dec**.  
This simulates the real world: you predict the future using only the past.

### Group-Based Split

If rows are **grouped/related** (for example, multiple rows from the same user/patient/device), you usually want each group to stay in only one subset. This avoids the model seeing the same group in training and evaluation.

If multiple rows come from the same user/patient/device/store, they must appear in **only one** of train/validation/test, or you leak identity patterns.

**Group Split Example**  
A patient has 6 visits in your dataset. All 6 visits must go into **only one** split (train or validation or test).  
If the same patient appears in both train and test, the model can memorize that patient’s patterns.

## Common Pitfalls (Leakage, Peeking, Ordering Bias, and Overfitting)

This section highlights common mistakes that make evaluation unreliable, and how those mistakes can hide problems like overfitting or underfitting.

Leakage and peeking make metrics look better than real life, you must keep anything that reveals the answer out of training, and keep the test set untouched until the end.

**Mental Mapping (Quick Definitions)**
- **Leakage:** The model gets information it would not have at prediction time  
- **Peeking:** You use the test set during tuning, so it stops being an unbiased final check  
- **Ordering Bias:** Your split is influenced by time/order effects, so evaluation is biased  
- **Overfitting vs Underfitting:** Splits reveal whether the model memorized or failed to learn patterns  
- **Non-Repeatable Preparation:** You clean/transform data differently in training vs production, so real predictions become unstable  

### Data Leakage
Data leakage happens when evaluation information accidentally influences training. A common example is using the **target** as an input feature, which makes performance look unrealistically strong.

**Data leakage = using information you would not have at prediction time.**  
If a field is only known **after** the real-world outcome happens, it must not be used as a feature.

Example: You are predicting **will a patient be readmitted within 30 days?**  
If your dataset includes **readmission_date** or **readmitted_flag**, those fields only exist **after** the readmission happens. Including them makes evaluation look great, but the model cannot rely on them in production.

**Leakage Example**  
You are predicting whether a loan will be repaid on time.  
If you include a feature like **default_status** (Yes = not repaid on time, No = repaid on time) or **collections_started**, you are using information that is only known after the outcome happens.

### Peeking at the Test Set
The **test set** is a final **unbiased** check. If you repeatedly check the test set during tuning, you turn it into part of your development loop and reduce trust in the final score.

Rule: check the test set only at the end, after finalizing your model decisions.

### Ordering Bias (Non-Random Splits on Ordered Data)
If data is time-ordered and you do a non-random split without thinking, early rows can differ from later rows (seasonality, collection changes), which can bias evaluation.

Rule: when time order matters, use a time-based split so evaluation reflects real-world prediction.

### Overfitting and Underfitting (What Splits Help You See)
Splitting data helps you detect whether the model is learning general patterns or not:

- **Overfitting:** performance looks strong on the **training set** but drops on **validation/test** (the model memorized training examples instead of generalizing)  
- **Underfitting:** performance is weak on both the **training set** and **validation/test** (the model did not learn useful patterns)  

## Summary

You should now be able to:
- Understand the **End-to-End** ML lifecycle and where **Data Ingestion** & **Data Preparation** fit  
- Explain how data flows from **Prepare Data** through **splitting**, **training**, and **deployment**  
- Prepare data for training by reducing noise and making inputs usable  
- Handle **Missing Values** as a design choice (drop vs impute)  
- Keep preparation repeatable so the same steps apply in production  
- Distinguish **Feature Engineering** (create/transform signals) from **Feature Selection** (choose inputs to keep)  
- Avoid leakage in preparation: fit prep on **training**, then apply to **validation/test** and production  
- Describe **features** & **labels** and why **IDs** and **targets** are not safe inputs  
- Apply supervised vs unsupervised framing: Clustering needs **features**, not **labels**  
- Explain why we split into **training/validation/test** and split by **rows** (not columns)  
- Choose **random**, **time-based**, **group-based**, or **stratified** splits based on the data  
- Recognize pitfalls like **leakage**, **peeking**, **ordering bias**, and how splits reveal **overfitting** and **underfitting**  
- Distinguish **Data Ingestion** from **Inference (Scoring)**  
- Explain why larger models need more **Training Compute** and **Inference Compute**


