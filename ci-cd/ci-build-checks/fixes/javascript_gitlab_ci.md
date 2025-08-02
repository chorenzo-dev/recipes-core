# Setting up GitLab CI Build Checks for JavaScript

## Installation

Create or update `.gitlab-ci.yml` in the repository root:

```yaml
stages:
  - build
  - test

variables:
  NODE_VERSION: "18"

cache:
  paths:
    - node_modules/

before_script:
  - node --version
  - npm --version
  - npm ci

typecheck:
  stage: build
  image: node:${NODE_VERSION}
  script:
    - npm run typecheck
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
    - exists:
        - tsconfig.json

lint:
  stage: build
  image: node:${NODE_VERSION}
  script:
    - npm run lint
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH

build:
  stage: build
  image: node:${NODE_VERSION}
  script:
    - npm run build
  artifacts:
    paths:
      - dist/
      - build/
    expire_in: 1 hour
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
    - exists:
        - package.json

test:
  stage: test
  image: node:${NODE_VERSION}
  script:
    - npm test
  coverage: '/All files[^|]*\|[^|]*\s+([\d\.]+)/'
  artifacts:
    reports:
      coverage_report:
        coverage_format: cobertura
        path: coverage/cobertura-coverage.xml
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
```

## Configuration

For monorepo projects, add parallel jobs:

```yaml
.node_template: &node_template
  image: node:${NODE_VERSION}
  before_script:
    - cd ${PROJECT_DIR}
    - npm ci

test:frontend:
  <<: *node_template
  variables:
    PROJECT_DIR: "frontend"
  script:
    - npm test

test:backend:
  <<: *node_template
  variables:
    PROJECT_DIR: "backend"
  script:
    - npm test
```

## Verification

Push changes and verify pipeline execution:
- Check Pipelines section in GitLab project
- Confirm all jobs complete successfully
- Verify merge request pipelines trigger correctly