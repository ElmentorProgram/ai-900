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

