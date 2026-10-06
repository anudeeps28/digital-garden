---
type: atomic
tags: [ai, ai/rag, ocr, coding/azure, coding/aws]
date: 2026-10-06
---

# Document Extraction Service

## Idea
A hosted service that reads PDFs, scans and photos and returns their contents as data: the text, where each word sits on the page, the tables, and named fields like "invoice total". It turns a picture of a document into something code can use.

## Definition
A scanned PDF is just a picture of text. A computer can display it but can't search it, copy a number out of it or put it in a database. A document extraction service does the reading for you. Azure calls its version **Document Intelligence**, which is the name you'll hear most. You send it a file and get back structured [[JSON]] in layers, each built on the one below:

| Layer | What you get | Plain English |
|---|---|---|
| **Read (OCR)** | Every word and line, with its position on the page | "What does it say, and where?" |
| **Layout** | Paragraphs, headings, tables (rows and columns kept intact), checkboxes, reading order | "How is the page organised?" |
| **Prebuilt models** | Named fields for common documents: invoices, receipts, ID cards, tax forms | "This is an invoice, and the total is $412.50" |
| **Custom models** | Named fields for *your* document types, trained on a handful of labelled examples | Same as prebuilt, for forms nobody else has |
| **Classification** | Which kind of document this is, or where one document ends in a combined PDF | "Pages 1–3 are a claim form, page 4 is a receipt" |

Three details matter in practice:
- **Every value comes with a [[Confidence Score]]** and a bounding box (the rectangle it was read from). Low-confidence fields can be sent for [[Field Verification|a second check]] or human review, and the box lets a UI highlight exactly where a value came from.
- **Big files are asynchronous.** You submit the document, get back an operation ID, and poll until it finishes. A 200-page PDF isn't answered in one request.
- **You pay per page**, and the richer layers cost more. Reading the text is cheap; prebuilt and custom field extraction cost several times as much.

In AI systems it usually sits at the very start of the pipeline. Documents land in [[Object Storage]], the extraction service turns them into text, often Markdown that keeps headings and tables, and that text is then [[Chunking|chunked]] for search or handed to a model for [[Template-Based Extraction]].

## Providers
- **Azure** — Azure AI Document Intelligence (called Form Recognizer until 2023): Read, Layout (with Markdown output), prebuilt models, custom template and neural models, classifiers.
- **AWS** — Amazon Textract: text detection, AnalyzeDocument (forms, tables, signatures, and "queries" where you ask for a field in plain English), plus specialised APIs for expenses, IDs and lending documents. Multi-page files go through the async APIs via S3.
- **Google Cloud** — Document AI: processors for OCR, form parsing and layout, specialised processors (invoices, IDs and so on), and a Custom Extractor.
- **Others** — open source: Tesseract (classic OCR), docTR, and Docling or Unstructured, which convert PDFs to clean Markdown for RAG. Vision-capable [[LLM (Large Language Model)|LLMs]] can also read page images directly.

## Source
Microsoft Learn, "What is Azure AI Document Intelligence?" (learn.microsoft.com/azure/ai-services/document-intelligence); AWS documentation, "What is Amazon Textract?"; Google Cloud documentation, "Document AI overview". OCR itself dates back decades; the cloud services added layout, table and field extraction from about 2019 onward.

---

## Compass

**Roots** — *where this comes from*
It's classic OCR grown up: the same "turn pixels into letters" step, with machine learning layered on top to understand page structure and meaning. It's the ingestion step that makes paper documents usable in [[RAG (Retrieval-Augmented Generation)]].

**Paths** — *where this leads*
Its output feeds [[Chunking]] and a [[Managed Search Service]] for question answering, or [[Template-Based Extraction]] when you need specific fields. Its per-field confidence scores are what make [[Field Verification]] and human review possible.

**Neighbors** — *what lives nearby*
A [[Managed LLM Service]] with vision can read the same pages, and the two are often combined: the extraction service handles layout and tables, and the model handles judgement. The [[Strategy Pattern]] is a clean way to swap between them, or to fall back from the cheap one to the expensive one.

**Clash** — *what pushes against this*
Vision LLMs now read messy documents surprisingly well and can be told what to extract in plain English, which eats into what custom-trained models were for. The dedicated service still wins on cost per page, on positions you can highlight, and on giving the same answer every time. It also struggles with handwriting, poor scans and unusual layouts, so its output still needs [[Structured Output Validation|checking]] before anyone trusts it.
