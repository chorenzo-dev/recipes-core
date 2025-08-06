# Ruff for Python

## Installation

Check installation: `ruff --version` or `pip list | grep ruff`

Install as development dependency using your project's package manager (pip, poetry, pipenv, uv, etc.).

## Configuration

Create or update `pyproject.toml` with Ruff configuration.

**Key configuration:**
- Set `target-version` based on minimum Python version (e.g., "py38")
- Ruff respects .gitignore by default
- Ruff acts as both linter and formatter

**Recommended lint rules to enable:**
- E (pycodestyle errors)
- W (pycodestyle warnings) 
- F (Pyflakes)
- B (flake8-bugbear)
- C4 (flake8-comprehensions)
- I (isort)

## Scripts

Add linting commands to your project's script runner:

**Makefile:**
- `lint: ruff check .`
- `lint-fix: ruff check --fix .`

**package.json:**
- `"lint:python": "ruff check ."`
- `"lint:fix:python": "ruff check --fix ."`

## Verification

Check for issues: `ruff check .`

Fix automatically: `ruff check --fix .`