# multimodal-rag-bedrock-nova
This project implements a Multimodal Retrieval-Augmented Generation (RAG) pipeline using AWS Bedrock's Nova and Titan models.  The system ingests PDFs and extracts: - Text - Tables - Embedded images - Full-page images  It performs similarity search using FAISS and generates grounded answers using "Amazon Nova" with both text and visual context.
