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

## Setup

```bash
pip install -r requirements.txt
```

Create a `.env` file:

```
OPENAI_API_KEY=sk-...
HUGGINGFACEHUB_API_TOKEN=hf_...
```

Get your HuggingFace token at [huggingface.co/settings/tokens](https://huggingface.co/settings/tokens).  
You need to accept the [Mistral-7B-Instruct-v0.3](https://huggingface.co/mistralai/Mistral-7B-Instruct-v0.3) model license on HuggingFace.

## Usage

Open `youtube_rag.ipynb` and run all cells.  
Change `DEMO_URL` to any YouTube video with captions.

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
