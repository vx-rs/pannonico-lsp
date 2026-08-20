# Pannonico LSP distribution

This repository is the distribution boundary for the Pannonico language
server. It contains documentation and repository metadata only. The language
server source, build scripts, and publication tooling live in the private
`pannonico-go` repository.

Language-server binaries are published as immutable GitHub Releases. They are
not committed to this Git repository.

## Release contract

The values below illustrate the schema. A client must use the manifest attached
to its selected release, not these example hashes or byte counts.

Each `v<version>` release contains exactly these assets:

- `pannonico-lsp.wasm`
- `manifest.json`

The WASM module targets `wasip1-wasm`. The schema-1 manifest identifies the
product version, full source revision, IDE contract, target, filename, byte
size, and lowercase SHA-256 digest:

```json
{
  "schemaVersion": 1,
  "product": "pannonico-lsp",
  "version": "0.0.0",
  "sourceRevision": "f9d00ddb4af745f594295d34cd97cec157508db1",
  "ideContract": "1",
  "artifacts": {
    "wasip1-wasm": {
      "filename": "pannonico-lsp.wasm",
      "size": 9843717,
      "sha256": "6443dd3ce1063c934d20cc08bb3679effe3339171888920b35ee8131e0ced829"
    }
  }
}
```

A published version is never overwritten. Changed bytes require a new version.
Release deletion or replacement is an incident-recovery action, not an update
workflow.

The future public download URL has this form:

```text
https://github.com/vx-rs/pannonico-lsp/releases/download/v<version>/pannonico-lsp.wasm
```

The repository is currently private. Pannonico editor extensions deliberately
contain no GitHub credentials, so ordinary end-user downloads begin only after
repository visibility and binary licensing permit public HTTPS access.

The implementation follows the producer, release-hosting, and consumer
ownership split described in the maintainer documentation. No license or
redistribution right is granted until a license is added explicitly.

The authenticated publication command, automated VS Code pin update, local
unpublished test loop, packaging steps, and recovery rules are documented in
the [Pannonico LSP distribution workflow](https://github.com/vx-rs/pannonico-go/blob/master/documentation/maintainers/lsp/distribution.md).

Use the [documentation table of contents](documentation/README.md) to separate
release-consumer guidance from maintainer ownership.
