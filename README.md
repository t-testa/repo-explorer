# Repo Explorer

A Python assistant that combines live GitHub metadata and weather tools with retrieval over a public repository's README.

## Implemented features

- A direct Anthropic tool-calling loop in `agent.py`.
- GitHub and weather requests with error handling in `api_tools.py`.
- README fetching, overlapping chunks, OpenAI embeddings and session-cached Chroma retrieval in `readme_rag.py`.
- Tests for API tools, agent behavior and README retrieval.

**Status:** the single-agent implementation is the documented entry point. `multi_agent.py` is an unfinished router experiment and currently contains a syntax error; it is not a runnable multi-agent system.

## Setup and run

From the repository root, in a Python virtual environment:

```powershell
python -m pip install -r requirements.txt
Copy-Item .env.example .env
```

Set `ANTHROPIC_API_KEY` for agent calls and `OPENAI_API_KEY` for README embeddings in your local `.env`.

```powershell
python agent.py
```

For a standalone live README retrieval example:

```powershell
python readme_rag.py
```

Live agent and embedding calls incur API usage. The GitHub tool and README fetcher access public repositories without GitHub authentication.

## Tests

```powershell
python -m pytest -v
```

The test files use mocks to exercise external API behavior. See [the test workflow](.github/workflows/tests.yml) for CI configuration.

## Files

| File | Purpose |
|---|---|
| `api_tools.py` | GitHub and weather tools |
| `agent.py` | Single-agent loop |
| `readme_rag.py` | README retrieval and in-memory index |
| `multi_agent.py` | Incomplete routing experiment |
| `test_api_tools.py`, `test_agent.py`, `test_readme_rag.py` | Automated tests |

## Limitations

README retrieval sees documentation only, not the repository's full source code. Indexes are cached in memory for the current process and do not automatically reflect upstream edits. Unauthenticated GitHub requests can be rate-limited. Weather lookup supports a fixed list of cities. This repository does not include a completed multi-agent workflow.
