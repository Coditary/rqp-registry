# Contribution Guide

## Add plugin

1. Copy `templates/plugin.template.json`
2. Fill all required fields
3. Place file into matching first-letter directory under `registry/`
4. Open pull request

Example:

- `registry/n/npm.json`

## Update plugin

1. Edit existing JSON file
2. Update version, source, hashes, description, aliases as needed
3. Open pull request

## Rules

1. One main plugin per JSON file
2. File name must match `name`
3. Aliases belong into `aliases`
4. Hashes should match real plugin payload
5. `source` should point to canonical plugin source repo or artifact source

## Docs

See `docs/` for authoring and registry workflow.
