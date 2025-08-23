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
- code-linting.variant: The specific linter tool detected (if any)

## Important: Configuration Standards
When setting up or configuring linters:
- ALWAYS use ONLY the recommended/standard rule sets (e.g., eslint:recommended, @typescript-eslint/recommended)
- NEVER add custom rules beyond the recommended configuration
- NEVER disable or weaken linting rules to make existing code pass
- NEVER add file-specific rule overrides (e.g., turning off rules for test files)
- Use the exact configuration shown in the fix templates without modifications

