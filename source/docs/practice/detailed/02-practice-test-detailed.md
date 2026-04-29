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
