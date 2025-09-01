# Setting up Import Sorting with Prettier Plugin

## Installation

Install the Prettier import sorting plugin: `npm install --save-dev @trivago/prettier-plugin-sort-imports`

## Configuration

Add import sorting configuration to your `.prettierrc` file with the following structure:

1. Add the plugin to the plugins array: `"plugins": ["@trivago/prettier-plugin-sort-imports"]`

2. Define import order with three groups:
   - External library imports: `"^(?![~@./]).*$|^@(?!/)"`
   - Internal/aliased imports: `"^[~@]/"`
   - Relative imports: `"^[./]"`

3. Enable import order separation: `"importOrderSeparation": true`

4. Enable specifier sorting: `"importOrderSortSpecifiers": true`

The complete configuration should be added to your existing `.prettierrc` file with these exact values.

## Verification

Run your configured format command: `npm run format`

If no format script exists, run Prettier directly to verify that imports are automatically grouped and sorted according to the defined order.