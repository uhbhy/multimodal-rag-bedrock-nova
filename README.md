# Multimodal-rag-AWS

PDF documents are ingested through a multimodal pipeline. Text is extracted using
LangChain, images using PyMuPDF, and tables using Tabula. All extracted content is
normalized and chunked before generating vector embeddings with AWS Titan.

Embeddings are stored in a FAISS vector database. At query time, relevant chunks
are retrieved via similarity search, assembled into a multimodal prompt, and
passed to Amazon Nova for answer generation.

## Architecture
flowchart LR
    A[PDF Documents] --> B[Multimodal Ingestion]

    subgraph Ingestion
        B --> B1[Text Extraction<br/>LangChain]
        B --> B2[Image Extraction<br/>PyMuPDF]
        B --> B3[Table Extraction<br/>Tabula]
    end

    B1 --> C[Chunking]
    B2 --> C
    B3 --> C

    C --> D[Embeddings<br/>AWS Titan]
    D --> E[FAISS Vector Store]

    E --> F[Similarity Retrieval]
    F --> G[Multimodal Prompt Assembly]
    G --> H[Amazon Nova]
    H --> I[Final Answer]
## Features
- Multimodal PDF ingestion (text, tables, images)
- Recursive text chunking with overlap
- FAISS-based vector search
- Amazon Bedrock Nova integration
- Vision + text grounded generation
- Robust error handling for real-world PDFs
