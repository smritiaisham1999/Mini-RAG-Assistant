# 🧠 Intelligent RAG Assistant
> Grounded • Explainable • Anti-Hallucination AI

![Python](https://img.shields.io/badge/Python-3.11-blue)
![Streamlit](https://img.shields.io/badge/Streamlit-1.31-red)
![LangChain](https://img.shields.io/badge/LangChain-0.1-orange)
![FAISS](https://img.shields.io/badge/VectorDB-FAISS-green)
![Status](https://img.shields.io/badge/Status-Prototype-yellow)

**Version:** 1.0  
**Type:** Standalone AI Application  

---

## 📌 Project Overview

**Intelligent RAG Assistant** is a **Retrieval-Augmented Generation (RAG)** system that delivers **accurate, source-grounded, and confidence-aware answers** from user-uploaded documents.

Unlike standard chatbots, this system:
- ❌ Prevents hallucinations
- 📊 Shows confidence scores
- 📄 Cites document sources
- 🔍 Answers strictly from uploaded files

---

## 🏗️ System Architecture

The application follows a **Unified Monolithic Microservice Architecture**, optimized for performance and simplicity.

### 🔹 Core Components

| Layer | Technology | Responsibility |
|------|-----------|---------------|
| UI | Streamlit | Chat UI, file upload, session state |
| Logic | LangChain | Chunking, retrieval, orchestration |
| Vector DB | FAISS | Semantic similarity search |
| Storage | SQLite | Chat history persistence |
| LLM | OpenAI / Gemini | Context-based generation |

---

## 🔄 Retrieval & Generation Pipeline

The system follows a strict **Load → Embed → Retrieve → Generate** workflow.

### 1️⃣ Ingestion
- Supports **PDF** and **DOCX**
- Text extracted and cleaned

### 2️⃣ Chunking
- Chunk Size: **1000 characters**
- Overlap: **200 characters**
- Uses `RecursiveCharacterTextSplitter`

### 3️⃣ Vectorization
- Embedding Size: **1536**
- Stored locally in **FAISS**

### 4️⃣ Retrieval
- Top **3** semantically closest chunks
- Based on cosine/L2 similarity

### 5️⃣ Generation
- LLM answers **only from retrieved context**
- External knowledge strictly blocked

---

## 🛡️ Confidence Scoring (Anti-Hallucination)

Each response includes a **Confidence Score** based on FAISS L2 distance.

### 📐 Formula
Score = 1 / (1 + (Distance × 0.3)) × 100


### 🔎 Rules
- **100%** → Exact match
- **< 30%** → Answer is rejected

---

## 🧪 Example Scenarios

### ✅ Scenario A: Successful Retrieval

**User Query**
What is the specific weightage for RAG integration?



**System Answer**
The RAG integration and functionality carries a weight of 40%.



**Metadata**
- 🟢 Confidence Score: **98.5%**
- 📄 Source: `Mini RAG Assistant (1).docx`
- 🔍 Evidence snippet included

---

### ❌ Scenario B: Hallucination Prevention

**User Query**
What is the CEO's salary?


**System Answer**
I cannot find this information in the provided documents.



**Metadata**
- 🔴 Confidence Score: **0%**
- ⚠️ No semantic match found

---

## ⚙️ Installation & Setup

### 🔧 Prerequisites
- Python **3.10+**
- OpenAI / Gemini API Key

### 📥 Installation
```bash
git clone https://github.com/smritiaisham1999/Mini-RAG-Assistant.git
cd Mini-RAG-Assistant
pip install -r requirements.txt
▶️ Run Application

streamlit run app.py
🎯 Key Features
✅ Retrieval-Augmented Generation (RAG)

🛡️ Anti-hallucination guardrails

📊 Confidence scoring

📄 Source-grounded answers

💬 Persistent chat memory

⚡ Lightweight local vector DB

🚀 Use Cases
Enterprise Knowledge Bases

Research & Documentation QA

Compliance Verification

Secure Internal Assistants
