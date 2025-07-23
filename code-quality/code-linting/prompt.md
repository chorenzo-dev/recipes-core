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
- code-linting.exists: Whether any code linter is configured for the project
- code-linting.applied: Whether linting passes with zero errors and warnings using recommended configuration
- code-linting.variant: The specific linter tool detected (if any)

## Important: Configuration Standards
When setting up or configuring linters:
- ALWAYS use ONLY the recommended/standard rule sets (e.g., eslint:recommended, @typescript-eslint/recommended)
- NEVER add custom rules beyond the recommended configuration
- NEVER disable or weaken linting rules to make existing code pass
- NEVER add file-specific rule overrides (e.g., turning off rules for test files)
- Use the exact configuration shown in the fix templates without modifications

## Verification Requirements
**CRITICAL**: The `code-linting.applied` status MUST be determined by actually executing the linter:

1. **Complete ALL configuration changes first** - Do not run the linter after each individual change
2. **If a lint fix command was created** (e.g., `npm run lint:fix`, `ruff format`, `rubocop --auto-correct`), run it ONCE to automatically fix any fixable issues
3. **MUST execute the linter command ONLY ONCE after all changes are complete** (e.g., `npm run lint`, `ruff check .`, `pylint .`)
4. **Check the exit status**: Only continue if the command exits with status 0
5. **Check the output**: Only continue if there are zero errors and zero warnings
6. **Set status accordingly**:
   - `code-linting.applied: true` ONLY if linter passes with zero errors/warnings
   - `code-linting.applied: false` if linter produces ANY errors or warnings

**IMPORTANT**: Do NOT run the linter multiple times during setup. Complete all installation, configuration, and file changes first, then run the fix command if available, then run the linter ONCE at the end for verification.

**Do NOT assume linting is applied just because configuration files exist or tools are installed.**