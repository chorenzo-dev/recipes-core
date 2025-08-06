# Ruff (Python)

## Installation Check
Run: `ruff --version` or `pip list | grep ruff`

## Installation Command
Install as a development/dev-group dependency using pip, poetry, pipenv, uv, etc.

## Configuration File
Create or update `pyproject.toml` with `[tool.ruff]` and `[tool.ruff.format]` sections with target Python version and Black-compatible defaults

## Ignore Rules (Optional)
Add extend-exclude patterns to `pyproject.toml` only if needed for migrations, generated files, or specific directories

## Script Commands
Add format and format-check targets to your Makefile or build scripts using `ruff format .` and `ruff format --check .`

For mixed projects, add format:python and format:check:python scripts to `package.json`

## Verification Commands
Run: `ruff format .` and `ruff format --check .`