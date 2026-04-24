# Language and Conversational Workloads

This document explains how language-based AI workloads differ across: text analysis, conversational understanding (**Intent & Entities**), question answering, translation, and speech.

It focuses on choosing the right capability using two questions:
- **What you start with:** Text or Audio  
- **What you need:** Extract signals, understand a command, answer from content, translate language, or transcribe speech  

It stays Vendor-Neutral first, then maps concepts to Azure in a dedicated **Azure Mapping** section.

**This Document Covers**
- Natural Language Processing (What It Is, Common Tasks)  
- Text Analytics Capabilities (Sentiment, Key Phrases, Named Entity Recognition, Language Detection)  
- Language Understanding (CLU: Intent & Entities Outputs)  
- Orchestration (Route Commands vs Questions)  
- Question Answering (Answer From Your Content)  
- Translation (Text Translation vs Speech Translation)  
- Speech (Speech-to-Text, Text-to-Speech, Speech Translation)  
- Common Confusions (Choose This, Not That)  
- Azure Mapping (Concept → Azure Service Family)  
- Summary  


## Natural Language Processing (What It Is, Common Tasks)  
Natural Language Processing (NLP) applies when the input is text and the goal is to analyze or work with language.  

Common NLP tasks include:  
- Sentiment analysis (positive/negative/neutral tone)  
- Key phrase extraction (main talking points)  
- Entity recognition (people, organizations, locations, dates, quantities)  
- Language detection (identify the language of the text)  
- Summarization (when available)  

NLP shows up in scenarios like analyzing customer reviews, extracting key topics from reports, tagging content with mentioned organizations or locations, and preparing text for search and indexing.  

> [!NOTE]  
> NLP works on text. If your input is a scanned image or PDF, you usually need OCR or document processing first to extract text, then you can run NLP on the extracted text.  

**Language Workload Router (Pick The Right Capability)**  
- If you need **key phrases, sentiment, language detection, entity recognition** → **Text Analytics**  
- If you need **intents & slots from user messages** → **CLU**  
- If you need **answers from a knowledge base** → **Question Answering**  
- If you need **translate text or speech** → **Translation**

## Text Analytics Capabilities (Sentiment, Key Phrases, Entities, Language Detection)  
Text analytics capabilities help you extract useful signals from text so it can be searched, categorized, routed, or summarized for humans.

**NLP** defines the big category “NLP”, meaning any work where the input is text and you’re doing language tasks. 

**Text Analytics** is a subset of NLP, it lists common “extract signals from text” capabilities (sentiment, key phrases, entities, language detection). 

So both say “this is for text”, because both are in the same family.

> [!NOTE]  
> Text Analytics is a set of **NLP** capabilities for extracting signals from text. Like all **NLP**, it requires text input, so use OCR or document processing first for scanned documents.

### Key Phrase Extraction  
Key phrase extraction pulls out the main talking points from a document or message.  
Use it when you want to quickly understand what a text is mostly about, or compare documents by their topics.  
**Study note:** If you need the main talking points, use key phrase extraction.  

### Entity Recognition (NER)  
Entity recognition finds named things in text, like people, organizations, locations, dates, and quantities.  
Use it when you want to tag content (for example, “mentions Microsoft” or “mentions London”) or enable filters in search.  
**Study note:** “Extract people and locations from articles” is NER.  

Use NER when you need to extract entities from written content like articles, reports, or messages so you can classify, tag, filter, or search that content later.
Use it when you want to classify content, build recommendations, or enable search and filtering based on mentioned people, organizations, or places.  


Examples:
- Extract people and locations from news articles
- Tag documents that mention Microsoft or London
- Build filters like **articles mentioning a company or city**

**Study note:** If the task is “extract people, organizations, or locations from articles,” that is **NER**, not CLU.


### Sentiment Analysis  
Sentiment analysis estimates the tone of text, usually positive, negative, or neutral.  
Use it on reviews, survey feedback, and support messages when you care about how people feel.  

### Language Detection  
Language detection identifies the language of the input text so you can route it to the right workflow (for example, translation or region-specific handling).  
It commonly returns the language name, an ISO 639-1 code, and a confidence score.  
**Study note:** Language detection outputs language name, ISO code, and score.  

## Language Understanding (Intent & Entities)  
When you need to interpret what a user means in a message like “Call me back later,” you are doing language understanding (often modeled as intent and entities).  

**Common entity extraction approaches:**  
- Learned entities: extracted from labeled examples and context  
- List entities: matched from known values  
- Prebuilt entities: recognized entity types provided by the service

Typical outputs:  
- Intent: what the user wants to do  
- Entities: important details inside the text  

Example:  
User says: “Play Blinding Lights by The Weeknd on the living room speaker.”  
- Intent: PlayMusic  
- Entities: SongName = “Blinding Lights”, Artist = “The Weeknd”, DeviceName = “living room speaker”  

A key point is that the language understanding model does not perform the action. It produces structured understanding so your app or bot can call the right APIs.  

**When CLU is the right choice**  
Use CLU when the user message is a **command or request** and your system must decide **what action to take**.

Examples:
- **Book a meeting tomorrow at 3**
- **Open ticket for billing**
- **Play jazz music**
- **Track my package**

**Study note:** CLU is for **understanding a user command**, not for answering from knowledge content and not for performing the action itself.

## Question Answering (Answer From Your Content)  
Question Answering is used when the user is asking for information and the answer should come from known content. It creates a conversational layer over your data to return the best-matching answer.  

### What You Feed It (Inputs / Sources)  
A Question Answering knowledge base can be created from three main source types:  
- Web pages (URLs)  
- Documents or FAQ files (content that contains question and answer pairs)  
- Manual Q&A entry (type question and answer pairs directly)  

### What It Outputs  
- Best-matching answer  
- Optional score or confidence (depends on settings and implementation)  

### Important Limitation  
You cannot directly import an image or an audio file as a knowledge base source. You would first need to extract text or transcripts into a supported text-based source.  

## Orchestration (Routing Between Intents and Question Answering)  
In real bots, users mix commands and questions. A common pattern is to route each message to either language understanding (intent and entities) or question answering (answer from content).  

A simple way to think about it:  
- If the message is “Do something” → route to language understanding (intent and entities)  
- If the message is “Tell me something” → route to question answering  
- If it is unclear or ambiguous → ask one short clarifying question, then route  

Example:  
- “Reset my password” is a request to do something, so it routes to intent and entities.  
- “What is your return policy?” is asking for information, so it routes to question answering.  

> [!NOTE]  
> Orchestration is about choosing the right path for each user message, it is not a single capability that replaces intent models or question answering.  


## Translation (Text vs Speech Translation)  
To support multilingual translation scenarios, choose the capability based on what format you start from.  

- Translator is used for text-to-text translation (convert written text between languages).  
- Speech is used for speech-related scenarios, including speech-to-text (transcription) and speech translation workflows.
- Use Translator when the input is text, the output should be translated text, and you want multilingual experiences in apps, websites, or workflows.  

A simple decision rule:  
- Text → Text translation: Translator  
- Audio → Text transcription: Speech to text  
- Text → Audio voice: Text to speech  
- Audio → Translated text or voice: Speech translation  

> [!NOTE]  
> Language detection can help you route text to the right translation workflow, but it is not the translation engine.

## Speech (Speech-to-Text, Text-to-Speech)  
Speech capabilities apply when the input or output involves spoken audio.  

Common Speech capabilities include:  
- Speech to text (transcription)  
- Text to speech (speech synthesis)  
- Speech translation (real-time multilingual translation of audio streams)


### Speech Recognition (Speech-to-Text)  
Speech recognition converts audio into text.  
Common uses include captions, transcripts, and turning spoken requests into text that can be processed by downstream language workflows.  

### Speech-to-Text: Universal Language Model (when to use it)
Use the Universal Language Model for general-purpose speech recognition scenarios, such as:
- **Conversation transcription**
- **Dictation**
- Mixed speakers and natural speech patterns

### Speech Synthesis (Text-to-Speech)  
Speech synthesis converts text into spoken audio.  
Common uses include reading messages aloud, automated announcements, and voice responses in assistants.  

> [!NOTE]  
> Speech recognition is audio → text, and text-to-speech is text → audio.  

## Common Confusions (Choose This, Not That)  
- Translator vs Speech: Translator is text → text translation, Speech is used when audio is involved (speech-to-text, text-to-speech, speech translation).  
- Speech recognition vs text-to-speech: speech recognition is audio → text (captions/transcripts), text-to-speech is text → audio (read aloud/announcements).  
- Question Answering vs language understanding: question answering returns information from known content, intent and entities interpret commands so your app can take action.  
- Entity Recognition (NER) vs CLU entities: NER extracts named things from text for analysis, CLU entities extract details from a user command to complete an action.  
- Text Analytics vs Question Answering: Text Analytics extracts signals (sentiment, entities, key phrases), Question Answering returns an answer from your curated content.  
- Language detection vs translation: language detection identifies the language, it does not translate.  
- Key phrase extraction vs entity recognition: key phrases are main topics/talking points, entities are named things (people, orgs, places, dates).  
- Transcription vs summarization: speech-to-text creates a transcript, summarization is an NLP step you do after you have text.
- CLU vs NER: CLU is for understanding **what the user wants to do** and extracting action details from a command; NER is for extracting named things from text for analysis or tagging.
- Question Answering vs CLU: Question Answering is for returning an answer from known content; CLU is for routing command-style messages to the correct action.
- NER is not a replacement for CLU: NER can extract named things from text, but it does not decide the user’s intended action.  
- Translator vs language detection: language detection tells you **what language the text is in**; Translator changes the text into another language.
- Translator vs CLU: Translator changes language, it does not identify intent.  
- Speech vs CLU: Speech converts spoken audio to or from text, it does not determine user intent.  

> [!IMPORTANT]
> **Entity means two different things here.**
> **NER entities** are named things in text (people, orgs, places, dates).
> **CLU entities** are slots in a user intent (the details your app needs to act, like destination, date, product).


## Azure Mapping (Concept → Azure Service Family)  
This document is Vendor-Neutral. This section maps the concepts in this document to common Azure services so you can connect the ideas to real implementations.  

Now let’s map the language concepts in this document to Azure services like **Concept → Service Family (Specific Capability Name)**:  
- **Natural Language Processing (NLP)** → Azure AI Language (Language Services)  
- **Text Analysis (Sentiment, Entities, Key Phrases, Language Detection)** → Azure AI Language (Text Analytics)  
- **Language Understanding (Intent & Entities)** → Azure AI Language (CLU: Conversational Language Understanding)  
- **Question Answering** → Azure AI Language (Question Answering)  
- **Translation (Text → Text)** → Azure AI Translator (Text Translation)  
- **Speech (Speech-to-Text, Text-to-Speech, Speech Translation)** → Azure AI Speech (Speech Services)  
- **Bots and Channels (Bot Runtime/Connector)** → Azure AI Bot Service (Bot Service)  

## Summary  
You should now be able to:  
- Explain what NLP means and recognize when the input is text and the goal is to analyze language.  
- Use Text Analytics capabilities like sentiment analysis, key phrase extraction, entity recognition, and language detection, and know what each one returns.  
- Explain language understanding as intent and entities, and how it supports command-style experiences.  
- Explain Question Answering as returning answers from known content and list the supported knowledge base sources.  
- Use orchestration rules to route “do something” messages to intent and entities, and “tell me something” messages to question answering.  
- Choose Translator vs Speech by the input type (text vs audio) and apply the translation and speech decision rules.  
- Recognize common confusions like language detection vs translation and transcription vs summarization.  
- Map the document concepts to Azure service families and specific capabilities (Text Analytics, CLU, Question Answering, Translator, Speech, Bot Service).  

