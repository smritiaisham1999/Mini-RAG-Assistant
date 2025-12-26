# 🧠 Intelligent RAG Assistant (Prototype)

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.11-blue" />
  <img src="https://img.shields.io/badge/Streamlit-1.31-red" />
  <img src="https://img.shields.io/badge/LangChain-0.1-orange" />
  <img src="https://img.shields.io/badge/FAISS-CPU-yellow" />
</p>

<p align="center">
A secure, production-grade Retrieval-Augmented Generation (RAG) system with strict grounding, confidence scoring, and role-based access control.
</p>

---

## 📋 Executive Summary

The **Intelligent RAG Assistant** is a **secure, production-ready AI application** designed to ingest corporate documents and generate **grounded, citation-backed answers** with zero hallucination.

This system runs as a **single unified Streamlit application** and enforces:

- 🚫 **Strict Anti-Hallucination Rules**
- 🔐 **Role-Based Access Control (RBAC)**
- 📚 **Transparent Source Citations**

It demonstrates a **pro-code RAG architecture** using **local FAISS vector stores**, tightly integrated with a reactive UI for simplicity, speed, and reliability.

---

## 🚀 Key Features

### 🛡️ 1. Anti-Hallucination & Grounding
- **Confidence Scoring:** Uses **L2 Euclidean Distance** from FAISS to compute an answer confidence score (0–100%).
- **Negative Constraint Enforcement:**  
  If confidence falls below a threshold (e.g. `< 30%`), the system responds:
  > *"I cannot find the answer."*
- **Citation Transparency:** Every answer includes a **Verified Sources** section with exact document names and text snippets.

---

### 🔐 2. Role-Based Access Control (RBAC)
- **Metadata Tagging:** Documents are tagged with:
  - `owner_id`
  - `privacy_mode`
- **Secure Filtering:**  
  Users **cannot retrieve private documents** belonging to other users, ensuring full data isolation.

---

### 🧠 3. Advanced Retrieval Logic
- **Multi-Query Expansion:**  
  Automatically expands queries using synonyms  
  *(e.g., “Cost” → “Price”, “Charges”, “Fee”)*.
- **Hybrid Chunking Strategy:**  
  Uses `RecursiveCharacterTextSplitter`  
  - Chunk Size: `1000`
  - Overlap: `200`

This ensures contextual continuity across long documents.

---

## ⚙️ Installation & Setup

### ✅ Prerequisites
- Python **3.10+**
- OpenAI **or** Google Gemini API Key

---

### 📥 1. Clone & Install Dependencies

```bash
git clone https://github.com/smritiaisham1999/Mini-RAG-Assistant.git
cd Mini-RAG-Assistant
pip install -r requirements.txt
🔑 2. Environment Variables
You can either:

Enter API keys directly from the Streamlit sidebar, or

Create a .env file in the project root:

env
OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxx
GOOGLE_API_KEY=AIzaxxxxxxxxxxxx
🏃‍♂️ 3. Run the Application

streamlit run app.py
The app will be available at:

https://mini-rag-assistant.streamlit.app
📂 Supported Data Sources
The system uses LangChain document loaders to support:

📄 PDF (.pdf) – via PyPDFLoader

📝 Word (.docx) – via Docx2txtLoader

📃 Text (.txt) – via TextLoader

📦 Key Dependencies
Streamlit – UI & application logic

LangChain – RAG orchestration

FAISS-CPU – Local vector database

SQLite – Chat history persistence

📁 Project Structure

├── app.py               # Main Streamlit App (UI + Logic)
├── rag_engine.py        # Core RAG Logic (Chunking, Retrieval, Scoring)
├── database.py          # SQLite Chat History Manager
├── main.py              # (Legacy / Optional) API wrappers
├── requirements.txt     # Python dependencies
├── faiss_db_store/      # Auto-generated FAISS vector database
└── README.md            # Project documentation
📊 Example Output
1️⃣ User Interface Response
User Question

What is the weight of RAG integration?
Assistant Response

The RAG integration and functionality carries a weight of 40%.
Metrics

Confidence: 🟢 98.5% (High)

Verified Sources:

Mini RAG Assistant (1).docx

"RAG Integration and Functionality... 40%"

2️⃣ Terminal Logs

INFO: Started Streamlit App
✅ Database loaded successfully
📂 Ingestion: Processing 'Mini RAG Assistant (1).docx'
✅ Processed: 1 file
🔍 Search Query: 'weight of rag integration'
✅ Retrieval: Found 3 relevant chunks
📊 Confidence Score: 98.5%
🔮 Future Improvements
🧾 OCR support for scanned PDFs

🔍 Hybrid Search (BM25 + Semantic Search)

🔐 User Authentication (Login / Signup)

🌐 Multi-tenant deployment support

⭐ Why This Project?
This project showcases enterprise-grade RAG best practices, including:

Zero hallucination guarantees

Explainable AI with confidence scoring

Secure document isolation

Clean, production-ready architecture

Perfect for AI portfolios, enterprise demos, and client-facing RAG solutions.
