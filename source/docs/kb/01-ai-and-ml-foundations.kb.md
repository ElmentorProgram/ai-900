# AI and ML Foundations

This document introduces the core AI concepts and the most common AI workloads. It focuses on how to choose the right workload based on your input data and the output you need, then connects those ideas to Azure services in a compact mapping section.

**This Document Covers**
- Core Definitions  
- Common AI Workloads (How to Choose)  
- Workloads and What They Do  
- Common Confusions (Choose This, Not That)  
- Azure Mapping (Concept → Azure Service Family)  
- Summary

## Core Definitions

- **Artificial Intelligence (AI):** Systems that perform tasks that usually require human intelligence (perception, language, reasoning, decision support).  
- **Machine Learning (ML):** AI where models learn patterns from data to make predictions or decisions.  
- **Features & Labels:** Features are the input signals you train on; Labels are the target outputs you want the model to learn (Labels are what make a dataset “supervised”).  
- **Training vs Inference:** Training is when the model learns from data; Inference is when the trained model makes predictions on new inputs.  
- **Supervised vs Unsupervised:** Supervised learning uses labeled data; Unsupervised learning has no Labels and finds structure (for example: Clustering).  
- **Deep Learning:** A neural-network approach in ML that learns complex patterns from lots of data (commonly used in Vision, Speech, and Language).  
- **Generative AI:** A branch of AI that enables software applications to generate new content; often natural language dialogs, but also images, video, code, and other formats.  
- **Language Models:** Models encapsulate semantic relationships between language elements (that’s what enables them to generate a meaningful sequence of text).  
- **LLMs vs SLMs:** LLMs are powerful and generalize well but can be more costly; SLMs tend to work well in more focused scenarios or when you need small models for local applications and agents on devices.  
- **Parameters:** The learned internal weights of a model. More parameters usually means more capacity, but it typically requires more compute both to train the model and to run inference (make predictions).  
- **Prompts:** Users interact with generative AI language models through prompts, natural language statements or questions.  
- **Tokens:** Language models process text as tokens (chunks of text), not characters or words; token limits shape how much input and output the model can handle at once.  
- **Vectorization (Embeddings):** Vectorization maps words (or sentences/documents) into numerical vectors so that items with similar meaning become close to each other (e.g., “plant” and “flower” are closer than “airplane”). This is the core idea behind Embeddings: represent language as vectors so you can compare similarity.  
- **Frequency analysis / N-grams vs Embeddings:** Frequency analysis and N-grams count occurrences and patterns, and lemmatization normalizes word forms; these techniques support text processing but do not create semantic vector spaces the way Embeddings do.  

**Embeddings Example (Similarity Intuition)**  
A search for **plant** will often return text about **flower** before text about **airplane**, because Embeddings place related meanings closer together in vector space.

> [!IMPORTANT]
> AI is the umbrella, ML is one way to build AI by learning patterns from data, Deep Learning is a neural-network approach inside ML, Generative AI generates new content from prompts.

## Common AI Workloads (How to Choose)

Start with two questions. A workload is the type of AI task or problem you are trying to solve (vision, language, document extraction, ML prediction, etc.). You choose it by matching the data you have to the output you need.

1) What is the **input**?
   - Images/video → **Computer Vision**
   - Text/documents → **Natural Language Processing (NLP)** or **Document Processing**
   - Conversations (chat/voice) → **Conversational AI**
   - Time-series/telemetry/transactions → **Anomaly Detection** or **Machine Learning**

2) What is the **output**?
   - A label/category → **Classification**
   - A number → **Regression**
   - Groups/segments → **Clustering**
   - Unusual/rare events → **Anomaly Detection**
   - Extracted text/fields/tables → **Document Processing**
   - Searchable results from lots of content → **Knowledge Mining**
   - Generated text/content → **Generative AI**
   - Answer a user in chat → **Conversational AI**

The same input can support different workloads depending on the output you need.

If the **text** is inside a scanned PDF/image, you usually need **OCR/Document Processing** before **NLP**.

> [!IMPORTANT]  
> Start from the workload, input type and output need, then map to the service, don’t start from the Azure service name and work backwards.

### Workload Landscape (Quick Map)

This is a wide-map view of the major AI workloads. The goal is to build a strong mental model first, then go deeper later. You can think of the landscape in five clusters: **Prediction** workloads (Regression, Classification, Clustering, Anomaly Detection), **Language/Search** workloads (NLP/Text Analysis, Knowledge Mining, Generative AI, Conversational AI), **Voice** workloads (Speech), **Vision** workloads (Computer Vision), and **Docs** workloads (Information Extraction, Document Processing). The detailed sections that follow use this same order so your mental map stays stable.

- **Regression**
- **Classification**
- **Clustering**
- **Anomaly Detection**
- **Natural Language Processing and Text Analysis**
- **Knowledge Mining**
- **Generative AI**
- **Conversational AI**
- **Speech**
- **Computer Vision**
- **Information Extraction**
- **Document Processing**


## Workloads and What They Do

### Regression

Regression predicts a **numeric value** (a number) from input features.  
Use it when the target you want to predict is a continuous number rather than a category.

Regression is common when you want to estimate **how much** or **how many** from past examples.  
You train on rows where the numeric target is known, then predict that value for new data.

**Highlights**
- Output is a numeric value  
- Use when the target is continuous (for example: price, demand, duration)  
- Typical scenarios include house price prediction, sales/demand forecasting, and time-to-failure estimation  
- Training is usually supervised because you train on known numeric targets  

### Classification

Classification predicts a **label/category** from input features (for example: yes/no, fraud/not fraud, class A/B/C).  
Use it when the target you want to predict is a category rather than a continuous number.

Classification is common when you want to decide **which group** something belongs to based on past labeled examples.  
You train on rows where the correct label is known, then predict the label for new data.

**Highlights**
- Output is a label/category  
- Use when the target is a category (binary or multi-class)  
- Typical scenarios include fraud detection, spam filtering, and defect detection (pass/fail)  
- Training is usually supervised because you train on known labels  

### Clustering

Clustering groups data into **clusters** without predefined labels (you do not have labels and want the algorithm to discover structure).  
Use it when you want to segment data into groups based on similarity and you don’t already have the correct group labels.

Clustering is common when you want to discover natural groupings in data rather than predict a known outcome.  
You run the algorithm on unlabeled data, then interpret and name the clusters based on what they represent.

**Highlights**
- Output is a cluster assignment (a group/segment for each item)  
- Use when you do not have labels and want the model to discover structure  
- Typical scenarios include customer segmentation, grouping similar documents, and organizing products into segments  
- Training is usually unsupervised because there are no target labels  

> [!NOTE]
> Machine Learning is for predicting labels or numbers from features, Computer Vision is for visual input, NLP is for meaning in text, Document Processing is for extracting text, fields, and tables from documents, Knowledge Mining is for making large content searchable.

### Anomaly Detection

Anomaly detection finds data points or events that are **unusual compared to normal behavior**.  
Use it when you have a notion of **normal** and you want to flag rare, suspicious, or abnormal patterns.

Anomaly detection is common when the important cases are rare and you can’t rely on a simple category label alone.  
You typically learn or estimate a baseline, then detect deviations from that baseline as potential anomalies.

**Highlights**
- Output is an anomaly flag and/or anomaly score (how unusual)  
- Use when you want to detect rare events or unusual behavior vs a baseline  
- Typical scenarios include fraud/suspicious transactions, equipment faults, intrusion detection, and metric spikes/drops  
- The key idea is comparing behavior to **normal** rather than predicting a fixed label  

### Natural Language Processing and Text Analysis

Use when the input is **text** and you want to analyze language.  
This workload focuses on extracting meaning and signals from text so your app can classify, extract, summarize, or route content.

Common capabilities include text classification (including sentiment analysis), key phrase extraction, entity recognition, language detection, and summarization.  
If the **text** is inside a scanned PDF/image, you usually need **OCR/Document Processing** first to extract text, then you can run NLP on the extracted text.

**Highlights**
- Use when the input is text and you want meaning-level analysis (not just OCR)  
- Typical tasks include sentiment analysis, key phrase extraction, and summarization  
- Also includes entity recognition (people, places, organizations, products) and language detection  
- Common scenarios include finding key subjects/topics in documents or transcripts  
- Also includes evaluating sentiment and opinion in reviews or social media  
- Also supports FAQ-style chatbots and predictable conversational dialogs (without needing Generative AI)  
- If the text comes from scans/images, OCR/Document Processing comes first, then NLP  

### Knowledge Mining

Knowledge mining is an AI workload whose primary purpose is to make large volumes of content searchable.  
Use it when you have lots of unstructured content and you want to query it like a search engine.

It commonly uses indexing plus AI enrichment to extract and enrich content so it becomes searchable.  
Enrichment can include extracting text from documents/images (OCR) and extracting entities and key phrases from text.

**Highlights**
- The goal is a searchable index you can query (not generated content)  
- Typical flow: data source → indexing → enrichment → search index → query  
- Enrichment often uses OCR (for documents/images) and NLP signals (entities, key phrases)  
- Output is searchable fields and ranked results  

### Generative AI Scenarios
Common uses of generative AI include implementing AI agents that assist human users by providing information or automating tasks, creating new documents or other content, automated translation of text between languages, and summarizing or explaining complex documents.

### Conversational AI  
Use when the system must interact with users through chat or voice.

#### Two Common Patterns
- **Language Understanding (Intent & Entities):** interpret what the user wants to do and extract the details needed to do it.
- **Question Answering:** find the best answer to a user’s question from known content (for example: FAQs, documents, or web pages).

#### Language Understanding (Intent & Entities)
When you need to interpret what a user means in a message like “Call me back later,” you are doing language understanding (often modeled as **Intent & Entities**).

Typical outputs:
- **Intent:** what the user wants to do  
- **Entities:** important details inside the text  

#### Question Answering
Use when the user is asking for information and the answer should come from known content.

Typical outputs:
- **Best-matching answer:** the most relevant response found in the content  
- **Optional score/confidence:** a signal of how well the content matched the question (when available)

#### How to Choose
- If the message is “Do something” → **Language Understanding (Intent & Entities)**
- If the message is “Tell me something” → **Question Answering**
- If it is unclear → ask one short clarifying question, then choose one of the two patterns

### Speech
Speech capabilities in AI applications and agents enable users to interact with them through spoken language.

#### Speech Recognition
Speech recognition is the ability of AI to “hear” and interpret speech. Usually this capability takes the form of **speech-to-text**, where the audio signal for the speech is transcribed into text.

#### Speech Synthesis
Speech synthesis is the ability of AI to vocalize words as spoken language. Usually this capability takes the form of **text-to-speech**, in which information in text format is converted into an audible signal.

#### Speech Scenarios
Common uses of AI speech technologies include:
- AI agents that understand spoken input, perform tasks, and respond with spoken results
- Automated transcription of calls or meetings
- Automating audio descriptions of video or text
- Automated speech translation between languages

### Computer Vision
Computer vision is the area of artificial intelligence that deals with the analysis of visual input; such as photographs, videos, and live camera feeds. Computer vision is accomplished by using large numbers of images to train a model.

There are multiple types of computer vision model.

- **Image Classification:** a model is trained with images that are labeled with the main subject of the image so it can analyze unlabeled images and predict the most appropriate label.  
- **Object Detection:** the model is trained to identify the location of specific objects in an image.  
- **Semantic Segmentation:** an advanced form of object detection where the model identifies the individual pixels in the image that belong to a particular object.  
- **Multi-modal Models:** combine visual features and associated text descriptions, enabling them to generate comprehensive descriptions of images.

Computer vision scenarios include AI agents that can interpret visual input, auto-captioning or tag-generation for photographs, visual search, monitoring stock levels or identifying items for checkout in retail scenarios, security video monitoring, authentication through facial recognition, and robotics and self-driving vehicles.

### Information Extraction
AI is commonly used to automate information extraction solutions that find information and unlock insights in unstructured data sources, such as scanned documents and forms, images, and audio or video recordings.

The basis for most document analysis solutions is a computer vision technology called optical character recognition (OCR), which can identify the location of text in an image. OCR is often combined with an analytical model that can interpret individual values in the document, and so extract specific fields.

Data and insight extraction scenarios include automated processing of forms and other documents in a business process, large-scale digitization of data from paper forms, indexing documents for search, and identifying key points and follow-up actions from meeting transcripts or recordings.

### Document Processing
Use when the input is a document (PDF/image/scan) and you need structured extraction.

When you have scanned documents (PDFs or images) and you want to automatically extract full text (OCR), key/value pairs, and tables, you need a document understanding service designed for forms and structured documents.

Typical workflow:
- Provide a scanned document (image/PDF) to the service
- The service detects layout and runs OCR
- It returns extracted text, detected fields as key/value pairs, and extracted tables
- Your app validates and maps results into your database or business process

## Common Confusions (Choose This, Not That)

- **OCR / Document Processing vs NLP:** OCR and document processing extract text and structure from images/PDFs; NLP analyzes meaning after you have text.  
- **Document Processing vs Knowledge Mining:** document processing extracts text/fields/tables from documents; knowledge mining builds a searchable index over lots of content (often using OCR/NLP as enrichment).  
- **Speech Recognition vs Text-to-Speech:** speech recognition is **audio → text** (captions/transcripts); text-to-speech is **text → audio** (read aloud/announcements).  
- **Translator vs Speech:** Translator is **text → text** translation; Speech is used when audio is involved (speech-to-text, text-to-speech, speech translation).  
- **Computer Vision vs Anomaly Detection:** if the input is images and the goal is recognizing objects by appearance/shape, treat it as computer vision; anomaly detection is about unusual behavior compared to a normal baseline.
- **Generative AI vs Question Answering:** generative AI produces new text; question answering retrieves an answer from known content (FAQs/docs) and returns the best match.  

> [!WARNING]
> OCR, Document Processing, NLP are often chained, OCR and Document Processing extract text and structure from images or PDFs, NLP analyzes meaning after you already have text, mixing them leads to the wrong design and wrong service choice.

## Azure Mapping (Concept → Azure Service Family)

This document is Vendor-Neutral. This section maps the concepts to common Azure services so you can connect the ideas to real implementations.

In Azure, you will often see AI services presented in two layers:
- **Service Family:** the main product area that groups related AI features
- **Specific Capability:** a named feature inside that family that solves a specific problem

> [!IMPORTANT]
> Service Family is the product area, Specific Capability is the feature you actually use, keep that separation so you map concepts to the right Azure tool

Now let’s map the AI and ML concepts in this document to Azure services like **AI and ML concept → Service Family (Specific Capability Name)**:

- **Language Understanding (Intent & Entities)** → Azure AI Language (CLU: Conversational Language Understanding)  
- **Question Answering** → Azure AI Language (Question Answering)  
- **Text Analysis (Sentiment, Entities, Key Phrases, Language Detection)** → Azure AI Language (Text Analytics)  
- **Translation (Text → Text)** → Azure AI Translator (Text Translation)  
- **Speech (Speech-to-Text, Text-to-Speech, Speech Translation)** → Azure AI Speech (Speech Services)  
- **General Vision (Tags, Captions, OCR)** → Azure AI Vision (Image Analysis)  
- **Face Detection and Face Operations** → Azure AI Face (Face)  
- **Custom Vision Models (Classification, Object Detection)** → Azure AI Custom Vision (Custom Vision)  
- **Document Processing (OCR, Key/Value, Tables)** → Azure AI Document Intelligence (Document Intelligence)  
- **Knowledge Mining (Indexing, Search, Enrichment)** → Azure AI Search (Search Indexing)  
- **Training and Operationalizing ML Models** → Azure Machine Learning (Azure ML)  
- **Bots and Channels (Bot Runtime/Connector)** → Azure AI Bot Service (Bot Service)  
- **Generative AI models (GPT, embeddings, DALL-E, Whisper)** → Azure OpenAI Service (Azure OpenAI)  

### Azure OpenAI Model Types (Fast Routing)
- **GPT models**: generate or transform text (chat, summarization, extraction)  
- **Embeddings models**: convert text to vectors for semantic search and similarity  
- **DALL-E**: generate images from text prompts  
- **Whisper**: speech-to-text transcription  

## Summary

You should now be able to:
- Explain what AI, ML, Deep Learning, and Generative AI are  
- Choose an AI workload by matching your **input type** and **output need**  
- Identify **Prediction** categories (Machine Learning, Anomaly Detection)  
- Identify **Language** categories (Natural Language Processing, Conversational AI, Speech)  
- Identify **Vision** categories (Computer Vision)  
- Identify **Document** categories (Document Processing, Information Extraction, Knowledge Mining)  
- Connect vendor-neutral concepts to Azure service families using the mapping section  
- Distinguish **OCR / Document Processing** from **NLP**  
- Recognize when they are chained (OCR/Document Processing first, then NLP)  
- Use **Concept → Service Family (Specific Capability Name)** when mapping to Azure  


