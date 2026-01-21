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

> [!WARNING]
> **DALL-E = Image Generation (text → new image).**
> It does **not** analyze an existing image (no captioning, no OCR, no object detection).
> If the task is **“what’s in this image?”** or **“read text from this image”**, use **Computer Vision** (and **OCR/Document Intelligence** for documents).

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

> [!IMPORTANT]
> **Low-resolution or poor scans can break extraction.**
> Even if the service returns a value, it can be wrong (blur, skew, shadows, handwriting, cut-off pages).
> **After extraction and before using the value in your app or in another model, validate critical fields** (totals, IDs, dates) using rules and/or human review.
>
> **Practical pipeline (high-signal):**
> OCR extracts text → Validate the extracted text → Document processing/Document Intelligence

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

> [!WARNING]
> **Face verification answers only: are these two faces the same person?**
> It is **not** used for counting people, detecting accessories, estimating age/emotion, or recognizing celebrities.
> If the task is detecting objects/attributes in an image, use **Computer Vision** (or other vision capabilities), not Face verification.

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

## Custom Vision (When You Need Your Own Labels)  
Sometimes “general vision” outputs like tags or captions are not specific enough. If you need the system to recognize your own categories (your product types, competitor SKUs, defect categories), you typically need a custom vision model trained on your labeled examples.  

There are two common custom vision outputs:  
- **Image classification:** assign one main label to the whole image (or multiple labels, depending on how you design it).  
- **Object detection:** find and label items with bounding boxes, used when multiple items can appear or location matters.  

Example (retail competitor products):  
If the goal is to identify specific competitor products from retail shelf images, generic tags like “bottle” or “snack” are not enough. You collect and label images of the products under real store conditions (lighting, angles, occlusion), then train a model to classify the image or detect multiple products on a shelf.  

> [!IMPORTANT]  
> If you need your own labels and consistent identification of specific products, use a custom vision model. General captions and tags are usually too broad for SKU-level identification.  

> [!WARNING]  
> Custom models learn what you show them. If your training images do not match real conditions (lighting, distance, clutter), accuracy will drop in production.  

## Common Confusions (Choose This, Not That)  
- Computer vision vs document processing: computer vision is for understanding what is in images (classification, detection, tags, captions), document processing is for extracting structured information from documents (OCR, key/value pairs, tables).  
- OCR vs document processing: OCR reads text from an image or scanned page, document processing adds layout understanding to extract fields and tables.  
- Image classification vs object detection: classification labels the whole image, detection returns labels plus bounding boxes (what and where).  
- Object detection vs semantic segmentation: detection gives bounding boxes, segmentation gives pixel-level masks when boundaries matter.  
- Face detection vs face verification: detection finds faces (and sometimes attributes), verification compares two faces to decide if they are the same person.  
- General tags/captions vs custom vision: tags and captions are broad, custom vision is used when you need your own labels (specific products, competitor SKUs, defect categories).  

> [!WARNING]  
> If your rule is about faces and a face-worn item (like sunglasses), use face detection with attributes. Face verification is for identity matching, not accessories filtering.  

> [!IMPORTANT]  
> Choose by the output you need: “what” (classification), “what and where (box)” (detection), “what and where (pixels)” (segmentation), “text on the page” (OCR), “fields and tables” (document processing).  


## Azure Mapping (Concept → Azure Service Family)  
This document is Vendor-Neutral. This section maps the concepts in this document to common Azure services so you can connect the ideas to real implementations.  
Now let’s map the vision and document concepts in this document to Azure services like **Concept → Service Family (Specific Capability Name)**:  
- **General Vision (Tags, Captions, OCR)** → Azure AI Vision (Image Analysis)  
- **Face Detection and Face Operations** → Azure AI Face (Face)  
- **Custom Vision Models (Classification, Object Detection)** → Azure AI Custom Vision (Custom Vision)  
- **Document Processing (OCR, Key/Value, Tables)** → Azure AI Document Intelligence (Document Intelligence)  


## Summary  
You should now be able to:  
- Explain what computer vision is and recognize common outputs like tags, captions, classification, detection, OCR, and segmentation.  
- Choose between image classification, object detection, and semantic segmentation based on whether you need “what,” “what and where (box),” or “what and where (pixels).”  
- Use OCR when you need to read text, and use document processing when you need structured extraction like key/value pairs and tables.  
- Distinguish face detection (find faces and attributes) from face verification (match identity).  
- Recognize when generic tags and captions are not enough and a custom vision model is needed for your own labels.  
- Avoid common confusion points by choosing the capability based on the output you need.  
- Map the vision and document concepts in this document to Azure service families (Vision, Face, Custom Vision, Document Intelligence).  
