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


**Question:** [005]  
Which scenario is the best example of **supervised learning**?

**Options:**  
A. Grouping customers into segments when no predefined categories exist  
B. Predicting house prices from historical examples with known prices  
C. Discovering hidden structure in product behavior without target values  
D. Organizing articles by similarity without predefined labels  

**Correct Answer(s):** B

**Explanation:**  
This is **supervised learning** because the model learns from historical examples where the correct target value is already known. In this case, the known target is the house price.

**Why the Correct Answer Is Correct:**  
- Supervised learning uses labeled data.  
- Known house prices act as the target values the model learns to predict.  
- Predicting a numeric value from known historical outcomes is a standard supervised ML pattern.

**Why the Other Options Are Wrong:**  

**A. Grouping customers into segments when no predefined categories exist**  
Wrong because this describes **unsupervised learning**, where the system finds structure without known labels.  

**C. Discovering hidden structure in product behavior without target values**  
Wrong because this also describes **unsupervised learning**. The key phrase is **without target values**.  

**D. Organizing articles by similarity without predefined labels**  
Wrong because organizing by similarity without labels is again an **unsupervised** pattern, not supervised learning.  

**Tips and Tricks:**  
- If the scenario includes **known correct outcomes**, think **supervised learning**.  
- If the task is **predicting a known target**, supervised is usually the right direction.  
- Watch for distractors that describe grouping or similarity without labels.

> [!IMPORTANT]  
> The strongest clue for **supervised learning** is the presence of a known answer in the training data.

**Source:**  
- [Introduction to machine learning concepts](https://learn.microsoft.com/en-us/training/modules/fundamentals-machine-learning/)  
- [A guide to artificial intelligence](https://learn.microsoft.com/en-us/training/modules/a-guide-to-artificial-intelligence/)  
- [How to select a machine learning algorithm](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-select-algorithms?view=azureml-api-1)  
- [Create machine learning models](https://learn.microsoft.com/en-us/training/paths/create-machine-learn-models/)  


**Question:** [006]  
Which scenario is the best example of **unsupervised learning**?

**Options:**  
A. Classifying emails as spam or not spam by using known past outcomes  
B. Predicting equipment failure time from historical records with known results  
C. Grouping customers into segments when no predefined categories exist  
D. Predicting whether a loan will be approved by using historical labeled cases  

**Correct Answer(s):** C

**Explanation:**  
This is **unsupervised learning** because the goal is to find structure in data when no predefined labels are available. Customer segmentation is a classic clustering-style example.

**Why the Correct Answer Is Correct:**  
- Unsupervised learning works with unlabeled data.  
- Grouping customers into segments is a standard clustering scenario.  
- The phrase **no predefined categories exist** is the clearest clue.

**Why the Other Options Are Wrong:**  

**A. Classifying emails as spam or not spam by using known past outcomes**  
Wrong because this is **supervised learning**. The known past outcomes act as labels.  

**B. Predicting equipment failure time from historical records with known results**  
Wrong because predicting from known results is a supervised learning pattern, not unsupervised learning.  

**D. Predicting whether a loan will be approved by using historical labeled cases**  
Wrong because the phrase **historical labeled cases** points directly to supervised learning.  

**Tips and Tricks:**  
- If the stem says **no labels**, **no predefined categories**, or **discover structure**, think **unsupervised learning**.  
- If the stem says **known outcomes** or **labeled cases**, it is not unsupervised.

> [!IMPORTANT]  
> The exam often tests **supervised vs unsupervised** by changing just one clue: **known labels** versus **no labels**.

**Source:**  
- [Introduction to machine learning concepts](https://learn.microsoft.com/en-us/training/modules/fundamentals-machine-learning/)  
- [A guide to artificial intelligence](https://learn.microsoft.com/en-us/training/modules/a-guide-to-artificial-intelligence/)  
- [How to select a machine learning algorithm](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-select-algorithms?view=azureml-api-1)  
- [K-Means Clustering: Component reference](https://learn.microsoft.com/en-us/azure/machine-learning/component-reference/k-means-clustering?view=azureml-api-2)  


**Question:** [007]  
A team says, “We have labeled data, so the model will learn from examples where the correct answer is already known.” Which concept are they describing?

**Options:**  
A. Inference  
B. Supervised learning  
C. Unsupervised learning  
D. Prompting  

**Correct Answer(s):** B

**Explanation:**  
They are describing **supervised learning** because the model learns from examples where the correct answers are already known. That is the defining idea behind supervised learning.

**Why the Correct Answer Is Correct:**  
- Supervised learning uses labeled data.  
- The phrase **correct answer is already known** directly points to labels.  
- The model learns from those known answers during training.

**Why the Other Options Are Wrong:**  

**A. Inference**  
Wrong because inference is the use of a trained model on new data, not the learning phase with labeled examples.  

**C. Unsupervised learning**  
Wrong because unsupervised learning does not rely on known correct answers or labels.  

**D. Prompting**  
Wrong because prompting refers to giving instructions or input to generative AI systems, not to the ML concept of learning from labeled datasets.  

**Tips and Tricks:**  
- **Known correct answer** usually means **label**.  
- **Label present during learning** usually means **supervised learning**.  
- Do not confuse **learning from labeled data** with **using a trained model**.

> [!IMPORTANT]  
> If a question says the model learns from examples where the answer is already known, **supervised learning** is the default answer unless the stem clearly says otherwise.

**Source:**  
- [Introduction to machine learning concepts](https://learn.microsoft.com/en-us/training/modules/fundamentals-machine-learning/)  
- [A guide to artificial intelligence](https://learn.microsoft.com/en-us/training/modules/a-guide-to-artificial-intelligence/)  
- [Endpoints for inference - Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/concept-endpoints?view=azureml-api-2)  
- [Introduction to generative AI and agents](https://learn.microsoft.com/en-us/training/modules/fundamentals-generative-ai/)  


**Question:** [008]  
Which statement about **deep learning** is correct?

**Options:**  
A. It is a neural-network approach inside machine learning that learns complex patterns from lots of data  
B. It is the same as generative AI because both produce text from prompts  
C. It is an unsupervised-only technique used mainly for clustering  
D. It refers to any model with a large number of parameters, regardless of method  

**Correct Answer(s):** A

**Explanation:**  
**Deep learning** is a neural-network-based approach within machine learning that can learn complex patterns, especially from large amounts of data. It is widely associated with tasks such as vision, speech, and language.

**Why the Correct Answer Is Correct:**  
- Deep learning is part of machine learning, not a separate category outside it.  
- It uses neural networks to learn complex patterns.  
- It is often useful when working with complex data such as images, audio, and language.

**Why the Other Options Are Wrong:**  

**B. It is the same as generative AI because both produce text from prompts**  
Wrong because deep learning and generative AI are related but not identical. Generative AI focuses on producing new content, while deep learning is a broader neural-network approach within ML.  

**C. It is an unsupervised-only technique used mainly for clustering**  
Wrong because deep learning is not limited to unsupervised learning and is not mainly defined by clustering. It can be used across different kinds of ML tasks.  

**D. It refers to any model with a large number of parameters, regardless of method**  
Wrong because parameter count alone does not define deep learning. The defining idea is the neural-network approach.  

**Tips and Tricks:**  
- Anchor on **neural networks** when you see **deep learning**.  
- Do not collapse **deep learning** into **generative AI**.  
- A model being large does not automatically make it deep learning.

> [!IMPORTANT]  
> A strong exam shortcut is: **Deep Learning = neural-network approach inside ML**.

**Source:**  
- [A guide to artificial intelligence](https://learn.microsoft.com/en-us/training/modules/a-guide-to-artificial-intelligence/)  
- [Create machine learning models](https://learn.microsoft.com/en-us/training/paths/create-machine-learn-models/)  
- [Introduction to generative AI and agents](https://learn.microsoft.com/en-us/training/modules/fundamentals-generative-ai/)  
- [Key concepts and considerations in generative AI](https://learn.microsoft.com/en-us/azure/developer/ai/gen-ai-concepts-considerations-developers)  


**Question:** [009]  
Which statement best distinguishes **Generative AI** from traditional prediction-focused machine learning tasks?

**Options:**  
A. Generative AI learns from data, while machine learning does not  
B. Generative AI generates new content, while traditional ML often predicts labels or values  
C. Generative AI uses features and labels, while machine learning uses only prompts  
D. Generative AI is limited to language, while machine learning is limited to numbers  

**Correct Answer(s):** B

**Explanation:**  
**Generative AI** is designed to create new content such as text, images, code, or other outputs. Traditional prediction-focused machine learning is usually centered on predicting a label or a numeric value from data, rather than generating new content.

**Why the Correct Answer Is Correct:**  
- Generative AI focuses on producing new content.  
- Traditional ML often focuses on prediction tasks such as classification or regression.  
- The key distinction is **generate** versus **predict**.

**Why the Other Options Are Wrong:**  

**A. Generative AI learns from data, while machine learning does not**  
Wrong because machine learning also learns from data. Learning from data is not unique to generative AI.

**C. Generative AI uses features and labels, while machine learning uses only prompts**  
Wrong because this reverses the normal pattern. Features and labels are standard ML concepts, while prompts are associated with interacting with generative AI systems.

**D. Generative AI is limited to language, while machine learning is limited to numbers**  
Wrong because generative AI can work across multiple content types, and machine learning is not limited to numeric-only use cases.

**Tips and Tricks:**  
- If the stem says **create**, **generate**, or **produce new content**, think **Generative AI**.  
- If the stem says **predict a class or value**, think traditional ML.  
- Do not confuse **content generation** with **classification/regression**.

> [!IMPORTANT]  
> A clean exam shortcut is: **Generative AI creates; traditional ML predicts**.

**Source:**  
- [Key concepts and considerations in generative AI](https://learn.microsoft.com/en-us/azure/developer/ai/gen-ai-concepts-considerations-developers)  
- [Introduction to generative AI and agents](https://learn.microsoft.com/en-us/training/modules/fundamentals-generative-ai/)  
- [A guide to artificial intelligence](https://learn.microsoft.com/en-us/training/modules/a-guide-to-artificial-intelligence/)  
- [Introduction to machine learning concepts](https://learn.microsoft.com/en-us/training/modules/fundamentals-machine-learning/)  


**Question:** [010]  
Which statement about **language models** is correct?

**Options:**  
A. They store documents exactly as written so they can be retrieved later word for word  
B. They encapsulate semantic relationships between language elements, enabling meaningful text generation  
C. They are mainly used to convert scanned pages into editable text  
D. They work by assigning fixed labels to each sentence in a dataset  

**Correct Answer(s):** B

**Explanation:**  
Language models learn relationships in language and use those relationships to generate meaningful text. They are not simply storing documents word for word, and they are not OCR tools or fixed-label classifiers by definition.

**Why the Correct Answer Is Correct:**  
- Language models learn semantic and contextual relationships in language.  
- Those learned relationships are what make meaningful text generation possible.  
- This matches the idea that a model can generate coherent sequences rather than just retrieve memorized text.

**Why the Other Options Are Wrong:**  

**A. They store documents exactly as written so they can be retrieved later word for word**  
Wrong because language models are not defined as exact document storage systems. They generate outputs based on learned patterns in language.

**C. They are mainly used to convert scanned pages into editable text**  
Wrong because converting scanned pages into text is closer to OCR or document processing, not the core role of language models.

**D. They work by assigning fixed labels to each sentence in a dataset**  
Wrong because fixed-label assignment is a classification idea, not the core definition of a language model.

**Tips and Tricks:**  
- Anchor on **language understanding and generation** when you see **language model**.  
- Do not confuse language models with **OCR** or basic **classification**.  
- If the option sounds like document storage or scanning, it is probably a trap.

> [!IMPORTANT]  
> Language models work because they learn relationships between language elements, not because they simply store exact text for replay.

**Source:**  
- [LLM Fundamentals](https://learn.microsoft.com/en-us/agent-framework/journey/llm-fundamentals)  
- [Introduction to generative AI and agents](https://learn.microsoft.com/en-us/training/modules/fundamentals-generative-ai/)  
- [Key concepts and considerations in generative AI](https://learn.microsoft.com/en-us/azure/developer/ai/gen-ai-concepts-considerations-developers)  
- [A guide to artificial intelligence](https://learn.microsoft.com/en-us/training/modules/a-guide-to-artificial-intelligence/)  


**Question:** [011]  
Which statement best compares **LLMs** and **SLMs**?

**Options:**  
A. LLMs are always the best choice because they are smaller and cheaper to run  
B. SLMs are more suitable for focused or local scenarios, while LLMs are often more powerful and general  
C. SLMs cannot be used in agents or on-device scenarios because they are too limited  
D. LLMs and SLMs differ only in training data size, not in practical usage tradeoffs  

**Correct Answer(s):** B

**Explanation:**  
LLMs are generally more powerful and broad, while SLMs are often a better fit for narrower, focused, or local/on-device scenarios. Microsoft documentation also shows SLM usage in local and self-contained deployments.

**Why the Correct Answer Is Correct:**  
- LLMs are generally stronger for broad generalization.  
- SLMs can be a good fit when the scenario is focused or local.  
- Microsoft documents local SLM deployment scenarios, which supports the idea that SLMs can suit constrained or on-device style use cases.

**Why the Other Options Are Wrong:**  

**A. LLMs are always the best choice because they are smaller and cheaper to run**  
Wrong because LLMs are not smaller by definition, and “always the best” ignores practical tradeoffs.

**C. SLMs cannot be used in agents or on-device scenarios because they are too limited**  
Wrong because Microsoft documentation explicitly covers local SLM scenarios. That makes this option directly opposite to the documented usage pattern.

**D. LLMs and SLMs differ only in training data size, not in practical usage tradeoffs**  
Wrong because the practical tradeoffs matter, especially around focus, locality, and deployment style.

**Tips and Tricks:**  
- Think **LLM = broader/general**, **SLM = smaller/focused/local**.  
- Avoid absolute choices like **always** unless the stem strongly supports them.  
- If the option ignores deployment tradeoffs, it is usually weak.

> [!IMPORTANT]  
> A strong exam-safe framing is: **LLMs usually offer broader capability, while SLMs often fit focused or local scenarios better**.

**Source:**  
- [Use local small language models (SLMs) in Azure App Service](https://learn.microsoft.com/en-us/azure/app-service/scenario-ai-local-small-language-model)  
- [Foundry Local architecture overview](https://learn.microsoft.com/en-us/azure/foundry-local/concepts/foundry-local-architecture)  
- [LLM Fundamentals](https://learn.microsoft.com/en-us/agent-framework/journey/llm-fundamentals)  
- [Introduction to generative AI and agents](https://learn.microsoft.com/en-us/training/modules/fundamentals-generative-ai/)  


**Question:** [012]  
In the context of AI models, what are **parameters**?

**Options:**  
A. The user instructions entered to guide the model  
B. The target outputs used during supervised learning  
C. The learned internal weights of the model  
D. The chunks of text a model processes at runtime  

**Correct Answer(s):** C

**Explanation:**  
Parameters are the learned internal weights of a model. Microsoft’s LLM fundamentals material describes model weights as numerical parameters learned during training.

**Why the Correct Answer Is Correct:**  
- Parameters are internal values learned during training.  
- They are not user input and not dataset labels.  
- In model discussions, “weights” and “parameters” are closely related ideas.

**Why the Other Options Are Wrong:**  

**A. The user instructions entered to guide the model**  
Wrong because those are **prompts**, not parameters.

**B. The target outputs used during supervised learning**  
Wrong because those are **labels**, not parameters.

**D. The chunks of text a model processes at runtime**  
Wrong because those are **tokens**, not parameters.

**Tips and Tricks:**  
- Think **parameters = inside the model**.  
- Think **prompts/tokens = outside interaction/input concepts**.  
- Think **labels = dataset target concept**.

> [!IMPORTANT]  
> The fastest distinction is: **parameters are learned weights inside the model; prompts, tokens, and labels are different concepts outside that role**.

**Source:**  
- [LLM Fundamentals](https://learn.microsoft.com/en-us/agent-framework/journey/llm-fundamentals)  
- [Prompts overview](https://learn.microsoft.com/en-us/microsoft-copilot-studio/prompts-overview)  
- [Understanding tokens](https://learn.microsoft.com/en-us/dotnet/ai/conceptual/understanding-tokens)  
- [Introduction to generative AI and agents](https://learn.microsoft.com/en-us/training/modules/fundamentals-generative-ai/)  
