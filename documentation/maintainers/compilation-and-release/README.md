# Compilation and release

The producer workflow lives in the Go repository:

1. `make lsp` creates `pannonico-lsp.wasm` and `manifest.json` under the ignored
   `build/lsp-release/` directory.
2. Local consumers test those exact unpublished bytes before publication.
3. The authenticated release command rebuilds from the reviewed Go revision and
   creates one immutable `v<version>` release with exactly two assets.
4. The VS Code repository updates its pin from the reviewed producer manifest
   and verifies the manifest contract in tests.

This release-hosting repository has no `Makefile`, `package.json`, build script,
or executable test suite. Run compilation and publication commands from the Go
producer:

```text
cd ../pannonico-go
make lsp VERSION=0.0.0-dev SOURCE_REVISION=development
make test-lsp-release
```

For an authenticated release, use `make publish-lsp VERSION=<version>` from a
clean reviewed Go revision. For the local consumer handoff, continue in the VS
Code repository with `make update-lsp-pin` and `make test-runtime`.

Use the canonical
[LSP distribution procedure](https://github.com/vx-rs/pannonico-go/blob/master/documentation/maintainers/lsp/distribution.md)
for commands, recovery rules, and consumer handoffs.

This repository does not contain build scripts, and language-server binaries
are not committed to Git.
