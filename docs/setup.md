# Environment setup

## 1. Install uv

**Windows:**

```powershell
winget install --id=astral-sh.uv -e
```

**Linux / macOS:**

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

## 2. Get the code and install the packages

```bash
git clone https://github.com/e-Watson-dot-ua/renascentia.git
cd renascentia
uv sync --all-packages
```

uv reads `.python-version` and installs Python 3.14 if it is not on the machine.

Run all `uv` commands in this guide from the repository root (`renascentia/`), not from a package folder.
The workspace has one virtual environment (`.venv`) and one lock file (`uv.lock`) for all packages.

## 3. Run the checks

From the repository root:

```bash
uv run ruff check
uv run ruff format --check
uv run pyright
uv run pytest
```

The CI workflow (`.github/workflows/ci.yml`) runs the same checks on each push and pull request.

## 4. Add a new package

1. Copy `templates/python-project/` to `projects/<name>/`.
2. Follow the steps in `projects/<name>/README.md`.

## Troubleshooting

### `git push` fails with "No configured push destination"

The local repository has no remote. Add the remote, then push and set the upstream branch:

```bash
git remote add origin https://github.com/e-Watson-dot-ua/renascentia.git
git push --set-upstream origin main
```

After this, a plain `git push` is sufficient.

### The remote URL is wrong

Check the current URL with `git remote -v`. Then set the correct URL:

```bash
git remote set-url origin https://github.com/e-Watson-dot-ua/renascentia.git
```
