🧠 Intelligent RAG Assistant

Grounded • Explainable • Anti-Hallucination AI




Version: 1.0
Type: Standalone AI Application

📌 Project Overview

Intelligent RAG Assistant is a Retrieval-Augmented Generation (RAG) system designed to deliver accurate, source-grounded, and confidence-aware answers from user-provided documents.

Unlike generic chatbots, this assistant:

❌ Prevents hallucinations

📊 Displays confidence scores

📄 Cites document evidence

🔍 Answers only from uploaded files

🏗️ System Architecture

The application follows a Unified Monolithic Microservice Architecture, optimized for simplicity, performance, and rapid deployment.

🔹 Core Components
Layer	Technology	Responsibility
UI Layer	Streamlit	Chat UI, file uploads, session handling
Orchestration	LangChain	Document parsing, chunking, retrieval logic
Vector Store	FAISS	Semantic similarity search
Persistence	SQLite	Chat history & session memory
LLM	OpenAI / Gemini	Context-grounded response generation

📌 Key Design Choice:
UI and backend logic are tightly coupled to reduce latency and complexity.

🔄 Retrieval & Generation Pipeline

The system strictly follows a Load → Embed → Retrieve → Generate workflow.

1️⃣ Ingestion

Supports PDF and DOCX

Text extracted and cleaned (formatting removed)

2️⃣ Chunking

Chunk Size: 1000 characters

Overlap: 200 characters

Method: RecursiveCharacterTextSplitter

Ensures semantic continuity

3️⃣ Vectorization

Embedding Size: 1536 dimensions

Model: OpenAI / Gemini Embeddings

Stored locally in FAISS

4️⃣ Retrieval

Top 3 most relevant chunks

Based on semantic similarity

5️⃣ Generation

LLM answers only from retrieved context

Strict prompt prevents external knowledge usage

🛡️ Confidence Scoring (Anti-Hallucination)

Every response includes a Confidence Score, computed using FAISS L2 Euclidean Distance.

📐 Formula
Score = 1 / (1 + (Distance × 0.3)) × 100

🧠 Interpretation

100% → Exact semantic match

Lower score → Weaker relevance

< 30% → Answer is blocked

🚫 If confidence drops below threshold, the system refuses to answer.

🧪 Example Scenarios
✅ Scenario A: Successful Retrieval

User Query

What is the specific weightage for RAG integration?


AI Response

The RAG integration and functionality carries a weight of 40%.


Metadata

🟢 Confidence Score: 98.5%

📄 Source File: Mini RAG Assistant (1).docx

🔎 Evidence:

"...Effectiveness of connecting retrieval... 40%..."

❌ Scenario B: Hallucination Prevention

User Query

What is the CEO's salary?


AI Response

I cannot find this information in the provided documents.


Metadata

🔴 Confidence Score: 0%

⚠️ Reason: No semantic match found in vector database

⚙️ Installation & Setup
🔧 Prerequisites

Python 3.10+

OpenAI / Gemini API Key

📥 Installation
git clone https://github.com/smritiaisham1999/Mini-RAG-Assistant.git
cd Mini-RAG-Assistant
pip install -r requirements.txt

▶️ Run the App
streamlit run app.py

🎯 Key Features

✅ Retrieval-Augmented Generation (RAG)

🧠 Context-aware answers

📊 Confidence scoring

🛡️ Anti-hallucination safeguards

📄 Source-verified responses

💬 Chat history persistence

⚡ Lightweight & local vector store

🚀 Use Cases

Internal Knowledge Bases

Research Document QA

Compliance & Policy Verification

Academic & Technical Review

Secure Enterprise AI Assistants

📌 Project Status

🧪 Prototype (Stable)
Ready for:

Demo presentations

Client showcases

Fiverr / freelance delivery

Further production hardening
