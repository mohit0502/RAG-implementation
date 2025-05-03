# RAG-implementation
This repository contains prototype notebooks exploring Retrieval-Augmented Generation (RAG) pipelines using Pinecone as the vector database for document retrieval.

## Notebooks Overview

| Notebook                         | Description                                                   |
|---------------------------------|---------------------------------------------------------------|
| **RAG_implementation_pinecone.ipynb** | Implements a RAG pipeline using **Pinecone** as the vector store. |
| **RAG_implementation_v2.ipynb**       | Implements a RAG pipeline using **FAISS** as the vector store. |

---

## Key Differences

| Feature             | `RAG_implementation_pinecone.ipynb`         | `RAG_implementation_v2.ipynb`                  |
|---------------------|----------------------------------------------|------------------------------------------------|
| **Vector Store**    | Pinecone                                       | FAISS                                          |
| **Code Structure**  | Linear, minimal modularization                | Modularized                                    |
| **Metadata Filtering** | Patient ID filtering after querying   | Patient ID filtering supported via metadata |
| **Prompt Design**   | Concatenation-based prompt creation           | Structured prompt creation                     |
| **Embedding Function** | Embedding generation and indexing combined | Embedding and indexing steps are modular       |

---

## Functions — Detailed Explanation

Below are the key functions implemented across both notebooks:

---

### `embed_query(query: str) -> List[float]`

**Purpose:**  
Converts a query string into an embedding vector using a selected embedding model.

**Used in:** Both notebooks.

---

###  `index_data(data: pd.DataFrame, index_name: str)`

**Purpose:**  
Generates embeddings for all text entries and upserts them into the vector index.

**Used in:** 
- **Pinecone notebook**: Direct indexing into Pinecone.
- **FAISS notebook**: Indexing into FAISS.

**Key Steps:**  
- Loop through text entries.
- Generate embeddings.
- Index into the chosen vector store.

---

### `retrieve_context(query: str, top_k: int, patient_id: int = None) -> List[str]`

**Purpose:**  
Retrieves the top `k` relevant entries from the vector store based on the query embedding.

**Used in:** Both notebooks.

**Notes:**  
- In both notebooks, results can be filtered by `patient_id` either during or after retrieval depending on the method used.

---

### `generate_response(context: List[str], query: str) -> str`

**Purpose:**  
Combines retrieved context and the user query to generate a response using a language model.

**Used in:** Both notebooks.

---

### `batch_embed_and_store(data: pd.DataFrame)`

**(Optional helper function in FAISS notebook)**

**Purpose:**  
Embeds and stores the dataset in a batch process for cleaner and reusable code.

---

## Summary

- Both notebooks demonstrate the core components of a RAG pipeline: **embedding**, **retrieval**, **prompt construction**, and **response generation**.
- One notebook uses **Pinecone** as the vector store while the other uses **FAISS**.
- Both implementations support metadata filtering and leverage language models for generation tasks.

---

