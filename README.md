# 🧠 Thai RAG for FahMai QA (Hybrid Retrieval + ThaiLLM)

An end-to-end **Retrieval-Augmented Generation (RAG)** system for answering Thai multiple-choice questions using hybrid retrieval and Thai Large Language Models (ThaiLLMs).

---

## 📌 Problem Overview

**FahMai (ฟ้าใหม่)** is a fictional Thai electronics store.

You are provided with a **Thai knowledge base** consisting of:

* 📦 Product pages
* 📜 Store policies
* 🏪 General store information

### 🎯 Objective

Build a system to answer **100 multiple-choice questions** about the store using only the provided knowledge base.

---

## ❓ Question Format

Each question contains **10 choices**:

* **1–8:** Answers derived from the knowledge base
* **9:** *"ไม่มีข้อมูลนี้ในฐานข้อมูล"* (No relevant information)
* **10:** *"คำถามนี้ไม่เกี่ยวข้องกับร้านฟ้าใหม่"* (Irrelevant question)

## 🚀 Key Features

* 🔍 **Hybrid Retrieval**

  * BM25 (keyword-based)
  * Dense embeddings (BGE-M3)
* 🔗 **Score Fusion + Reranking**
* 🇹🇭 **Thai Tokenization (PyThaiNLP)**
* 🧠 **LLM-based Reasoning**
* ❌ **Detection for:**

  * Missing information (Choice 9)
  * Irrelevant queries (Choice 10)
* 🔁 **Answer refinement loop**

---

## 🏗️ System Pipeline

```text
Knowledge Base → Chunking → Indexing
                         ↓
              BM25 + Embedding Search
                         ↓
                 Hybrid Retrieval
                         ↓
                    Reranking
                         ↓
                 Context Selection
                         ↓
                    ThaiLLM
                         ↓
                  Answer (1–10)
```

---

## 🧩 Methodology

### 1. Document Processing

* Split documents into chunks (~1000 tokens)
* Preserve semantic coherence

### 2. Retrieval

* **BM25** for lexical matching
* **BGE-M3** for semantic similarity

### 3. Hybrid Scoring

Combine scores:

```
score = α * BM25 + β * cosine_similarity
```

### 4. Context Selection

* Select top-k relevant chunks
* Remove noise / duplicates

### 5. Answer Generation

* Feed question + context to ThaiLLM
* Force output to be a single choice (1–10)

### 6. Post-processing

* Detect:

  * Low-confidence → reconsider
  * No evidence → choose 9
  * Irrelevant → choose 10

---


## 🧪 Challenges

* Thai language ambiguity
* Long context retrieval
* Avoiding hallucination
* Correctly identifying:

  * Missing info (Choice 9)
  * Irrelevant questions (Choice 10)

---

## 📊 Possible Improvements

* Cross-encoder reranker
* Query expansion
* Better threshold tuning
* Multi-hop retrieval
* Caching embeddings

---

## 🧠 Use Cases

* Thai QA systems
* RAG benchmarking
* Knowledge-based assistants
* AI competitions

---

## 👨‍💻 Author

Developed for Thai NLP and RAG system experimentation

---

