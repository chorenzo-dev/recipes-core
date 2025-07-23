# Setting up Husky and lint-staged for JavaScript/TypeScript

## Prerequisites Check

Before setting up pre-commit hooks, verify that type checking, code formatting, or code linting scripts exist in `package.json`. Do not proceed if no relevant scripts are found.

Required scripts (at least one must exist):
- Type checking: `typecheck`, `type-check`, `tsc`, `check-types`
- Formatting: `format`, `format:fix`, `prettier`, `fmt`
- Linting: `lint`, `lint:fix`, `eslint`, `eslint:fix`

## Installation

Check if Husky and lint-staged are already installed:

```bash
npm list husky lint-staged
```

If not found, install as development dependencies:

```bash
npm install --save-dev husky lint-staged
```

## Husky Setup

Initialize Husky:

```bash
npx husky init
```

This creates `.husky/` directory and adds a prepare script to `package.json`.

## lint-staged Configuration

Create a separate `.lintstagedrc.json` file for cleaner configuration management:

```bash
touch .lintstagedrc.json
```

Add lint-staged configuration based on available scripts. Only include commands that exist in the project's scripts.

Example configuration structure:
```json
{
  "*.{js,jsx,ts,tsx}": [
    // Add commands based on available scripts in this order:
    // 1. Type checking first (catches compilation errors early)
    // 2. Linting second (no point linting code that doesn't compile)
    // 3. Formatting last (cosmetic changes)
  ],
  "*.{json,md,yml,yaml}": [
    // Add formatting commands if available
  ]
}
```

Configure based on which scripts are available, in this recommended order:
1. **Type checking first**: Add `"npm run typecheck"` if `typecheck`, `type-check`, `tsc`, or `check-types` script exists
2. **Linting second**: Add `"npm run lint:fix"` if available, otherwise `"npm run lint"` or `"npm run eslint"`
3. **Formatting last**: Add `"npm run format"` if available, otherwise `"npm run prettier"` if available
- Only include file patterns that have corresponding available commands

## Pre-commit Hook

Create the pre-commit hook file:

```bash
echo 'npx lint-staged' > .husky/pre-commit
chmod +x .husky/pre-commit
```

## Verification

The setup is now complete. The pre-commit hooks will run automatically on your next commit.

The hooks will run automatically and either pass or prevent the commit if issues are found.

## Troubleshooting

If hooks don't run:
- Ensure the `.husky/pre-commit` file is executable
- Verify that all referenced npm scripts exist in `package.json`
- Check that Husky is properly initialized with `npx husky init`