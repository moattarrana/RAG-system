# RAG-system

User Query
   ↓
Preference Extraction (manual / rule-based)
   ↓
TF-IDF Vectorization
   ↓
FAISS Similarity Search (Retrieval)
   ↓
Metadata Filtering (city, category, price)
   ↓
Re-ranking (rule-based scoring)
   ↓
Context Quality Check
   ↓
Groq LLM (Answer Generation)
   ↓
Final Travel Response
**DATASET**
Wikipedia / Wikivoyage Berlin pages
Each entry contains metadata:
city
category (food / art / sightseeing)
price_level (cheap / medium / expensive)
url

**1. TF-IDF Embeddings**
**Why TF-IDF?**
Avoids heavy dependencies like PyTorch
Lightweight and fast
Works well for small datasets
Suitable for educational RAG pipelines

TF-IDF converts text into numerical vectors based on word importance.

**2. FAISS Vector Database
Why FAISS?**
Efficient similarity search
Handles dense vector retrieval quickly
Industry-standard tool for vector search

**3. Metadata Filtering**

After retrieval, results are filtered using structured metadata:

City match (e.g., Berlin)
Category match (food, art, sightseeing)
Price level (cheap, medium, expensive)
To ensure context relevance beyond semantic similarity.

**4. Re-ranking (Rule-based scoring)**

A simple scoring system is used to improve ranking quality:

Keyword overlap with query
Boost for relevant categories (food, art)
Boost for budget-friendly options
Why?

To simulate a lightweight ranking model without using an LLM or deep learning re-ranker.

**5. Context Quality Check (LLM-style gate)**

Before sending data to the LLM:

If retrieved context is too weak → mark as context_insufficient
Otherwise → proceed
Why?

Prevents hallucination and ensures only meaningful context is sent to Groq.

**6. Groq LLM (Answer Generation)**

The final step uses Groq’s LLM API to generate a travel response.

Why Groq?
Fast inference
Lightweight API integration
Suitable for real-time RAG pipelines

The model is prompted with:

User query
Retrieved context chunks

The output is a grounded travel plan.

**Design Decisions**
Why no PyTorch / Sentence Transformers?

Due to environment issues (DLL / compatibility problems), a lightweight alternative was chosen:

TF-IDF instead of transformer embeddings
FAISS instead of deep embedding pipelines

**This ensures:**

Stability
Simplicity
Reproducibility on any system
**Limitations**
Dataset is small and simplified
No real-time web scraping
Re-ranking is rule-based (not ML-based)
TF-IDF has limited semantic understanding compared to transformers
🧪 Example Query
Input:

“3-day Berlin trip with cheap food and art”

Output:
Berlin food recommendations
Art and cultural places
Budget-friendly suggestions
Generated structured travel plan from Groq


