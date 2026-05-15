# Registry Submission

## How entry gets into registry

1. Plugin code or package index lives in its own repo or canonical source location
2. Registry PR adds or updates JSON metadata file
3. Review checks source URL, version, description, hashes, aliases, and metadata quality
4. After merge, ReqPack can learn the plugin during registry sync

Package entries should set:

1. `role` to `package`
2. `targetSystem` to resolver system such as `rqp`
3. `source` to repository index URL, not direct package asset URL

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
