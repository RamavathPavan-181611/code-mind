# Codebase RAG

Repository-aware Retrieval-Augmented Generation system for codebase understanding.

## Current Status

### Indexed Repositories

* Flask
* Werkzeug

### Current Graph Statistics

* Chunks: ~4,056
* Edges: ~15,670
* Calls: ~12,791
* Resolved Calls: ~3,806

### Stack

* Python
* Qdrant
* Sentence Transformers
* Cross Encoder Reranking
* AST-based Code Parsing

## Pipeline
``` mermaid 
graph TD
     A[Repository Source Code] --> B[AST Chunking]
     B --> C[Symbol Extraction]
     C --> D[Call Graph Construction]
     D --> E[Embedding Generation]
     E --> F[Qdrant Storage]
     F --> G[Hybrid Retrieval]
     G --> H[Cross Encoder Reranking]
     H --> I[LLM Answer Generation]

     %% Styling to make it look clean
     style F fill:#f9f, stroke : #333, stroke-width:2px


```


## Setup

### Create Environment

```bash
python -m venv venv
venv\Scripts\activate
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Start Qdrant

```bash
docker run -p 6333:6333 qdrant/qdrant
```

## Index Repositories

Configure repositories in:

```text
rag_config.json
```

Example:

```json
{
  "repos": [
    "flask_repo",
    "werkzeug_repo"
  ]
}
```

Build graph:

```bash
python chunker.py
```

Generate embeddings:

```bash
python ingest.py
```

## Run Agent

```bash
python agent.py
```

Example questions:

* How are blueprints registered?
* How does request dispatch work?
* How is session handling implemented?
* How does template rendering work?

## Current Limitations

* Symbol resolution still misses many indirect calls.
* Retrieval occasionally surfaces tests instead of implementation code.
* Multi-hop graph traversal needs improvement.
* Repository-specific ranking is not implemented yet.

## Next Priorities

1. Improve retrieval quality.
2. Improve symbol resolution.
3. Better graph traversal.
4. Strong benchmark suite.
5. Multi-repository support beyond Flask/Werkzeug.

## Version

Current checkpoint: v0.1
