## Goal
Ensure consistent code formatting across the codebase with an automated formatter.

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
- code-formatting.exists: Whether any code formatter is configured for the project
- code-formatting.applied: Whether formatting appears to be consistently enforced
- code-formatting.variant: The specific formatter tool detected (if any)