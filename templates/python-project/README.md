# package-name

One sentence that says what the package does.

## Use this template

1. Copy this folder to `projects/<name>/`. Use lowercase words with hyphens, for example `docx-lint`.
2. In `pyproject.toml`, set `name` to `<name>` and write the `description`.
3. Rename `src/package_name/` to `src/<name with underscores>/`, for example `src/docx_lint/`.
4. Replace the first two lines of this README with the package name and description. Delete this section.
5. From the repository root, install the package into the workspace:

   ```bash
   uv sync --all-packages
   ```

6. Add the dependencies of the package:

   ```bash
   uv add --package <name> <dependency>
   ```

7. Run the checks: `uv run ruff check`, `uv run pyright`, `uv run pytest`.

## Layout

- `src/package_name/` — the package code (src layout)
- `src/package_name/py.typed` — tells type checkers that the package has type hints
- `tests/` — pytest tests for this package
