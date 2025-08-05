# Black (Python)

## Installation Check
Run: `black --version` or `pip list | grep black`

## Installation Command
Install as a development/dev-group dependency using pip, poetry, pipenv, uv, etc.

## Configuration File
Create or update `pyproject.toml` with `[tool.black]` section and target Python version

## Ignore Rules (Optional)
Add extend-exclude patterns to `pyproject.toml` only if needed for generated files, vendored code, or legacy directories

## Script Commands
Add format and format-check targets to your Makefile or build scripts

For mixed projects, add format:python and format:check:python scripts to `package.json`

## Verification Commands
Run: `black .` and `black --check .`