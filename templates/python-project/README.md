# package-name

One sentence that says what the package does.

## Use this template

Run all commands from the repository root: the folder with `uv.lock`, for example `c:\Projects\Renascentia`.
Do not run them from the package folder. The workspace has one virtual environment (`.venv`) and one lock file for all packages.

The examples use the package `docx-lint`. Replace it with the name of your package.

1. Copy this folder to `projects/docx-lint/`. Use lowercase words with hyphens for the folder name.

   Run in: the repository root.

   ```bash
   cp -r templates/python-project projects/docx-lint
   ```

2. In `projects/docx-lint/pyproject.toml`, set `name = "docx-lint"` and write the `description`.
   Delete the two template comment lines at the top of the file.
3. Rename `projects/docx-lint/src/package_name/` to `projects/docx-lint/src/docx_lint/`.
   The import name uses underscores, because a Python identifier cannot contain a hyphen.
4. Install the package into the workspace.

   Run in: the repository root.

   ```bash
   uv sync --all-packages
   ```

   Result: uv adds `docx-lint` to `uv.lock` and installs it into `.venv/`. Both are in the repository root.

5. Add the dependencies of the package.

   Run in: the repository root. You do not need to go to the package folder.
   The `--package docx-lint` option selects the `pyproject.toml` that gets the dependencies.

   ```bash
   uv add --package docx-lint <dependency> [<dependency> ...]
   ```

   For example, `docx-lint` needs `typer` and `python-docx`:
   `uv add --package docx-lint typer python-docx`.

   Result: uv writes the dependencies into `projects/docx-lint/pyproject.toml`.
   It also updates `uv.lock` and installs the dependencies into `.venv/` in the repository root.

6. Run the checks.

   Run in: the repository root.

   ```bash
   uv run ruff check
   uv run pyright
   uv run pytest
   ```

   Result: the tools check all packages in `projects/`.

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
