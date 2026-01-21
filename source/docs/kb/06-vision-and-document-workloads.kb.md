# Vision and Document Workloads

This document explains how vision and document workloads differ, and how to choose the right capability based on your input (images, video, scanned documents) and what you want the system to return (tags, captions, detected objects, extracted text, extracted fields, tables). It stays Vendor-Neutral, then maps key concepts to Azure where helpful.

**This Document Covers**  
- Computer Vision (What It Is, Common Outputs)  
- Image Classification vs Object Detection vs Semantic Segmentation  
- OCR vs Document Processing (Text, Key/Value, Tables)  
- Face Detection vs Face Verification (Identity vs Attributes)  
- Custom Vision (When You Need Your Own Labels)  
- Common Confusions (Choose This, Not That)  
- Azure Mapping (Concept → Azure Service Family)  
- Summary  

## Computer Vision (What It Is, Common Outputs)  
Computer vision is the area of AI that deals with analyzing visual input like photos, video, and camera feeds. The goal is to return structured results that your system can use, for example labels, locations, text, or descriptions.  

Common outputs you will see from vision systems include:  
- **Tags:** descriptive keywords about what is in the image (objects, setting, attributes).  
- **Caption/description:** a short sentence-like description of what is happening in the image.  
- **Image classification:** a label for the whole image (or a main label).  
- **Object detection:** labels plus bounding boxes, so you get what was found and where it is.  
- **OCR:** extracted printed or handwritten text found inside the image.  
- **Semantic segmentation:** a class label for each pixel (a mask), used when precise boundaries matter.  

> [!NOTE]  
> These outputs answer different questions. Choose the capability by the output you need, not by the input alone. For example, “find bottles” is object detection, while “read the sign” is OCR.  

## Image Classification vs Object Detection vs Semantic Segmentation  
These three vision tasks produce different outputs, so you choose based on what your system must return.  

### Image Classification  
Image classification assigns a label to the whole image (or the main label).  
Use it when the entire image represents one thing you care about and you do not need locations.  
Example: classify an X-ray image into a fracture type, or classify a product photo as Product A vs Product B.  

### Object Detection  
Object detection finds objects in an image and returns labels plus bounding boxes.  
Use it when location matters, multiple items can appear, or you need counts.  
Example: detect all bottles on a conveyor and label their type, or detect multiple vehicles in a traffic camera image.  

### Semantic Segmentation  
Semantic segmentation labels each pixel, producing a mask instead of a bounding box.  
Use it when precise shape or boundaries matter, not just a rectangle.  
Example: highlight the exact defective region on a surface, or separate a product from the background precisely.  

> [!IMPORTANT]  
> Classification answers “what is in this image”, detection answers “what and where (box)”, segmentation answers “what and where (pixels)”.  

## OCR vs Document Processing (Text, Key/Value, Tables)  
OCR (Optical Character Recognition) is used when you need to read printed or handwritten text that appears inside an image or scanned document. It turns “text in pixels” into machine-readable text, so you can store it, search it, or pass it to NLP later.  

Document processing goes beyond OCR. It uses layout understanding to extract structured data from documents, such as key/value pairs and tables, not just raw text.  

How to choose:  
- Use OCR when you mainly need the text content (for example, make scanned pages searchable).  
- Use document processing when you need structured fields (Invoice Number, Date, Total) and tables (line items).  

Example (expense receipt scanning):  
- If you only need the receipt text for search, OCR is enough.  
- If you need merchant, date, total, and line items as structured fields, use document processing (OCR + layout understanding).  

> [!IMPORTANT]  
> OCR answers “what text is on the page.” Document processing answers “what text is on the page, and what it means structurally (fields and tables).”  

## Face Detection vs Face Verification (Identity vs Attributes)  
Face scenarios often sound similar, but they are different tasks depending on whether you need to detect faces, read attributes, or match identity.  

### Face Detection (Find Faces and Their Attributes)  
Face detection answers questions like:  
- “Is there a face in this image?”  
- “How many faces are there, and where are they located?”  

In many solutions, face detection can also return face-related attributes, depending on the capability used. For example, accessories like glasses or sunglasses.  

Example (faces and sunglasses rule):  
If you want to automatically keep only photos that:  
- include one or more faces, and  
- include at least one person wearing sunglasses,  
then you are doing face detection and reading face-related attributes, so you can apply a rule like:  
“Face count ≥ 1” AND “At least one detected face indicates sunglasses.”  

### Face Verification (Match Two Faces, Same Person or Not)  
Face verification answers a different question:  
- “Are these two faces the same person?”  

Verification is used for identity matching (one face compared to another), not for counting faces or checking accessories like sunglasses.  

> [!IMPORTANT]  
> Face detection is for finding faces (and sometimes attributes). Face verification is for matching identity.  

> [!WARNING]  
> If your goal is “detect faces and check sunglasses,” verification is the wrong task type. It will not reliably answer “who is wearing sunglasses” or “how many faces are present.”  
