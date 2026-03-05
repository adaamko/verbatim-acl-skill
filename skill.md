# Verbatim ACL Skill

Search and query 90,000+ ACL Anthology papers with verbatim, cited answers.

## Setup

You need a Verbatim API key. Get one at https://verbatim.krlabs.eu (sign up → API Keys).

Set it as an environment variable:
```
export VERBATIM_API_KEY=vb_your_key_here
```

## Endpoints

Base URL: `https://verbatim.krlabs.eu`

All requests require the header: `Authorization: Bearer $VERBATIM_API_KEY`

---

### Ask a Research Question (RAG Query)

The primary tool. Ask a question and get a verbatim answer with citations to source papers.

```bash
curl -s -X POST "https://verbatim.krlabs.eu/api/query" \
  -H "Authorization: Bearer $VERBATIM_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "question": "What is the attention mechanism in transformers?",
    "hybrid_weights": {"full_text": 0.5, "dense": 0.5}
  }'
```

Optional filter parameter for scoping results:
```json
{
  "question": "What are recent advances in NER?",
  "filter": "metadata[\"year\"] >= 2022",
  "hybrid_weights": {"full_text": 0.5, "dense": 0.5}
}
```

Filter examples:
- `metadata["year"] == 2023` — papers from 2023
- `metadata["year"] >= 2020 and metadata["year"] <= 2024` — year range
- `metadata["booktitle"] == "Proceedings of ACL"` — specific proceedings

---

### Search Papers

Search papers by keywords with optional year filter.

```bash
curl -s "https://verbatim.krlabs.eu/api/papers/search?query=attention+mechanisms&limit=10" \
  -H "Authorization: Bearer $VERBATIM_API_KEY"
```

With year filter:
```bash
curl -s "https://verbatim.krlabs.eu/api/papers/search?query=attention&year=2023&limit=10" \
  -H "Authorization: Bearer $VERBATIM_API_KEY"
```

---

### Get Paper Metadata

```bash
curl -s "https://verbatim.krlabs.eu/api/papers/{paper_id}" \
  -H "Authorization: Bearer $VERBATIM_API_KEY"
```

---

### Get Paper Content (Full Text)

```bash
curl -s "https://verbatim.krlabs.eu/api/papers/{paper_id}/content" \
  -H "Authorization: Bearer $VERBATIM_API_KEY"
```

---

### Get BibTeX Citation

```bash
curl -s "https://verbatim.krlabs.eu/api/papers/{paper_id}/bibtex" \
  -H "Authorization: Bearer $VERBATIM_API_KEY"
```

---

### Browse Authors

Search authors by name (fuzzy, typo-tolerant).

```bash
curl -s "https://verbatim.krlabs.eu/api/facets?field=author&q=vaswani&limit=20" \
  -H "Authorization: Bearer $VERBATIM_API_KEY"
```

---

### Browse Venues

```bash
curl -s "https://verbatim.krlabs.eu/api/facets?field=venue&q=acl&limit=50" \
  -H "Authorization: Bearer $VERBATIM_API_KEY"
```

---

### Browse Booktitles

```bash
curl -s "https://verbatim.krlabs.eu/api/facets?field=booktitle&q=emnlp&limit=50" \
  -H "Authorization: Bearer $VERBATIM_API_KEY"
```

---

### List Publication Years

```bash
curl -s "https://verbatim.krlabs.eu/api/facets?field=year&limit=100" \
  -H "Authorization: Bearer $VERBATIM_API_KEY"
```

## Usage Notes

- RAG queries (`/api/query`) count towards your monthly quota (50 free, 1000 pro)
- Search and browse endpoints don't count towards the quota
- The RAG query may take a few seconds — it performs retrieval + LLM generation
- Responses include verbatim citations from source papers with highlights
- Use `jq` to parse JSON responses, e.g. `| jq '.answer'`
