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
Wrong because deep learning specifically uses **multi-layer neural networks** and is more commonly associated with tasks like image, speech, or language processing. Here, the case is simply learning from past sales data to predict future results, which fits **Machine Learning** more precisely.

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
Wrong because parameters are values inside the model itself, such as weights adjusted during training. A weight is a numeric value that shows how strongly one input affects the prediction. For example, the model may learn to give one feature more importance than another. **Fraud = Yes/No** is a dataset column that provides the expected outcome, so it is a label, not a parameter.

**D. Tokens**  
Wrong because tokens are **units of text**, such as whole words or parts of words. **Fraud = Yes/No** is not a text unit being broken down for processing; it is the target column that the model is trying to predict.

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


**Question:** [013]  
Which statement about **prompts** is correct?

**Options:**  
A. Prompts are the internal weights learned by a model during training  
B. Prompts are natural language statements or questions used to interact with generative AI models  
C. Prompts are the same as labels because both guide the model toward an output  
D. Prompts are the semantic vectors produced by embeddings models

**Correct Answer(s):** B

**Explanation:**  
A **prompt** is the input you give a generative AI model, usually as a natural language instruction, question, or request. It guides the model on what kind of output to generate.

**Why the Correct Answer Is Correct:**  
- Prompts are used to instruct a generative AI model what to do.  
- They are typically written in natural language.  
- They shape the structure and content of the model’s response.

**Why the Other Options Are Wrong:**  

**A. Prompts are the internal weights learned by a model during training**  
Wrong because internal learned weights are **parameters**, not prompts. Prompts are user or system inputs given at interaction time.

**C. Prompts are the same as labels because both guide the model toward an output**  
Wrong because **labels** are target outputs used in supervised learning datasets, while **prompts** are interaction inputs used with generative AI models.

**D. Prompts are the semantic vectors produced by embeddings models**  
Wrong because semantic vectors are **embeddings**, not prompts.

**Tips and Tricks:**  
- Think **prompt = instruction/request to the model**.  
- Do not confuse prompts with **parameters**, **labels**, or **embeddings**.  
- If the stem is about interacting with a generative model, **prompt** is usually in play.

> [!IMPORTANT]  
> A strong shortcut is: **prompt = what you ask the model; parameter = what the model learned**.

**Source:**  
- [Prompts overview](https://learn.microsoft.com/en-us/microsoft-copilot-studio/prompts-overview)  
- [Prompt engineering techniques](https://learn.microsoft.com/en-us/azure/foundry/openai/concepts/prompt-engineering)  
- [Write effective prompts for Azure Copilot](https://learn.microsoft.com/en-us/azure/copilot/write-effective-prompts)  
- [Create effective prompts for generative AI training tools](https://learn.microsoft.com/en-us/training/modules/create-prompts-for-generative-ai-training-tools/)  


**Question:** [014]  
Which statement about **tokens** is correct?

**Options:**  
A. Tokens are always full words, never parts of words or punctuation  
B. Tokens are chunks of text processed by language models, and token limits affect how much input and output can be handled at once  
C. Tokens are the same as prompts, because both are entered by the user  
D. Tokens are the output labels predicted by a classifier

**Correct Answer(s):** B

**Explanation:**  
**Tokens** are the chunks of text a language model processes. They are not always full words; they can also be parts of words or punctuation, and token limits affect how much text the model can take in and produce at one time.

**Why the Correct Answer Is Correct:**  
- Language models process text as tokens rather than raw characters or whole words only.  
- Tokens can be smaller than full words.  
- Input and output token counts affect model usage and limits.

**Why the Other Options Are Wrong:**  

**A. Tokens are always full words, never parts of words or punctuation**  
Wrong because tokens are not limited to whole words. They can represent subword pieces and punctuation too.

**C. Tokens are the same as prompts, because both are entered by the user**  
Wrong because a **prompt** is the instruction or input request, while **tokens** are the units the model uses internally to process that text.

**D. Tokens are the output labels predicted by a classifier**  
Wrong because labels belong to supervised learning targets, not tokenization.

**Tips and Tricks:**  
- Think **token = unit of text processing**.  
- Do not assume **1 token = 1 word**.  
- If a question mentions model input/output size limits, tokens are usually the key concept.

> [!IMPORTANT]  
> A reliable shortcut is: **prompt is what you send; tokens are how the model breaks that text down for processing**.

**Source:**  
- [Understanding tokens](https://learn.microsoft.com/en-us/dotnet/ai/conceptual/understanding-tokens)  
- [Prompt tokens](https://learn.microsoft.com/en-us/ai-builder/licensing-prompt-tokens)  
- [Key concepts and considerations in generative AI](https://learn.microsoft.com/en-us/azure/developer/ai/gen-ai-concepts-considerations-developers)  
- [LLM Fundamentals](https://learn.microsoft.com/en-us/agent-framework/journey/llm-fundamentals)  


**Question:** [015]  
Which statement about **embeddings** is correct?

**Options:**  
A. They convert text into numerical vectors so items with similar meaning are closer together  
B. They count how often words appear but do not represent semantic meaning  
C. They are the same as parameters because both are numbers inside a model  
D. They are labels represented in numeric form for supervised learning

**Correct Answer(s):** A

**Explanation:**  
**Embeddings** represent text as numerical vectors in a semantic space. Texts with similar meaning end up closer together, which is why embeddings are useful for similarity search and semantic matching.

**Why the Correct Answer Is Correct:**  
- Embeddings convert text into vectors.  
- These vectors are useful for comparing similarity between texts.  
- That makes embeddings central to semantic search and related retrieval scenarios.

**Why the Other Options Are Wrong:**  

**B. They count how often words appear but do not represent semantic meaning**  
Wrong because that is closer to frequency-based methods, not embeddings. Embeddings are specifically used to capture semantic similarity.

**C. They are the same as parameters because both are numbers inside a model**  
Wrong because embeddings are vector representations of text, while parameters are learned internal weights of the model.

**D. They are labels represented in numeric form for supervised learning**  
Wrong because labels are target outputs in supervised learning, not semantic vector representations.

**Tips and Tricks:**  
- Think **embedding = semantic vector**.  
- If the stem mentions **similarity**, **semantic search**, or **vector space**, embeddings are a strong candidate.  
- Do not confuse embeddings with **labels**, **parameters**, or simple word-count methods.

> [!IMPORTANT]  
> A fast shortcut is: **embeddings turn meaning into vectors**.

**Source:**  
- [How to generate embeddings with Azure OpenAI](https://learn.microsoft.com/en-us/azure/foundry/openai/how-to/embeddings)  
- [Azure OpenAI embeddings tutorial](https://learn.microsoft.com/en-us/azure/foundry/openai/tutorials/embeddings)  
- [How Embeddings Extend Your AI Model's Reach](https://learn.microsoft.com/en-us/dotnet/ai/conceptual/embeddings)  
- [Azure OpenAI embeddings (classic) - understand embeddings](https://learn.microsoft.com/en-us/azure/foundry-classic/openai/concepts/understand-embeddings)  


**Question:** [016]  
A search for **plant** returns results about **flower** before results about **airplane**. Which concept best explains this behavior?

**Options:**  
A. Frequency analysis  
B. N-grams  
C. Embeddings  
D. Labels

**Correct Answer(s):** C

**Explanation:**  
This behavior is best explained by **embeddings** because embeddings place semantically related meanings closer together in vector space. Since **plant** and **flower** are more related in meaning than **plant** and **airplane**, the search can rank **flower**-related results higher.

**Why the Correct Answer Is Correct:**  
- Embeddings are designed to capture semantic similarity.  
- Vector similarity can be used to rank related results.  
- That makes embeddings the best explanation for meaning-based closeness like **plant** and **flower**.

**Why the Other Options Are Wrong:**  

**A. Frequency analysis**  
Wrong because frequency analysis focuses on counts and occurrences, not semantic closeness of meaning.

**B. N-grams**  
Wrong because N-grams focus on local text patterns and co-occurrence structure, not the broader semantic similarity represented by embeddings.

**D. Labels**  
Wrong because labels are target outputs in supervised learning, not the mechanism behind semantic ranking in search.

**Tips and Tricks:**  
- If the question is about **meaning-based closeness**, think **embeddings**.  
- If it is about **counting patterns**, think frequency methods or N-grams instead.  
- Semantic search questions often point to vector representations.

> [!IMPORTANT]  
> The key clue is not just that the words are different. The key clue is that they are **closer in meaning**, which is exactly what embeddings are designed to represent.

**Source:**  
- [Azure OpenAI embeddings (classic) - understand embeddings](https://learn.microsoft.com/en-us/azure/foundry-classic/openai/concepts/understand-embeddings)  
- [How Embeddings Extend Your AI Model's Reach](https://learn.microsoft.com/en-us/dotnet/ai/conceptual/embeddings)  
- [Azure OpenAI embeddings tutorial](https://learn.microsoft.com/en-us/azure/foundry/openai/tutorials/embeddings)  
- [Generate Vector Embeddings with Azure OpenAI](https://learn.microsoft.com/en-us/azure/postgresql/azure-ai/generative-ai-azure-openai)  

**Question:** [017]  
Which statement best distinguishes **frequency analysis / N-grams** from **embeddings**?

**Options:**  
A. Frequency analysis and N-grams create semantic vector spaces, while embeddings only count occurrences  
B. Frequency analysis and N-grams focus on occurrence patterns, while embeddings represent semantic similarity in vector space  
C. Embeddings are used only in supervised learning, while N-grams are used only in unsupervised learning  
D. Embeddings and N-grams are two names for the same semantic representation method  

**Correct Answer(s):** B

**Explanation:**  
**Frequency analysis** and **N-grams** focus on counting terms or local word patterns, while **embeddings** represent text as vectors that capture semantic similarity. The key difference is **pattern counting** versus **meaning-based vector representation**.

**Why the Correct Answer Is Correct:**  
- Frequency analysis and N-grams are based on occurrences and local text patterns.  
- Embeddings map text into vector space.  
- Those vectors make it possible to compare similarity based on meaning, not just count patterns.

**Why the Other Options Are Wrong:**  

**A. Frequency analysis and N-grams create semantic vector spaces, while embeddings only count occurrences**  
Wrong because this reverses the concepts. Embeddings are the vector-based semantic representation method, not frequency analysis or N-grams.

**C. Embeddings are used only in supervised learning, while N-grams are used only in unsupervised learning**  
Wrong because this is not the real distinction. The difference is about representation method, not a strict supervised-versus-unsupervised split.

**D. Embeddings and N-grams are two names for the same semantic representation method**  
Wrong because they are different approaches. N-grams focus on token patterns, while embeddings focus on semantic closeness in vector space.

**Tips and Tricks:**  
- Think **N-grams = pattern/count based**.  
- Think **embeddings = meaning/vector based**.  
- If the question mentions **semantic similarity**, embeddings are usually the better answer.

> [!IMPORTANT]  
> The cleanest shortcut is: **N-grams count patterns; embeddings represent meaning**.

**Source:**  
- [Azure OpenAI embeddings (classic) - understand embeddings](https://learn.microsoft.com/en-us/azure/foundry-classic/openai/concepts/understand-embeddings)  
- [How to generate embeddings with Azure OpenAI](https://learn.microsoft.com/en-us/azure/foundry/openai/how-to/embeddings)  
- [Azure OpenAI embeddings tutorial](https://learn.microsoft.com/en-us/azure/foundry/openai/tutorials/embeddings)  
- [LLM Fundamentals](https://learn.microsoft.com/en-us/agent-framework/journey/llm-fundamentals)  


**Question:** [018]  
Which statement is the most accurate relationship among **AI**, **ML**, **Deep Learning**, and **Generative AI**?

**Options:**  
A. AI is inside ML, ML is inside Deep Learning, and Generative AI is outside all of them  
B. ML is one way to build AI, Deep Learning is a neural-network approach inside ML, and Generative AI focuses on generating new content  
C. Deep Learning and Generative AI are the same thing, and both replace machine learning  
D. AI and ML are identical terms, while Deep Learning refers only to language models  

**Correct Answer(s):** B

**Explanation:**  
This is the most accurate relationship because **AI** is the broad umbrella, **ML** is one way to build AI by learning from data, **Deep Learning** is a neural-network approach inside ML, and **Generative AI** focuses on generating new content such as text, images, code, and more.

**Why the Correct Answer Is Correct:**  
- AI is the broadest concept.  
- Machine Learning is a subset-style approach within AI.  
- Deep Learning is a neural-network approach within ML.  
- Generative AI is defined by generating new content rather than just predicting labels or values.

**Why the Other Options Are Wrong:**  

**A. AI is inside ML, ML is inside Deep Learning, and Generative AI is outside all of them**  
Wrong because the hierarchy is reversed. AI is the broad umbrella, not the smaller inner category.

**C. Deep Learning and Generative AI are the same thing, and both replace machine learning**  
Wrong because deep learning and generative AI are related but not identical, and neither replaces machine learning as a whole.

**D. AI and ML are identical terms, while Deep Learning refers only to language models**  
Wrong because AI and ML are not identical, and deep learning is used beyond language, including areas such as vision and speech.

**Tips and Tricks:**  
- Anchor on the hierarchy: **AI → ML → Deep Learning**.  
- Treat **Generative AI** as defined by **content generation**.  
- Be careful with choices that use absolute wording like **identical** or **replace**.

> [!IMPORTANT]  
> A strong exam-safe memory line is: **AI is the umbrella, ML learns from data, Deep Learning is neural-network-based ML, and Generative AI creates new content**.

**Source:**  
- [A guide to artificial intelligence](https://learn.microsoft.com/en-us/training/modules/a-guide-to-artificial-intelligence/)  
- [Introduction to machine learning concepts](https://learn.microsoft.com/en-us/training/modules/fundamentals-machine-learning/)  
- [Deep Learning vs. Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/concept-deep-learning-vs-machine-learning?view=azureml-api-2)  
- [Introduction to generative AI and agents](https://learn.microsoft.com/en-us/training/modules/fundamentals-generative-ai/)  


**Question:** [019]  
Which set contains only **prediction-oriented machine learning workloads**?

**Options:**  
A. Regression, Classification, Clustering, Anomaly Detection  
B. Regression, Knowledge Mining, Clustering, Anomaly Detection  
C. Classification, Generative AI, Clustering, Document Processing  
D. Regression, Classification, Speech, Anomaly Detection  

**Correct Answer(s):** A

**Explanation:**  
The correct set is **Regression, Classification, Clustering, and Anomaly Detection**. Microsoft documentation commonly presents these as core machine learning task types. They all work with data to produce predictions, groupings, or unusual-pattern detection results.

**Why the Correct Answer Is Correct:**  
- **Regression** predicts a numeric value.  
- **Classification** predicts a label or category.  
- **Clustering** groups similar items based on patterns in the data.  
- **Anomaly Detection** identifies unusual data points or rare behavior.  

**Why the Other Options Are Wrong:**  

**B. Regression, Knowledge Mining, Clustering, Anomaly Detection**  
Wrong because **Knowledge Mining** is a search-oriented workload, not one of these core machine learning prediction-oriented tasks.

**C. Classification, Generative AI, Clustering, Document Processing**  
Wrong because **Generative AI** focuses on generating new content, and **Document Processing** focuses on extracting structure from documents.

**D. Regression, Classification, Speech, Anomaly Detection**  
Wrong because **Speech** is an audio-language workload, not one of these machine learning task types.

**Tips and Tricks:**  
- When you see **Regression**, **Classification**, **Clustering**, and **Anomaly Detection** together, think of common **machine learning workload types**.  
- Eliminate any option that mixes in search, document, speech, or generative workloads.  
- Check every item in the option, not just the first two.

> [!IMPORTANT]  
> A common trap is mixing one unrelated workload into an otherwise correct set. Verify that **all four items** belong together.

**Source:**  
- [Introduction to machine learning concepts](https://learn.microsoft.com/en-us/training/modules/fundamentals-machine-learning/)  
- [How to select a machine learning algorithm](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-select-algorithms?view=azureml-api-1)  
- [Machine Learning Algorithm Cheat Sheet](https://learn.microsoft.com/en-us/azure/machine-learning/algorithm-cheat-sheet?view=azureml-api-1)  
- [What is Azure Machine Learning?](https://learn.microsoft.com/en-us/azure/machine-learning/overview-what-is-azure-machine-learning?view=azureml-api-2)  
