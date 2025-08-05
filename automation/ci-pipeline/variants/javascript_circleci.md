## JavaScript + CircleCI Specifics

### File Structure
- Create `.circleci/config.yml` file in repository root
- Define workflows with build and test jobs

### Environment Setup
- Use Node.js Docker image: `cimg/node:20.0` or similar
- Install Node.js orb for convenience: `circleci/node@5.1.0`

### Change Detection
- Use `CIRCLE_COMPARE_URL` for commit range detection
- Parse commit range and run git diff for file changes
- Use workspace persistence to share change detection results
- Include JavaScript/TypeScript extensions and package files

### Job Configuration
- Use `circleci step halt` to skip jobs when no changes detected
- Configure workspace attachment for sharing data between jobs
- Set up proper job dependencies with `requires`

### JavaScript Commands
- Install: Use Node orb `node/install-packages` or `npm ci`
- Build: `npm run build`, `npm run typecheck`, `npm run lint`
- Test: `npm test`, `npm run test:coverage`

### Artifacts & Reports
- Store test results: `store_test_results` with path `./test-results`
- Store coverage artifacts: `store_artifacts` with path `./coverage`
- Persist build outputs to workspace for downstream jobs

### Monorepo Integration
- For Nx: Use `nx affected:build --base=$CIRCLE_COMPARE_URL`
- For Turborepo: Use `turbo run build --filter=...[${CIRCLE_COMPARE_URL}]`