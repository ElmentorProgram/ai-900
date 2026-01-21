# Azure Mapping: ML, Search, and Services Reference

This document is a Vendor-Neutral reference that maps the core concepts from the repo to common Azure service families and their key capabilities. Use it as a fast “which Azure service fits this concept” guide, not as a full product manual.  

**This Document Covers**  
- How To Read This Mapping (Concept → Service Family, Capability)  
- Machine Learning (Training, Evaluation, Deployment)  
- Azure Machine Learning (Designer, AutoML, Jobs, Endpoints)  
- Knowledge Mining (Search, Indexing, Enrichment)  
- Language Workloads (Text Analytics, CLU, Question Answering)  
- Speech and Translation  
- Vision, Face, and Custom Vision  
- Document Processing (OCR, Key/Value, Tables)  
- Summary  

## How To Read This Mapping (Concept → Service Family, Capability)  
In Azure, you will often see AI services presented in two layers:  
- Service Family: the main product area that groups related AI features.  
- Specific Capability: a named feature inside that family that solves a specific problem.  

This document uses the format:  
Concept → Service Family (Specific Capability Name)  

Example:  
- Language Understanding (Intent & Entities) → Azure AI Language (CLU: Conversational Language Understanding)  

Naming notes (AKA, older names you may still see):  
- **LUIS (Language Understanding Intelligent Service)** is the older name you may still see for intent and entities, Microsoft guidance points to **Azure AI Language, CLU (Conversational Language Understanding)** as the current service.  
- **QnA Maker** is the older name you may still see for FAQ-style responses from your content, the current service is **Azure AI Language, Question Answering** (you may also see “Custom Question Answering” in some materials).  
- **Form Recognizer** is the older name you may still see for extracting text, key/value pairs, and tables from documents, the current name is **Azure AI Document Intelligence**.  

> [!NOTE]  
> This is a reference guide. It maps common concept names to common Azure names (including older names you may still see), it does not cover every configuration choice.  

## Machine Learning (Training, Evaluation, Deployment)  
This section is only a bridge from Vendor-Neutral lifecycle concepts to the Azure places you will see them. It does not re-explain the lifecycle.  

You will commonly map these ML lifecycle concepts to Azure terms like:  
- **Training** → training runs and experiments (Azure ML training jobs)  
- **Evaluation** → metrics produced during validation/testing (model evaluation outputs)  
- **Inference (scoring)** → running a trained model on new inputs (scoring)  
- **Deployment** → publishing the model behind a hosted interface (endpoint)  

> [!IMPORTANT]
> Training happens on historical labeled data (when supervised), inference happens later on new inputs. Evaluation measures how well the model generalizes to unseen examples.

> [!NOTE]  
> The next sections list the Azure service families and the concrete capability names you will see for these concepts (Designer, AutoML, Jobs, Endpoints).  

## Azure Machine Learning (Designer, AutoML, Jobs, Endpoints)  
This section maps common ML build and deployment concepts to Azure Machine Learning terms you will see in practice.  

### Azure ML (Core)  
- **Train a model in Azure ML Studio** → create and run a **job**.  
- A **workspace** is the container you need to use Azure ML Studio, but it is not the thing you run to train a model.  
- **ACI** and **AKS** are primarily deployment targets (after training), not what you create first to train the model.  

### Azure ML Designer (Visual Pipelines)  
- **Designer** is a drag-and-drop way to build an ML workflow as a visual graph.  
- You start by creating a **pipeline**, then add **datasets** and **modules** to build the workflow.  
- To create training and validation subsets from a dataset, use **Split Data** (splits rows into two outputs).  

### Automated ML (AutoML)  
AutoML automates repeated experimentation to find a strong model for your data. In an AutoML experiment, you typically configure:  
- The **label/target column**  
- The **target metric** (what AutoML optimizes)  
- Limits/stop conditions (time, maximum iterations)  
- Validation settings (how models are evaluated during training)  

### Deployment and Endpoints (Inference)  
- To make a trained model usable by applications, deploy it to an **endpoint**.  
- To call a deployed inference service, you need the **REST endpoint** (service URL) and an **authentication key**.  

> [!IMPORTANT]  
> Training builds the model, inference uses the model to score new data. When a question asks how to call a deployed model, you are in the inference endpoint world (REST endpoint + key).  

## Knowledge Mining (Search, Indexing, Enrichment)  
Knowledge mining is used when the primary goal is to make large volumes of content searchable. The core idea is: build an index you can query, and enrich content so it becomes easier to search and filter.  

In Azure, this commonly maps to:  
- **Knowledge mining (search & indexing at scale)** → Azure AI Search (Search indexing)  
- **Indexers** → automated ingestion from data sources into a search index  
- **AI enrichment (skills)** → extract and enrich content during indexing, for example:  
  - OCR text extraction from documents and images  
  - Entity recognition and key phrase extraction for better search filters and retrieval  

> [!NOTE]  
> Computer vision can extract text/tags from a single image, but knowledge mining is about building a searchable index across lots of content (documents, images, metadata) so you can query it at scale.  

## Language Workloads (Text Analytics, CLU, Question Answering)  
This section maps common language concepts to Azure AI Language capabilities.  

Concept → Service Family (Specific Capability Name)  
- **Text Analytics (Sentiment, Key Phrases, Entities, Language Detection)** → Azure AI Language (Text Analytics)  
- **Language Understanding (Intent & Entities)** → Azure AI Language (CLU: Conversational Language Understanding)  
- **Question Answering (Answer From Your Content)** → Azure AI Language (Question Answering)  

Naming notes (AKA, older names you may still see):  
- **LUIS (Language Understanding Intelligent Service)** is the older name you may still see for intent and entities, Microsoft guidance points to **Azure AI Language, CLU** as the current service.  
- **QnA Maker** is the older name you may still see for this capability, the current service is **Azure AI Language, Question Answering** (you may also see “Custom Question Answering” in some materials).  

> [!IMPORTANT]  
> Text Analytics is a set of NLP capabilities for extracting signals from text. Like all NLP, it requires text input, so use OCR or document processing first for scanned documents.  

## Speech and Translation  
This section maps speech and translation concepts to Azure service families.  

Concept → Service Family (Specific Capability Name)  
- **Translation (Text → Text)** → Azure AI Translator (Text Translation)  
- **Speech-to-Text (Audio → Text)** → Azure AI Speech (Speech to text)  
- **Text-to-Speech (Text → Audio)** → Azure AI Speech (Text to speech)  
- **Speech Translation (Audio → Translated text/voice)** → Azure AI Speech (Speech translation)  

> [!IMPORTANT]  
> Choose by input and output. Translator is text-to-text. Speech is used when audio is involved (speech-to-text, text-to-speech, speech translation).  

Example (speech-to-speech translation):  
A user speaks Spanish, and you want the system to reply in English audio. That typically means:  
1) **Speech-to-text**: convert the Spanish audio into Spanish text.  
2) **Translation**: translate Spanish text into English text.  
3) **Text-to-speech**: convert the English text into English audio.  

> [!NOTE]  
> Even when a service offers “speech translation,” you can still think of it as these steps under the hood: speech recognition, translation, then speech synthesis.  

What this means (capability and ML type):  
- **Speech-to-text** is a **Speech AI capability**. ML type: supervised learning on labeled audio transcripts (the model learns audio-to-text patterns).  
- **Translation (text-to-text)** is an **NLP capability**. ML type: supervised learning on bilingual text pairs (the model learns language-to-language mappings).  
- **Text-to-speech** is a **Speech AI capability**. ML type: supervised learning on text and voice/audio pairs (the model learns text-to-audio generation).  

So “speech-to-speech” is usually **multiple capabilities chained together**, each one solving a different task (audio → text, text → text, text → audio).  
