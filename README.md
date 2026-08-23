# Pannonico LSP distribution

This repository distributes the edition-neutral Pannonico language server for
editor clients. Binaries are attached to immutable GitHub Releases and are not
committed to this Git tree.

## Release assets

Each [`v<version>` release](https://github.com/vx-rs/pannonico-lsp/releases)
contains exactly two assets:

- `pannonico-lsp.wasm`
- `manifest.json`

For version `0.1.0`, the immutable download URLs are:

```text
https://github.com/vx-rs/pannonico-lsp/releases/download/v0.1.0/pannonico-lsp.wasm
https://github.com/vx-rs/pannonico-lsp/releases/download/v0.1.0/manifest.json
```

A published version is never overwritten. Changed bytes require a new version.
Release deletion or replacement is an incident-recovery action, not an update
workflow.

## Manifest contract

The WASM module targets `wasip1-wasm`. Its schema-1 manifest identifies the
release version, full source revision, IDE protocol contract, target, filename,
byte size, and lowercase SHA-256 digest. The placeholders below illustrate the
structure only; use the manifest attached to the selected release:

```json
{
  "schema": "lsp-release/v1",
  "schemaVersion": 1,
  "product": "pannonico-lsp",
  "version": "<release version>",
  "sourceRevision": "<full source commit>",
  "ideContract": "1",
  "artifacts": {
    "wasip1-wasm": {
      "filename": "pannonico-lsp.wasm",
      "size": 12345678,
      "sha256": "<64 lowercase hexadecimal characters>"
    }
  }
}
```

Clients must read the manifest from the same selected release as the module.
They must require schema version `1`, product `pannonico-lsp`, the selected
release version, a supported `ideContract`, target `wasip1-wasm`, and filename
`pannonico-lsp.wasm`. Before execution, compare the downloaded file's byte size
and SHA-256 digest with the manifest and verify that it is a WASM binary.

For a manual check after downloading both assets:

```sh
wc -c pannonico-lsp.wasm
sha256sum pannonico-lsp.wasm
```

Compare both values with `artifacts.wasip1-wasm` in the downloaded
`manifest.json`. Do not use an unrelated checksum, a mutable latest-release URL,
or a manifest from another version.

## License

Pannonico Free is available under either the
[PolyForm Noncommercial License 1.0.0](LICENSES/PolyForm-Noncommercial-1.0.0.md)
or the
[PolyForm Small Business License 1.0.0](LICENSES/PolyForm-Small-Business-1.0.0.md),
at your option. Organizations whose use is not permitted by either license
require a separate commercial Pannonico license. See [LICENSE](LICENSE).

## Support and security

Use the Pannonico product repository's [support process](SUPPORT.md) for usage
and compatibility issues. Report suspected vulnerabilities through the private
process in [SECURITY.md](SECURITY.md).
