# AI and ML Foundations

This document gives you a stable mental map of the most common AI workloads and the core terms you’ll reuse across the repo. It helps you choose the right workload by matching what you have (**input**) to what you need (**output**), then connects those workload choices to Azure services in a compact mapping section.

It’s designed to stay **consistent and reusable**: The workload order and labels here are the same ones used in later docs, so your understanding builds layer by layer.

**This Document Covers**
- Core Definitions  
- Common AI Workloads (How to Choose)  
- Workload Landscape (Quick Map)  
- Workloads and What They Do  
- Common Confusions (Choose This, Not That)  
- Azure Mapping (Concept → Azure Service Family)  
- Summary  

## Core Definitions

Core definitions are here to lock the mental model early. Treat each line as a **label → meaning** anchor you will reuse across the rest of the docs, so the same terms keep the same meaning everywhere.

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

Start with two questions. A workload is the type of AI task or problem you are trying to solve, such as vision, language, document extraction, speech, or ML prediction. You choose it by matching the data you have to the output you need.

What is the **input**?

- Images → **Computer Vision**, **Document Processing** (OCR), or **Information Extraction**
- Video → **Computer Vision**, **Speech**, or **Information Extraction**
- Scanned Documents → **Document Processing** (OCR, Fields, Tables) or **Information Extraction**
- Text/Documents → **Natural Language Processing (NLP)**, **Knowledge Mining**, or **Generative AI**
- Audio/Speech → **Speech**, **Conversational AI**, or **Information Extraction**
- Conversations (Chat) → **Conversational AI** or **Generative AI**
- Time-Series/Telemetry/Transactions → **Regression**, **Classification**, **Clustering**, or **Anomaly Detection**

What is the **output**?

- A Number → **Regression**
- A Label/Category → **Classification**
- Groups/Segments → **Clustering**
- Unusual/Rare Events → **Anomaly Detection**
- Extracted Text/Fields/Tables → **Document Processing**
- Extracted Facts/Actions/Insights → **Information Extraction**
- Searchable Results From Lots of Content → **Knowledge Mining**
- Generated Text/Content → **Generative AI**
- Answer a User in Chat → **Conversational AI**
- Transcribed or Spoken Language → **Speech**

The same input can support different workloads depending on the output you need.

If the **text** is inside an image or scanned document, you usually need **Document Processing** before **NLP**.

> [!IMPORTANT]  
> Start from the workload, input type, and output need, then map to the service. Do not start from the Azure service name and work backwards.

## Workload Landscape (Quick Map)

This is a wide-map view of the major AI workloads. The goal is to build a strong mental model first, then go deeper later. The simplest way to read the landscape is to treat each workload as part of a broader problem family.

- **Regression** (Prediction)
- **Classification** (Prediction)
- **Clustering** (Prediction)
- **Anomaly Detection** (Prediction)
- **Natural Language Processing and Text Analysis** (Language and Search)
- **Knowledge Mining** (Language and Search)
- **Generative AI** (Language and Search)
- **Conversational AI** (Language and Search)
- **Speech** (Voice)
- **Computer Vision** (Vision)
- **Information Extraction** (Docs)
- **Document Processing** (Docs)


## Workloads and What They Do

This section is a quick tour of the major AI workloads. The goal is to give each workload a consistent, high-signal description so you can recognize it and avoid common confusion. Later documents go deeper into each workload, but the order and mental map stay the same.

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
- Typical flow: Data source → indexing → enrichment → search index → query  
- Enrichment often uses OCR (for documents/images) and NLP signals (entities, key phrases)  
- Output is searchable fields and ranked results  

### Generative AI Scenarios

Common uses of generative AI include implementing AI agents that assist human users by providing information or automating tasks.  
It is also used for creating new documents or other content, automated translation of text between languages, and summarizing or explaining complex documents.

Generative AI focuses on producing new content from prompts (most commonly text, but also other formats).  
Use it when you want the model to generate or transform content rather than only classify, extract, or search.

**Highlights**
- Common uses include content generation, summarization, explanation, and translation  
- Often used in assistants/agents to help users complete tasks  
- Output is generated content (not just retrieved text from a source)  
- Prompts guide what the model generates and how it responds  

### Conversational AI

Use when the system must interact with users through chat or voice.  
The goal is to interpret user messages and respond appropriately using common conversational patterns.

A conversational system often either understands what the user wants to do or answers questions from known content.  
If it is unclear what the user wants, the system can ask one short clarifying question, then choose the right pattern.

**Highlights**
- Two common patterns are **Language Understanding (Intent & Entities)** and **Question Answering**  
- Use Language Understanding when the message is **do something** (intent + entities)  
- Use Question Answering when the message is **tell me something** (answer from known content)  
- When unclear, ask one clarifying question, then route to the right pattern  

### Speech

Speech capabilities enable users to interact with AI applications and agents through spoken language.  
Use it when audio is involved and you need to convert between speech and text or generate spoken output.

Speech recognition converts spoken audio into text (speech-to-text).  
Speech synthesis converts text into spoken audio (text-to-speech).

**Highlights**
- **Speech-to-Text:** Transcribe calls/meetings, captions, voice input for agents  
- **Text-to-Speech:** Read content aloud, voice responses from assistants  
- **Speech Translation:** Translate spoken language between languages  
- Common scenarios include spoken agents, transcription, and real-time voice experiences  

### Computer Vision

Computer vision analyzes visual input such as photographs, videos, and live camera feeds.  
Use it when the input is visual and you want labels, locations, or pixel-level understanding.

Computer vision models are trained on large numbers of images to learn visual patterns.  
Different model types are used depending on whether you need classification, detection, or segmentation.

**Highlights**
- **Image Classification:** Predict the most appropriate label for an image  
- **Object Detection:** Identify the location of specific objects in an image  
- **Semantic Segmentation:** Identify the pixels that belong to a particular object  
- **Multi-modal Models:** Combine visual features with text to generate richer descriptions  

### Information Extraction

Information extraction automates finding information and unlocking insights in unstructured sources such as scanned documents and forms, images, and audio or video recordings.  
Use it when you want to pull useful fields, facts, or action items out of content that is not already structured.

The basis for many document analysis solutions is optical character recognition (OCR), which identifies the location of text in an image.  
OCR is often combined with a model that interprets values in the content so you can extract specific fields.

**Highlights**
- Common inputs include scanned forms/documents, images, and audio/video recordings  
- OCR is a common foundation when text is inside images or scans  
- The goal is extracting usable fields or insights for downstream systems  
- Scenarios include business form processing, digitization, indexing for search, and extracting follow-up actions from transcripts  

### Document Processing

Use when the input is a document (PDF/image/scan) and you need structured extraction.  
This workload focuses on extracting full text (OCR), key/value pairs, and tables from documents so the results can be used in business processes.

A typical workflow is to provide a scanned document, then the service detects layout and runs OCR to extract text and structure.  
It returns extracted text, detected fields (key/value pairs), and extracted tables that your app validates and maps into downstream systems.

**Highlights**
- Use when you need structured extraction from documents (text, fields, tables)  
- OCR & layout understanding are key building blocks for document results  
- Output is structured results you can validate and store (not just raw text)  
- Common scenarios include forms processing and automating document-heavy workflows  

## Common Confusions (Choose This, Not That)

These are the confusion points that cause most wrong workload choices. Use this list as a fast check: if two options feel similar, match them by **input type** and **output need**, and remember that some workloads are commonly chained (for example: **OCR/Document Processing** first, then **NLP**).

- **OCR / Document Processing vs NLP:** OCR and document processing extract text and structure from images/PDFs; NLP analyzes meaning after you have text.  
- **Document Processing vs Knowledge Mining:** Document Processing extracts text/fields/tables from documents; Knowledge Mining builds a searchable index over lots of content (often using OCR/NLP as enrichment).  
- **Speech Recognition vs Text-to-Speech:** Speech Recognition is **audio → text** (captions/transcripts); Text-to-Speech is **text → audio** (read aloud/announcements).  
- **Translator vs Speech:** Translator is **text → text** translation; Speech is used when audio is involved (speech-to-text, text-to-speech, speech translation).  
- **Computer Vision vs Anomaly Detection:** If the input is images and the goal is recognizing objects by appearance/shape, treat it as Computer Vision; Anomaly Detection is about unusual behavior compared to a normal baseline.  
- **Generative AI vs Question Answering:** Generative AI produces new content; Question Answering retrieves an answer from known content (FAQs/docs) and returns the best match.
- **Text Translation vs Speech Translation**: Use **Translator** when the input is text and the output is translated text. Use **Speech** when audio is involved, such as transcription, text-to-speech, or spoken translation.

> [!WARNING]
> OCR, Document Processing, NLP are often chained, OCR and Document Processing extract text and structure from images or PDFs, NLP analyzes meaning after you already have text, mixing them leads to the wrong design and wrong service choice.

## Azure Mapping (Concept → Azure Service Family)

This document is Vendor-Neutral. This section is a compact map from the workloads and concepts above to common Azure service families, so you can connect the ideas to real implementations without starting from product names.

In Azure, you will often see AI services presented in two layers:
- **Service Family:** The main product area that groups related AI features  
- **Specific Capability:** A named feature inside that family that solves a specific problem  

> [!IMPORTANT]
> Service Family is the product area, Specific Capability is the feature you actually use, keep that separation so you map concepts to the right Azure tool

Now let’s map the AI and ML concepts in this document to Azure services like **AI and ML concept → Service Family (Specific Capability Name)**:

- **Regression** → Azure Machine Learning (Azure ML)  
- **Classification** → Azure Machine Learning (Azure ML)  
- **Clustering** → Azure Machine Learning (Azure ML)  
- **Anomaly Detection** → Azure Machine Learning (Azure ML)  
- **Natural Language Processing and Text Analysis** → Azure AI Language (Text Analytics)  
- **Knowledge Mining** → Azure AI Search (Search Indexing)  
- **Generative AI models (GPT, Embeddings, DALL-E, Whisper)** → Azure OpenAI Service (Azure OpenAI)  
- **Language Understanding (Intent & Entities)** → Azure AI Language (CLU: Conversational Language Understanding)  
- **Question Answering** → Azure AI Language (Question Answering)  
- **Translation (Text → Text)** → Azure AI Translator (Text Translation)  
- **Speech (Speech-to-Text, Text-to-Speech, Speech Translation)** → Azure AI Speech (Speech Services)  
- **General Vision (Tags, Captions, OCR)** → Azure AI Vision (Image Analysis)  
- **Face Detection and Face Operations** → Azure AI Face (Face)  
- **Custom Vision Models (Classification, Object Detection)** → Azure AI Custom Vision (Custom Vision)  
- **Information Extraction** → Azure AI Document Intelligence (Document Intelligence)  
- **Document Processing (OCR, Key/Value, Tables)** → Azure AI Document Intelligence (Document Intelligence)  
- **Bots and Channels (Bot Runtime/Connector)** → Azure AI Bot Service (Bot Service)  

## Azure OpenAI Model Types

This section is a fast routing guide for choosing the right model category inside **Azure OpenAI Service** after you already know that Azure OpenAI is the right service family for your scenario.

- **GPT Models** → Generate or transform text, such as chat, summarization, extraction, and rewriting
- **Embedding Models** → Convert text to vectors for semantic search, retrieval, and similarity
- **Image Generation Models** (**DALL-E**, now typically **gpt-image**) → Generate images from prompts
- **Audio Models** (**Whisper**) → Transcribe speech and handle audio-based generation tasks


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


