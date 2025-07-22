## Goal
Set up automated pre-commit hooks to run type checking, code formatting, and code linting before each commit.

## Investigation
1. **Detect available quality check scripts**
   Search for type checking, code formatting, and code linting commands only. Do not include testing or other quality concerns. Look in common locations across different ecosystems (examples include):
   - Project configuration files: `package.json` scripts, `Makefile` targets, `pyproject.toml` scripts, `Cargo.toml` configurations
   - Type checking examples: `typecheck`, `type-check`, `tsc`, `check-types`, `mypy`
   - Code formatting examples: `format`, `format:fix`, `prettier`, `fmt`, `black`, `ruff format`, `go fmt`, `cargo fmt`
   - Code linting examples: `lint`, `lint:fix`, `eslint`, `eslint:fix`, `ruff check`, `flake8`, `pylint`, `golint`, `cargo clippy`
   
   If no type checking, formatting, or linting commands are found, do not proceed with setting up pre-commit hooks.

2. **Check for existing pre-commit setup**
   Look for existing pre-commit hook files or configurations in various formats (examples include):
   - Hook configuration files: `.husky/` directory, `lint-staged` in package.json, `.pre-commit-config.yaml`, `.pre-commit-hooks.yaml`
   - Git hooks: Check `.git/hooks/` directory for existing pre-commit scripts
   - Identify if any quality checks are already automated

## Expected Output
- pre-commit-checks.checks_found: Whether any type checking, formatting, or linting commands were found in the project
- pre-commit-checks.hooks_configured: Whether pre-commit hooks are already set up