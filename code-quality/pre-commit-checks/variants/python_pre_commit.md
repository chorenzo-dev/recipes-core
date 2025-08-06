# Setting up pre-commit for Python

## Prerequisites Check

Verify that type checking, code formatting, or code linting commands exist in the project. Look for:
- Makefile targets: lint, format, typecheck
- pyproject.toml scripts or tool configurations
- Installed packages: mypy, black, ruff, flake8, pylint, isort

Do not proceed if no relevant tools are found.

## Installation

Check if pre-commit is already installed: `pre-commit --version`

Or check in project dependencies: `pip list | grep pre-commit`

If not found, install pre-commit: `pip install pre-commit`

For project-specific installation, add to your requirements or pyproject.toml as a development dependency.

## Configuration

Create .pre-commit-config.yaml in the project root. Start with basic file maintenance hooks from the pre-commit repository, then add tool-specific repositories only for tools that are installed in your project.

Common tool repositories:
- Ruff: https://github.com/astral-sh/ruff-pre-commit
- Black: https://github.com/psf/black
- isort: https://github.com/pycqa/isort
- mypy: https://github.com/pre-commit/mirrors-mypy
- flake8: https://github.com/pycqa/flake8

For each tool, check the repository for the latest version tag and available hook IDs.

## Installation

Install the git hook scripts: `pre-commit install`

## Verification

Test the setup by running pre-commit on all files: `pre-commit run --all-files`

Or stage some files and attempt a commit to see the hooks in action.

## Updating

Update hook versions periodically: `pre-commit autoupdate`

## Troubleshooting

If hooks fail, ensure all referenced tools are installed in the project environment. Check that tool configurations in pyproject.toml or setup.cfg are valid. Run individual tools manually to debug configuration issues.