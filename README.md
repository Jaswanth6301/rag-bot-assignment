# RAG Document Q&A Bot

## Project Overview

This project is a Retrieval-Augmented Generation (RAG) based Document Question Answering Bot developed in Python.

The system allows users to upload documents, create a searchable vector index, and ask natural language questions. The bot retrieves relevant document chunks and generates grounded answers using Google's Gemini LLM.

The application supports both command-line interaction and a Streamlit web interface.

---

## Objective

The objective of this project is to build a document-based question answering system that:

- Accepts multiple document formats
- Processes and chunks document content
- Generates vector embeddings
- Stores embeddings in a vector database
- Retrieves relevant chunks for a user query
- Uses a Large Language Model to generate accurate grounded answers
- Displays source citations for transparency

---

## Features

- Supports PDF, TXT, and DOCX files
- Automatic document chunking with overlap
- Semantic search using vector embeddings
- FAISS vector database for fast retrieval
- Gemini 2.5 Flash for answer generation
- Streamlit frontend for interactive chat UI
- Source citation display with file name and page number
- Persistent index storage

---

## Tech Stack

### Programming Language
- Python

### Libraries / Frameworks
- Streamlit
- FAISS
- Sentence Transformers
- LangChain
- Google Gemini API
- PyMuPDF
- python-docx
- NumPy
- python-dotenv

---

## Project Architecture

```text
User Query
   ↓
Streamlit Frontend / CLI
   ↓
Query Embedding Generation
   ↓
FAISS Vector Search
   ↓
Relevant Document Chunk Retrieval
   ↓
Gemini LLM Answer Generation
   ↓
Answer + Source Display
```

---

## Project Structure

```text
RAG_Document_QA_Bot/
│
├── data/
│   ├── blockchain_crypto.txt
│   ├── climate_change.txt
│   ├── sample.pdf
│   └── notes.docx
│
├── index/
│   ├── faiss.index
│   └── chunks.pkl
│
├── ingest.py
├── app.py
├── requirements.txt
├── .env
└── README.md
```

---

## Working Principle

### 1. Document Loading

The ingestion pipeline reads documents from the `data/` folder.

Supported formats:

- PDF
- TXT
- DOCX

Document loaders used:

- PyMuPDF for PDF parsing
- python-docx for DOCX parsing
- Native file reading for TXT

---

### 2. Chunking

Documents are split into smaller chunks for efficient retrieval.

Configuration:

```python
CHUNK_SIZE = 500
CHUNK_OVERLAP = 100
```

Reason:

Chunk overlap preserves context between consecutive chunks and improves retrieval accuracy.

---

### 3. Embedding Generation

Each chunk is converted into vector embeddings using:

```python
all-MiniLM-L6-v2
```

Library:

```python
sentence-transformers
```

Embeddings represent semantic meaning, enabling similarity search.

---

### 4. Vector Database

Generated embeddings are stored using FAISS.

Files created:

```text
index/faiss.index
index/chunks.pkl
```

Purpose:

- Fast nearest-neighbor similarity search
- Persistent storage for reuse

---

### 5. Query Processing

When the user asks a question:

- Query is converted into embedding
- FAISS retrieves top matching chunks
- Relevant context is constructed

---

### 6. Answer Generation

Retrieved context is passed to Gemini:

```python
gemini-2.5-flash
```

Prompt engineering ensures:

- Answers use only retrieved context
- No hallucinated information
- Unknown answers are explicitly stated

---

### 7. Frontend

Streamlit provides a chat-based interface with:

- Question input
- AI-generated answers
- Source document display
- Chat history

---

## Setup Instructions

### Step 1: Clone / Download Project

Place project files in a folder.

---

### Step 2: Create Virtual Environment

Windows:

```bash
python -m venv venv
```

Activate:

```bash
.\venv\Scripts\Activate
```

---

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

---

### Step 4: Add API Key

Create `.env`

```env
GEMINI_API_KEY=your_google_api_key
```

---

## Execution Steps

### Create Vector Index

Run:

```bash
python ingest.py
```

Output:

```text
RAG INDEXING STARTED
Loading documents...
Loaded Pages: X
Total Chunks: X
INDEX CREATED SUCCESSFULLY
```

---

### Run Streamlit Frontend

```bash
streamlit run app.py
```

Browser opens:

```text
http://localhost:8501
```

---

## Sample Usage

Question:

```text
What is blockchain?
```

Answer:

```text
Blockchain is a distributed digital ledger maintained by a peer-to-peer network.
```

Sources:

```text
blockchain_crypto.txt (Page 1)
```

---

## Advantages

- Fast document retrieval
- Grounded answers
- Supports multiple document formats
- Persistent indexing
- User-friendly frontend
- Scalable architecture

---

## Limitations

- Requires valid Gemini API access
- Limited by chunk retrieval quality
- Supports only PDF/TXT/DOCX
- No OCR support for scanned PDFs

---

## Future Enhancements

- OCR support for scanned documents
- Multi-user authentication
- Cloud deployment
- Upload documents directly from frontend
- Chat memory
- Better reranking
- Hybrid retrieval (BM25 + Dense Search)

---

## Conclusion

This project demonstrates a complete Retrieval-Augmented Generation pipeline for document question answering.

It combines semantic retrieval, vector databases, and LLM-based generation to provide accurate, context-grounded answers from uploaded documents.
