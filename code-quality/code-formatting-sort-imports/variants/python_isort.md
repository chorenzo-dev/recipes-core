# Setting up Import Sorting with isort

## Installation

Install isort as a development dependency: `pip install isort`

## Configuration

Configure isort in `pyproject.toml` with the following settings:

1. Set profile to match your formatter: `profile = "black"`
2. Configure multi-line output: `multi_line_output = 3`
3. Set line length to match your formatter: `line_length = 88`
4. Define your package name: `known_first_party = ["your_package_name"]`
5. Enable standard sections: `sections = ["FUTURE", "STDLIB", "THIRDPARTY", "FIRSTPARTY", "LOCALFOLDER"]`
6. Disable grid wrap: `force_grid_wrap = 0`
7. Enable combined imports: `combine_as_imports = true`

All settings should be placed under the `[tool.isort]` section in `pyproject.toml`.

## Integration with Ruff

If using Ruff as your formatter, configure Ruff to handle import sorting instead:

1. Enable import sorting in Ruff: Add `"I"` to the select list under `[tool.ruff]`
2. Configure known first-party packages: Set `known-first-party = ["your_package_name"]` under `[tool.ruff.isort]`

## Verification

Run isort on your project: `isort .`

Or use your project's format command if configured: `npm run format`

Verify that imports are automatically grouped into the defined sections with proper separation.