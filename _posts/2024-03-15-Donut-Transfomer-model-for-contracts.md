

Challenges of Contract Interpretation.

First approach OCR with NER  
Not enough training data so used 10 contracts
https://prodi.gy/docs/named-entity-recognition

The Donut model is a Transformer-based visual encoder and textual decoder model that understands document images. It is an end-to-end model that does not use optical character recognition (OCR). Instead, it uses a visual encoder to extract features from a document. The model is trained to read all text in an image in reading order, from top-left to bottom-right. 

Ritvik Rastogi  ·  
Medium · 1y
Papers Explained 20: Donut. Donut is an end-to-end (i.e… | by Ritvik Rastogi | DAIR.AI | Medium
Feb 6, 2023

konfuzio.com
Donut Deep Dive - Document Understanding - Konfuzio
(2021) in their paper "OCR-free Document Understanding Transformer (Donut)," is a unique approach to document image processing that does not rely on optical character recognition (OCR). The model is designed to work efficiently in multiple languages and is computationally cheaper than traditional OCR-based methods.
The Donut model is designed to work efficiently in multiple languages and is computationally cheaper than traditional OCR-based methods. It has achieved state-of-the-art performance in terms of speed, accuracy, and memory usage. 
The Donut model consists of an image Transformer encoder and an autoregressive text Transformer decoder. It can perform document understanding tasks such as document image classification, form understanding, and visual question answering. 
The Donut model is trained using a synthetic document generator (SDG), which is a technique for generating data that can be used to pre-train a model to help it understand a given document. 
The Donut model has some limitations, such as struggling to accurately interpret documents that contain a mix of text and non-text elements, such as images and graphs. 

https://arxiv.org/abs/2111.15664

https://github.com/OptumInsight-Platform/oi-ds-paymentintegrity/tree/main/src/model/odocu/prep