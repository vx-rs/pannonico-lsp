# Pannonico language server

This repository distributes the edition-neutral Pannonico WASI language server
for editor and tool integrations. It contains integration documentation only;
language-server source and binary files are not committed to this Git tree.

> **Pre-1.0 development notice:** Pannonico is under active development. Until version 1.0.0, public contracts and user-visible behavior may change between releases. Expect breaking changes while the program and distribution model are being stabilized.

## Acquire and verify a release

Each immutable [`v<version>` release](https://github.com/vx-rs/pannonico-lsp/releases)
contains exactly:

- `pannonico-lsp.wasm`
- `manifest.json`

Download both files anonymously from the same versioned release. Require the
manifest's `lsp-release/v1` identity, selected version, full source revision,
supported IDE contract, `wasip1-wasm` target, and
`pannonico-lsp.wasm` filename. Verify the file size, lowercase SHA-256 digest,
and WASM header before execution. Never combine a manifest and module from
different releases or replace a published version in place.

## Host contract

The module targets WASI Preview 1 and communicates through Language Server
Protocol JSON-RPC over stdio. A host preopens the selected trusted project
directory, reserves stdout for protocol messages, sends normal initialize,
initialized, shutdown, and exit lifecycle messages, and terminates the process
if orderly shutdown cannot complete.

The server provides completion, hover, definitions, and definite saved-file
diagnostics for Pannonico configuration, templates, layouts, partials, data,
and navigation. A client should replace diagnostics per document and clear
them when the server publishes an empty set.

## Cache and updates

Cache modules by immutable release identity. Revalidate file type, size,
SHA-256, and WASM bytes before every use. Install downloads atomically, keep
different versions separate, and update only after explicitly selecting and
verifying a newer release. Do not use a mutable latest-release URL as the
runtime identity.

## Compatibility and limits

All 0.x releases may introduce breaking protocol or diagnostic changes. Pin a
version and IDE contract, retain its matching documentation, and follow
migration notes. Strict cross-version compatibility begins with 1.0.0.

The module does not provide an authenticated network service, remote project
filesystem, arbitrary Go-template interpretation, or automatic release
discovery. The integrating host owns workspace trust, process isolation,
downloads, cache permissions, and update policy.

## Support, security, and licensing

Use [pannonico-lsp Issues](https://github.com/vx-rs/pannonico-lsp/issues) for
language-server acquisition, protocol, diagnostic, lifecycle, and third-party
integration reports. Read [SUPPORT.md](SUPPORT.md) first. Suspected
vulnerabilities use the shared private process in [SECURITY.md](SECURITY.md),
not a public issue.

Pannonico Free is available under either included PolyForm license, at your
option. See [LICENSE](LICENSE).
