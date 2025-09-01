## JavaScript + CircleCI Specifics

### CircleCI Configuration
Use `.circleci/config.yml` with Node.js orb `circleci/node@5.1.0`. Configure Docker image `cimg/node:${version}` based on `.nvmrc` or package.json engines.

### Workflow Filters
```yaml
filters:
  branches:
    only: [main]
```

### Change Detection
Utilize `CIRCLE_COMPARE_URL` environment variable for commit range detection. Share results between jobs using workspace persistence.

### Job Optimization
- Skip unchanged jobs: `circleci step halt`
- Share artifacts: `persist_to_workspace` and `attach_workspace`
- Chain jobs: Use `requires` in workflow definition

### CircleCI-Specific Commands
- Dependency installation: `node/install-packages` (orb) or `npm ci`
- Test results: `store_test_results` with path `./test-results`
- Coverage artifacts: `store_artifacts` with path `./coverage`

### Monorepo with CircleCI
- Nx: `nx affected:build --base=$CIRCLE_COMPARE_URL`
- Turborepo: `turbo run build --filter=...[${CIRCLE_COMPARE_URL}]`
- Lerna: Parse `CIRCLE_COMPARE_URL` and use `--since` flag