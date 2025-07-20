## Goal
Set up and configure code formatting tools for the project.

## Investigation
1. **Detect existing formatters**
   - Look for any code formatter configuration files in the repository root and common config directories
   - Check project dependency files (package.json, requirements.txt, pyproject.toml, Gemfile, etc.) for formatter-related packages
   - Search for format-related scripts or commands in build files
   - Note: Only identify tools that format code (prettier, black, rustfmt, gofmt, etc.). Linters (eslint, pylint) and type checkers (mypy, tsc) are not code formatters unless they have formatting capabilities enabled

2. **Verify formatter presence**
   - If configuration files exist, check if the corresponding formatter tool is actually installed
   - Look for any formatter-specific ignore files (.prettierignore, .blackignore, etc.)
   - Identify which languages have formatters configured

## Expected Output
- setup-code-formatting.installed: Whether formatter tools are installed and available
- setup-code-formatting.configured: Whether formatter configuration files are properly set up
- setup-code-formatting.variant: The specific formatter tool configured (if any)