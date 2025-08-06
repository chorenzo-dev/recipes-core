# Prettier (JavaScript/TypeScript)

## Installation Check
Run: `npm list prettier`

## Installation Command
Run: `npm install --save-dev prettier`

## Configuration File
Create `.prettierrc` with basic configuration for single quotes and preferred settings

## Ignore File (Optional)
Create `.prettierignore` only if needed for files not already in `.gitignore` (lock files, generated files, legacy directories)

## Script Commands
Add format and format:check scripts to `package.json` for running `prettier --write .` and `prettier --check .`

## Verification Commands
Run: `npm run format` and `npm run format:check`