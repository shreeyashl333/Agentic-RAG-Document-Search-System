# 🔍 Agentic RAG Document Search System

A **production‑style Retrieval‑Augmented Generation (RAG)** application that demonstrates how modern AI teams build **document‑grounded question‑answering systems** using **LangChain, LangGraph, FAISS, and OpenAI models**.

This project is designed to be **recruiter‑believable**: clean architecture, agentic orchestration, transparent sources, and an interactive UI.

---

## 🚀 What This Project Demonstrates

* End‑to‑end **RAG pipeline** (ingestion → chunking → embeddings → retrieval → answer generation)
* **Agentic reasoning** using **LangGraph + ReAct agents**
* Support for **multiple data sources**:

  * 🌐 Web URLs
  * 📄 Local PDFs / text files
* **Vector search** with FAISS
* **Source‑aware answers** (documents shown alongside responses)
* **Streamlit UI** for interactive exploration
* Clean separation of concerns (config, ingestion, vector store, graph, UI)

---

## 🧠 System Architecture

```
User Question
     │
     ▼
LangGraph Orchestrator
     │
     ├── Retrieve Relevant Chunks (FAISS)
     │
     ├── Tool‑aware ReAct Agent
     │       ├── Vector Retriever Tool
     │       └── Wikipedia Tool (fallback knowledge)
     │
     ▼
Final Answer + Source Documents
```

The **agent** decides *how* to answer using tools rather than blindly stuffing context into a prompt.

---

## 📂 Project Structure

```
rag-document-search/
├── src/
│   ├── config/                # LLM + system configuration
│   ├── document_ingestion/    # URL / PDF ingestion + chunking
│   ├── vectorstore/           # FAISS + embeddings
│   ├── graph_builder/         # LangGraph orchestration
│   ├── node/                  # Retrieval + ReAct agent nodes
│   └── state/                 # Graph state definitions
├── data/
│   ├── urls.txt               # List of URLs to ingest
│   └── attention.pdf          # Example local document
├── streamlit_app.py           # Interactive UI
├── main.py                    # CLI entrypoint
├── requirements.txt
└── README.md
```

---

## 📸 Application Screenshots

> These screenshots were captured from a real run of the system.

### System Ready – Documents Indexed

<img width="1912" height="947" alt="Doc Search pic1" src="https://github.com/user-attachments/assets/853ccd8b-230b-4de5-8ca5-445799666e37" />

### Asking a Question

<img width="1342" height="658" alt="doc search pic 2" src="https://github.com/user-attachments/assets/241c765e-a978-4020-b773-4a48a46ba64f" />


### Generated Answer

<img width="1778" height="869" alt="doc search pic 3" src="https://github.com/user-attachments/assets/74772adb-ec70-4e60-bfae-86739fa8ceb1" />


### Retrieved Source Documents

<img width="1641" height="919" alt="doc search pic 4" src="https://github.com/user-attachments/assets/2fe0d01e-d824-4e22-b9a4-ff6bcedfcb8a" />


### Response Timing & History

<img width="1755" height="926" alt="doc search pic 5" src="https://github.com/user-attachments/assets/3817d874-44b4-4dbd-93c9-ecaa51582cec" />


---

## ⚙️ How It Works (Detailed Flow)

### 1. Document Ingestion

* URLs loaded via `WebBaseLoader`
* PDFs parsed using `PyPDFLoader`
* All documents normalized into LangChain `Document` objects

### 2. Chunking Strategy

* Recursive text splitting
* Configurable `chunk_size` and `chunk_overlap`
* Designed to balance retrieval precision vs context recall

### 3. Embeddings & Vector Store

* OpenAI embeddings
* FAISS index built in‑memory (optionally persistable)
* Retriever exposed as a **tool** to the agent

### 4. Agentic Reasoning (LangGraph)

* Graph nodes:

  * **Retriever Node** – fetches relevant chunks
  * **Responder Node** – ReAct agent decides how to answer
* Agent can:

  * Use retrieved documents
  * Fall back to Wikipedia for general knowledge

### 5. Answer Generation

* ReAct agent synthesizes a grounded answer
* Returns:

  * Final answer
  * Retrieved source documents

---

## 🖥️ Running the Project Locally

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/yourusername/rag-document-search.git
cd rag-document-search
```

### 2️⃣ Create Virtual Environment

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
```

### 3️⃣ Install Dependencies

```bash
pip install -r requirements.txt
```

### 4️⃣ Set Environment Variables

Create a `.env` file:

```bash
OPENAI_API_KEY=your_api_key_here
```

> ⚠️ Never commit `.env` to GitHub

### 5️⃣ Run the Streamlit App

```bash
streamlit run streamlit_app.py
```

### 6️⃣ Run via CLI (Optional)

```bash
python main.py
```

---

## 🔎 Example Questions

* *What are transformers?*
* *What problem does self‑attention solve?*
* *Summarize the key ideas from the Attention Is All You Need paper*

---

## 🧪 Design Decisions (Why This Matters)

* **Agentic RAG** instead of naive RAG → closer to production systems
* **LangGraph** for explicit orchestration → debuggable + extensible
* **Tool‑based retrieval** → scalable beyond single vector store
* **Source transparency** → critical for trust and debugging

---

## 📈 Future Enhancements

* Persistent FAISS index
* Hybrid search (BM25 + dense)
* RAG evaluation harness (precision@k, faithfulness)
* Multi‑document citations
* Auth‑enabled deployment

---

## 🧑‍💻 Who This Project Is For

* Recruiters evaluating **Applied AI / ML / LLM Engineers**
* Engineers looking for a **clean RAG reference implementation**
* Teams exploring **agent‑based LLM systems**

---

## 📜 License

MIT License

---

**If you’re a recruiter:** this project mirrors how modern AI teams build retrieval‑augmented systems in production environments, with attention to correctness, modularity, and explainability.
