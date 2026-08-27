# Repository Guidelines

## Project Structure & Module Organization

This repository stores reusable Node-RED scripts for a Home Assistant setup. Keep integrations grouped by device or service. The current `lametric/` directory contains LaMetric payload helpers:

- `lametric/get-global-data.js` reads the cached payload from Node-RED global context.
- `lametric/set-lametric-payload.json` is JavaScript intended for a Node-RED function node, despite its `.json` extension.
- `README.md` provides the repository overview.

Add new scripts to the relevant integration directory. Create a new lowercase directory when introducing another service, and avoid mixing unrelated automations in one file.

## Build, Test, and Development Commands

There is currently no package manifest, build step, or automated test suite. Changes are validated by reviewing the script and running it in the target Node-RED flow.

Useful lightweight checks:

```sh
git diff --check              # Detect whitespace errors
node --check lametric/get-global-data.js
```

For function-node snippets that use Node-RED globals such as `msg` or `global`, `node --check` validates syntax only. Import the snippet into a development Node-RED instance and exercise it with representative messages before deployment.

## Coding Style & Naming Conventions

Use modern JavaScript with `const` by default and `let` only when reassignment is required. Follow the existing four-space indentation, double-quoted strings, semicolons, and trailing commas only when consistent with the surrounding file. Prefer descriptive camelCase identifiers such as `bitcoinEur`; preserve external message-field names when they are part of the flow contract. Use lowercase, hyphenated filenames that describe the action, such as `get-global-data.js`.

## Testing Guidelines

Test both expected sensor values and missing or invalid inputs. Confirm numeric rounding, units, frame order, durations, and the final `msg.payload`. Verify global-context reads and writes in Node-RED. When fixing a bug, document the input that reproduced it in the pull request.

## Commit & Pull Request Guidelines

The existing history uses Conventional Commit style with a scope, for example `feat(lametric): add Node-RED payload scripts`. Continue with concise forms such as `fix(lametric): handle missing temperature`.

Pull requests should explain the affected flow, summarize visible behavior changes, and include manual validation steps. Link related issues when available. Attach screenshots only when a dashboard or device display changes visually; never commit Home Assistant secrets, tokens, webhook URLs, or personal location data.
