# Registry Submission

## How plugin gets into registry

1. Plugin code lives in its own repo or canonical source location
2. Registry PR adds or updates JSON metadata file
3. Review checks source URL, version, description, hashes, aliases, and metadata quality
4. After merge, ReqPack can learn the plugin during registry sync

## Required review checks

1. file path matches plugin name
2. `name` matches file name
3. `source` is valid
4. `schemaVersion` supported
5. hashes are present when required
6. aliases are unique and sensible

## Directory layout

- `registry/d/dnf.json`
- `registry/m/maven.json`
- `registry/j/java.json`
- `registry/s/sys.json`
