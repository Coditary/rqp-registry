# rqp-registry

Main plugin registry for ReqPack / `rqp`.

This repository stores versioned JSON metadata for main plugins. ReqPack reads these files, syncs filtered changes into LMDB, and only fetches plugin payloads lazily when needed.

## Layout

- `docs/` documentation for plugin authors and contributors
- `registry/` plugin metadata grouped by first letter
- `templates/` JSON templates for new entries
- `CONTRIBUTION.md` contribution workflow
- `LICENCE` repository licence

## First plugins

- `dnf`
- `maven`
- `java`
- `sys`

## Registry shape

One file per main plugin:

- `registry/d/dnf.json`
- `registry/m/maven.json`
- `registry/j/java.json`
- `registry/s/sys.json`

Aliases live inline in the same file.
