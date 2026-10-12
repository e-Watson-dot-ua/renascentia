# package-name

One sentence that says what the package does.

## Use this template

Run all commands from the repository root (the folder with `uv.lock`), not from the package folder.
The workspace has one virtual environment (`.venv`) and one lock file for all packages.

The examples use the package `docx-lint`. Replace it with the name of your package.

1. Copy this folder to `projects/docx-lint/`. Use lowercase words with hyphens for the folder name.

   ```bash
   cp -r templates/python-project projects/docx-lint
   ```

2. In `projects/docx-lint/pyproject.toml`, set `name = "docx-lint"` and write the `description`.
3. Rename `projects/docx-lint/src/package_name/` to `projects/docx-lint/src/docx_lint/`.
   The import name uses underscores, because a Python identifier cannot contain a hyphen.
4. Install the package into the workspace:

   ```bash
   uv sync --all-packages
   ```

5. Add the dependencies of the package. The `--package` option selects the package that gets the dependency:

   ```bash
   uv add --package docx-lint <dependency> [<dependency> ...]
   ```

   For example, `docx-lint` needs `typer` and `python-docx`.

6. Run the checks:

   ```bash
   uv run ruff check
   uv run pyright
   uv run pytest
   ```

7. In `projects/docx-lint/README.md`, replace the first two lines with the package name and description.
   Then delete this section.

## Names

```text
┌──────────────────────────────┬───────────┬────────────────────────────┐
│ Where                        │ Example   │ What it names              │
├──────────────────────────────┼───────────┼────────────────────────────┤
│ Folder projects/<name>/      │ docx-lint │ The workspace member       │
│ name in pyproject.toml       │ docx-lint │ The distribution (package) │
│ Folder src/<name>/           │ docx_lint │ The import package         │
│ import statement             │ docx_lint │ The same import package    │
└──────────────────────────────┴───────────┴────────────────────────────┘
```

## Layout

- `src/package_name/` — the package code (src layout)
- `src/package_name/py.typed` — tells type checkers that the package has type hints
- `tests/` — pytest tests for this package
