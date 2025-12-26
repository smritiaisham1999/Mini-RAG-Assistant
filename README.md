# 🧠 Intelligent RAG Assistant (Prototype)

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.11-blue" />
  <img src="https://img.shields.io/badge/FastAPI-0.109-green" />
  <img src="https://img.shields.io/badge/Streamlit-1.31-red" />
  <img src="https://img.shields.io/badge/LangChain-0.1-orange" />
</p>

---

## 📋 Executive Summary

The **Intelligent RAG Assistant** is a **decoupled, microservices-based prototype** designed to securely ingest corporate documents and generate **grounded, citation-backed answers**.

Unlike traditional chatbots, this system enforces:

- 🚫 **Strict Anti-Hallucination Rules**
- 🔐 **Role-Based Access Control (RBAC)**
- 📚 **Transparent Source Citations**

This project demonstrates a **Pro-Code Retrieval-Augmented Generation (RAG)** architecture using **local FAISS vector stores** with a **separated frontend and backend** for scalability.

---

## 🚀 Key Features

### 🛡️ 1. Strict Anti-Hallucination & Grounding

- **Confidence Scoring**  
  Uses **L2 Euclidean Distance** from the FAISS vector store to calculate a confidence score (0–100%) for every answer.

- **Negative Constraint Enforcement**  
  If confidence drops below a defined threshold (e.g., `< 30%`), the system **strictly responds**:  
  > _"I cannot find the answer"_  
  ensuring **zero fabrication**.

- **Citation Transparency**  
  Each response includes a **Verified Sources** section showing:
  - Document name  
  - Exact text snippet used for grounding

---

### 🔐 2. Role-Based Access Control (RBAC)

- **Metadata Tagging**  
  Every document is tagged with:
  - `owner_id` (username)
  - `privacy_mode` (Public / Private)

- **Secure Retrieval Filtering**  
  Users **cannot retrieve private documents** belonging to other users — even if queries match semantically.

---

### 🧠 3. Advanced Retrieval Logic

- **Multi-Query Expansion**  
  Automatically generates query synonyms  
  *(e.g., “Cost” → “Price”, “Budget”)*  
  to improve recall.

- **Hybrid Chunking Strategy**  
  Uses `RecursiveCharacterTextSplitter`  
  - Chunk Size: `1000`
  - Overlap: `200`  
  ensuring contextual continuity.

---

## 🏗️ System Architecture

The system follows a **Decoupled Architecture** for scalability and maintainability.

### 🧠 The Brain — Backend (FastAPI)
Handles:
- Document parsing (PDF, DOCX, TXT)
- Vector embeddings (OpenAI / Gemini)
- FAISS similarity search
- SQLite-based chat memory

### 🎭 The Face — Frontend (Streamlit)
Handles:
- User session management
- Confidence score visualization (Green / Red)
- REST API communication with backend

---

## 🛠️ Technology Stack

| Layer | Technology |
|------|------------|
| Language | Python 3.11 |
| API | FastAPI + Uvicorn |
| UI | Streamlit |
| RAG Orchestration | LangChain |
| Vector DB | FAISS (Local CPU) |
| Persistence | SQLite |
| Deployment | Railway (Backend), Streamlit Cloud (Frontend) |

---

## ⚙️ Installation & Setup

### ✅ Prerequisites
- Python **3.10+**
- OpenAI or Google Gemini API Key

---

### 📥 1. Clone the Repository

```bash
git clone https://github.com/your-username/rag-agent.git
cd rag-agent
📦 2. Install Dependencies
bash
Copy code
pip install -r requirements.txt
🔑 3. Environment Variables
Create a .env file in the project root (optional):

env
Copy code
OPENAI_API_KEY=sk-...
GOOGLE_API_KEY=AIza...
BACKEND_URL=http://localhost:8000
🏃‍♂️ Running the Application (Local)
⚠️ Important:
This is a decoupled system — the backend and frontend must run in separate terminals.

🧠 Terminal 1 — Start Backend API
bash
Copy code
uvicorn main:app --reload --host 0.0.0.0 --port 8000
📍 API Docs:
http://localhost:8000/docs

🎭 Terminal 2 — Start Frontend UI
bash
Copy code
streamlit run app.py
📍 UI URL:
http://localhost:8501

📖 Usage Guide
🔐 Login
Enter a Username in the sidebar
(Required for RBAC enforcement)

⚙️ Configuration
Select AI Provider (OpenAI / Gemini)

Enter API Key

📥 Document Ingestion
Choose Public or Private mode

Upload PDF or DOCX files

Click Process Documents

💬 Querying
Ask questions via chat interface

🟢 Green Score: High confidence

🔴 Red Score: Low confidence / Uncertainty

📎 Expand Verified Sources to view raw evidence

📂 Project Structure
plaintext
Copy code
├── main.py              # FastAPI Backend Entry Point
├── app.py               # Streamlit Frontend Interface
├── rag_engine.py        # Core RAG Logic
├── database.py          # SQLite Chat History Handler
├── requirements.txt     # Dependencies
├── faiss_db_store/      # Local Vector Database (auto-generated)
└── data/                # Temporary Upload Storage
🔮 Future Improvements
🧾 OCR support for scanned PDFs

🔍 Hybrid Search (BM25 + Semantic)

🔐 JWT-based Authentication
