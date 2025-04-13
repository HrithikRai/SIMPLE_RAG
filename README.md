# RAG Powered Financial Compliance Analyst

**By – Hrithik Rai**

---

## 📌 Problem Statement

Build a Retrieval-Augmented Generation (RAG) based LLM application that:

- Indexes a provided dataset of fictional organization descriptions.
- Retrieves the most relevant organizations based on a natural language query.
- Constructs an effective prompt using the retrieved context.
- Uses a LLM to generate a coherent answer addressing the query.

---

## ⚙️ Tech Stack

| Component              | Tool/Service                  |
|------------------------|-------------------------------|
| **LLM Model**          | Cohere (Command R+)           |
| **Embeddings**         | Cohere (embed-english-v3.0)   |
| **LLM Orchestration**  | Langchain                     |
| **Vector DB**          | Chroma                        |
| **Language**           | Python                        |

> ℹ️ Note: API keys and configurations are managed via `.env` and `.toml` files. Dependencies listed in `requirements.txt`.

---

## 📥 Data Ingestion

- Created a **custom document loader** using `BaseLoader` from Langchain.
- Regex used to split documents by `Document X:` for parsing.
- Skipped lazy loading due to low document size.

---

## 📦 Indexing Strategy

- Cleaned and preprocessed documents to remove newline characters for token efficiency.
- Embedded using **Cohere** embeddings.
- Vector store created using **Chroma**, with a persistent collection: `organizations_profile`.

---

## 🔍 Retrieval Approaches

- Evaluated:
  - **Vanilla Similarity Search**
  - **Maximal Marginal Relevance (MMR)**
  - **Similarity + Threshold**

> 🏆 **MMR** was chosen as the final strategy due to its ability to reduce redundancy and improve relevance.

---

## 🧠 Prompt Engineering

Tested six different prompt formats:

1. **Base Prompt** – for baseline comparison.
2. **Risk-Focused Framing** – directs attention to red flags.
3. **Regulatory Tone + Evaluation Metric** – makes the LLM evaluate responses.
4. **Chain-of-Thought Prompting** – encourages reasoning.
5. **Focused Extraction** – restricts answers to relevant entities.
6. **Summarize + Analyze** – encourages internal summarization before answering.

---

## 🔄 Query Pipeline

`User Query → Retriever → Retrieved Docs → Prompt Template → LLM → Response`

### 🧪 Sample Query:
> _"Which organizations show signs of financial red flags like money laundering and insider trading?"_

---

## 📊 Evaluation Metrics

Two utility functions implemented to evaluate:

- `calculate_precision_recall` → For retrieval evaluation.
- `compute_clarity` → For LLM response evaluation.

### Metrics Measured:

- Relevance & precision
- Clarity & verbosity
- Coherence & token efficiency
- Named entity density
- Response time
- Token consumption (input/output/total)

---

## 📈 Summary of Results

| Prompt Variation                | Precision | Clarity | Response Time | Token Usage |
|---------------------------------|-----------|---------|----------------|--------------|
| 🧠 **Chain-of-Thought**          | High      | High    | ⏱️ ~15.88s     | 🔺 Highest   |
| 🎯 **Focused Extraction**        | 🔥 Highest| 🔥 High | ⏱️ Fast         | 🔻 Lowest    |
| 🏛️ **Regulatory Tone + Eval**    | Balanced  | High    | Moderate        | Moderate     |
| 🧾 **Summarize + Analyze**       | Moderate  | Good    | Moderate        | Moderate     |

---

## 🧩 Use Case Recommendations

- **Chain-of-Thought**: Best for in-depth forensic/risk assessments.
- **Focused Extraction**: Ideal for dashboards needing named-entity precision.
- **Regulatory + Eval**: Best suited for compliance reporting interfaces.
- **Summarize + Analyze**: Balanced insights for general dashboards.

---

## 📁 Notebooks & Code

📓 **Notebook**: [Click here to open analysis](https://github.com/HrithikRai/SIMPLE_RAG/blob/main/proof_of_concept/solution.ipynb)  
📄 **Project Files**: Include `.env`, `.toml`, `requirements.txt`, and source scripts.

---

## 📬 Contact

For questions or discussions, feel free to reach out!

---
