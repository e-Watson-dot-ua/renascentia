# Renascentia

A learning path into AI engineering: Python → Claude API → RAG → agents and MCP → production.
The author is an experienced C#/.NET developer (ASP.NET Core, Clean Architecture, custom CQRS,
Dapper, PostgreSQL, Angular) who studies Python. The goal of the repository is skills and a portfolio,
not a fast result. The main interaction language is English.

## Current phase: 1 — Python for a C# developer

Rules for this phase:
- Do NOT write code in `projects/*/src/` and `projects/*/tests/` unless I ask for it directly.
  Instead of ready code, give a hint, a direction, or a question that leads me to the solution.
- Review my code: what is not idiomatic for Python, why, and what the idiomatic version is.
- Explain through analogies with C#/.NET, and state clearly where the analogy breaks
  (mutability, asyncio, structural typing, decorators).
- You can generate scaffolding without limits: CI, Dockerfile, docker-compose, configs, README skeletons.

## Structure

- `projects/<name>/` — uv workspace packages (src layout, own `pyproject.toml`, `tests/`)
  - `docx-lint` (phase 1), `doc-extract` (2), `doc-search` (3), `doc-agent` (4)
  - `mcp-tabula-cs` — a C# project, outside the uv workspace
- `templates/python-project/` — the template for new packages
- `docs/journal/` — weekly notes (template: `_template.md`); do not edit without a request
- `docs/adr/` — architecture decisions
- `data/synthetic/` — only synthetic or open data

## Commands

Run all commands from the repository root. The workspace has one `.venv` and one `uv.lock`.

```bash
uv sync --all-packages           # install all workspace packages + dev tools
uv run pytest                    # tests of all packages
uv run ruff check --fix          # linter
uv run ruff format               # formatting
uv run pyright                   # type checking (strict)
cp -r templates/python-project projects/<name>   # new package (then see its README)
```

## Conventions

- Python ≥ 3.14, full type hints; pyright strict with no errors is mandatory.
- Pydantic v2 for data models and validation; dataclasses for simple internal structures.
- pytest: fixtures instead of setup classes, `parametrize` for sets of cases.
- PostgreSQL access: psycopg 3 and raw SQL (no ORM, like Dapper).
- Secrets only in `.env` (in .gitignore); in code, read environment variables.
- Formatting: follow the user-level `box-tables` skill (no long dash dividers;
  tables as aligned box-drawing tables in a `text` code block).

## Hard constraints

- No real official or military documents and data: not in code, not in tests,
  not in prompts, not in examples. Only synthetic or public data.
- Do not commit `.env`, API keys, or large data corpora.
