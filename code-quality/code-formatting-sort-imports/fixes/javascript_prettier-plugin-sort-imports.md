# Setting up Import Sorting with Prettier Plugin

## Installation

Install the Prettier import sorting plugin:

```bash
npm install --save-dev @trivago/prettier-plugin-sort-imports
```

## Configuration

Add import sorting configuration to your Prettier config file with the following import order:

1. External library imports (npm packages, including @scoped packages)
2. Internal/aliased imports (~ or @/ prefixed paths for locally configured module aliases)
3. Relative imports (. and .. prefixed paths)

Each group should be separated by blank lines.

**.prettierrc**
```json
{
  "plugins": ["@trivago/prettier-plugin-sort-imports"],
  "importOrder": [
    "^(?![~@./]).*$|^@(?!/)",
    "^[~@]/",
    "^[./]"
  ],
  "importOrderSeparation": true,
  "importOrderSortSpecifiers": true
}
```

Note: Common internal alias patterns include `~` and `@/` prefixes, both pointing to src/ or other project root directories.

## Verification

Run the configured format command from package.json scripts:

```bash
npm run format
```

If no format script exists, run Prettier directly and verify that imports are automatically grouped and sorted according to the defined order.