# Verbatim ACL Plugin

A [Claude Code plugin](https://code.claude.com/docs/en/plugins) for querying 90,000+ academic papers from the [ACL Anthology](https://aclanthology.org/) via [Verbatim RAG](https://verbatim.krlabs.eu).

Also includes a general-purpose **Verbatim Transform** — give it any question + context documents and get a verbatim, cited answer.

## Install

First add the marketplace:

```bash
claude plugin marketplace add https://github.com/adaamko/verbatim-acl-skill
```

Then install:

```bash
claude plugin install verbatim-acl
```

Or test locally without installing:

```bash
claude --plugin-dir /path/to/verbatim-acl-skill
```

## Setup

1. Go to [verbatim.krlabs.eu](https://verbatim.krlabs.eu) and sign up
2. Navigate to **API Keys** and create a new key
3. Set the environment variable:

```bash
export VERBATIM_API_KEY=vb_your_key_here
```

## Commands

| Command | Description |
|---------|-------------|
| `/verbatim-acl:search` | Search ACL papers, ask research questions, browse authors/venues |
| `/verbatim-acl:transform` | Verbatim transform any question + context into cited answers |

## Example Usage

**ACL Paper Search:**
- `/verbatim-acl:search papers about transformer efficiency from 2023`
- `/verbatim-acl:search what does the research say about attention mechanisms?`

**Verbatim Transform:**
- `/verbatim-acl:transform what are the main findings?` (with context provided)

Or just ask Claude naturally — it will use the API endpoints from the skill.

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
- [Claude Code Plugins](https://code.claude.com/docs/en/plugins) — Plugin documentation

## License

Apache 2.0
