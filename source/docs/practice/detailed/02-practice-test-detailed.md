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

**Question:** [033]  
A team is building a model to predict **house sale price**. They start with fields such as **LivingAreaSqFt**, **Bedrooms**, **Neighborhood**, **YearBuilt**, and **SaleDate**. During preparation, they consider these changes:

- Create **HouseAge** from SaleYear minus YearBuilt  
- Convert **SaleDate** into **SaleMonth**  
- Keep only the most useful input fields and drop weak or noisy ones  
- Add **PricePerSqFt** using SalePrice divided by LivingAreaSqFt  

Which statement is the most accurate?

**Options:**  
A. Creating **HouseAge** and **SaleMonth** is feature selection, while dropping weak fields is feature engineering  
B. Creating **HouseAge** and **SaleMonth** is feature engineering, dropping weak fields is feature selection, and **PricePerSqFt** should not be used because it leaks the target  
C. All four actions are feature engineering because they all change the dataset before training  
D. **PricePerSqFt** is a strong feature because it uses the label directly, so it should be kept for better accuracy  

**Correct Answer(s):** B

**Explanation:**  
The correct idea is:
- **Create or Transform Inputs = Feature Engineering**
- **Choose Which Inputs to Keep = Feature Selection**
- **Use Only Information Available at Prediction Time = Safe Feature**
- **Use the Target Inside a Feature = Leakage**

**Why the Correct Answer Is Correct:**  
- Creating **HouseAge** and **SaleMonth** means transforming raw fields into more useful signals. That is **feature engineering**. Microsoft describes featurization and feature engineering as transforming data into features that help models learn better.  
- Dropping weak or noisy fields is **feature selection** because you are choosing which inputs to keep. Microsoft documentation describes feature selection as identifying the most useful predictive features.  
- **PricePerSqFt** uses **SalePrice**, which is the label being predicted. That makes it unsafe because it uses information that would not be available at prediction time. Microsoft describes this as data leakage or target leakage.  

**Why the Other Options Are Wrong:**  

**A. Creating HouseAge and SaleMonth is feature selection, while dropping weak fields is feature engineering**  
Wrong because it reverses the definitions. Creating new or transformed inputs is **feature engineering**, while choosing which existing inputs to keep is **feature selection**.  

**C. All four actions are feature engineering because they all change the dataset before training**  
Wrong because **feature selection** is different from feature engineering, and using the target inside a feature is not a valid preparation step. It creates leakage.  

**D. PricePerSqFt is a strong feature because it uses the label directly, so it should be kept for better accuracy**  
Wrong because using the label directly can make evaluation look better than real life, but the model would not have that information at prediction time. That is leakage, not good feature design.  

**Tips and Tricks:**  
- **Create New Signals = Feature Engineering**  
- **Choose Which Features Stay = Feature Selection**  
- **Known Only After Outcome = Leakage**  
- **Safe Feature = Available at Prediction Time**

> [!IMPORTANT]  
> A common pitfall is engineering a feature using information you would not know at prediction time. That creates leakage, even if the feature looks helpful.

**Source:**  
- [Filter Based Feature Selection: Component reference - Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/component-reference/filter-based-feature-selection?view=azureml-api-2)  
- [Data Featurization in Automated Machine Learning - Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-configure-auto-features?view=azureml-api-1)  
- [Offline feature retrieval using a point-in-time join - Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/offline-retrieval-point-in-time-join-concepts?view=azureml-api-2)  
- [Design training data for AI workloads on Azure](https://learn.microsoft.com/en-us/azure/well-architected/ai/training-data-design)  

**Question:** [034]  
A team is building a model from a housing dataset. Each row represents one house sale. Available columns include **HouseID**, **LivingAreaSqFt**, **Bedrooms**, **Neighborhood**, and **SalePrice**. The team wants to predict sale price on future houses.

Which statement is the most accurate?

**Options:**  
A. **HouseID** is a strong feature because unique identifiers help the model recognize each house, and **SalePrice** should also be included as an input to improve training  
B. **LivingAreaSqFt**, **Bedrooms**, and **Neighborhood** are reasonable features, **SalePrice** is the label, and **HouseID** is usually not a safe feature because it can encourage memorization instead of generalization  
C. **SalePrice** should be treated as a feature because it is numeric, and **Neighborhood** should be the label because it is categorical  
D. This is an unsupervised learning problem because the dataset contains rows and columns, so no label is needed  

**Correct Answer(s):** B

**Explanation:**  
The correct idea is:
- **Features are the inputs the model uses**
- **The label is the value the model is trying to predict**
- **IDs are usually unsafe features**
- **If you have a known target, this is supervised learning**

**Why the Correct Answer Is Correct:**  
- **LivingAreaSqFt**, **Bedrooms**, and **Neighborhood** are reasonable candidate features because they can be known at prediction time and may help explain price.  
- **SalePrice** is the **label** because it is the target the model is trying to predict.  
- **HouseID** is usually not a good feature because identifiers often let the model memorize records instead of learning patterns that generalize.  
- Because the dataset has a known target column, this is a **supervised learning** setup, not clustering.  

**Why the Other Options Are Wrong:**  

**A. HouseID is a strong feature because unique identifiers help the model recognize each house, and SalePrice should also be included as an input to improve training**  
Wrong because IDs usually encourage memorization rather than generalization, and using the target itself as an input is leakage.  

**C. SalePrice should be treated as a feature because it is numeric, and Neighborhood should be the label because it is categorical**  
Wrong because numeric does not automatically mean feature, and categorical does not automatically mean label. The label is the field you want to predict. Here, the team wants to predict **SalePrice**, so **SalePrice** is the label.  

**D. This is an unsupervised learning problem because the dataset contains rows and columns, so no label is needed**  
Wrong because the presence of a known target to predict makes this a **supervised** problem. Microsoft’s clustering guidance describes clustering as **unsupervised** and based on unlabeled data.  

**Tips and Tricks:**  
- First ask: **What am I trying to predict?** That field is usually the **label**.  
- Then ask: **What will I still know at prediction time?** Those fields are the safer **feature** candidates.  
- Be suspicious of **IDs** and of any field that directly reveals the answer.

> [!IMPORTANT]  
> A simple rule: if you will not know it at prediction time, it is not a safe feature, even if it makes the metrics look better.  

**Source:**  
- [How to select a machine learning algorithm](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-select-algorithms?view=azureml-api-1)  
- [Train Clustering Model: Component Reference - Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/component-reference/train-clustering-model?view=azureml-api-2)  
- [Offline feature retrieval using a point-in-time join - Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/offline-retrieval-point-in-time-join-concepts?view=azureml-api-2)  
- [What is automated ML? AutoML - Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/concept-automated-ml?view=azureml-api-2)  


**Question:** [035]  
A team is building a fraud detection model. It trains on one part of the data, compares model versions by adjusting thresholds and hyperparameters on another part, and then runs one last check on a separate unseen subset after all decisions are finished.

Which statement best describes the role of these three subsets?

**Options:**  
A. The training set is used to learn patterns, the validation set is used during development to compare and tune models, and the test set is the final unbiased check  
B. The training set is used for learning, the test set is used during tuning, and the validation set is the final unbiased check  
C. The validation set is used to fit the model, the training set is used to compare versions, and the test set is optional if accuracy already looks good  
D. The training, validation, and test sets all serve the same purpose, so using any one of them for tuning or final evaluation is acceptable  

**Correct Answer(s):** A

**Explanation:**  
The correct role split is:
- **Training Set = Learn Patterns**
- **Validation Set = Compare and Tune During Development**
- **Test Set = Final Unbiased Check**

**Why the Correct Answer Is Correct:**  
- The **training set** is the subset the model learns from. Azure Machine Learning documentation describes training data as the data used to fit the model.  
- The **validation set** is used during development to compare model versions and tune settings such as thresholds or hyperparameters.  
- The **test set** is kept separate until the end so it remains an unbiased final check on unseen data.  

**Why the Other Options Are Wrong:**  

**B. The training set is used for learning, the test set is used during tuning, and the validation set is the final unbiased check**  
Wrong because this swaps **validation** and **test**. Once you use the **test set** during tuning, it is no longer a trustworthy final check.  

**C. The validation set is used to fit the model, the training set is used to compare versions, and the test set is optional if accuracy already looks good**  
Wrong because the **training set** is used to fit the model, not the validation set. It is also wrong to treat the **test set** as optional when you need a final unbiased evaluation on unseen data.  

**D. The training, validation, and test sets all serve the same purpose, so using any one of them for tuning or final evaluation is acceptable**  
Wrong because these subsets have different roles. Mixing them weakens the reliability of evaluation and can hide overfitting.  

**Tips and Tricks:**  
- Ask yourself **when** the subset is used. If it is used **during model improvement**, that is usually **validation**.  
- If it is the subset kept untouched until everything is finalized, that is the **test set**.  
- A strong exam shortcut is: **Train = Learn, Validation = Tune, Test = Final Check**.

> [!IMPORTANT]  
> A common trap is mixing **validation** and **test**. Use **validation** during iteration, and keep the **test set** untouched until the end so it remains a trustworthy final check.

**Source:**  
- [Data splits and cross-validation in automated machine learning](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-configure-cross-validation-data-splits?view=azureml-api-1)  
- [Prevent overfitting and imbalanced data with automated ML](https://learn.microsoft.com/en-us/azure/machine-learning/concept-manage-ml-pitfalls?view=azureml-api-2)  
- [Build and train models with Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/concept-train-machine-learning-model?view=azureml-api-2)  

**Question:** [036]  
A team is preparing an ML dataset and debating how to split it for evaluation:

- One engineer wants to split by **rows** so the model is tested on unseen examples  
- Another wants to split by **columns** so some input fields are removed during evaluation  
- A third wants to use a **random split** on time-ordered sales data  
- A fourth says that if multiple rows belong to the same patient, those rows should stay in only one subset  

Which statement is the most accurate?

**Options:**  
A. Splitting by columns is the standard way to test generalization, and random split is always safe even for time-ordered data  
B. Splitting by rows is usually correct for evaluation, time-ordered data often needs a time-based split, and grouped records such as the same patient should stay in only one split  
C. Random split should always be avoided, and grouped records should appear in every subset so the model sees enough examples  
D. Splitting by columns is better than splitting by rows because it proves the model can handle unseen cases with less information  

**Correct Answer(s):** B

**Explanation:**  
The correct idea is:
- **Generalization Is Tested by Holding Out Rows**
- **Splitting by Columns Changes the Problem**
- **Time-Ordered Data Often Needs Past-to-Future Splitting**
- **Grouped Records Should Stay in One Split to Avoid Leakage**

**Why the Correct Answer Is Correct:**  
- **Splitting by rows** is the usual evaluation method because it tests performance on **new examples** the model did not train on. Azure ML split guidance focuses on dividing data into subsets for training and evaluation.  
- **Splitting by columns** does not answer the main evaluation question. It changes the task into whether the model can work with fewer inputs, not whether it can generalize to new cases.  
- For **time-ordered data**, random split is often not the best choice. A past-to-future split better matches real deployment.  
- If multiple rows belong to the same **patient, user, or device**, keeping that group in one split helps avoid leakage and unrealistic evaluation.

**Why the Other Options Are Wrong:**  

**A. Splitting by columns is the standard way to test generalization, and random split is always safe even for time-ordered data**  
Wrong because generalization is usually tested by holding out **rows**, not columns. It is also unsafe to assume random split is always appropriate for time-ordered data.  

**C. Random split should always be avoided, and grouped records should appear in every subset so the model sees enough examples**  
Wrong because **random split** is still a common default when rows are independent. It is also wrong to spread grouped records across subsets when that can leak identity patterns.  

**D. Splitting by columns is better than splitting by rows because it proves the model can handle unseen cases with less information**  
Wrong because removing columns changes the information available, but it does not simulate evaluation on **new cases**. That is a different question from generalization.  

**Tips and Tricks:**  
- When the goal is **generalization**, think about **new rows**, not missing columns.  
- If the data has a real **time order**, ask whether evaluation should mimic the future instead of a random shuffle.  
- If several rows belong to the same real-world entity, be alert for **identity leakage** across splits.

> [!IMPORTANT]  
> A common trap is using the wrong split pattern for the data shape. **Rows** are usually held out to test generalization, **time-based split** is safer for time-ordered data, and **group-based split** is safer when multiple rows belong to the same person, device, or patient.

**Source:**  
- [Split Data: Component reference - Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/component-reference/split-data?view=azureml-api-2)  
- [Data splits and cross-validation in automated machine learning](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-configure-cross-validation-data-splits?view=azureml-api-1)  
- [Set up AutoML for time-series forecasting - Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-auto-train-forecast?view=azureml-api-2)  
- [Build & train models - Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/concept-train-machine-learning-model?view=azureml-api-2)  

**Question:** [037]  
A team trains a model and gets these results:

- Training score is **very high**
- Validation score is **much lower**
- During development, the team keeps checking the **test set** after each change
- One feature uses information that is only known **after the real outcome happens**

Which statement is the most accurate?

**Options:**  
A. The model is underfitting, checking the test set repeatedly is fine, and using post-outcome information is acceptable if it improves accuracy  
B. The model is overfitting, repeatedly checking the test set is peeking, and using post-outcome information is leakage  
C. The model is generalizing well, the test set should guide tuning, and post-outcome information is a valid engineered feature  
D. The model is underfitting, the validation set should be avoided, and leakage only happens when rows are duplicated  

**Correct Answer(s):** B

**Explanation:**  
The correct idea is:
- **High Training Score + Much Lower Validation Score = Overfitting**
- **Using the Test Set During Tuning = Peeking**
- **Using Information Not Available at Prediction Time = Leakage**

**Why the Correct Answer Is Correct:**  
- A model that performs very well on training data but drops on validation data is showing **overfitting**. Microsoft describes overfitting as fitting the training data too well and then failing to predict unseen data accurately.  
- Repeatedly checking the **test set** during model changes turns it into part of the development loop, so it no longer serves as a trustworthy final check. Microsoft’s data-split guidance separates tuning-time data from final evaluation data.  
- Using a feature that is only known **after** the outcome happens is **leakage** because that information would not exist at real prediction time. Microsoft warns that leakage can make performance look unrealistically strong.  

**Why the Other Options Are Wrong:**  

**A. The model is underfitting, checking the test set repeatedly is fine, and using post-outcome information is acceptable if it improves accuracy**  
Wrong because the pattern described is **overfitting**, not underfitting. It is also wrong to use the **test set** repeatedly during tuning, and wrong to use post-outcome information as a feature.  

**C. The model is generalizing well, the test set should guide tuning, and post-outcome information is a valid engineered feature**  
Wrong because a large gap between training and validation performance is evidence against good generalization. The **test set** should not guide tuning, and post-outcome information is leakage, not valid feature engineering.  

**D. The model is underfitting, the validation set should be avoided, and leakage only happens when rows are duplicated**  
Wrong because underfitting usually means weak performance on both training and validation data. The **validation set** is useful during development, and leakage is broader than duplication.  

**Tips and Tricks:**  
- If **training looks great** but **validation drops**, suspect **memorization**, not success.  
- If a field is only known **after the outcome**, treat it as unsafe immediately.  
- If you are still making model decisions, you are not ready to touch the **test set**.

> [!IMPORTANT]  
> Leakage and peeking can make a model look better than it really is. Keep answer-revealing information out of features, and keep the **test set** untouched until the end so your final score stays trustworthy.  

**Source:**  
- [Prevent overfitting and imbalanced data with automated ML](https://learn.microsoft.com/en-us/azure/machine-learning/concept-manage-ml-pitfalls?view=azureml-api-2)  
- [Data splits and cross-validation in automated machine learning](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-configure-cross-validation-data-splits?view=azureml-api-1)  
- [Frequently asked questions about forecasting in automated ML](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-automl-forecasting-faq?view=azureml-api-2)  
- [Build and train models with Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/concept-train-machine-learning-model?view=azureml-api-2)  

**Question:** [038]  
A team is comparing two model options for the same task. One model is much larger and has many more parameters. The team discusses both the **training phase** and the **inference phase**.

Which statement is the most accurate?

**Options:**  
A. More parameters mainly matter during training, but they usually do not affect inference latency, throughput, or cost  
B. More parameters usually mean more work during training and more work during inference, so larger models often need more training resources and can also increase serving latency or cost  
C. More parameters mainly reduce the amount of data and memory needed, because a larger model learns faster by default  
D. Parameter count matters only for generative AI models, not for other machine learning models or production serving decisions  

**Correct Answer(s):** B

**Explanation:**  
The correct idea is:
- **More Parameters Increase Training Work**
- **More Parameters Also Affect Inference Serving**
- **Larger Models Usually Cost More to Build and Run**

**Why the Correct Answer Is Correct:**  
- During **training**, a larger model generally means more values must be updated, which increases compute and memory demands. Microsoft guidance on AI infrastructure says hardware selection should match **model complexity**, **data size**, and **training needs**.  
- During **inference**, the compute target and serving setup affect cost and availability, and Microsoft’s Azure OpenAI performance guidance explicitly discusses **latency** and **throughput** as key serving concerns.  
- For language models in particular, inference cost and performance also depend on factors such as **input size**, **output size**, and throughput limits.  

**Why the Other Options Are Wrong:**  

**A. More parameters mainly matter during training, but they usually do not affect inference latency, throughput, or cost**  
Wrong because serving and inference performance are influenced by model size and deployment characteristics. Microsoft documentation explicitly treats **latency**, **throughput**, and inference compute targets as important production concerns.  

**C. More parameters mainly reduce the amount of data and memory needed, because a larger model learns faster by default**  
Wrong because Microsoft guidance points the other way: larger and more complex workloads usually require more suitable compute planning, not less memory or less compute by default.  

**D. Parameter count matters only for generative AI models, not for other machine learning models or production serving decisions**  
Wrong because compute planning for training and inference is a broader ML and AI deployment concern, not something limited only to generative models. Microsoft’s Azure ML and Azure infrastructure guidance discusses training and inference compute more generally.  

**Tips and Tricks:**  
- If the question mentions **model size**, do not think only about training time. Also think about **serving impact** later.  
- A larger model can create pressure in two places: **while learning** and **while answering requests**.  
- For inference questions, watch for words like **latency**, **throughput**, **endpoint**, and **cost per request**.

> [!IMPORTANT]  
> A common mistake is to think compute sizing matters only during training. It matters in **both** phases: training affects build cost and time, while inference affects production latency, throughput, and serving cost.  

**Source:**  
- [Compute recommendations for AI workloads on Azure infrastructure](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ai/infrastructure/compute)  
- [Understand compute targets in Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/concept-compute-target?view=azureml-api-2)  
- [Azure OpenAI in Microsoft Foundry Models performance and latency](https://learn.microsoft.com/en-us/azure/foundry/openai/how-to/latency)  
- [Azure OpenAI in Microsoft Foundry Models quotas and limits](https://learn.microsoft.com/en-us/azure/foundry/openai/quotas-limits)  

**Question:** [039]  
A fraud detection team defines these success targets for its model on held-out data:

- **Recall must be at least 0.80** to catch most fraud cases  
- **Precision must be at least 0.20** to limit false alarms  

After training, the team evaluates the model on the **validation set**. The model flags **500** transactions as fraud. Out of those, **50** are truly fraud. In the whole validation set, there are **100** real fraud cases.

What should the team conclude?

**Options:**  
A. Precision = 0.50 and Recall = 0.10, so the model already meets both targets and should go straight to the final test set  
B. Precision = 0.10 and Recall = 0.50, so the model misses both targets and the team should iterate using the validation set  
C. Precision = 0.20 and Recall = 0.80, so the model exactly meets both targets and should be deployed immediately  
D. Precision = 0.10 and Recall = 0.50, so the model should now be tuned by repeatedly checking the test set until the targets are met  

**Correct Answer(s):** B

**Explanation:**  
The correct result is:
- **Precision = 50 / 500 = 0.10**
- **Recall = 50 / 100 = 0.50**
- **Both Targets Are Missed**
- **Next Step = Iterate on the Validation Set**

**Why the Correct Answer Is Correct:**  
- **Precision** measures how many predicted positives were actually correct. Microsoft defines precision as the ratio of correctly identified positives to all identified positives. Here that is **50 / 500 = 0.10**.  
- **Recall** measures how many actual positives the model successfully found. Here that is **50 / 100 = 0.50**.  
- The targets were **precision ≥ 0.20** and **recall ≥ 0.80**, so this model misses both targets.  
- Because this is still the development stage, the team should iterate using the **validation set** by adjusting thresholds, features, or model choices. The **test set** should remain a final unbiased check.  

**Why the Other Options Are Wrong:**  

**A. Precision = 0.50 and Recall = 0.10, so the model already meets both targets and should go straight to the final test set**  
Wrong because the calculations are reversed. Precision is **50 / 500 = 0.10**, not 0.50, and recall is **50 / 100 = 0.50**, not 0.10. It also does not meet either target.  

**C. Precision = 0.20 and Recall = 0.80, so the model exactly meets both targets and should be deployed immediately**  
Wrong because those numbers are the **target thresholds**, not the actual results from the validation set. The actual results are much lower.  

**D. Precision = 0.10 and Recall = 0.50, so the model should now be tuned by repeatedly checking the test set until the targets are met**  
Wrong because although the calculations are correct, the action is wrong. The team should iterate on the **validation set**, not keep checking the **test set**, because the test set is supposed to remain the final unbiased check.  

**Tips and Tricks:**  
- When you see counts, calculate **precision** from **predicted positives** and **recall** from **actual positives**.  
- Do not confuse **target thresholds** with **measured results**.  
- If the model misses the target during development, that means **iterate on validation**, not **peek at test**.

> [!IMPORTANT]  
> A common trap is doing the math correctly but taking the wrong next step. Missing the target on the **validation set** means you should keep iterating there. The **test set** is only for the final unbiased confirmation after changes stop.  

**Source:**  
- [Evaluate AutoML experiment results - Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-understand-automated-ml?view=azureml-api-2)  
- [Data splits and cross-validation in automated machine learning](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-configure-cross-validation-data-splits?view=azureml-api-1)  
- [Custom text classification evaluation metrics - Foundry Tools](https://learn.microsoft.com/en-us/azure/ai-services/language-service/custom-text-classification/concepts/evaluation-metrics)  
- [Prevent overfitting and imbalanced data with automated ML](https://learn.microsoft.com/en-us/azure/machine-learning/concept-manage-ml-pitfalls?view=azureml-api-2)  

**Question:** [040]  
A manufacturing team is building a model to detect **defective products** before shipment. It sets these success targets for held-out data:

- **Recall must be at least 0.90** so most defective items are caught  
- **Precision must be at least 0.60** so too many good items are not sent for unnecessary reinspection  

After training, the team evaluates the model on the **validation set**. The model flags **200** products as defective. Out of those, **140** are truly defective. In the whole validation set, there are **160** real defective products.

What is the best conclusion?

**Options:**  
A. Precision = 0.70 and Recall = 0.875, so the model meets both targets and should move straight to deployment  
B. Precision = 0.875 and Recall = 0.70, so the model misses both targets and should be retrained from scratch immediately  
C. Precision = 0.70 and Recall = 0.875, so the model meets the precision target but misses the recall target, and the team should iterate on the validation set  
D. Precision = 0.60 and Recall = 0.90, so the model exactly meets both targets and should now be tested by tuning on the test set  

**Correct Answer(s):** C

**Explanation:**  
The correct result is:
- **Precision = 140 / 200 = 0.70**
- **Recall = 140 / 160 = 0.875**
- **Precision Target Is Met**
- **Recall Target Is Missed**
- **Next Step = Iterate on the Validation Set**

**Why the Correct Answer Is Correct:**  
- **Precision** is the ratio of correct positive predictions to all positive predictions. Here that is **140 / 200 = 0.70**.  
- **Recall** is the ratio of correct positive predictions to all actual positives. Here that is **140 / 160 = 0.875**.  
- The model **meets** the precision target of **0.60** but **misses** the recall target of **0.90**, so it is not ready for a final test yet.  
- During development, the team should keep iterating on the **validation set** by adjusting thresholds, features, or model settings. The **test set** should remain the final unbiased check after model decisions stop.  

**Why the Other Options Are Wrong:**  

**A. Precision = 0.70 and Recall = 0.875, so the model meets both targets and should move straight to deployment**  
Wrong because the calculations are correct, but the conclusion is wrong. The model still **misses the recall target** of **0.90**.  

**B. Precision = 0.875 and Recall = 0.70, so the model misses both targets and should be retrained from scratch immediately**  
Wrong because the calculations are reversed. Precision comes from **predicted positives**, while recall comes from **actual positives**. It is also too strong to conclude that the only next step is retraining from scratch. Iteration can include threshold changes, feature updates, or hyperparameter tuning.  

**D. Precision = 0.60 and Recall = 0.90, so the model exactly meets both targets and should now be tested by tuning on the test set**  
Wrong because those are the **target thresholds**, not the measured results. It is also wrong to use the **test set** for tuning.  

**Tips and Tricks:**  
- First calculate the metrics from the counts. Only after that should you compare them to the target thresholds.  
- A model is **not ready** just because one metric looks good. Check whether **all required targets** were met.  
- If development decisions are still being made, stay on the **validation set**.

> [!IMPORTANT]  
> Another common trap is meeting **one** target and assuming the model is ready. In practice, you compare the validation results against **all required success targets**, and you keep iterating until the full target condition is satisfied.  

**Source:**  
- [Evaluate AutoML experiment results - Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-understand-automated-ml?view=azureml-api-2)  
- [Data splits and cross-validation in automated machine learning](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-configure-cross-validation-data-splits?view=azureml-api-1)  
- [Custom text classification evaluation metrics - Foundry Tools](https://learn.microsoft.com/en-us/azure/ai-services/language-service/custom-text-classification/concepts/evaluation-metrics)  
- [Hyperparameter tuning a model (v2) - Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-tune-hyperparameters?view=azureml-api-2)  

**Question:** [041]  
A team improves its model’s validation score after tuning thresholds and features. One engineer says, “Great, iteration is only about getting a higher metric.” Another engineer disagrees and says iteration also helps reduce real-world risk before deployment.

Which statement is the most accurate?

**Options:**  
A. Iteration is only for increasing the validation score. Once the score improves, stability and production behavior are separate concerns  
B. Iteration is mainly for making the training score look stronger. Generalization matters less if the training performance is high  
C. Iteration helps improve held-out performance, but it also helps check generalization, choose a more stable configuration, and reduce production surprises  
D. Iteration and fine-tuning mean the same thing in all machine learning cases, so any model adjustment is best described as fine-tuning  

**Correct Answer(s):** C

**Explanation:**  
The correct idea is:
- **Iteration Is Not Only About a Better Score**
- **Iteration Also Tests Generalization**
- **Iteration Helps Find a More Stable Setup**
- **Iteration Reduces Production Surprises**

**Why the Correct Answer Is Correct:**  
- Iteration is used to improve results on held-out data, but that is not the whole story. The real goal is a model that works well on **new, unseen inputs**, not just one that looks good on a development score. Azure ML guidance on ML pitfalls emphasizes generalization and avoiding overfitting.  
- Iteration also helps the team choose a configuration that stays reliable when conditions shift slightly, which is part of building a more stable solution before deployment. Microsoft’s production monitoring guidance also reinforces that models can drift over time, so reducing surprises before deployment matters.  
- During iteration, teams may adjust thresholds, features, models, or hyperparameters. That is usually described as **tuning** or **iteration** in classic ML, not automatically **fine-tuning**. Fine-tuning is a more specific term, commonly used for adapting a pre-trained model with additional training.  

**Why the Other Options Are Wrong:**  

**A. Iteration is only for increasing the validation score. Once the score improves, stability and production behavior are separate concerns**  
Wrong because iteration is not just about pushing one metric upward. It also helps reveal whether the model generalizes, behaves consistently, and is less likely to create surprises later in production.  

**B. Iteration is mainly for making the training score look stronger. Generalization matters less if the training performance is high**  
Wrong because strong **training** performance alone is not trustworthy. Microsoft’s guidance on overfitting warns that a model can perform well on training data and still fail on unseen data.  

**D. Iteration and fine-tuning mean the same thing in all machine learning cases, so any model adjustment is best described as fine-tuning**  
Wrong because **fine-tuning** is a narrower term. In many classic ML workflows, teams say **train**, **tune**, or **iterate** rather than fine-tune.  

**Tips and Tricks:**  
- A better validation score is important, but ask one more question: **Will this still work on real future data?**  
- Be careful when a choice improves one score but makes the system more fragile or less trustworthy.  
- In classic ML, think **iterate / tune** first. Use **fine-tuning** only when the context truly fits that term.

> [!IMPORTANT]  
> A common trap is reducing iteration to “make the number bigger.” The stronger goal is to improve the model in a way that also supports **generalization**, **stability**, and safer behavior in production.  

**Source:**  
- [Prevent overfitting and imbalanced data with automated ML](https://learn.microsoft.com/en-us/azure/machine-learning/concept-manage-ml-pitfalls?view=azureml-api-2)  
- [Model monitoring in production - Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/concept-model-monitoring?view=azureml-api-2)  
- [Hyperparameter tuning a model (v2) - Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-tune-hyperparameters?view=azureml-api-2)  
- [Build and train models with Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/concept-train-machine-learning-model?view=azureml-api-2)  
