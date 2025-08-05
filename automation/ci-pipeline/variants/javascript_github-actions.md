## JavaScript + GitHub Actions Specifics

### File Structure
- Create `.github/workflows/` directory for workflow files
- Use separate `build.yml` and `test.yml` workflow files

### Environment Setup
- Configure Node.js with `actions/setup-node@v4` action
- Use npm cache for faster dependency installation: `cache: 'npm'`
- Consider multiple Node versions (18, 20) for compatibility testing

### Change Detection
- Use `dorny/paths-filter@v2` action for efficient change detection
- Include JavaScript/TypeScript extensions: `**/*.js`, `**/*.ts`, `**/*.jsx`, `**/*.tsx`
- Include package files: `package.json`, `packages/*/package.json`
- For tests, also include: `**/*.test.*`, `**/*.spec.*`

### JavaScript Commands
- Install: `npm ci` (faster than npm install in CI)
- Build commands: `npm run build`, `npm run typecheck`
- Test commands: `npm test`, `npm run test:coverage`
- Format: `npm run format:check`, `npm run lint`

### Monorepo Integration
- For Nx projects: Replace npm commands with `nx affected:build`, `nx affected:test`
- For Turborepo: Use `turbo run build --filter=[HEAD^1]`, `turbo run test --filter=[HEAD^1]`