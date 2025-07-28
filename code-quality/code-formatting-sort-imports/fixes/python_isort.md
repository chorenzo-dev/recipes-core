# Setting up Import Sorting with isort

## Installation

Install isort as a development dependency:

```bash
pip install isort
```

## Configuration

Configure isort with the following import order:

1. Future imports
2. Standard library imports  
3. Third-party library imports
4. First-party/local application imports
5. Relative imports from current package

Each group should be separated by blank lines and sorted alphabetically within the group.

**pyproject.toml**
```toml
[tool.isort]
profile = "black"
multi_line_output = 3
line_length = 88
known_first_party = ["your_package_name"]
sections = ["FUTURE", "STDLIB", "THIRDPARTY", "FIRSTPARTY", "LOCALFOLDER"]
force_grid_wrap = 0
combine_as_imports = true
```

## Integration with Existing Formatters

### With Black
If using Black, isort is already configured to be compatible via the `profile = "black"` setting above.

### With Ruff  
If using Ruff as your formatter, configure Ruff to handle import sorting instead:

**pyproject.toml**
```toml
[tool.ruff]
select = ["I"]  # Enable import sorting

[tool.ruff.isort]
known-first-party = ["your_package_name"]
```

## Verification

Run the configured format command from your project:

```bash
# If using a format script in package.json or similar
npm run format

# Or run isort directly
isort .
```

Verify that imports are automatically grouped and sorted according to the defined sections.