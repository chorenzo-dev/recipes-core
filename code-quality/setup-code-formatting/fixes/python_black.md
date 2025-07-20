# Setting up Black for Python

## Installation

Check if Black is already installed:

```bash
black --version
# or check in project dependencies:
pip list | grep black
```

If not found, install Black as a development dependency using the project's package manager:

- Ensure installation occurs in the project's virtual environment if one exists
- Add Black as a development/dev-group dependency (pip, poetry, pipenv, uv, etc.)

## Configuration

Black is opinionated with minimal configuration by design. It automatically respects `.gitignore` for exclusions.

If the project has specific formatting needs, create or update `pyproject.toml`:

```toml
[tool.black]
target-version = ['py38']  # Adjust based on your minimum Python version
```

Only add `extend-exclude` for files that aren't in `.gitignore` but shouldn't be formatted:

```toml
[tool.black]
extend-exclude = '''
(
  # Examples:
  # - Generated files not in gitignore: *_pb2.py
  # - Vendored code not in gitignore
  # - Files that must preserve legacy formatting
)
'''
```

## Scripts

Add formatting commands to the project:

**For projects using Makefile:**
```makefile
format:
	black .

format-check:
	black --check .
```

**For projects using package.json (with Python):**
```json
{
  "scripts": {
    "format:python": "black .",
    "format:check:python": "black --check ."
  }
}
```

## Verification

Check if all files are formatted correctly (without modifying them):

```bash
black --check .
```

This command will:
- Exit with code 0 if all files are properly formatted
- Exit with code 1 and show which files need formatting if changes are required