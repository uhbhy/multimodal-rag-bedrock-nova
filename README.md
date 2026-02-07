Multimodal RAG on AWS (Bedrock + Nova)

A production-style multimodal Retrieval-Augmented Generation (RAG) system built on AWS.
The system ingests PDFs containing text, images, and tables, embeds them using AWS Titan, retrieves relevant context via FAISS, and generates grounded answers using Amazon Nova.

✨ Key Highlights

📄 Multimodal PDF ingestion (text, images, tables)

🧠 RAG-only architecture (no agents, deterministic retrieval)

🧩 Modality-aware chunking and indexing

🔍 FAISS-powered similarity search

🤖 Multimodal prompting with Amazon Nova

☁️ Built entirely on AWS Bedrock-compatible components

🧱 System Architecture

The diagram below shows both indexing-time and query-time flows, making the system easy to understand at a glance.

```` ```mermaid ````
flowchart LR
    %% =======================
    %% Indexing Pipeline
    %% =======================
    subgraph Indexing["📦 Indexing Pipeline"]
        A[PDF Documents] --> B[Multimodal Ingestion]

        B --> T[Text Extraction]
        B --> I[Image Extraction]
        B --> Tb[Table Extraction]

        T --> C[Chunking & Normalization]
        I --> C
        Tb --> C

        C --> E[Embeddings<br/>AWS Titan]
        E --> V[FAISS Vector Store]
    end

    %% =======================
    %% Query Pipeline
    %% =======================
    subgraph Query["🔎 Query & Generation Pipeline"]
        Q[User Query] --> R[Similarity Retrieval]
        R --> P[Multimodal Prompt Assembly]
        P --> N[Amazon Nova]
        N --> O[Final Answer]
    end

    %% =======================
    %% Shared Connections
    %% =======================
    V --> R
 ```` ``` ````
🧠 Architecture Walkthrough
1. Multimodal Ingestion

PDF documents are parsed using best-in-class tools for each modality:

Text → LangChain loaders

Images → PyMuPDF

Tables → Tabula

Each modality is extracted independently to preserve semantic structure.

2. Chunking & Embeddings

All extracted content is:

Normalized

Chunked (recursive, overlapping where needed)

Embedded using AWS Titan Embeddings

This ensures high-quality retrieval across different content types.

3. Vector Storage & Retrieval

Embeddings are stored in a FAISS vector database

Queries perform similarity search to retrieve the most relevant chunks

4. Multimodal Generation

Retrieved chunks are assembled into a multimodal prompt and passed to:

Amazon Nova (via AWS Bedrock)

Nova reasons over text + visual context to generate grounded answers.

🧰 Tech Stack
Layer	Technology
PDF Parsing	LangChain, PyMuPDF, Tabula
Embeddings	AWS Titan
Vector Store	FAISS
LLM	Amazon Nova
Platform	AWS Bedrock
Language	Python
🚀 Features

Multimodal PDF ingestion (text, tables, images)

Recursive text chunking with overlap

FAISS-based vector similarity search

Amazon Bedrock Nova integration

Vision + text grounded generation

Robust handling of noisy, real-world PDFs

📌 Design Choices

RAG-only (no agents) → predictable, debuggable behavior

FAISS (local) → fast iteration & cost control

Modality-aware ingestion → better grounding and fewer hallucinations
