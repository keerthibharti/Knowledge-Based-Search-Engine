
# Knowledge-base Search Engine

## Submitted by:
**Name:** Keerthi Bharti  
**Registration Number:** 22BCE9187  
**For:** Unthinkable Recruitment Assignment  
**Date:** 2025-10-15

---

## 1. Abstract

This project implements a Knowledge-base Search Engine that retrieves and synthesizes information from multiple documents using Retrieval-Augmented Generation (RAG). The system allows users to upload text or PDF documents, stores their embeddings in a vector database, and uses an LLM (GPT-based) to generate synthesized answers for user queries.

---

## 2. System Architecture

### Workflow:
1. **Document Ingestion:** Upload PDFs or text documents.
2. **Embedding Generation:** Convert document chunks into embeddings using OpenAI Embeddings API.
3. **Vector Storage:** Store embeddings in FAISS vector database.
4. **Query Handling:** Convert the user query into an embedding, retrieve similar documents.
5. **Answer Synthesis:** Use an LLM (GPT-4) to synthesize an answer based on retrieved documents.

### Architecture Diagram:
```
User Query → Embed Query → Retrieve Relevant Docs (FAISS) →
LLM (GPT-4) → Synthesized Answer
```

---

## 3. Technical Stack

| Component | Technology |
|------------|-------------|
| Backend API | FastAPI |
| Embeddings | OpenAI Embeddings / SentenceTransformers |
| Vector Store | FAISS |
| LLM | OpenAI GPT-4 |
| Frontend (Optional) | Streamlit |
| File Handling | PyPDF2, langchain.text_splitter |

---

## 4. Implementation Details

### Key Steps:
- **Document Upload:** `/upload` endpoint accepts PDFs or text files.
- **Embedding Creation:** Documents are split into chunks (e.g., 500 tokens each) and converted into embeddings.
- **Storage:** Embeddings are stored locally using FAISS index.
- **Querying:** `/query` endpoint takes user input, retrieves top matches, and sends context to LLM for answer generation.

### Example Prompt:
```
Using these documents, answer the user’s question succinctly.
Documents:
{{retrieved_texts}}

Question: {{user_query}}
Answer:
```

---

## 5. Sample API Structure

```
app/
│
├── main.py                # FastAPI entry point
├── embeddings.py          # Generate embeddings
├── retriever.py           # FAISS retrieval logic
├── llm.py                 # GPT-based synthesis
├── utils.py               # PDF/Text extraction helpers
├── requirements.txt       # Dependencies
└── README.md              # Setup guide
```

---

## 6. Example Code Snippet

```python
# main.py
from fastapi import FastAPI, UploadFile, Form
from retriever import retrieve_docs
from llm import generate_answer
import os

app = FastAPI()

@app.post("/query")
async def query_knowledge_base(query: str = Form(...)):
    context = retrieve_docs(query)
    answer = generate_answer(query, context)
    return {"answer": answer}
```

---

## 7. Evaluation

| Metric | Description |
|--------|--------------|
| Retrieval Accuracy | How well the system retrieves relevant chunks |
| Synthesis Quality | Clarity and correctness of generated answers |
| Latency | Average response time |
| Code Modularity | Ease of extension and debugging |

---

## 8. Challenges & Future Work

- Improving retrieval relevance for complex queries.
- Supporting larger document sets efficiently.
- Adding UI for document management and visualization.

---

## 9. Conclusion

This project demonstrates a scalable Knowledge-base Search Engine leveraging RAG with FastAPI, FAISS, and GPT-4. It effectively retrieves, ranks, and synthesizes information from uploaded documents, showcasing practical LLM integration.

---

## 10. References

- OpenAI API Documentation  
- LangChain Documentation  
- FastAPI Official Docs  
- FAISS GitHub Repository
