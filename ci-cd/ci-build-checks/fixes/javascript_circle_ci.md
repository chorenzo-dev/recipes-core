# Setting up CircleCI Build Checks for JavaScript

## Installation

Create or update `.circleci/config.yml`:

```yaml
version: 2.1

orbs:
  node: circleci/node@5.1.0

workflows:
  build-and-test:
    jobs:
      - build-and-test

jobs:
  build-and-test:
    executor: node/default
    steps:
      - checkout
      
      - node/install-packages:
          pkg-manager: npm
          
      - run:
          name: Type check
          command: |
            if [ -f "tsconfig.json" ]; then
              npm run typecheck
            else
              echo "No TypeScript configuration found, skipping type check"
            fi
            
      - run:
          name: Lint
          command: npm run lint
          
      - run:
          name: Build
          command: |
            if npm run | grep -q "build"; then
              npm run build
            else
              echo "No build script found, skipping build"
            fi
            
      - run:
          name: Test
          command: |
            if npm run | grep -q "test"; then
              npm test
            else
              echo "No test script found, skipping tests"
            fi
            
      - store_test_results:
          path: ./test-results
          
      - store_artifacts:
          path: ./coverage
```

## Configuration

For monorepo projects, use parallelism and workspaces:

```yaml
workflows:
  build-and-test:
    jobs:
      - build-and-test:
          matrix:
            parameters:
              project: ["frontend", "backend", "shared"]

jobs:
  build-and-test:
    parameters:
      project:
        type: string
    executor: node/default
    working_directory: ~/project/<< parameters.project >>
    steps:
      - checkout:
          path: ~/project
      - node/install-packages:
          pkg-manager: npm
      - run:
          name: Test << parameters.project >>
          command: npm test
```

## Verification

Push changes and verify build execution:
- Check CircleCI dashboard for project
- Confirm all steps complete successfully
- Verify parallel jobs run for monorepo projects