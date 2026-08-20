# Pannonico LSP distribution

This repository is the distribution boundary for the Pannonico language
server. It contains documentation and repository metadata only. The language
server source, build scripts, and publication tooling live in the private
`pannonico-go` repository.

Language-server binaries are published as immutable GitHub Releases. They are
not committed to this Git repository.

## Release contract

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
  "sourceRevision": "64e406d2ac871a6ff872dd55928d0d82da238c28",
  "ideContract": "1",
  "artifacts": {
    "wasip1-wasm": {
      "filename": "pannonico-lsp.wasm",
      "size": 9843717,
      "sha256": "e21289337c7a4a7bc742d7d9e473be9cecc497964e0dcf1d46c0f7996717b25f"
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

The implementation follows the workspace architecture note at
`../notes/three-repo-binary-workflow.md`. No license or redistribution right is
granted until a license is added explicitly.
