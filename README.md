# Dingo's Python Project Template

This repository is a **template** for creating high‑quality Python projects with a fully configured development environment.
It includes strict linting, formatting, type checking, commit‑message validation, and custom code‑quality hooks — all automated through **pre‑commit**.

Use this template to start new Python projects with consistent, modern, and maintainable standards.

---

## Features Included

### Ruff (Linter + Formatter)
Ruff is configured to enforce:

- **PEP8 errors & warnings** (`E`, `W`)
- **Pyflakes** (`F`)
- **Import sorting** (`I`)
- **Naming conventions** (`N`)
- **Type annotation rules** (`ANN`)
- **Quote consistency** (`Q`)
- **No commented‑out code** (`ERA`)
- **Refactor rules** (`PLR`)
- **No shadowing builtins** (`A`)
- **Async best practices** (`ASYNC`)
- **Pathlib enforcement (no os.path)** (`PTH`)
- **No FIXME / XXX** (`FIX`)
- **TODO rules** (`TD`)
- **Docstring rules** (`D`)

Formatting is handled by `ruff-format`, enforcing:

- double quotes
- 4‑space indentation
- consistent whitespace
- consistent import formatting

All configuration lives in `pyproject.toml`.

---

## Pre‑commit Hooks

Pre‑commit automatically runs checks on every commit, including:

- Ruff (lint + format)
- Mypy (type checking)
- Gitlint (commit message validation)
- Custom hooks:
  - require docstrings for private methods
  - enforce blank line after docstring
  - enforce section header formatting
- Standard hygiene checks:
  - trailing whitespace
  - end‑of‑file newline
  - merge conflict markers
  - YAML/JSON/TOML validation
  - executable script checks

Install hooks after cloning:

```bash
pre-commit install --install-hooks
pre-commit install --hook-type commit-msg
```

Run all hooks manually on the entire repository:

```bash
pre-commit run --all-files
```

Run a specific hook:

```bash
pre-commit run ruff
```

---

## Mypy (Static Type Checking)

Mypy enforces type correctness across the codebase.

Run manually:

```bash
mypy .
```

You can also run it with pretty output (already configured in pre‑commit):

```bash
mypy --pretty .
```

---

## Gitlint (Commit Message Rules)

Gitlint validates commit messages using the `commit-msg` hook.

Enforced rules include:

- Title must start with a capital letter
- No “WIP” in commit titles
- Minimum title length
- No trailing punctuation
- No excessive line length
- No empty commit messages

Run manually:

```bash
gitlint
```

---

## Custom Hooks

Located in `g_tools/hooks/`:

### `check_private_docstrings.py`
Ensures all private methods (`_method_name`) include docstrings.

### `enforce_blank_line_after_docstring.py`
Requires a blank line after a functions docstring.

### `enforce_section_headers.py`
Validates consistency for section headers format inside code.

These run automatically via pre‑commit.

---

## Project Structure

```
project/
│
├── src/                # Application code
│   └── ...
│
├── tests/              # Test suite
│   └── ...
│
├── g_tools/            # Custom pre-commit hooks
│   └── hooks/
│
├── pyproject.toml      # Ruff configuration
├── .pre-commit-config.yaml
├── .gitlint
├── requirements.txt
└── README.md
```

---

## Running Tests

This template assumes **pytest** for testing.

Run all tests:

```bash
pytest
```

Run tests with verbose output:

```bash
pytest -v
```

Run a specific test file:

```bash
pytest tests/test_example.py
```

Run a specific test function:

```bash
pytest tests/test_example.py::test_function_name
```

Stop on first failure:

```bash
pytest -x
```

Show print/log output:

```bash
pytest -s
```

---

## Useful Development Commands

### Run Ruff linter only
```bash
ruff check .
```

### Run Ruff formatter only
```bash
ruff format .
```

### Run all pre‑commit hooks on all files
```bash
pre-commit run --all-files
```

### Run type checking
```bash
mypy .
```

---

## Extending the Template

You can customize:

- Ruff rules in `pyproject.toml`
- Pre‑commit hooks in `.pre-commit-config.yaml`
- Commit message rules in `.gitlint`
- Add CI workflows

This template is intentionally minimal and focused on code quality and workflow automation.
