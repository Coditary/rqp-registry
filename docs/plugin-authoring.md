# Plugin Authoring

ReqPack plugins are Lua-based thin wrappers around package-manager behavior.

## Minimal plugin

Required functions usually include:

- `getName()`
- `getVersion()`
- `getRequirements()`
- `getCategories()`
- `getMissingPackages()`
- `install()`
- `installLocal()`
- `remove()`
- `update()`
- `list()`
- `outdated()`
- `search()`
- `info()`
- `shutdown()`

Optional:

- `getSecurityMetadata()`
- `resolveProxyRequest()`

## Security metadata

Use `getSecurityMetadata()` to declare fields like:

- `role`
- `capabilities`
- `ecosystemScopes`
- `writeScopes`
- `networkScopes`
- `privilegeLevel`
- `osvEcosystem`
- `purlType`
- `versionComparatorProfile`

## Registry entry

Each plugin should also have one registry JSON file in `registry/<letter>/`.
