# Detailed Practice Test 02 - Answer Sheet & Explanation
**Question:** [031]  
A team is building a machine learning solution to **forecast demand**. They agree on the target output and success metric, prepare the dataset, train several versions, compare them on held-out data, run one final unbiased check, and then deploy the chosen model while monitoring it in production.

Which option best matches the correct end-to-end lifecycle flow?

**Options:**  
A. Define the problem → Train the model → Prepare the data → Evaluate on the test set during tuning → Deploy  
B. Define the problem → Prepare data → Split data → Train → Evaluate and tune on validation data → Final test on unseen test data → Deploy and monitor  
C. Prepare data → Deploy the model → Train on production traffic → Evaluate using the training set → Final test  
D. Define the problem → Split columns → Train → Use the validation set as the final unbiased check → Deploy  

**Correct Answer(s):** B

**Explanation:**  
The correct lifecycle flow is:
- **Define the Problem First**
- **Prepare Data Before Training**
- **Split Data Before Trustworthy Evaluation**
- **Use Validation for Tuning**
- **Use Test for Final Unbiased Check**
- **Deploy and Monitor After Model Selection**

**Why the Correct Answer Is Correct:**  
- The lifecycle starts by defining **what to predict**, **which inputs are available at prediction time**, and **what metric target means success**.  
- Data preparation happens before meaningful training and evaluation. Azure Machine Learning documentation treats data, training, deployment, and monitoring as connected lifecycle stages.  
- Validation data is used during development to compare versions and tune decisions, while the test set is kept for the final unbiased check.  
- After model selection, deployment is followed by monitoring for issues such as drift and production performance changes.  

**Why the Other Options Are Wrong:**  

**A. Define the problem → Train the model → Prepare the data → Evaluate on the test set during tuning → Deploy**  
Wrong because training does not come before data preparation, and the **test set must not be used during tuning** if you want it to remain an unbiased final check.  

**C. Prepare data → Deploy the model → Train on production traffic → Evaluate using the training set → Final test**  
Wrong because deployment comes after training and evaluation, not before them. It is also wrong to rely on the **training set** as the evaluation proof of generalization.  

**D. Define the problem → Split columns → Train → Use the validation set as the final unbiased check → Deploy**  
Wrong because evaluation is usually simulated by **splitting rows**, not columns, and the **test set** is the final unbiased check, not the validation set.  

**Tips and Tricks:**  
- **Define First = Target, Inputs, Success Metric**  
- **Validation = Tune**  
- **Test = Final Check**  
- **Deploy = Not the End, Monitor After Deployment**

> [!IMPORTANT]  
> A common trap is mixing **validation** and **test**. Use **validation** during iteration, and keep the **test set** untouched until the end so it remains a trustworthy final check.  

**Source:**  
- [Azure Machine Learning documentation](https://learn.microsoft.com/en-us/azure/machine-learning/?view=azureml-api-2)  
- [Build and train models with Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/concept-train-machine-learning-model?view=azureml-api-2)  
- [Data splits and cross-validation in automated machine learning](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-configure-cross-validation-data-splits?view=azureml-api-1)  
- [Model monitoring in production - Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/concept-model-monitoring?view=azureml-api-2)  

**Question:** [032]  
A team is preparing data for a supervised learning model. Their raw data comes from files and logs, some fields are missing, some rows are duplicated, and a few columns need type fixes and category encoding. They also want to avoid making validation and test results look better than real life.

Which action plan is the most appropriate?

**Options:**  
A. Ingest the raw data, prepare the full dataset, calculate evaluation metrics, and then train on the prepared data  
B. Ingest the raw data, split it first, fit transformation steps on the training set, apply the same steps to validation and test, then train and evaluate later  
C. Skip data preparation, train the model first, and use missing-value handling only if training fails  
D. Ingest the raw data, remove every row with any missing value, use IDs as features, and evaluate quality during preparation  

**Correct Answer(s):** B

**Explanation:**  
The correct plan is:
- **Get Raw Data Into the Pipeline = Data Ingestion**
- **Split Before Fitting Transformations = Avoid Leakage**
- **Fit Transformations on Training Data Only = Keep Evaluation Fair**
- **Apply the Same Transformations to Validation and Test = Stay Consistent**
- **Evaluate After Training = Not During Data Preparation**

**Why the Correct Answer Is Correct:**  
- **Data ingestion** is about getting raw data from sources such as files, databases, or logs into a usable dataset.  
- Splitting first helps prevent preparation steps from learning from validation and test data.  
- Fitting transformation steps on the **training set only** and then applying the same steps to validation and test helps keep evaluation realistic.  
- Model evaluation belongs later in the lifecycle, after training, using held-out data.  

**Why the Other Options Are Wrong:**  

**A. Ingest the raw data, prepare the full dataset, calculate evaluation metrics, and then train on the prepared data**  
Wrong because preparing the **full dataset before splitting** can leak information into validation and test data. It is also wrong to calculate evaluation metrics before training.  

**C. Skip data preparation, train the model first, and use missing-value handling only if training fails**  
Wrong because data preparation is part of building a usable training dataset. Missing values, duplicates, and incorrect types can reduce model quality or even break training.  

**D. Ingest the raw data, remove every row with any missing value, use IDs as features, and evaluate quality during preparation**  
Wrong because dropping every incomplete row can bias the dataset, IDs are usually unsafe features, and evaluation belongs after training rather than during preparation.  

**Tips and Tricks:**  
- **Get Raw Data In = Data Ingestion**  
- **Split First = Safer Preparation**  
- **Fit on Training Only = Avoid Leakage**  
- **Evaluate Later = After Training**

> [!IMPORTANT]  
> A common trap is treating data preparation as the place where you prove the model is good. It is not. Data preparation builds a reliable dataset; trustworthy performance checking happens later on held-out data.  

**Source:**  
- [Azure Machine Learning documentation](https://learn.microsoft.com/en-us/azure/machine-learning/?view=azureml-api-2)  
- [Build and train models with Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/concept-train-machine-learning-model?view=azureml-api-2)  
- [Clean Missing Data: Component Reference - Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/component-reference/clean-missing-data?view=azureml-api-2)  
- [Design training data for AI workloads on Azure](https://learn.microsoft.com/en-us/azure/well-architected/ai/training-data-design)  
