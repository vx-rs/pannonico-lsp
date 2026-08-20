# LSP release user manual

1. [Release assets and integrity](lsp/README.md)
2. [Release repository contract](../../README.md)
3. [VS Code extension manual](https://github.com/vx-rs/pannonico-vscode/blob/master/README.md)

The release repository distributes an edition-neutral WASI language server.
The editor client selects a version, downloads its manifest and module, and
verifies the declared SHA-256 digest before execution.
