# The path into AI engineering: a detailed learning plan

Oct 1, 2026 · @Eduard

## How to use the plan

The plan is for approximately 33 weeks (≈8 months), at 3–4 hours each evening, 5 evenings each week. The goal is not certificates. The goal is a portfolio of 4 working AI projects and the ability to build production systems on Claude.

- **Transition rule.** The next phase starts only when the project of the previous phase works and its checklist is complete. The dates are approximate. The checklist is not.
- **Proportion.** Approximately 30% of the time goes to courses and 70% to the project. The course explains the concept. The project makes it stay.
- **Weekly rhythm.** 4 evenings for study and code, 1 evening for review: read your code again and write down what transfers from C# and what does not.
- **Claude Code.** In phase 1, you write the code, and Claude works as a mentor (output style Learning). From phase 2, you write the AI part yourself (prompts, schemas, evals, retrieval). You delegate the scaffolding (skeletons, Docker, configs).
- **Portfolio.** Each project is a separate public GitHub repository with a README, open or synthetic data, and eval results.
- **Mastery test.** After each project, you can explain each file and write the key part again without help.

## Phase 0. Preparation (1 week)

Python becomes the main language for AI work. .NET stays the production stack. The Node track goes on pause. This week removes decisions and setup from the path, so that later you study and do not configure.

**Stack decisions**

- TypeScript course (54%): finish it only if this takes ≤ 2 weeks of evenings. If not, pause it. You will need TS for MCP and frontend later.
- Freeze NestJS, Node.js Complete Guide, and the other JS courses until the end of phase 5.
- Do not buy new courses outside this plan.

**Environment (WSL2)**

- [ ] Install **uv**. It manages Python versions, virtual environments, and packages (analogue of dotnet CLI + NuGet + global.json).
- [ ] Install **ruff**. It is a linter and a formatter in one tool (analogue of analyzers + dotnet format).
- [ ] Configure **pyright** or mypy in strict mode. This is static type checking. Without it, Python is not comfortable for a C# developer.
- [ ] VS Code: install the Python, Pylance, and Ruff extensions. Enable format on save.
- [ ] Create a project template: `uv init`, `pyproject.toml`, `src/` layout, pytest, ruff, pyright. Each later project starts from it.
- [ ] Get a Claude Platform API key and set a spend limit in the console (for phase 2).
- [ ] Claude Code: enable the output style Learning for phase 1.

## Phase 1. Python for a C# developer (6 weeks)

The goal is to write idiomatic, typed Python without help, and to understand where it behaves differently from C#. From the Fred Baptiste courses, take approximately 25–30% of the *Python 3: Deep Dive* series. The rest stays as a reference.

**Phase project: `docx-lint`**. This is a CLI that checks the structure of a Word document against a set of rules and gives a JSON report. At the end of the phase, the same validator also runs as an HTTP service. The domain is familiar (like Verify), so you can focus on the language.

```text
┌──────┬─────────────────────────────────────────┬─────────────────────────────────────────────────┐
│ Week │ Theory                                  │ Project                                         │
├──────┼─────────────────────────────────────────┼─────────────────────────────────────────────────┤
│ 1    │ Deep Dive 1: variables and references,  │ CLI skeleton on Typer (analogue of              │
│      │ mutability, is / == comparison;         │ System.CommandLine), read .docx with            │
│      │ functions, arguments, *args / **kwargs, │ python-docx                                     │
│      │ keyword-only, the mutable default value │                                                 │
│      │ trap                                    │                                                 │
├──────┼─────────────────────────────────────────┼─────────────────────────────────────────────────┤
│ 2    │ Deep Dive 1: scopes (LEGB), closures,   │ The first 3–5 check rules; a decorator to       │
│      │ decorators, also with parameters; type  │ register rules                                  │
│      │ hints and pyright strict                │                                                 │
├──────┼─────────────────────────────────────────┼─────────────────────────────────────────────────┤
│ 3    │ Deep Dive 2: iterators, generators,     │ The check as a generator pipeline that gives    │
│      │ yield from, context managers (a wider   │ violations one at a time                        │
│      │ analogue of using)                      │                                                 │
├──────┼─────────────────────────────────────────┼─────────────────────────────────────────────────┤
│ 4    │ Deep Dive 4, selected parts: classes,   │ Rule configuration and JSON report with         │
│      │ properties, dataclasses, enum, Protocol │ Pydantic models                                 │
│      │ (structural analogue of interface);     │                                                 │
│      │ Pydantic v2 documentation               │                                                 │
├──────┼─────────────────────────────────────────┼─────────────────────────────────────────────────┤
│ 5    │ asyncio: event loop, async/await, why a │ Test coverage, asynchronous processing of a     │
│      │ blocking call stops everything, gather; │ folder of documents                             │
│      │ pytest: fixtures (analogue of setup     │                                                 │
│      │ through DI), parametrize (analogue of   │                                                 │
│      │ [Theory])                               │                                                 │
├──────┼─────────────────────────────────────────┼─────────────────────────────────────────────────┤
│ 6    │ FastAPI: routes, Pydantic request and   │ HTTP endpoint: upload .docx → JSON report;      │
│      │ response models, Depends (DI), async    │ Dockerfile + docker-compose                     │
│      │ endpoints                               │                                                 │
└──────┴─────────────────────────────────────────┴─────────────────────────────────────────────────┘
```

**What to skip in Baptiste:** all of *Python 3: Fundamentals*, numeric types (only look through them), most of part 3 (hash table internals), the deep sections about metaclasses.

**Completion checklist**

- [ ] `docx-lint` works as a CLI and as a FastAPI service in Docker
- [ ] pyright strict and ruff pass without errors
- [ ] Tests cover the key rules, with parametrized tests
- [ ] I can write a decorator, a generator, a context manager, and a Pydantic model with validation without hints
- [ ] I can explain how asyncio is different from `Task` in .NET

## Phase 2. LLM basics and the Claude API (7 weeks)

The goal is to get structured data from the model reliably and to measure quality with numbers, not by eye. The main change of thinking in this phase is **evals**. The result is probabilistic. Thus, instead of a unit test with one correct output, you build a set of examples and metrics, and you check each prompt change against them.

**Courses:** Claude Platform 101 (quick start), then *Building with the Claude API* (the main course, long). Also the Claude Platform documentation: the sections about prompting, tool use, and prompt caching.

**Phase project: `doc-extract`**. It extracts metadata from official letters (date, number, sender, recipient, type, short summary) into JSON, validated with Pydantic. It has an eval set and a comparison of models by quality and cost. Use only synthetic or open sample data.

```text
┌──────┬──────────────────────────────────────────────┬────────────────────────────────────────────┐
│ Week │ Theory                                       │ Project                                    │
├──────┼──────────────────────────────────────────────┼────────────────────────────────────────────┤
│ 1    │ Messages API, roles, system prompt, tokens   │ The first call through the Python SDK;     │
│      │ and the context window, parameters, model    │ generate 50 synthetic letters              │
│      │ selection (quality vs cost vs speed)         │                                            │
├──────┼──────────────────────────────────────────────┼────────────────────────────────────────────┤
│ 2    │ Prompting: clear instructions, XML tags,     │ Prompt v1 for extraction                   │
│      │ examples (few-shot), extended thinking       │                                            │
├──────┼──────────────────────────────────────────────┼────────────────────────────────────────────┤
│ 3    │ Structured outputs: JSON by schema, Pydantic │ Pydantic schema of the result, handling of │
│      │ validation, retry on a validation error      │ invalid responses                          │
├──────┼──────────────────────────────────────────────┼────────────────────────────────────────────┤
│ 4    │ Evals: a labeled set, per-field metrics,     │ Eval harness: 50 examples, accuracy for    │
│      │ code-based graders vs LLM-as-judge,          │ each field, report                         │
│      │ regression after prompt changes              │                                            │
├──────┼──────────────────────────────────────────────┼────────────────────────────────────────────┤
│ 5    │ Tool use: tool descriptions, the call loop,  │ A "department directory" tool to normalize │
│      │ error handling; streaming                    │ sender names                               │
├──────┼──────────────────────────────────────────────┼────────────────────────────────────────────┤
│ 6    │ Cost and speed: prompt caching, Batch API,   │ Compare 2 models: accuracy, cost for 1000  │
│      │ token counting, routing between models       │ documents, latency                         │
├──────┼──────────────────────────────────────────────┼────────────────────────────────────────────┤
│ 7    │ Integration: a FastAPI service, logging of   │ README with a table of eval results        │
│      │ prompts and responses                        │                                            │
└──────┴──────────────────────────────────────────────┴────────────────────────────────────────────┘
```

**Completion checklist**

- [ ] *Building with the Claude API* is complete
- [ ] `doc-extract` returns valid JSON for 100% of the examples (after retries)
- [ ] The eval harness runs with one command and shows accuracy for each field
- [ ] There is a documented comparison of models by quality and cost
- [ ] I can explain when to use tool use and when a structured output is sufficient

## Phase 3. RAG and document automation (7 weeks)

The goal is a system that finds the necessary fragments in a document corpus and answers with references to the sources, with measured search quality. This is your target domain. Here your .NET experience with PostgreSQL applies directly: you do not need a separate vector DB, pgvector is sufficient.

**Phase project: `doc-search`**. Search and answers with citations over a corpus of open Ukrainian-language regulatory documents (for example, public legislation texts). The corpus is public, and the language is the same as in your work domain.

```text
┌──────┬─────────────────────────────────────────────┬─────────────────────────────────────────────┐
│ Week │ Theory                                      │ Project                                     │
├──────┼─────────────────────────────────────────────┼─────────────────────────────────────────────┤
│ 1    │ Embeddings and cosine similarity            │ Load the corpus, compare 2 embeddings       │
│      │ (intuition, not math); selection of an      │ models on 20 queries                        │
│      │ embeddings model with Ukrainian support:    │                                             │
│      │ cloud or local                              │                                             │
├──────┼─────────────────────────────────────────────┼─────────────────────────────────────────────┤
│ 2    │ Chunking: fixed size, by structure          │ A chunker by document structure             │
│      │ (headings, clauses, articles), overlap,     │                                             │
│      │ fragment metadata                           │                                             │
├──────┼─────────────────────────────────────────────┼─────────────────────────────────────────────┤
│ 3    │ pgvector: vector column, HNSW index,        │ DB schema, corpus indexing, migrations      │
│      │ distance operators; DB access through       │                                             │
│      │ psycopg 3 (raw SQL is the closest to        │                                             │
│      │ Dapper)                                     │                                             │
├──────┼─────────────────────────────────────────────┼─────────────────────────────────────────────┤
│ 4    │ Hybrid search: full-text + vector, rank     │ Hybrid search; compare with pure vector     │
│      │ fusion (RRF); the Contextual Retrieval      │ search                                      │
│      │ approach from Anthropic                     │                                             │
├──────┼─────────────────────────────────────────────┼─────────────────────────────────────────────┤
│ 5    │ Reranking; answer generation with source    │ Answers with references to specific         │
│      │ citations                                   │ articles                                    │
├──────┼─────────────────────────────────────────────┼─────────────────────────────────────────────┤
│ 6    │ Evals for retrieval: recall@k, MRR; evals   │ A set of 40 questions with reference        │
│      │ for answers: does the answer rely on the    │ fragments, metrics                          │
│      │ retrieved sources                           │                                             │
├──────┼─────────────────────────────────────────────┼─────────────────────────────────────────────┤
│ 7    │ Summary and documentation                   │ README: architecture, metrics before and    │
│      │                                             │ after each improvement                      │
└──────┴─────────────────────────────────────────────┴─────────────────────────────────────────────┘
```

**Important detail:** PostgreSQL full-text search has no built-in configuration for Ukrainian morphology. Examine the possible solutions in advance (the `simple` configuration, dictionaries, or BM25 at the application level).

**Completion checklist**

- [ ] `doc-search` answers with references to specific fragments
- [ ] There is a measured recall@k for vector and hybrid search
- [ ] A number confirms each improvement (chunking, hybrid, reranking)
- [ ] I can explain why RAG makes mistakes and how to diagnose them

## Phase 4. Agents, MCP, and Claude Code (7 weeks)

The goal is to expose your systems to the model through MCP and to build agents that do multi-step tasks under human control. The key skill of the phase is to know where you need an agent and where a fixed workflow is sufficient. Most document automation tasks are workflows.

**Courses:** *Introduction to MCP* → *MCP: Advanced Topics* → *Introduction to Agent Skills*; Claude Code in depth (if necessary, *Claude Code in Action*); the Claude Agent SDK documentation; the Anthropic article "Building effective agents".

**Phase project: `doc-agent`**. An agent that gets a folder of documents, checks them (`docx-lint`), extracts metadata (`doc-extract`), finds related documents (`doc-search`), and prepares a draft registry entry with human confirmation. The previous projects become its tools through MCP.

```text
┌──────┬──────────────────────────────────────────────┬────────────────────────────────────────────┐
│ Week │ Theory                                       │ Project                                    │
├──────┼──────────────────────────────────────────────┼────────────────────────────────────────────┤
│ 1    │ MCP: host, client, server; tools, resources, │ MCP server for doc-search (tools to search │
│      │ prompts; stdio and streamable HTTP           │ and get a document)                        │
│      │ transports; Python SDK                       │                                            │
├──────┼──────────────────────────────────────────────┼────────────────────────────────────────────┤
│ 2    │ Tool design: names, descriptions, parameter  │ MCP servers for docx-lint and doc-extract; │
│      │ schemas, error messages that the model can   │ check in Claude Desktop                    │
│      │ understand                                   │                                            │
├──────┼──────────────────────────────────────────────┼────────────────────────────────────────────┤
│ 3    │ MCP Advanced: sampling, notifications,       │ HTTP server authentication, limits on tool │
│      │ authentication, tool security                │ permissions                                │
├──────┼──────────────────────────────────────────────┼────────────────────────────────────────────┤
│ 4    │ Claude Agent SDK: the agent loop, tools,     │ The doc-agent skeleton                     │
│      │ subagents, permissions; agent vs workflow    │                                            │
├──────┼──────────────────────────────────────────────┼────────────────────────────────────────────┤
│ 5    │ Human-in-the-loop, failure handling (retry   │ The full scenario with human confirmation, │
│      │ vs fail vs escalation), limits on steps and  │ eval on 10 scenarios                       │
│      │ cost                                         │                                            │
├──────┼──────────────────────────────────────────────┼────────────────────────────────────────────┤
│ 6    │ Claude Code in depth: the CLAUDE.md          │ A skill with your document formatting      │
│      │ hierarchy, .claude/rules, skills, subagents, │ conventions                                │
│      │ hooks; Agent Skills                          │                                            │
├──────┼──────────────────────────────────────────────┼────────────────────────────────────────────┤
│ 7    │ MCP in C#: the official C# SDK               │ A read-only MCP server over Tabula, only   │
│      │                                              │ locally and on test data                   │
└──────┴──────────────────────────────────────────────┴────────────────────────────────────────────┘
```

**Completion checklist**

- [ ] Three MCP servers in Python and one in C# work in Claude Desktop or Claude Code
- [ ] `doc-agent` passes 10 test scenarios, failures included
- [ ] There is a custom skill and a configured CLAUDE.md hierarchy in the work repository
- [ ] For a specific task, I can justify the choice: agent, workflow, or one model call

## Phase 5. Production, portfolio, and certification (5 weeks)

The goal is to bring one project to a level that you can show at a job interview, and to pass the exam. Here your .NET experience with production systems is the main advantage over a typical AI engineering candidate.

```text
┌──────┬─────────────────────────────────────────────┬─────────────────────────────────────────────┐
│ Week │ Topic                                       │ Result                                      │
├──────┼─────────────────────────────────────────────┼─────────────────────────────────────────────┤
│ 1    │ Observability: tracing of model calls,      │ Tracing in doc-agent, cost dashboard        │
│      │ logging of prompts and responses, cost and  │                                             │
│      │ latency metrics                             │                                             │
├──────┼─────────────────────────────────────────────┼─────────────────────────────────────────────┤
│ 2    │ Security: prompt injection through document │ A set of attack documents in evals; tests   │
│      │ content, limits on tool permissions,        │ confirm the protection                      │
│      │ validation of model output                  │                                             │
├──────┼─────────────────────────────────────────────┼─────────────────────────────────────────────┤
│ 3    │ Reliability: timeouts, retry with backoff,  │ Resilience to API failures, verified by     │
│      │ rate limits, fallback to a different model, │ tests                                       │
│      │ caching                                     │                                             │
├──────┼─────────────────────────────────────────────┼─────────────────────────────────────────────┤
│ 4    │ Portfolio: README, architecture diagrams,   │ 4 public repositories, ready to show        │
│      │ eval tables, a short demo video             │                                             │
├──────┼─────────────────────────────────────────────┼─────────────────────────────────────────────┤
│ 5    │ Certification: the official exam guide, a   │ The exam is passed                          │
│      │ practice test, review of weak domains       │                                             │
└──────┴─────────────────────────────────────────────┴─────────────────────────────────────────────┘
```

**Which exam:** first **Claude Certified Developer – Foundations (CCDV-F)**, because it is the closest to your role. **Architect – Foundations (CCAR-F)** comes later, after some months of real work with agents. Before you plan, make sure that an individual outside the Claude Partner Network can register. Also check that Pearson VUE is available in your situation.

**Completion checklist**

- [ ] At least one project has tracing, protection against prompt injection, and failure handling
- [ ] 4 repositories with a README and eval results
- [ ] The practice test is passed with a margin
- [ ] The exam is passed

## .NET → Python map

Most concepts have direct equivalents. Go more slowly where the "Difference" column has text.

```text
┌─────────────────────────────────┬───────────────────────────┬────────────────────────────────────┐
│ .NET                            │ Python                    │ Difference                         │
├─────────────────────────────────┼───────────────────────────┼────────────────────────────────────┤
│ dotnet CLI, NuGet, global.json  │ uv, pyproject.toml        │ One virtual environment for each   │
│                                 │                           │ project                            │
├─────────────────────────────────┼───────────────────────────┼────────────────────────────────────┤
│ Roslyn analyzers, dotnet format │ ruff                      │ —                                  │
├─────────────────────────────────┼───────────────────────────┼────────────────────────────────────┤
│ Compiler, static types          │ type hints + pyright      │ A tool checks the types, not the   │
│                                 │                           │ runtime                            │
├─────────────────────────────────┼───────────────────────────┼────────────────────────────────────┤
│ DTO + FluentValidation          │ Pydantic                  │ Validation occurs when you create  │
│                                 │                           │ the object                         │
├─────────────────────────────────┼───────────────────────────┼────────────────────────────────────┤
│ record                          │ @dataclass(frozen=True)   │ —                                  │
├─────────────────────────────────┼───────────────────────────┼────────────────────────────────────┤
│ interface                       │ Protocol                  │ Structural typing: no explicit     │
│                                 │                           │ implementation is necessary        │
├─────────────────────────────────┼───────────────────────────┼────────────────────────────────────┤
│ using / IDisposable             │ with / context manager    │ You can write your own with a      │
│                                 │                           │ generator                          │
├─────────────────────────────────┼───────────────────────────┼────────────────────────────────────┤
│ IEnumerable + yield return      │ generators, yield         │ —                                  │
├─────────────────────────────────┼───────────────────────────┼────────────────────────────────────┤
│ LINQ                            │ comprehensions, itertools │ Only generator expressions are     │
│                                 │                           │ lazy                               │
├─────────────────────────────────┼───────────────────────────┼────────────────────────────────────┤
│ attributes                      │ decorators                │ A decorator runs code and wraps    │
│                                 │                           │ the function                       │
├─────────────────────────────────┼───────────────────────────┼────────────────────────────────────┤
│ Task, async/await               │ asyncio                   │ One thread, event loop; a blocking │
│                                 │                           │ call stops everything              │
├─────────────────────────────────┼───────────────────────────┼────────────────────────────────────┤
│ ASP.NET Minimal APIs            │ FastAPI                   │ —                                  │
├─────────────────────────────────┼───────────────────────────┼────────────────────────────────────┤
│ built-in DI container           │ Depends in FastAPI        │ DI at the endpoint level, not a    │
│                                 │                           │ global container                   │
├─────────────────────────────────┼───────────────────────────┼────────────────────────────────────┤
│ Dapper                          │ psycopg 3                 │ —                                  │
├─────────────────────────────────┼───────────────────────────┼────────────────────────────────────┤
│ DbUp                            │ yoyo-migrations, Alembic  │ Alembic pulls in SQLAlchemy        │
├─────────────────────────────────┼───────────────────────────┼────────────────────────────────────┤
│ xUnit, [Theory]                 │ pytest, parametrize       │ Fixtures instead of the test class │
│                                 │                           │ constructor                        │
├─────────────────────────────────┼───────────────────────────┼────────────────────────────────────┤
│ Shouldly                        │ assert in pytest          │ pytest shows the details of the    │
│                                 │                           │ mismatch itself                    │
└─────────────────────────────────┴───────────────────────────┴────────────────────────────────────┘
```

## Risks and rules

**Data.** Do not send documents from military systems to a cloud API without permission. Build all learning projects only on open or synthetic data. Before you plan an AI layer for Tabula, find out what is permitted: cloud, local models, or nothing. The architecture depends on this.

**Dispersion.** Several work projects run in parallel, and the plan is realistic only when the AI track is the main one. If a phase takes more than 50% longer than its term, review the plan. Do not add new courses.

**What we do not study on purpose** (for now): model training, PyTorch, deep ML math, algorithms and DSA, NestJS. For the use of LLMs through an API, these are outside the critical path.

**Obsolescence.** The Claude ecosystem changes each month. Before each phase, compare the course names in Claude Academy and make sure that the documentation is current.
