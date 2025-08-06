# ESLint for JavaScript/TypeScript

## Installation

Check installation: `npm list eslint`

Install ESLint: `npm install --save-dev eslint`

For TypeScript projects: `npm install --save-dev @typescript-eslint/parser @typescript-eslint/eslint-plugin`

Install flat config dependencies: `npm install --save-dev @eslint/js globals`

## Configuration

Create `eslint.config.mjs` file in project root using the flat config format (required for ESLint 9+).

**TypeScript-specific requirements:**
- Extend `@typescript-eslint/recommended` configuration for TypeScript projects
- Apply TypeScript rules to `**/*.ts` and `**/*.tsx` files
- Apply JavaScript rules to `**/*.js` and `**/*.cjs` files

**Common ignore patterns:** Include `dist/**`, `build/**`, and `**/*.generated.*` in the ignores array.

**Language options:** Set `ecmaVersion: 'latest'` and appropriate `sourceType` (module/commonjs).

Note: ESLint 9+ flat config deprecates .eslintignore files in favor of ignores array in configuration.

## Scripts

Add to package.json scripts:
- `"lint": "eslint ."`
- `"lint:fix": "eslint --fix ."`

## Verification

Check for issues: `npm run lint`

Fix automatically: `npm run lint:fix`