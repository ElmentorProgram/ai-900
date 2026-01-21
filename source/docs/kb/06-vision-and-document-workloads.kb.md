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
