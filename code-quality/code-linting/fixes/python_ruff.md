# Setting up Ruff for Python

## Installation

Check if Ruff is already installed:

```bash
ruff --version
# or check in project dependencies:
pip list | grep ruff
```

If not found, install Ruff as a development dependency using the project's package manager:

- Ensure installation occurs in the project's virtual environment if one exists
- Add Ruff as a development/dev-group dependency (pip, poetry, pipenv, uv, etc.)

## Configuration

Ruff can act as both a linter and formatter. For linting configuration, create or update `pyproject.toml`:

```toml
[tool.ruff]
# Ruff respects .gitignore by default
target-version = "py38"  # Adjust based on minimum Python version

[tool.ruff.lint]
# Enable recommended rules
extend-select = [
    "E",  # pycodestyle errors
    "W",  # pycodestyle warnings
    "F",  # Pyflakes
    "B",  # flake8-bugbear
    "C4", # flake8-comprehensions
    "I",  # isort
]
```

Only add exclusions for files not in `.gitignore`:

```toml
[tool.ruff]
extend-exclude = [
    # Examples:
    # "*/migrations/*",  # If migrations aren't gitignored
    # "*_pb2.py",       # Generated files not in gitignore
]
```

## Scripts

Add linting commands to the project:

**For projects using Makefile:**
```makefile
lint:
	ruff check .

lint-fix:
	ruff check --fix .
```

**For projects using package.json (with Python):**
```json
{
  "scripts": {
    "lint:python": "ruff check .",
    "lint:fix:python": "ruff check --fix ."
  }
}
```

## Verification

Run the linter to check for issues:

```bash
ruff check .
```

Fix automatically fixable issues:

```bash
ruff check --fix .
```