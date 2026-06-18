# YouTube Transcript RAG

Ask questions about any YouTube video using Retrieval-Augmented Generation (RAG).

## How It Works

```
YouTube URL
    ↓
youtube-transcript-api  →  raw transcript text
    ↓
RecursiveCharacterTextSplitter  →  chunks (1000 chars, 200 overlap)
    ↓
OpenAI text-embedding-3-small  →  vector embeddings
    ↓
FAISS vector store  →  similarity search on query
    ↓
Mistral-7B-Instruct (HuggingFace)  →  answer grounded in retrieved chunks
```

## Features

- Single-video Q&A
- Multi-video RAG (query across multiple videos with source attribution)
- Persistent FAISS index (avoids re-embedding on every run)
- Works with any public YouTube video that has captions (auto-generated or manual)

## Tech Stack

| Component | Library |
|-----------|---------|
| Transcript fetch | `youtube-transcript-api` |
| Embeddings | `langchain-openai` + `text-embedding-3-small` |
| Vector store | `FAISS` (CPU) |
| LLM | `HuggingFaceEndpoint` + `Mistral-7B-Instruct-v0.3` |
| Orchestration | `LangChain` |
