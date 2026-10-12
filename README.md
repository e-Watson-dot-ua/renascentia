# Renascentia

A learning path into AI engineering, from Python to production systems on Claude.
The author is a C#/.NET developer. The goal is skills and a portfolio of four working AI projects.

## Roadmap

```text
┌───────┬───────────────────────────────┬──────────────────────────────────────────────────────────┐
│ Phase │ Topic                         │ Project                                                  │
├───────┼───────────────────────────────┼──────────────────────────────────────────────────────────┤
│ 1     │ Python for a C# developer     │ docx-lint: a CLI and HTTP service that checks the        │
│       │                               │ structure of Word documents                              │
├───────┼───────────────────────────────┼──────────────────────────────────────────────────────────┤
│ 2     │ LLM basics and the Claude API │ doc-extract: metadata extraction to validated JSON, with │
│       │                               │ evals                                                    │
├───────┼───────────────────────────────┼──────────────────────────────────────────────────────────┤
│ 3     │ RAG and document automation   │ doc-search: hybrid search with citations on PostgreSQL + │
│       │                               │ pgvector                                                 │
├───────┼───────────────────────────────┼──────────────────────────────────────────────────────────┤
│ 4     │ Agents, MCP, and Claude Code  │ doc-agent: an agent that uses the earlier projects as    │
│       │                               │ MCP tools                                                │
├───────┼───────────────────────────────┼──────────────────────────────────────────────────────────┤
│ 5     │ Production and portfolio      │ Observability, security, and reliability for one project │
└───────┴───────────────────────────────┴──────────────────────────────────────────────────────────┘
```

The full plan is in [docs/learning-plan.md](docs/learning-plan.md).

## Structure

- `projects/` — Python packages of the uv workspace, one for each project
- `docs/` — the learning plan, setup notes, journal, and architecture decisions
- `data/synthetic/` — synthetic or public sample data only

## Quick start

1. Install [uv](https://docs.astral.sh/uv/). See [docs/setup.md](docs/setup.md).
2. Install the packages and the development tools:

   ```bash
   uv sync --all-packages
   ```

3. Run the checks:

   ```bash
   uv run pytest
   uv run ruff check
   uv run pyright
   ```

## Data

This repository contains only synthetic or public data. It does not contain real official documents.
