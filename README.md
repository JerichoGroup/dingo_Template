# Dingo's Python Project Template

This repository is a **template** for creating high‑quality Python projects with a fully configured development environment.
It includes strict linting, formatting, type checking, and commit‑message validation — all automated through **pre‑commit**.

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

## Requirements

- **Python 3.10+**
- **pre-commit >= 3.2** — install via `pip install pre-commit`, not your OS package manager.
  Distro-packaged versions (e.g. `apt install pre-commit`) commonly lag years behind and may not
  understand this config's stage names, causing an `InvalidConfigError` on commit. Check your
  version with `pre-commit --version` before reporting a hook issue.

---

## Installation

Dependencies are declared in `pyproject.toml` — there is no `requirements.txt`.

Install the project in editable mode along with the development tools
(pytest, mypy, ruff, pre-commit, gitlint):

```bash
pip install -e ".[dev]"
```

Add runtime dependencies your project needs under `[project.dependencies]` in
`pyproject.toml`. Add/adjust dev-only tooling under
`[project.optional-dependencies.dev]`.

---

## Pre‑commit Hooks

Pre‑commit automatically runs checks on every commit, including:

- Ruff (lint + format)
- Mypy (type checking)
- Gitlint (commit message validation)
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

Mypy enforces type correctness across the codebase. All settings (strictness,
excludes, target Python version) live in `[tool.mypy]` in `pyproject.toml`,
so running `mypy .` locally behaves identically to the pre-commit hook —
there are no extra flags hidden in `.pre-commit-config.yaml`.

The baseline is strict-ish: untyped/incomplete function definitions,
unused ignores, and implicit `Optional` are all flagged. Tighten further
(e.g. `strict = true`) once the codebase is fully typed.

If a third-party dependency ships no type stubs, add the stub package
(e.g. `types-requests`) under `additional_dependencies` for the `mypy` hook
in `.pre-commit-config.yaml`, or add a targeted per-module override in
`pyproject.toml` — avoid a blanket `--ignore-missing-imports`, which silently
disables type checking for anything unresolved.

Run manually:

```bash
mypy .
```

You can also run it with pretty output (already the default via `pretty = true`):

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

## Excluding Files and Directories

Every tool in this template has a single, obvious place to add per-project
excludes — useful for generated code, vendored dependencies, or legacy
directories you don't want linted/type-checked/hooked:

- **Pre-commit (all hooks):** top-level `exclude:` regex at the top of
  `.pre-commit-config.yaml`. Uncomment and add your own alternatives inside
  the `(?x)` block.
- **Ruff:** the `exclude` list in `[tool.ruff]` in `pyproject.toml` already
  covers common VCS/venv/cache directories; add project-specific paths at
  the bottom of that list.
- **Mypy:** the `exclude` list in `[tool.mypy]` in `pyproject.toml` (regex
  patterns).

Prefer excluding at the narrowest scope that solves your problem (a single
tool) over the top-level pre-commit exclude, which skips a path for every
hook.

---

## Project Structure

```
project/
│
├── src/
│   └── dingo_project/   # Application code (rename to your package name)
│       ├── __init__.py
│       └── example.py
│
├── tests/               # Test suite
│   ├── __init__.py
│   └── test_example.py
│
├── pyproject.toml       # Project metadata, dependencies, Ruff/mypy/pytest config
├── .pre-commit-config.yaml
├── .gitlint
├── LICENSE
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

---

## License

Licensed under the [Apache License, Version 2.0](LICENSE).

When forking this template for a new project, update the copyright holder
name in the `LICENSE` file and the `license`/`name` fields in
`pyproject.toml`.
