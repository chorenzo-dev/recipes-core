## JavaScript + GitHub Actions Specifics

### Node.js Environment
Use `actions/setup-node@v4` with Node version detection from `.nvmrc` or `package.json` engines field. Enable npm caching with `cache: 'npm'`.

### GitHub Actions Syntax
```yaml
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
```

### Change Detection Filter
Use `dorny/paths-filter@v2` action with paths:
- Source files: `**/*.js`, `**/*.ts`, `**/*.jsx`, `**/*.tsx`
- Package files: `package.json`, `packages/*/package.json`, `package-lock.json`
- Test files: `**/*.test.*`, `**/*.spec.*`

### JavaScript-Specific Commands
- Dependency installation: `npm ci`
- Build verification: `npm run build`
- Type checking: `npm run typecheck`
- Test with coverage: `npm run test:coverage` or `npm test`
- Formatting check: `npm run format:check`
- Linting: `npm run lint`

### Monorepo Optimizations
- Nx: Use `nx affected:build --base=origin/main` and `nx affected:test --base=origin/main`
- Turborepo: Use `turbo run build --filter=[HEAD^1]` and `turbo run test --filter=[HEAD^1]`
- Lerna: Use `lerna run build --since HEAD^1` and `lerna run test --since HEAD^1`