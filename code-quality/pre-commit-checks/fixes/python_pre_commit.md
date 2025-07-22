# Setting up pre-commit for Python

## Prerequisites Check

Before setting up pre-commit hooks, verify that type checking, code formatting, or code linting commands exist in the project. Do not proceed if no relevant tools are found.

Look for commands in:
- `Makefile`: targets like `lint`, `format`, `typecheck`
- `pyproject.toml`: scripts or tool configurations
- Installed packages: `mypy`, `black`, `ruff`, `flake8`, `pylint`, `isort`

## Installation

Check if pre-commit is already installed:

```bash
pre-commit --version
# or check in project dependencies:
pip list | grep pre-commit
```

If not found, install pre-commit:

```bash
pip install pre-commit
```

For project-specific installation, add to your requirements or pyproject.toml as a development dependency.

## Configuration

Create `.pre-commit-config.yaml` in the project root. Pre-commit works by referencing external Git repositories that contain hook definitions.

Start with a basic configuration including general file maintenance:
```yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.4.0  # Use the latest tag from the repository
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
      - id: check-added-large-files
```

Add tool-specific repositories only for tools that are installed/configured in the project. Each tool has its own repository with hook definitions:

- **Ruff**: `https://github.com/astral-sh/ruff-pre-commit`
- **Black**: `https://github.com/psf/black` 
- **isort**: `https://github.com/pycqa/isort`
- **mypy**: `https://github.com/pre-commit/mirrors-mypy`
- **flake8**: `https://github.com/pycqa/flake8`

For each tool, find the latest version tag in its repository and configure accordingly. Example for Ruff:
```yaml
  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.1.0  # Check repository for latest tag
    hooks:
      - id: ruff
        args: [--fix]
      - id: ruff-format
```

Configuration guidelines:
- Only include repositories for tools that are actually installed/configured in the project
- Use the latest stable version tags available at time of setup
- Add project-specific arguments if needed
- Check each repository's README for available hook IDs and configuration options

## Installation

Install the git hook scripts:

```bash
pre-commit install
```

## Verification

Test the setup by running pre-commit on all files:

```bash
pre-commit run --all-files
```

Or stage some files and attempt a commit:

```bash
git add .
git commit -m "test pre-commit hooks"
```

## Updating

Update hook versions periodically:

```bash
pre-commit autoupdate
```

## Troubleshooting

If hooks fail:
- Ensure all referenced tools are installed in the project environment
- Check that tool configurations (pyproject.toml, setup.cfg, etc.) are valid
- Run individual tools manually to debug configuration issues