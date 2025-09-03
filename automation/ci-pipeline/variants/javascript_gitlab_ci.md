## JavaScript + GitLab CI Specifics

### GitLab CI Configuration
Define stages in `.gitlab-ci.yml`: `changes`, `build`, `test`. Use Node.js Docker image `node:${version}` based on `.nvmrc` or package.json engines.

### Rules Syntax
Configure rules with conditions for main branch commits and merge requests targeting main branch using GitLab CI variables.

### Change Detection with GitLab
Export change detection results as dotenv artifacts using the artifacts reports dotenv configuration.

### GitLab-Specific Optimizations
- Cache configuration: `cache: key: $CI_COMMIT_REF_SLUG-$CI_PROJECT_DIR paths: [node_modules/, .npm/]`
- Parallel jobs: Use `needs: []` for independent jobs
- Conditional execution: `rules: - if: $JS_CHANGED == "true"`

### GitLab Commands
- Optimized install: `npm ci --cache .npm --prefer-offline`
- Coverage regex: `/Lines\s*:\s*(\d+\.\d+)%/`
- Artifacts: Configure `expire_in: 1 week` for build outputs

### Monorepo with GitLab CI
- Nx: `nx affected:build --base=origin/$CI_MERGE_REQUEST_TARGET_BRANCH_NAME`
- Turborepo: `turbo run build --filter=...[origin/$CI_MERGE_REQUEST_TARGET_BRANCH_NAME]`
- Use `$CI_MERGE_REQUEST_DIFF_BASE_SHA` for accurate base comparison