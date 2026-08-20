# LSP ownership

The workspace separates three responsibilities:

1. [`pannonico-go`](https://github.com/vx-rs/pannonico-go/blob/master/documentation/maintainers/lsp/README.md)
   owns language-server source, protocol behavior, builds, and publication.
2. This repository owns release hosting and documents the immutable two-asset
   contract.
3. [`pannonico-vscode`](https://github.com/vx-rs/pannonico-vscode/blob/master/documentation/maintainers/lsp/README.md)
   pins, downloads, verifies, caches, and starts one release through WASI Core.

The payload is edition-neutral. Free and Pro product capabilities do not change
the editor protocol artifact.
