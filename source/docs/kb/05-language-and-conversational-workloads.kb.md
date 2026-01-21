# Language and Conversational Workloads

This document explains how language-based AI workloads differ, including text analysis, language understanding (intent & entities), question answering, translation, and speech. It focuses on how to choose the right capability based on your input (text or audio) and what you want the system to do (analyze text, answer from content, route a command, translate, or transcribe). It stays Vendor-Neutral, then maps key concepts to Azure where helpful.

**This Document Covers**  
- Natural Language Processing (What It Is, Common Tasks)  
- Text Analytics Capabilities (Sentiment, Key Phrases, Entities, Language Detection)  
- Language Understanding (Intent & Entities)  
- Question Answering (Answer From Your Content)  
- Orchestration (Routing Between Intents and Question Answering)  
- Translation (Text vs Speech Translation)  
- Speech (Speech-to-Text, Text-to-Speech)  
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

### Sentiment Analysis  
Sentiment analysis estimates the tone of text, usually positive, negative, or neutral.  
Use it on reviews, survey feedback, and support messages when you care about how people feel.  

### Language Detection  
Language detection identifies the language of the input text so you can route it to the right workflow (for example, translation or region-specific handling).  
It commonly returns the language name, an ISO 639-1 code, and a confidence score.  
**Study note:** Language detection outputs language name, ISO code, and score.  

## Language Understanding (Intent & Entities)  
When you need to interpret what a user means in a message like “Call me back later,” you are doing language understanding (often modeled as intent and entities).  

Typical outputs:  
- Intent: what the user wants to do  
- Entities: important details inside the text  

Example:  
User says: “Play Blinding Lights by The Weeknd on the living room speaker.”  
- Intent: PlayMusic  
- Entities: SongName = “Blinding Lights”, Artist = “The Weeknd”, DeviceName = “living room speaker”  

A key point is that the language understanding model does not perform the action. It produces structured understanding so your app or bot can call the right APIs.  


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

A simple decision rule:  
- Text → Text translation: Translator  
- Audio → Text transcription: Speech to text  
- Text → Audio voice: Text to speech  
- Audio → Translated text or voice: Speech translation  

> [!NOTE]  
> Language detection can help you route text to the right translation workflow, but it is not the translation engine.

## Speech (Speech-to-Text, Text-to-Speech)  
Speech capabilities apply when the input or output involves spoken audio.  

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

