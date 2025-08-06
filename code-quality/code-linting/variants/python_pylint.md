# Pylint for Python

## Installation

Check installation: `pylint --version` or `pip list | grep pylint`

Install as development dependency using your project's package manager (pip, poetry, pipenv, uv, etc.).

## Configuration

Create `.pylintrc` file in project root or add configuration to `pyproject.toml`.

**Configuration sections:**
- Use `[MAIN]` section for general settings
- Use `[MESSAGES CONTROL]` section for enabling/disabling specific checks
- Pylint respects .gitignore by default

**Common useful checks to enable:** C0116, C0115, C0114, W0613

**Common overly strict checks to disable:** C0103 (Invalid name), R0903 (Too few public methods), R0913 (Too many arguments)

## Scripts

Add linting commands to your project's script runner:

**Makefile:**
- `lint: pylint src/`
- `lint-verbose: pylint --verbose src/`

**package.json:**
- `"lint:python": "pylint src/"`
- `"lint:verbose:python": "pylint --verbose src/"`

## Verification

Check for issues: `pylint src/`

Verbose analysis: `pylint --verbose src/`