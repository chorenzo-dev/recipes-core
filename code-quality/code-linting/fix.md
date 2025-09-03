# Setting up Code Linting

## Installation

Check if the linter is already installed using the tool's version command or by checking project dependencies.

If not found, install the linter as a development dependency using the project's package manager (npm, pip, poetry, pipenv, uv, etc.). Ensure installation occurs in the project's virtual environment if one exists.

## Configuration

Create a configuration file in the project root using the appropriate format for your linter.

**Configuration standards:**
- **ALWAYS use ONLY the recommended/standard rule sets** (e.g., eslint:recommended, @typescript-eslint/recommended)
- **NEVER add custom rules** beyond the recommended configuration
- **NEVER disable or weaken linting rules** to make existing code pass
- **NEVER add file-specific rule overrides** (e.g., turning off rules for test files)
- **Use the exact configuration** shown in the fix templates without modifications
- **Respect existing ignore patterns**: Linters should respect .gitignore by default
- **File targeting**: Apply rules to appropriate file extensions and directories

## Scripts

Add linting commands to your project's script runner (package.json, Makefile, etc.):
- A basic `lint` command to check for issues
- A `lint:fix` command to automatically fix fixable issues

## Verification

Run the linter to check for issues using your project's lint command.

Fix automatically fixable issues using your project's lint:fix command.

## Integration

Ensure the linter integrates properly with your existing development workflow and build process.