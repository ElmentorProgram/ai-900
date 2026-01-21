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
