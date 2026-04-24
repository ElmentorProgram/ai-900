# Detailed Practice Test 01 - Answer Sheet & Explanation

**Question:** [001]  
A company wants a system that can review past sales data, learn patterns from it, and then predict future sales results. Which term best describes this?

**Options:**  
A. Artificial Intelligence  
B. Machine Learning  
C. Deep Learning  
D. Generative AI

**Correct Answer(s):** B

**Explanation:**  
This is **Machine Learning** because the system learns patterns from historical data and uses those learned patterns to predict future results. Machine learning is a way to build AI by learning from data rather than relying only on fixed rules.

**Why the Correct Answer Is Correct:**  
- Machine Learning is a branch of AI where models learn patterns from data.  
- The scenario focuses on learning from past sales data.  
- The goal is prediction, which is a core ML use case.

**Why the Other Options Are Wrong:**  

**A. Artificial Intelligence**  
Wrong because AI is the broader umbrella term. The question asks for the more specific term that describes learning patterns from data to make predictions.

**C. Deep Learning**  
Wrong because deep learning is a more specific neural-network approach inside machine learning. The scenario does not mention neural networks or the kind of complexity that would justify choosing deep learning over ML.

**D. Generative AI**  
Wrong because generative AI focuses on generating new content such as text, images, or code. This scenario is about prediction from historical data, not content generation.

**Tips and Tricks:**  
- If the stem says **learn from data** and **predict**, think **Machine Learning**.  
- Do not choose the umbrella term when a more precise term fits.  
- Do not confuse **prediction** with **generation**.

> [!IMPORTANT]  
> **AI** is the umbrella. **Machine Learning** is one way to build AI by learning patterns from data.

**Source:**  
- [A guide to artificial intelligence](https://learn.microsoft.com/en-us/training/modules/a-guide-to-artificial-intelligence/)  
- [Introduction to machine learning concepts](https://learn.microsoft.com/en-us/training/modules/fundamentals-machine-learning/)  
- [What is Azure Machine Learning?](https://learn.microsoft.com/en-us/azure/machine-learning/overview-what-is-azure-machine-learning?view=azureml-api-2)  
- [Key concepts and considerations in generative AI](https://learn.microsoft.com/en-us/azure/developer/ai/gen-ai-concepts-considerations-developers)  


**Question:** [002]  
A dataset contains input columns and a target column called **Fraud = Yes/No**. What does the target column represent?

**Options:**  
A. Features  
B. Labels  
C. Parameters  
D. Tokens

**Correct Answer(s):** B

**Explanation:**  
The target column represents the **label** because it is the known output the model is trying to learn and predict. In supervised learning, labels are the correct answers provided during training.

**Why the Correct Answer Is Correct:**  
- Labels are the target outputs in supervised learning.  
- **Fraud = Yes/No** is the known outcome column.  
- The model uses input features to learn how to predict that target.

**Why the Other Options Are Wrong:**  

**A. Features**  
Wrong because features are the input signals used by the model, not the output it is trying to predict.

**C. Parameters**  
Wrong because parameters are the learned internal weights of the model, not dataset columns such as **Fraud = Yes/No**.

**D. Tokens**  
Wrong because tokens are chunks of text processed by language models. They are unrelated to a target column in a supervised learning dataset.

**Tips and Tricks:**  
- If the question points to the **known result** or **target column**, think **label**.  
- Features are inputs. Labels are outputs.  
- Do not confuse dataset columns with internal model components.

> [!IMPORTANT]  
> In supervised learning, the presence of a known target column is one of the clearest signs that the dataset contains **labels**.

**Source:**  
- [Introduction to machine learning concepts](https://learn.microsoft.com/en-us/training/modules/fundamentals-machine-learning/)  
- [A guide to artificial intelligence](https://learn.microsoft.com/en-us/training/modules/a-guide-to-artificial-intelligence/)  
- [What is Machine Learning?](https://learn.microsoft.com/en-us/shows/azure-for-academics/what-is-machine-learning-9-of-19)  
- [Key concepts and considerations in generative AI](https://learn.microsoft.com/en-us/azure/developer/ai/gen-ai-concepts-considerations-developers)  


**Question:** [003]  
Which statement best describes the difference between **features** and **labels**?

**Options:**  
A. Features are the predictions made by the model, while labels are the raw inputs  
B. Features are the input signals used for learning, while labels are the target outputs  
C. Features are the internal weights of the model, while labels are user prompts  
D. Features are chunks of text, while labels are semantic vectors

**Correct Answer(s):** B

**Explanation:**  
**Features** are the inputs the model uses to learn patterns, while **labels** are the outputs the model is trying to predict. This input-to-target structure is central to supervised learning.

**Why the Correct Answer Is Correct:**  
- Features provide the signal the model learns from.  
- Labels provide the correct target answer during supervised learning.  
- This relationship is the basis of many prediction tasks in ML.

**Why the Other Options Are Wrong:**  

**A. Features are the predictions made by the model, while labels are the raw inputs**  
Wrong because this reverses the definitions. Features are inputs, while predictions and labels relate to outputs.

**C. Features are the internal weights of the model, while labels are user prompts**  
Wrong because internal weights are **parameters**, not features, and user prompts are not labels in ML datasets.

**D. Features are chunks of text, while labels are semantic vectors**  
Wrong because chunks of text are **tokens**, and semantic vectors are associated with **embeddings**. Those are different concepts from features and labels.

**Tips and Tricks:**  
- Think of **features = what goes in** and **labels = what should come out**.  
- Watch for options that swap the two definitions.  
- If the model is learning from examples with correct answers, features and labels usually appear together.

> [!IMPORTANT]  
> A very common trap is reversal: the exam may swap **input** and **target** to see whether you truly know the difference between features and labels.

**Source:**  
- [Introduction to machine learning concepts](https://learn.microsoft.com/en-us/training/modules/fundamentals-machine-learning/)  
- [A guide to artificial intelligence](https://learn.microsoft.com/en-us/training/modules/a-guide-to-artificial-intelligence/)  
- [How to generate embeddings with Azure OpenAI](https://learn.microsoft.com/en-us/azure/foundry/openai/how-to/embeddings)  
- [Prompt engineering techniques](https://learn.microsoft.com/en-us/azure/foundry/openai/concepts/prompt-engineering)  


**Question:** [004]  
Which statement best describes the difference between **training** and **inference**?

**Options:**  
A. Training is when a model learns from data, while inference is when the trained model makes predictions on new inputs  
B. Training is when a trained model responds to new inputs, while inference is when it learns from labeled data  
C. Training is the process of grouping similar items, while inference is the process of assigning labels  
D. Training and inference are two names for the same phase

**Correct Answer(s):** A

**Explanation:**  
**Training** is the phase where the model learns patterns from data. **Inference** is the phase where the trained model is used to make predictions on new inputs. This distinction applies broadly across machine learning systems.

**Why the Correct Answer Is Correct:**  
- During training, the model learns from examples and adjusts itself based on data.  
- During inference, the model is already trained and is being used to produce outputs for new inputs.  
- This is one of the most basic operational distinctions in ML.

**Why the Other Options Are Wrong:**  

**B. Training is when a trained model responds to new inputs, while inference is when it learns from labeled data**  
Wrong because it reverses the definitions. Responding to new inputs is inference, while learning from data is training.

**C. Training is the process of grouping similar items, while inference is the process of assigning labels**  
Wrong because grouping similar items describes a task such as clustering, not the general meaning of training. Assigning labels can happen in prediction, but that is not the definition of inference itself.

**D. Training and inference are two names for the same phase**  
Wrong because they are different phases: one learns the model, the other uses the model.

**Tips and Tricks:**  
- Think **training = learn**, **inference = use**.  
- If the model is still learning from examples, it is training.  
- If the model is already deployed or answering new inputs, it is inference.

> [!IMPORTANT]  
> A standard exam trap is to reverse **training** and **inference**. Always anchor on this rule: **training learns from data; inference applies the trained model to new data**.

**Source:**  
- [Introduction to machine learning concepts](https://learn.microsoft.com/en-us/training/modules/fundamentals-machine-learning/)  
- [What is Azure Machine Learning?](https://learn.microsoft.com/en-us/azure/machine-learning/overview-what-is-azure-machine-learning?view=azureml-api-2)  
- [Azure Machine Learning documentation](https://learn.microsoft.com/en-us/azure/machine-learning/?view=azureml-api-2)  
- [How to select a machine learning algorithm](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-select-algorithms?view=azureml-api-1)  
