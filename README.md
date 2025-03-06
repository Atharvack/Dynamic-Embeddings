# Dynamic Embedding Model for Retrieval-Augmented Generation (RAG)

This project implements a dynamic embedding system that classifies incoming queries into domains (e.g., Medical, Mathematics, Programming, Science, or General-Knowledge), re-embeds them using domain-specific models (when applicable), and indexes both query and document embeddings into ChromaDB for efficient retrieval. It demonstrates the complete workflow for a RAG pipeline—from dynamic embedding selection to document retrieval. 

## Table of Contents

- [Overview](#overview)
- [Architecture and Workflow](#architecture-and-workflow)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Code Overview](#code-overview)
- [Future Work](#future-work)
- [License](#license)

## Overview

In modern retrieval-augmented generation (RAG) pipelines, accurately fetching the most relevant context is critical for generating precise answers. To achieve this, our system:
- Uses a universal embedding model for initial query processing.
- Applies a trained Random Forest classifier to determine the query's domain.
- Uses domain-specific models (e.g., Bio_ClinicalBERT for Medical, math-specific models for Mathematics) to re-embed queries and related documents when necessary.
- Indexes both the query and document embeddings into an in-memory vector store (ChromaDB) for rapid similarity search based on cosine similarity.
- Constructs a final prompt that combines the user query and retrieved contextual document content for final answer generation by an LLM.

## Architecture and Workflow

### High-Level Workflow

1. **Query Classification:**
   - Input query is embedded using a universal model.
   - A Random Forest classifier predicts the query's domain (e.g., Medical, Programming, etc.).
2. **Dynamic Query Re-embedding:**
   - If the domain is not "General-Knowledge," the query (and the related documents) are re-embedded using a domain-specific model.
3. **Document Indexing:**
   - The system loads document data (via DuckDuckGo web loader) as JSON.
   - Each document's content is preprocessed, embedded, and stored in ChromaDB along with metadata and the original text.
4. **Retrieval:**
   - The query embedding is used to perform a similarity search in ChromaDB.
   - The top result (or results) are retrieved.
5. **Context Construction and Final Prompt:**
   - The retrieved document’s text is concatenated with the original query to create a final prompt.
   - This prompt can then be passed to a language model to generate an answer, thereby completing the RAG pipeline.

### Diagram

graph TD
A[User Query] --> B[Universal Embedding]
B --> C[RF Classifier]
C -->|General-Knowledge| D[Use Universal Model for Q & Docs]
C -->|Other Domains| E[Re-embed Query & Docs via Domain-Specific Model]
D --> F[Index Query & Docs in ChromaDB]
E --> F
F --> G[Query ChromaDB for Similarity]
G --> H[Retrieve Top Document]
H --> I[Construct Final Prompt]
I --> J[Pass Prompt to LLM for Generation]

##This final prompt is printed to the console, ready to be passed on to an LLM for answer generation


## Features

- **Dynamic Query Embedding:** Automatically adjusts the embedding model based on query classification.
- **Domain-Specific Re-embedding:** Uses specific models (e.g., Bio_ClinicalBERT, math models) ensuring contextual relevance.
- **ChromaDB Integration:** Indexes and retrieves embeddings using an ephemeral (in-memory) vector database.
- **Context Construction:** Merges the relevant document content with the query to create a rich prompt for LLMs.
- **Modular Design:** Clear separation between classification, embedding, indexing, and retrieval processes.

## Installation

First, clone this repository and install the required dependencies. 



## Jupyter Notebooks

<div id="notebook-content"></div>

<script>
  fetch('embeddings.html')
    .then(response => response.text())
    .then(data => {
      document.getElementById('notebook-content').innerHTML = data;
    });
</script>


## Future Work

- **LLM Integration:** Connect the final prompt to a language model (such as GPT, Llama, or others) for answer generation.
- **Persistent Storage:** Explore using a persistent ChromaDB client for long-term indexing.
- **Improved Document Ranking:** Fine-tune the retrieval or re-ranking mechanisms.
- **User Interface:** Build a simple web interface or CLI for easier interaction.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

