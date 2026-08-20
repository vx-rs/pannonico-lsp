# LSP release assets

Each published `v<version>` release contains:

- `manifest.json`
- `pannonico-lsp.wasm`

The schema-1 manifest identifies the product, version, full Go source revision,
IDE contract, `wasip1-wasm` target, filename, byte size, and lowercase SHA-256
digest. Validate the downloaded module against that manifest before starting
it.

Published versions are immutable. Changed bytes require a new version. Release
deletion or replacement is incident recovery, not an update mechanism.

The repository is currently private and grants no redistribution right because
it contains no license. The VS Code extension has no GitHub credentials, so
ordinary public HTTPS downloads require both public repository visibility and
an explicit binary license.

Use the [release repository README](../../../README.md) for the URL shape and
manifest example. Extension users should read the
[VS Code manual](https://github.com/vx-rs/pannonico-vscode/blob/master/README.md).
