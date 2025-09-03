## Goal
Ensure consistent code linting across the codebase with an automated linter to catch code quality issues.

## Investigation
1. **Detect existing linters**
   - Look for any linter configuration files in the repository root and common config directories
   - Check project dependency files (package.json, requirements.txt, pyproject.toml, Gemfile, etc.) for linter-related packages
   - Search for lint-related scripts or commands in build files
   - Note: Only identify tools that analyze code for quality issues (eslint, pylint, ruff, flake8, etc.). Code formatters (prettier, black) and type checkers (mypy, tsc) are not linters unless they have linting capabilities enabled

2. **Verify linter presence**
   - If configuration files exist, check if the corresponding linter tool is actually installed
   - Look for linter-specific ignore files (SpotBugs filter files, .rubocop.yml exclude patterns)
   - Identify which languages have linters configured

## Expected Output

This recipe relies on the automatic `code-linting.applied` field to indicate successful configuration.

