---
title: "Autonomous Knowledge Retrieval Engine"
date: 2026-01-04
description: "An enterprise-grade RAG pipeline that synchronizes cloud storage with a vector database to provide real-time, context-aware AI assistance."
tags: ["AI/LLM", "Vector Databases", "Automation", "Architecture"]
showTableOfContents: true
---

## Project Overview

I engineered a **Retrieval-Augmented Generation (RAG)** system designed to bridge the gap between static corporate documentation and interactive AI. The system autonomously monitors internal directories, processes unstructured data, and provides a conversational interface for complex policy queries.

### 1. Automated ETL Pipeline (Data Sync)

Instead of manual data entry, I built an automated ingestion layer that keeps the AI's "brain" current:

* **Source Integration:** Monitors Google Drive repositories for new or updated policy documentation.
* **Vectorization:** Utilizes **Google Gemini Embeddings** to convert text into high-dimensional vectors.
* **Database Management:** Automates the flushing and re-indexing of a **Pinecone Vector Database** to ensure 100% data consistency.

### 2. Intelligent Document Processing

To ensure the AI handles large documents accurately, the engine employs sophisticated text-handling logic:

* **Recursive Chunking:** Breaks down large PDF/Docx files into optimized segments with a 100-character overlap to maintain semantic context across chunks.
* **Metadata Tagging:** Ensures every piece of retrieved information is traceable back to its source.

### 3. Agentic Logic & Retrieval

The front-end interface utilizes an "Agentic" model rather than a simple prompt:

* **Contextual Memory:** Implemented a **Window Buffer Memory** system, allowing the AI to remember the last several turns of a conversation for fluid follow-up questions.
* **Semantic Search Tooling:** The agent is equipped with a custom-tooled vector retriever, allowing it to perform "lookups" in real-time before formulating a response.
* **Zero-Shot Guardrails:** Engineered strict system prompts to prevent the AI from speculating; if the answer isn't in the verified docs, it will not provide a false answer.

---

### Technical Architecture Summary

| Component | Technology | Role |
| :--- | :--- | :--- |
| **Model** | Gemini 2.0 Flash | Primary Reasoning Engine |
| **Vector Store** | Pinecone | Semantic Long-term Memory |
| **Data Source** | Google Drive API | Source of Truth |
| **Orchestration** | Event-Driven Middleware | Pipeline Logic & API Glue |
| **Embeddings** | Google PaLM/Gemini | Text-to-Vector Transformation |
