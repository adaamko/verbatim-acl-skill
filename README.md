# Verbatim ACL Skill

A [Claude Code](https://claude.ai/code) skill for querying 90,000+ academic papers from the [ACL Anthology](https://aclanthology.org/) via [Verbatim RAG](https://verbatim.krlabs.eu).

Ask research questions and get verbatim, cited answers. Search papers, browse authors and venues, export BibTeX citations.

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

- *"Search for papers about transformer efficiency from 2023"*
- *"What does the research say about attention mechanisms?"*
- *"Find papers by Ashish Vaswani"*
- *"Get the BibTeX citation for that paper"*
- *"List the top NLP venues in the corpus"*
- *"What are recent advances in named entity recognition?"*

Claude will use the Verbatim API to search, query, and retrieve papers on your behalf.

## Available Endpoints

| Action | Endpoint | Quota |
|--------|----------|-------|
| Ask a research question (RAG) | `POST /api/query` | Counts |
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

MIT
