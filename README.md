# Verbatim ACL Skill

A [Claude Code](https://claude.ai/code) skill for querying 90,000+ academic papers from the [ACL Anthology](https://aclanthology.org/) via [Verbatim RAG](https://verbatim.krlabs.eu).

Also includes a general-purpose **Verbatim Transform** — give it any question + context documents and get a verbatim, cited answer. Not limited to ACL papers.

## Install

```bash
claude skill add --url https://github.com/adaamko/verbatim-acl-skill
```

## Setup

1. Go to [verbatim.krlabs.eu](https://verbatim.krlabs.eu) and sign up
2. Navigate to **API Keys** and create a new key
3. Set the environment variable:

```bash
export VERBATIM_API_KEY=vb_your_key_here
```

## What You Can Do

Once installed, just ask Claude naturally:

**ACL Paper Search:**
- *"Search for papers about transformer efficiency from 2023"*
- *"What does the research say about attention mechanisms?"*
- *"Find papers by Ashish Vaswani"*
- *"Get the BibTeX citation for that paper"*
- *"List the top NLP venues in the corpus"*

**Verbatim Transform (any documents):**
- *"Read these meeting notes and answer: what were the action items? Cite the sources verbatim."*
- *"Here are 3 research papers. What do they say about X? Use verbatim citations."*
- *"Summarize this document with exact quotes as citations."*

## Available Endpoints

| Action | Endpoint | Quota |
|--------|----------|-------|
| Verbatim Transform (any context) | `POST /api/transform/verbatim` | Counts |
| Ask a research question (ACL RAG) | `POST /api/query` | Counts |
| Search papers | `GET /api/papers/search` | Free |
| Get paper metadata | `GET /api/papers/{id}` | Free |
| Get full paper content | `GET /api/papers/{id}/content` | Free |
| Get BibTeX citation | `GET /api/papers/{id}/bibtex` | Free |
| Browse authors/venues/years | `GET /api/facets` | Free |

## Links

- [Verbatim RAG](https://verbatim.krlabs.eu) — The service
- [API Documentation](https://verbatim.krlabs.eu/docs) — Full API docs
- [KR Labs](https://krlabs.eu) — Built by KR Labs

## License

Apache 2.0
