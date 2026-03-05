# Verbatim ACL Plugin

You have access to the Verbatim RAG API for searching 90,000+ ACL Anthology papers. Use these endpoints whenever the user asks about academic NLP/CL papers, wants citations, bibtex, or research answers.

**API Key:** Use `$VERBATIM_API_KEY` environment variable. All requests need `Authorization: Bearer $VERBATIM_API_KEY`.

**Base URL:** `https://verbatim.krlabs.eu`

## Available Endpoints

| Action | Method | Endpoint | Quota |
|--------|--------|----------|-------|
| Ask research question (RAG) | POST | `/api/query` | Counts |
| Verbatim Transform (any context) | POST | `/api/transform/verbatim` | Counts |
| Search papers | GET | `/api/papers/search?query=...&limit=10&year=2023` | Free |
| Paper metadata | GET | `/api/papers/{id}` | Free |
| Paper full text | GET | `/api/papers/{id}/content` | Free |
| BibTeX citation | GET | `/api/papers/{id}/bibtex` | Free |
| Browse facets | GET | `/api/facets?field=author|venue|booktitle|year&q=...` | Free |

## Typical Workflows

- **Research question:** Use `/api/query` with `{"question": "...", "hybrid_weights": {"full_text": 0.5, "dense": 0.5}}`. Add `"filter": "metadata[\"year\"] >= 2022"` to scope by year.
- **Find papers then get bibtex:** Search with `/api/papers/search`, then call `/api/papers/{id}/bibtex` for each result.
- **Get full paper text:** `/api/papers/{id}/content`
- **Verbatim Transform (general):** POST to `/api/transform/verbatim` with `{"question": "...", "context": [{"content": "...", "title": "..."}]}`

## Notes

- RAG queries and Transform count towards quota (50 free, 1000 pro). Search/browse are free.
- Use `curl -s` and pipe through `jq` for clean output.
- Paper IDs come from search results or RAG query responses.
