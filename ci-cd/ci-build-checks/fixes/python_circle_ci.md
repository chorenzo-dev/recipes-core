# Setting up CircleCI Build Checks for Python

## Installation

Create or update `.circleci/config.yml`:

```yaml
version: 2.1

orbs:
  python: circleci/python@2.1.1

workflows:
  build-and-test:
    jobs:
      - build-and-test

jobs:
  build-and-test:
    executor: python/default
    steps:
      - checkout
      
      - python/install-packages:
          pkg-manager: pip
          
      - run:
          name: Install dependencies
          command: |
            if [ -f requirements.txt ]; then
              pip install -r requirements.txt
            elif [ -f pyproject.toml ]; then
              pip install -e .
            fi
            
      - run:
          name: Type check
          command: |
            if command -v mypy &> /dev/null; then
              mypy .
            else
              echo "mypy not available, skipping type check"
            fi
            
      - run:
          name: Lint
          command: |
            if command -v flake8 &> /dev/null; then
              flake8 .
            elif command -v pylint &> /dev/null; then
              pylint **/*.py
            elif command -v ruff &> /dev/null; then
              ruff check .
            else
              echo "No linter found, skipping lint check"
            fi
            
      - run:
          name: Format check
          command: |
            if command -v black &> /dev/null; then
              black --check .
            else
              echo "Black not available, skipping format check"
            fi
            
      - run:
          name: Build
          command: |
            if [ -f setup.py ] || [ -f pyproject.toml ]; then
              pip install build
              python -m build
            else
              echo "No build configuration found, skipping build"
            fi
            
      - run:
          name: Test
          command: |
            if command -v pytest &> /dev/null; then
              pytest --cov=. --cov-report=xml --junitxml=test-results/junit.xml
            else
              python -m unittest discover
            fi
            
      - store_test_results:
          path: test-results
          
      - store_artifacts:
          path: coverage.xml
          
      - store_artifacts:
          path: dist/
```

## Configuration

For multi-version testing, add matrix builds:

```yaml
workflows:
  build-and-test:
    jobs:
      - build-and-test:
          matrix:
            parameters:
              python-version: ["3.8", "3.9", "3.10", "3.11"]

jobs:
  build-and-test:
    parameters:
      python-version:
        type: string
    docker:
      - image: cimg/python:<< parameters.python-version >>
```

## Verification

Push changes and verify build execution:
- Check CircleCI dashboard for project
- Confirm all Python versions pass
- Verify test results and coverage reports are stored