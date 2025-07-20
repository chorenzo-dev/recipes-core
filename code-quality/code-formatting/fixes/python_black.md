# Setting up Black for Python

## Installation

Install Black as a development dependency using your project's package manager (pip, poetry, pipenv, uv, etc.):

- Ensure you're using the project's virtual environment if one exists
- Add Black as a development/dev-group dependency

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

Add formatting commands to your project:

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

Run the formatter to verify it's working:

```bash
black .
```

Check if all files are formatted correctly:

```bash
black --check .
```