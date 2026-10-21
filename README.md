# AI Medical Assistant Chatbot — RAG-Based Application

## Project Overview

The AI Medical Assistant Chatbot is a medical-domain application built using **Retrieval-Augmented Generation (RAG)**. It allows users to upload medical documents, such as textbooks, notes, and reports, and ask questions based on their content.

The application retrieves relevant information from uploaded documents and uses a Large Language Model (LLM) to generate responses to user queries.

## What is RAG?

**Retrieval-Augmented Generation (RAG)** combines information retrieval with language generation. Instead of relying only on the knowledge learned during model training, it retrieves relevant information from an external knowledge base and provides it as context to the language model.

This approach helps improve the relevance and accuracy of generated responses, especially in specialized domains such as healthcare and medical documentation.

## System Architecture

The application follows a document retrieval and question-answering workflow:

```text
User Input
    |
    v
Query Embedding
    |
    v
Pinecone Vector Database <--- Embedded Chunks <--- Text Chunking <--- PDF Loader
    |
    v
Relevant Document Retrieval
    |
    v
RAG Chain (Groq + LangChain)
    |
    v
LLM-Generated Answer
```

## Key Features

- **Medical PDF Upload:** Allows users to upload medical documents, including notes, textbooks, and reports.
- **Text Extraction and Chunking:** Extracts text from uploaded PDFs and divides it into smaller chunks for efficient retrieval.
- **Text Embeddings:** Converts document chunks into vector representations using Google Generative AI or BGE embedding models.
- **Vector Storage:** Stores document embeddings in Pinecone for similarity-based retrieval.
- **Question Answering:** Retrieves relevant document sections and uses Groq's LLaMA 3 70B model through LangChain to generate responses.
- **REST API Backend:** Uses FastAPI to handle document uploads and question-answering requests.
- **Web Interface:** Provides an interface for uploading documents and interacting with the chatbot.

## Technology Stack

| Component | Technology |
|---|---|
| Large Language Model (LLM) | Groq API — LLaMA 3 70B |
| Embedding Models | Google Generative AI / BGE |
| Vector Database | Pinecone |
| LLM Orchestration | LangChain |
| Backend Framework | FastAPI |
| Client Interface | Streamlit |

## API Endpoints

The FastAPI backend provides the following endpoints:

| HTTP Method | Endpoint | Description |
|---|---|---|
| POST | `/upload_pdfs/` | Uploads one or more PDF files for processing and indexing. |
| POST | `/ask/` | Accepts a question through the `question` form field and returns an answer. |

### Request Details

**1. Upload Medical Documents**

- Endpoint: `/upload_pdfs/`
- Method: `POST`
- Purpose: Uploads PDF documents for text extraction, chunking, embedding, and vector storage.

**2. Ask a Question**

- Endpoint: `/ask/`
- Method: `POST`
- Form field: `question`
- Purpose: Retrieves relevant information from indexed documents and generates an answer using the RAG pipeline.

## Project Structure

```text
medicalAssistant/
|
├── assets/
│   ├── DIABETES.pdf
│   └── MedicalAssistant.pdf
|
├── client/
│   ├── components/
│   │   ├── chatUI.py
│   │   ├── history_download.py
│   │   └── upload.py
│   |
│   ├── utils/
│   │   └── api.py
│   |
│   ├── app.py
│   ├── config.py
│   └── requirements.txt
|
└── server/
    ├── middlewares/
    │   └── exception_handlers.py
    |
    ├── modules/
    │   ├── llm.py
    │   ├── load_vectorstore.py
    │   ├── pdf_handlers.py
    │   └── query_handlers.py
    |
    ├── routes/
    │   ├── ask_question.py
    │   └── upload_pdfs.py
    |
    ├── uploaded_docs/
    ├── logger.py
    ├── main.py
    ├── requirements.txt
    └── test.py
```

The `client` directory contains the Streamlit interface and supporting utilities. The `server` directory handles API requests, document processing, vector retrieval, and LLM-based responses.

## Installation and Setup

### Prerequisites

Make sure the following are available on your system:

- Python
- `uv` package manager
- Google Generative AI API key
- Groq API key
- Pinecone API key

### 1. Clone the Repository

```bash
git clone https://github.com/AnkitMnnit007/Medical-Assistant-RAG-Project.git
cd Medical-Assistant-RAG-Project
```

### 2. Set Up the Backend

Navigate to the server directory:

```bash
cd server
```

Create a virtual environment:

```bash
uv venv
```

On Windows, activate it using:

```bash
.venv\Scripts\activate
```

Install the required dependencies:

```bash
uv pip install -r requirements.txt
```

### 3. Configure Environment Variables

Create a `.env` file inside the `server` directory and add the following API credentials:

```env
GOOGLE_API_KEY=your_google_api_key
GROQ_API_KEY=your_groq_api_key
PINECONE_API_KEY=your_pinecone_api_key
```

Replace the placeholder values with your actual API keys. Keep the `.env` file private and do not commit it to your public repository.

### 4. Start the Backend Server

Run the FastAPI application using Uvicorn:

```bash
uvicorn main:app --reload --port 8000
```

The backend server will run on port `8000`.

### 5. Set Up the Client

Open a new terminal and navigate to the client directory from the project root:

```bash
cd client
```

Create a virtual environment:

```bash
uv venv
```

On Windows, activate it using:

```bash
.venv\Scripts\activate
```

Install the client dependencies:

```bash
uv pip install -r requirements.txt
```

### 6. Launch the Streamlit Application

Run the client interface:

```bash
streamlit run app.py
```

Open the local URL displayed in the terminal to access the chatbot.

## License

This project was developed by Ankit Kumar. All rights reserved.

## Author

**Ankit Kumar**
