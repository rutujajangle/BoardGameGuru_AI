# BoardGameGuru_AI: A Board Game Rule Q&A with Retrieval‑Augmented Generation (RAG)

A lightweight Python pipeline that turns lengthy board‑game rule PDFs into an interactive Q&A experience powered by Google Generative AI’s embedding & text‑generation APIs.

---

## 🚀 Features

- **Document Understanding**  
  Automatically extracts and splits PDF rulebooks into ~300‑word chunks using **PyPDF2**.

- **Embeddings & Vector Search**  
  Converts each chunk into a semantic embedding via Google GenAI’s `text‑embedding‑004` model.  
  Retrieves the top‑K most relevant chunks with a cosine‑similarity search.

- **Retrieval‑Augmented Generation (RAG)**  
  Grounds answers in the official rulebook text by feeding retrieved chunks into a controlled prompt.

- **Controlled Few‑Shot Prompting**  
  Builds structured prompts and calls the **Gemini‑2.0‑Flash** model (`client.models.generate_content`) to generate concise, factual answers.

- **Interactive CLI**  
  Query any rule (“How do I set up the game board?”) and receive instant answers with context previews.

---

## 🏗 Architecture

1. **PDF Ingestion**  
   Read & extract text from `/kaggle/input/boardgame-rulebooks/…/*.pdf`.

2. **Chunking**  
   Split each document into ~300‑word segments.

3. **Embedding Generation**  
   Batch‑embed text chunks via `genai.embed_content(content, model="text‑embedding‑004")`.

4. **Vector Retrieval**  
   Embed user query, compute cosine similarity against all chunk embeddings, and select top‑K matches.

5. **Answer Synthesis**  
   Insert retrieved context into a few‑shot prompt and generate the final answer with the Gemini‑2.0‑Flash model.

---

## 🔧 Getting Started

### Prerequisites

- Python 3.8+  
- A Google Cloud Generative AI API key (store as `GOOGLE_API_KEY` via Kaggle Secrets or env var)

### Installation

```bash
git clone https://github.com/rutujajangle/BoardGameGuru_AI.git
cd BoardGameGuru_AI

# Create a virtual environment
python -m venv .venv && source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt

