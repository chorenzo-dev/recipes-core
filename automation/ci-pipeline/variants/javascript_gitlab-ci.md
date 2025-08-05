## JavaScript + GitLab CI Specifics

### File Structure
- Create `.gitlab-ci.yml` file in repository root
- Define stages: changes, build, test

### Environment Setup
- Use Node.js Docker image: `node:20` or `node:22`
- Set NODE_VERSION variable for consistency
- Configure cache with lock file key for efficient builds

### Change Detection Setup
- Create separate job to check for JavaScript/TypeScript changes
- Use git diff with GitLab CI variables for change detection
- Export results as dotenv artifacts for downstream jobs
- Include extensions: `.js`, `.ts`, `.jsx`, `.tsx`, `package.json`, lock files

### Job Configuration
- Use `rules` with change detection variables to skip unnecessary jobs
- Configure `needs` dependencies between jobs for parallel execution
- Set appropriate cache paths: `node_modules/`, `.npm/`

### JavaScript Commands
- Install: `npm ci --cache .npm --prefer-offline`
- Build: `npm run build`, `npm run typecheck`, `npm run lint`
- Test: `npm test`, `npm run test:coverage`
- Coverage regex: `'/Lines\s*:\s*(\d+\.\d+)%/'`

### Artifacts & Reports
- Store build outputs: `dist/`, `build/`
- Configure coverage reports with cobertura format
- Set reasonable expire times for artifacts

### Monorepo Integration  
- For Nx: Use `nx affected:build --base=origin/$CI_MERGE_REQUEST_TARGET_BRANCH_NAME`
- For Turborepo: Use `turbo run build --filter=...[origin/$CI_MERGE_REQUEST_TARGET_BRANCH_NAME]`