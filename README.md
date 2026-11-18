# Bangla Knowledge Base RAG Chatbot — শ্রীকান্ত (প্রথম পর্ব)

A Retrieval-Augmented Generation (RAG) chatbot built with LangChain, FAISS, HuggingFace multilingual embeddings, Groq LLM, and Gradio that answers questions strictly from Sarat Chandra Chattopadhyay's novel শ্রীকান্ত (প্রথম পর্ব) with exact chapter citations.

## Book Source
- Title: শ্রীকান্ত (প্রথম পর্ব) — Sarat Chandra Chattopadhyay
- Bengali Wikisource URL: [https://bn.wikisource.org/wiki/শ](https://bn.wikisource.org/wiki/শ)্রীকান্ত_(প্রথম_পর্ব)
- Chapters Crawled: All 12 chapter subpages (প্রথম পরিচ্ছেদ through দ্বাদশ পরিচ্ছেদ) via the MediaWiki API and BeautifulSoup.

## Embedding Model & Justification
- Model: BAAI/bge-m3
- Why: bge-m3 is a state-of-the-art multilingual dense retrieval model supporting 100+ languages including Bengali, with a large context window (8192 tokens) and strong semantic alignment for literary Bangla prose where standard English models fail.

## Chunking Strategy & Bonus Experiment
- Chosen Strategy: RecursiveCharacterTextSplitter with chunk_size=800, chunk_overlap=150, and Bangla-aware punctuation separators.
- Why: Splitting on the Bengali দাঁড়ি (।) preserves complete sentences, while 150-character overlap prevents narrative context loss across chunk boundaries.
- Bonus Hit-Rate Comparison (@3 across 6 benchmark chapter queries):
  - Strategy A (chunk_size=800, overlap=150): 424 chunks | 50.0% Hit-Rate @3
  - Strategy B (chunk_size=300, overlap=30): 1,194 chunks | 50.0% Hit-Rate @3
  - Strategy A achieved the exact same retrieval hit-rate with ~2.8x fewer chunks and richer narrative context per retrieved passage.

## How to Run
1. Install dependencies: pip install -r requirements.txt
2. Set your Groq API key: export GROQ_API_KEY='your_groq_api_key'
3. Run the notebook (Bangla_RAG_Chatbot.ipynb) in Google Colab (T4 GPU recommended) or locally to crawl the chapters, build the FAISS index, and launch the Gradio chat interface.
