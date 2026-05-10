# Package Manager Registry Entries Design

## Goal

Add missing registry entries for all package-manager plugins that already exist in this workspace.
Scope is limited to registry onboarding inside `0_registry`.

## In Scope

- create missing registry JSON files for existing package-manager plugins
- keep file layout aligned with `registry/<first-letter>/<name>.json`
- map minimal metadata from each plugin `metadata.json` into registry shape
- preserve existing registry entries without modification

## Out Of Scope

- changing plugin implementation files
- changing existing registry entries such as `dnf`
- adding extra aliases, hashes, or advanced security metadata not already defined for this task
- updating README or contribution docs only to mention new examples

## Current State

Existing plugin directories in workspace include:

- `a/apt`
- `d/dnf`
- `d/dpkg`
- `f/flatpak`
- `h/homebrew`
- `n/nix`
- `p/pacman`
- `r/rpm`

Existing registry entries currently include:

- `registry/d/dnf.json`
- `registry/j/java.json`
- `registry/m/maven.json`
- `registry/s/sys.json`

Missing registry entries for current package-manager plugins are therefore:

- `registry/a/apt.json`
- `registry/d/dpkg.json`
- `registry/f/flatpak.json`
- `registry/h/homebrew.json`
- `registry/n/nix.json`
- `registry/p/pacman.json`
- `registry/r/rpm.json`

## Design Choice

Use minimal registry-entry addition.
Each missing package-manager plugin gets one registry JSON file with only required fields plus conservative ecosystem scope values.

This approach is preferred because it:

- satisfies registry onboarding goal directly
- avoids guessing aliases or richer metadata not present in plugin metadata
- keeps changes small and easy to review

Alternative approaches considered but not chosen:

- richer metadata population now, which adds avoidable assumptions
- script-based generation, which is unnecessary for seven files

## Registry File Shape

Each new file will follow existing template shape:

```json
{
  "schemaVersion": 1,
  "name": "example",
  "version": "1.0.0",
  "source": "git+https://github.com/example/repo.git@main",
  "description": "Short plugin description",
  "role": "package-manager",
  "capabilities": [],
  "ecosystemScopes": [],
  "writeScopes": [],
  "networkScopes": [],
  "privilegeLevel": "none",
  "scriptSha256": "",
  "bootstrapSha256": "",
  "aliases": []
}
```

## Field Mapping Rules

- `schemaVersion`: always `1`
- `name`: from plugin `metadata.json`
- `version`: from plugin `metadata.json`
- `description`: from plugin `metadata.json`
- `role`: always `package-manager`
- `capabilities`: empty array
- `writeScopes`: empty array
- `networkScopes`: empty array
- `privilegeLevel`: `none`
- `scriptSha256`: empty string
- `bootstrapSha256`: empty string
- `aliases`: empty array

## Source Handling

`source` should point to canonical plugin source location.
Each plugin directory is its own Git repository with its own `origin` remote, so new registry entries will use those canonical repository URLs.

Planned source mapping:

- `apt`: `git+https://github.com/Coditary/rqp-plugin-apt.git@main`
- `dpkg`: `git+https://github.com/Coditary/rqp-plugin-dpkg.git@main`
- `flatpak`: `git+https://github.com/Coditary/rqp-plugin-flatpak.git@main`
- `homebrew`: `git+https://github.com/Coditary/rqp-plugin-homebrew.git@main`
- `nix`: `git+https://github.com/Coditary/rqp-plugin-nix.git@main`
- `pacman`: `git+https://github.com/Coditary/rqp-plugin-pacman.git@main`
- `rpm`: `git+https://github.com/Coditary/rqp-plugin-rpm.git@main`

## Ecosystem Scope Mapping

Minimal `ecosystemScopes` values:

- `apt`: `["deb"]`
- `dpkg`: `["deb"]`
- `flatpak`: `["flatpak"]`
- `homebrew`: `["homebrew"]`
- `nix`: `["nix"]`
- `pacman`: `["pacman"]`
- `rpm`: `["rpm"]`

## Planned File Additions

- `0_registry/registry/a/apt.json`
- `0_registry/registry/d/dpkg.json`
- `0_registry/registry/f/flatpak.json`
- `0_registry/registry/h/homebrew.json`
- `0_registry/registry/n/nix.json`
- `0_registry/registry/p/pacman.json`
- `0_registry/registry/r/rpm.json`

`0_registry/registry/d/dnf.json` remains unchanged.

## Validation

Implementation is correct when:

- each file path matches first letter of plugin name
- each file name matches `name`
- each JSON document matches registry template field set
- values for `name`, `version`, and `description` match source plugin metadata
- `ecosystemScopes` match mapping in this design
- no unrelated plugin or doc files are modified

## Risks And Constraints

- source URLs assume default branch remains `main` for each plugin repository
- minimal privilege and empty capability values may need later refinement if registry policy becomes stricter

These risks are acceptable for this scoped change because user requested registry inclusion only, not richer security metadata design.
