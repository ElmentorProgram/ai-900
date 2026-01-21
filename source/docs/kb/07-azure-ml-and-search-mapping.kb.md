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
