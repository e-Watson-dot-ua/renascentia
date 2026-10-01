# Renascentia

Навчальний шлях в AI engineering: Python → Claude API → RAG → агенти й MCP → production.
Автор — досвідчений C#/.NET-розробник (ASP.NET Core, Clean Architecture, власний CQRS,
Dapper, PostgreSQL, Angular), який вивчає Python. Мета репозиторію — навички й портфоліо,
а не швидкий результат. Спілкування українською.

## Поточна фаза: 1 — Python для C#-розробника

Правила для цієї фази:
- НЕ пиши код у `projects/*/src/` і `projects/*/tests/`, якщо я прямо не попросив.
  Замість готового коду — підказка, напрям або питання, яке наведе мене на рішення.
- Роби рев'ю мого коду: що неідіоматично для Python, чому, як було б ідіоматично.
- Пояснюй через аналогії з C#/.NET і окремо наголошуй, де аналогія ламається
  (mutability, asyncio, структурна типізація, декоратори).
- Обв'язку можна генерувати без обмежень: CI, Dockerfile, docker-compose, конфіги, README-скелети.

<!-- При переході на фазу 2+ замінити блок вище на:
## Поточна фаза: N — <назва>
- AI-частину (промпти, схеми structured outputs, evals, chunking, retrieval, дизайн
  MCP-інструментів) пишу сам; ти робиш рев'ю і пропонуєш альтернативи.
- Скелети FastAPI, Docker, міграції, шаблонні тести — можеш генерувати.
-->

## Структура

- `projects/<name>/` — пакети uv workspace (src-layout, власний `pyproject.toml`, `tests/`)
  - `docx-lint` (фаза 1), `doc-extract` (2), `doc-search` (3), `doc-agent` (4)
  - `mcp-tabula-cs` — C#-проєкт, поза uv workspace
- `templates/python-project/` — шаблон для нових пакетів
- `docs/journal/` — тижневі нотатки (шаблон: `_template.md`); не редагуй без прохання
- `docs/adr/` — архітектурні рішення
- `data/synthetic/` — лише синтетичні або відкриті дані

## Команди

```bash
uv sync --all-packages           # встановити всі пакети workspace + dev-інструменти
uv run pytest                    # тести всіх пакетів
uv run ruff check --fix          # лінтер
uv run ruff format               # форматування
uv run pyright                   # перевірка типів (strict)
uv init --lib projects/<name>    # новий пакет у workspace
```

## Конвенції

- Python ≥ 3.13, повні type hints; pyright strict без помилок — обов'язково.
- Pydantic v2 для моделей даних і валідації; dataclasses — для простих внутрішніх структур.
- pytest: fixtures замість setup-класів, `parametrize` для наборів випадків.
- Доступ до PostgreSQL — psycopg 3 і сирий SQL (без ORM, як Dapper).
- Секрети лише в `.env` (у .gitignore); у коді — читання змінних середовища.

## Жорсткі обмеження

- Жодних реальних службових чи військових документів і даних — ні в коді, ні в тестах,
  ні в промптах, ні в прикладах. Лише синтетичні або публічні.
- Не коміть `.env`, API-ключі, великі корпуси даних.
