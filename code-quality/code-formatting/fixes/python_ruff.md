# Setting up Ruff for Python

## Installation

Install Ruff as a development dependency using the project's package manager (pip, poetry, pipenv, uv, etc.):

- Ensure installation occurs in the project's virtual environment if one exists
- Add Ruff as a development/dev-group dependency

## Configuration

Ruff can act as both a linter and formatter. For formatting configuration, create or update `pyproject.toml`:

```toml
[tool.ruff]
# Ruff respects .gitignore by default
target-version = "py38"  # Adjust based on minimum Python version

[tool.ruff.format]
# Ruff formatter uses Black-compatible defaults
# Only add configuration if different behavior is required
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

Add formatting commands to the project:

**For projects using Makefile:**
```makefile
format:
	ruff format .

format-check:
	ruff format --check .
```

**For projects using package.json (with Python):**
```json
{
  "scripts": {
    "format:python": "ruff format .",
    "format:check:python": "ruff format --check ."
  }
}
```

## Verification

Run the formatter:

```bash
ruff format .
```

Check formatting without making changes:

```bash
ruff format --check .
```