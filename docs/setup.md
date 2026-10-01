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

## 2. Minimal setup

```bash
git init
uv sync --all-packages
```

## 3. Connect to GitHub

### Problem: `git push` fails with "No configured push destination"

The error message suggests running `git remote add <name> <url>`. This means
the local repository has no remote yet.

**Fix:** add the remote, then push and set the upstream branch:

```bash
git remote add origin https://github.com/e-Watson-dot-ua/renascentia.git
git push --set-upstream origin main
```

After this, a plain `git push` is enough.

### If the remote URL is wrong

```bash
git remote set-url origin https://github.com/e-Watson-dot-ua/renascentia.git
git push
```

Check the current URL with `git remote -v`.
