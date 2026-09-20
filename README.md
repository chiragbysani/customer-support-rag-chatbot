# Customer Support Chatbot — E-Commerce (RAG-Based)
An end to end Retrieval Augmented Generation (RAG) chatbot built for e-commerce customer support. The chatbot answers queries on refund policy, shipping, product sizing, and payment grounded strictly in company documents, with source citations on every answer.

#What It Does:

-Answers customer queries using only retrieved company documents no hallucinations.

-Cites the source document for every answer (e.g., [source: ROX-2025-05]).

-Supports multi turn conversation with full chat history awareness.

-Retrieves the top 3 most relevant document chunks per query using semantic search.

#Tech Stack:

-LLM	:Gemma 3 4B (via Ollama).

-Embeddings: nomic-embed-text (via Ollama).

-Vector Store: FAISS.

-RAG Framework: LangChain (ConversationalRetrievalChain).

-Document Loader: PyPDFLoader.

-Text Splitter: RecursiveCharacterTextSplitter.

-Runtime: Google Colab (T4 GPU).

#Project Architecture:
PDF Documents
     →
PyPDFLoader → RecursiveCharacterTextSplitter (chunk_size=300, overlap=30)
     →
nomic-embed-text (OllamaEmbeddings)
     →
FAISS Vector Store
     →
Retriever (top-k=3)
     →
ConversationalRetrievalChain + Gemma 3 4B
     →
Answer with Source Citation.

#Sample Output:

Q: If I'm not happy with my purchase, what is your refund policy and how do I start a return?

A: If your gear doesn't fit or just isn't your vibe, send it back within 30 days of delivery
   for a refund or free size exchange. [source: ROX-2025-05]


Q: How long will delivery take for a standard order, and where can I track my package?

A: A tracking link is emailed upon label creation. Status updates may take up to 12h to
   appear after the parcel is scanned at origin terminal. [source: 6]

# How to Run:

#1.Install dependencies:

!apt-get install -y zstd

!curl -fsSL https://ollama.com/install.sh | sh

!pip install langchain langchain-community langchain-core langchain-text-splitters langchain-classic faiss-cpu pypdf ollama

#2.Start Ollama server:

import subprocess, time

subprocess.Popen(["ollama","serve"])

time.sleep(5)

#3.Pull models:

!ollama pull gemma3:4b

!ollama pull nomic-embed-text

#4.Mount Drive and run notebook:

from google.colab import drive

drive.mount('/content/drive')

#5.Step 5 — Run the notebook:

#Author:
Chirag A Bysani

-GitHub: chiragbysani.

-Email: chiragbysani98@gmail.com


#
