# 📘 Day 2: Embeddings & Vector Stores

**Podcast:** [Whitepaper Companion - Embeddings & Vector Stores](https://www.youtube.com/watch/xCAVsst6WJ8)  
**Transcript Source:** tactiq.io  
**Part of:** 5-Day Generative AI Intensive  
**Author:** Rishabh Tiwari (rishtiwari98@gmail.com)  

---

## 🎯 Purpose of This Session

This session is a deep technical exploration of **embeddings**, **vector stores**, and **retrieval-based systems**. Topics include:

- What embeddings are
- How they work and why they’re important
- Applications in retrieval, recommendation, RAG
- Evaluation methods and metrics
- Vector search algorithms (ANN, HNSW, SCaNN)
- Real-world implementation techniques
- Multimodal and structured data embeddings

---

## 🧠 What Are Embeddings?

### 🔍 Definition
- Embeddings = low-dimensional numerical representations of data (text, images, audio, etc.)
- Used to **preserve semantic meaning** and make data machine-interpretable.

### 🧭 Analogy
- Like latitude & longitude for data — reduces complex input to compact vectors without losing context.

### 🔄 Benefits
- Enables pattern recognition across modalities
- Improves efficiency in storage, retrieval, and processing
- Used extensively with LLMs to **represent meaning** numerically

---

## ⚙️ Why Embeddings Matter

- Enable **semantic understanding** — e.g., “king” is closer to “queen” than to “bicycle”
- Allow comparisons and clustering of data by meaning, not syntax
- Useful across **text, image, audio, video**, and **structured data**

---

## 🔍 Applications of Embeddings

### 🔎 Retrieval Systems
- Web search: convert queries and documents to embeddings → find nearest neighbors
- Pre-compute embeddings for all documents
- User query is embedded → top matches are retrieved based on similarity

### 🤝 Recommendation Systems
- Suggest similar items based on embedding proximity to user history
- Leverages implicit preferences

### 🧭 Joint Embeddings (Multimodal)
- Align **text and images** in the same space → e.g., find videos/images from a textual description

---

## 📏 Measuring Embedding Effectiveness

### 🔑 Retrieval Quality
- Key goal: distinguish **relevant vs. irrelevant** items

### 📊 Metrics

| Metric         | Description |
|----------------|-------------|
| Precision      | % of retrieved items that are relevant |
| Recall         | % of relevant items that were retrieved |
| Precision@k    | Precision among top-k results |
| Recall@k       | Recall among top-k results |
| nDCG (Normalized Discounted Cumulative Gain) | Penalizes relevant items ranked lower in result list |

### 📐 Benchmarks
- BEIR, MTEB — standardized datasets and tasks for fair comparisons
- Libraries: `trec_eval`, `pytrec_eval`, `scikit-learn`

---

## 🧮 Factors in Choosing Embedding Models

- **Model Size**
- **Embedding Dimension**
- **Latency**
- **Cost**
- Trade-off between accuracy and deployment feasibility

---

## 🧰 Retrieval-Augmented Generation (RAG)

### 🔁 Two-Stage Process

1. **Index Creation**
   - Chunk documents
   - Generate embeddings with document encoder
   - Store in vector DB

2. **Query Processing**
   - Encode user query
   - Search for top-matching chunks in vector DB
   - Inject retrieved context into LLM prompt

➡️ Greatly boosts accuracy and **reduces hallucinations**.

---

## 💥 Real-World Example

- Google's embedding model **BGE** improved average BEIR score from **10.6 to 55.7**
- Emphasizes: design systems to **swap in better models** as they evolve

---

## 🧑‍💻 Code Snippet 1 (NF Corpus Example)

- Embed questions & documents using Vertex AI
- Use `FAISS` for efficient similarity search
- Evaluate results using `pytrec_eval`

---

## 📚 Text Embeddings

### 🔁 Tokenization
- Break text into tokens (words, subwords, characters)
- Assign IDs → feed to models

### 🧊 One-Hot Encoding
- Binary vector representation — **sparse**, lacks semantic relationships

---

## 📦 Word Embeddings

| Model      | Notes |
|------------|-------|
| Word2Vec   | Predict context (CBOW) or target word (Skip-Gram) |
| GloVe      | Global co-occurrence statistics (matrix factorization) |
| Swivel     | Like GloVe but distributed and scalable |
| FastText   | Includes subword info |

- **CBOW**: predict word from context
- **Skip-Gram**: predict context from word

🔎 “You shall know a word by the company it keeps”

### 📊 Visualization
- Snippet 3: Load + project embeddings with `TSNE`
- Find nearest neighbors in 2D

---

## 📰 Document Embeddings

| Technique   | Description |
|-------------|-------------|
| Bag of Words | Simple word frequency count |
| TF-IDF       | Weight rare terms more |
| BM25         | TF-IDF improvement, strong baseline |
| LSA          | Matrix factorization on word-document matrix |
| LDA          | Probabilistic topic modeling |
| Doc2Vec      | Extends Word2Vec by learning a **paragraph vector** |

### ➕ Advanced Techniques

- **BERT-based** encoders produce contextualized embeddings
- Use `[CLS]` token to represent full sequence

### 🔥 Modern Models

| Model     | Purpose |
|-----------|---------|
| BERT      | Contextual token embeddings |
| Sentence-BERT | Sentence-level embeddings |
| SimCSE    | Self-supervised |
| E5        | Pretrained for embedding tasks |
| GTR       | Gemini-powered encoder |
| Sentence-T5 | T5-based embeddings |

🧪 Snippets 4 & 5:
- Use TensorFlow Hub, Vertex AI, LangChain + BigQuery for full stack usage

---

## 🖼️ Image & Multimodal Embeddings

### 🧠 How They Work
- Use **CNNs** or **Vision Transformers**
- Extract embeddings from **later layers**

### 📸 Joint Embeddings
- Combine image and text into single representation
- Used for image search, captioning, etc.

### 🧪 Snippet 6
- Use Vertex AI to compute image & multimodal embeddings
- **KALI**: Retrieve content from text/image docs without OCR

---

## 🧮 Structured Data Embeddings

### Types:

- **Tabular** (rows & columns): Use PCA or other reduction
- **User & Item**: Recommendation systems → shared embedding space
- **Hybrid**: Combine structured + unstructured (e.g. product reviews + metadata)

---

## 🌐 Graph Embeddings

### 🕸️ Purpose
- Encode **nodes and edges** from graphs (social networks, knowledge graphs)

### 🔍 Popular Algorithms

| Name       | Type |
|------------|------|
| DeepWalk   | Random walks → word2vec |
| node2vec   | Biased random walks |
| LINE       | Large-scale info network embeddings |
| GraphSAGE  | Uses node features during training |

---

## 🧪 Training Embedding Models

### 🧠 Dual Encoder Setup

- One encoder for queries
- One for documents
- Trained with **contrastive loss**: similar = close, dissimilar = far

### 🔄 Workflow

1. **Pretraining**
   - Train on huge corpus
   - Often start from LLM weights (BERT, GPT, Gemini, etc.)

2. **Fine-Tuning**
   - Task-specific labeled or synthetic data
   - Techniques:
     - **Manual labeling**
     - **Synthetic generation**
     - **Hard negative mining**
     - **Distillation**

🧪 Snippet 7: Use TensorFlow to build classifier on top of embeddings

---

## 🔍 Vector Search

### 🔍 How It Works

1. Embed all data
2. Store in vector DB
3. Embed query
4. Find **nearest neighbors**

### ⚡ ANN (Approximate Nearest Neighbor)

| Technique | Description |
|----------|-------------|
| LSH      | Hash similar vectors into same buckets |
| KD Trees / Ball Trees | Partition data space recursively |
| HNSW     | Hierarchical proximity graph |
| SCaNN    | Google's scalable ANN algorithm |

🧪 Snippets:
- 8: Brute Force, Ball Tree, LSH with Scikit-learn
- 9: Vertex AI Vector Search index
- 10: FAISS + HNSW
- 11: SCaNN + TensorFlow Recommenders

---

## 🧱 Vector Databases

| Type | Examples |
|------|----------|
| Dedicated | Pinecone, Weaviate, Chroma, FAISS |
| Cloud-native | Vertex AI Vector Search, AlloyDB, Cloud SQL |
| Hybrid (traditional + vector) | Postgres with pgvector, Redis, Elasticsearch |

### 🧠 Operational Considerations

- Scalability
- Availability
- Updates & reindexing
- Security
- Versioned embeddings (as models evolve)

---

## 🧪 Use Cases

- Information retrieval
- Recommendation systems
- Semantic search
- Classification & clustering
- RAG
- Anomaly detection
- Few-shot classification

---

## 🧵 Final Thoughts

- Embeddings are foundational for modern AI systems.
- Constantly evolving: from Word2Vec → BERT → Gemini
- Paired with vector stores, embeddings unlock scalable, semantic applications across all data modalities.
- Know your task and data type → pick the right embedding + search + infra.

---

*Prepared by: **Rishabh Tiwari***  
📧 *rishtiwari98@gmail.com*  
📅 *Day 2 – 5-Day Generative AI Intensive*
