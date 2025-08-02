# Setting up GitLab CI Build Checks for Python

## Installation

Create or update `.gitlab-ci.yml` in the repository root:

```yaml
stages:
  - build
  - test

variables:
  PIP_CACHE_DIR: "$CI_PROJECT_DIR/.cache/pip"

cache:
  paths:
    - .cache/pip/
    - venv/

.python_template: &python_template
  image: python:3.11
  before_script:
    - python --version
    - pip install --upgrade pip
    - python -m venv venv
    - source venv/bin/activate
    - |
      if [ -f requirements.txt ]; then
        pip install -r requirements.txt
      elif [ -f pyproject.toml ]; then
        pip install -e .
      fi

typecheck:
  <<: *python_template
  stage: build
  script:
    - source venv/bin/activate
    - |
      if command -v mypy &> /dev/null; then
        mypy .
      else
        echo "mypy not available, skipping type check"
      fi
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
    - exists:
        - pyproject.toml
        - mypy.ini

lint:
  <<: *python_template
  stage: build
  script:
    - source venv/bin/activate
    - |
      if command -v flake8 &> /dev/null; then
        flake8 .
      elif command -v pylint &> /dev/null; then
        pylint **/*.py
      elif command -v ruff &> /dev/null; then
        ruff check .
      fi
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH

format-check:
  <<: *python_template
  stage: build
  script:
    - source venv/bin/activate
    - |
      if command -v black &> /dev/null; then
        black --check .
      fi
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH

build:
  <<: *python_template
  stage: build
  script:
    - source venv/bin/activate
    - pip install build
    - python -m build
  artifacts:
    paths:
      - dist/
    expire_in: 1 hour
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
    - exists:
        - setup.py
        - pyproject.toml

test:
  <<: *python_template
  stage: test
  script:
    - source venv/bin/activate
    - |
      if command -v pytest &> /dev/null; then
        pytest --cov=. --cov-report=xml
      else
        python -m unittest discover
      fi
  coverage: '/TOTAL.*\s+(\d+%)$/'
  artifacts:
    reports:
      coverage_report:
        coverage_format: cobertura
        path: coverage.xml
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
```

## Configuration

For projects requiring specific services:

```yaml
services:
  - postgres:13
  - redis:6

variables:
  POSTGRES_DB: test_db
  POSTGRES_USER: test_user
  POSTGRES_PASSWORD: test_pass
  DATABASE_URL: postgresql://test_user:test_pass@postgres:5432/test_db
```

## Verification

Push changes and verify pipeline execution:
- Check Pipelines section in GitLab project
- Confirm all jobs complete successfully
- Verify coverage reports are generated