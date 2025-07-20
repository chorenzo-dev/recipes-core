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

Check formatting without making changes:

```bash
ruff format --check .
```

This command will:
- Exit with code 0 if all files are properly formatted
- Exit with code 1 and show which files need formatting if changes are required