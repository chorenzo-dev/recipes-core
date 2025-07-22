# Setting up Pylint for Python

## Installation

Check if Pylint is already installed:

```bash
pylint --version
# or check in project dependencies:
pip list | grep pylint
```

If not found, install Pylint as a development dependency using the project's package manager:

- Ensure installation occurs in the project's virtual environment if one exists
- Add Pylint as a development/dev-group dependency (pip, poetry, pipenv, uv, etc.)

## Configuration

Create a `.pylintrc` file in the project root or add configuration to `pyproject.toml`:

**Using .pylintrc:**
```ini
[MAIN]
# Pylint respects .gitignore by default

[MESSAGES CONTROL]
# Enable useful checks
enable=C0116,C0115,C0114,W0613

# Disable overly strict checks
disable=
    C0103,  # Invalid name
    R0903,  # Too few public methods
    R0913,  # Too many arguments
```

**Using pyproject.toml:**
```toml
[tool.pylint.main]
# Pylint respects .gitignore by default

[tool.pylint."messages control"]
# Enable useful checks
enable = ["C0116", "C0115", "C0114", "W0613"]

# Disable overly strict checks
disable = [
    "C0103",  # Invalid name
    "R0903",  # Too few public methods
    "R0913",  # Too many arguments
]
```

Only add exclusions for files not in `.gitignore`:

```ini
[MAIN]
ignore-paths = [
    # Examples:
    # ".*/migrations/.*",  # If migrations aren't gitignored
    # ".*_pb2\.py",       # Generated files not in gitignore
]
```

## Scripts

Add linting commands to the project:

**For projects using Makefile:**
```makefile
lint:
	pylint src/

lint-verbose:
	pylint --verbose src/
```

**For projects using package.json (with Python):**
```json
{
  "scripts": {
    "lint:python": "pylint src/",
    "lint:verbose:python": "pylint --verbose src/"
  }
}
```

## Verification

Run the linter to check for issues:

```bash
pylint src/
```

Run with verbose output to see detailed analysis:

```bash
pylint --verbose src/
```