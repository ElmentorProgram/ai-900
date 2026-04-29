# Raw Practice Test 02

031. A team is building a machine learning solution to **forecast demand**. They agree on the target output and success metric, prepare the dataset, train several versions, compare them on held-out data, run one final unbiased check, and then deploy the chosen model while monitoring it in production.

     Which option best matches the correct end-to-end lifecycle flow?

     A. Define the problem → Train the model → Prepare the data → Evaluate on the test set during tuning → Deploy  
     B. Define the problem → Prepare data → Split data → Train → Evaluate and tune on validation data → Final test on unseen test data → Deploy and monitor  
     C. Prepare data → Deploy the model → Train on production traffic → Evaluate using the training set → Final test  
     D. Define the problem → Split columns → Train → Use the validation set as the final unbiased check → Deploy  


032. A team is preparing data for a supervised learning model. Their raw data comes from files and logs, some fields are missing, some rows are duplicated, and a few columns need type fixes and category encoding. They also want to avoid making validation and test results look better than real life.

     Which action plan is the most appropriate?

     A. Ingest the raw data, prepare the full dataset, calculate evaluation metrics, and then train on the prepared data  
     B. Ingest the raw data, split it first, fit transformation steps on the training set, apply the same steps to validation and test, then train and evaluate later  
     C. Skip data preparation, train the model first, and use missing-value handling only if training fails  
     D. Ingest the raw data, remove every row with any missing value, use IDs as features, and evaluate quality during preparation  


033. A team is building a model to predict **house sale price**. They start with fields such as **LivingAreaSqFt**, **Bedrooms**, **Neighborhood**, **YearBuilt**, and **SaleDate**. During preparation, they consider these changes:

     - Create **HouseAge** from SaleYear minus YearBuilt  
     - Convert **SaleDate** into **SaleMonth**  
     - Keep only the most useful input fields and drop weak or noisy ones  
     - Add **PricePerSqFt** using SalePrice divided by LivingAreaSqFt  

     Which statement is the most accurate?

     A. Creating **HouseAge** and **SaleMonth** is feature selection, while dropping weak fields is feature engineering  
     B. Creating **HouseAge** and **SaleMonth** is feature engineering, dropping weak fields is feature selection, and **PricePerSqFt** should not be used because it leaks the target  
     C. All four actions are feature engineering because they all change the dataset before training  
     D. **PricePerSqFt** is a strong feature because it uses the label directly, so it should be kept for better accuracy  


034. A team is building a model from a housing dataset. Each row represents one house sale. Available columns include **HouseID**, **LivingAreaSqFt**, **Bedrooms**, **Neighborhood**, and **SalePrice**. The team wants to predict sale price on future houses.

     Which statement is the most accurate?

     A. **HouseID** is a strong feature because unique identifiers help the model recognize each house, and **SalePrice** should also be included as an input to improve training  
     B. **LivingAreaSqFt**, **Bedrooms**, and **Neighborhood** are reasonable features, **SalePrice** is the label, and **HouseID** is usually not a safe feature because it can encourage memorization instead of generalization  
     C. **SalePrice** should be treated as a feature because it is numeric, and **Neighborhood** should be the label because it is categorical  
     D. This is an unsupervised learning problem because the dataset contains rows and columns, so no label is needed  


035. A team is building a fraud detection model. It trains on one part of the data, compares model versions by adjusting thresholds and hyperparameters on another part, and then runs one last check on a separate unseen subset after all decisions are finished.

     Which statement best describes the role of these three subsets?

     A. The training set is used to learn patterns, the validation set is used during development to compare and tune models, and the test set is the final unbiased check  
     B. The training set is used for learning, the test set is used during tuning, and the validation set is the final unbiased check  
     C. The validation set is used to fit the model, the training set is used to compare versions, and the test set is optional if accuracy already looks good  
     D. The training, validation, and test sets all serve the same purpose, so using any one of them for tuning or final evaluation is acceptable  


036. A team is preparing an ML dataset and debating how to split it for evaluation:

     - One engineer wants to split by **rows** so the model is tested on unseen examples  
     - Another wants to split by **columns** so some input fields are removed during evaluation  
     - A third wants to use a **random split** on time-ordered sales data  
     - A fourth says that if multiple rows belong to the same patient, those rows should stay in only one subset  

     Which statement is the most accurate?

     A. Splitting by columns is the standard way to test generalization, and random split is always safe even for time-ordered data  
     B. Splitting by rows is usually correct for evaluation, time-ordered data often needs a time-based split, and grouped records such as the same patient should stay in only one split  
     C. Random split should always be avoided, and grouped records should appear in every subset so the model sees enough examples  
     D. Splitting by columns is better than splitting by rows because it proves the model can handle unseen cases with less information  


037. A team trains a model and gets these results:

     - Training score is **very high**  
     - Validation score is **much lower**  
     - During development, the team keeps checking the **test set** after each change  
     - One feature uses information that is only known **after the real outcome happens**  

     Which statement is the most accurate?

     A. The model is underfitting, checking the test set repeatedly is fine, and using post-outcome information is acceptable if it improves accuracy  
     B. The model is overfitting, repeatedly checking the test set is peeking, and using post-outcome information is leakage  
     C. The model is generalizing well, the test set should guide tuning, and post-outcome information is a valid engineered feature  
     D. The model is underfitting, the validation set should be avoided, and leakage only happens when rows are duplicated  


038. A team is comparing two model options for the same task. One model is much larger and has many more parameters. The team discusses both the **training phase** and the **inference phase**.

     Which statement is the most accurate?

     A. More parameters mainly matter during training, but they usually do not affect inference latency, throughput, or cost  
     B. More parameters usually mean more work during training and more work during inference, so larger models often need more training resources and can also increase serving latency or cost  
     C. More parameters mainly reduce the amount of data and memory needed, because a larger model learns faster by default  
     D. Parameter count matters only for generative AI models, not for other machine learning models or production serving decisions  


039. A fraud detection team defines these success targets for its model on held-out data:

     - **Recall must be at least 0.80** to catch most fraud cases  
     - **Precision must be at least 0.20** to limit false alarms  

     After training, the team evaluates the model on the **validation set**. The model flags **500** transactions as fraud. Out of those, **50** are truly fraud. In the whole validation set, there are **100** real fraud cases.

     What should the team conclude?

     A. Precision = 0.50 and Recall = 0.10, so the model already meets both targets and should go straight to the final test set  
     B. Precision = 0.10 and Recall = 0.50, so the model misses both targets and the team should iterate using the validation set  
     C. Precision = 0.20 and Recall = 0.80, so the model exactly meets both targets and should be deployed immediately  
     D. Precision = 0.10 and Recall = 0.50, so the model should now be tuned by repeatedly checking the test set until the targets are met  


040. A manufacturing team is building a model to detect **defective products** before shipment. It sets these success targets for held-out data:

     - **Recall must be at least 0.90** so most defective items are caught  
     - **Precision must be at least 0.60** so too many good items are not sent for unnecessary reinspection  

     After training, the team evaluates the model on the **validation set**. The model flags **200** products as defective. Out of those, **140** are truly defective. In the whole validation set, there are **160** real defective products.

     What is the best conclusion?

     A. Precision = 0.70 and Recall = 0.875, so the model meets both targets and should move straight to deployment  
     B. Precision = 0.875 and Recall = 0.70, so the model misses both targets and should be retrained from scratch immediately  
     C. Precision = 0.70 and Recall = 0.875, so the model meets the precision target but misses the recall target, and the team should iterate on the validation set  
     D. Precision = 0.60 and Recall = 0.90, so the model exactly meets both targets and should now be tested by tuning on the test set  


041. A team improves its model’s validation score after tuning thresholds and features. One engineer says, “Great, iteration is only about getting a higher metric.” Another engineer disagrees and says iteration also helps reduce real-world risk before deployment.

     Which statement is the most accurate?

     A. Iteration is only for increasing the validation score. Once the score improves, stability and production behavior are separate concerns  
     B. Iteration is mainly for making the training score look stronger. Generalization matters less if the training performance is high  
     C. Iteration helps improve held-out performance, but it also helps check generalization, choose a more stable configuration, and reduce production surprises  
     D. Iteration and fine-tuning mean the same thing in all machine learning cases, so any model adjustment is best described as fine-tuning  


042. A team is preparing data for a supervised learning model. Its raw data comes from several files and systems, some records are duplicated, some numeric fields were imported as text, some categorical fields need encoding, and some rows contain missing values or unusual outlier values.

     Which action plan best fits the **data preparation** stage?

     A. Merge the datasets, remove duplicates, fix data types, standardize formats, handle missing values using a scenario-appropriate choice, deal with outliers, select relevant columns, and encode categorical values before training  
     B. Skip most preparation, train the model first, and only fix the data later if the training job fails  
     C. Use the test set to decide which preparation steps give the best score, then apply a different cleaned version of the data in production  
     D. Focus only on deployment format and endpoint design, because preparation is mainly about how the trained model will be called  


043. A team is preparing a dataset for supervised learning. It notices two issues:

     - Some rows are missing the **target label**  
     - Other rows are missing one or two **input feature values**  

     The team also sees that one important feature has many missing values, and removing every affected row would shrink the dataset so much that the remaining data may become biased.

     Which statement is the most accurate?

     A. Missing labels and missing feature values should always be handled the same way, so the team should impute both and keep all rows  
     B. Missing target labels are usually a bigger problem for supervised training, while missing feature values may sometimes be handled by imputation if dropping rows would bias the dataset  
     C. Missing feature values are always worse than missing labels, because the model can still learn the target from the rest of the row  
     D. The safest approach is always to remove every row with any missing value, because imputation always weakens the dataset  


044. A team is deciding how to split its dataset before training:

     - One engineer wants a **quick experiment** with only a training set and a final test set  
     - Another wants a more **disciplined tuning workflow** with separate training, validation, and test sets  
     - A third says the dataset is **large**, so giving more rows to evaluation could provide a stronger signal  
     - A fourth says that if the task is **imbalanced classification**, each split should keep a similar class ratio  

     Which option is the most appropriate?

     A. Quick experiment = **80/20** train/test, disciplined tuning = **70/15/15** train/validation/test, large dataset with stronger evaluation signal = **60/20/20**, and imbalanced classification should use a **stratified split**  
     B. Quick experiment = **60/20/20**, disciplined tuning = **80/20**, large dataset with stronger evaluation signal = **70/15/15**, and imbalanced classification should avoid stratification  
     C. Quick experiment = **70/15/15**, disciplined tuning = **60/20/20**, large dataset with stronger evaluation signal = **80/20**, and imbalanced classification should always use random split only  
     D. Quick experiment = **80/20**, disciplined tuning = **70/15/15**, large dataset with stronger evaluation signal = **60/20/20**, and imbalanced classification should be evaluated by splitting columns instead of rows  


045. A team has already trained a machine learning model and now wants to use it on **new incoming data** to generate outputs. One engineer calls this **inference**, while another calls it **scoring**.

     Which statement is the most accurate?

     A. Inference and scoring both refer to using a trained model on new data to generate outputs, while training is the earlier phase where the model learns from examples  
     B. Inference means tuning the model on validation data, while scoring means running the final unbiased test  
     C. Scoring is the same as data ingestion, because both happen before deployment  
     D. Inference only applies to classification models, while scoring only applies to regression models
