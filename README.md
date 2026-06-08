# css-class-mapper-lsp

A native Rust LSP server that powers the [CSS Class Mapper](https://github.com/joshuaerney/css-class-mapper) Zed extension.

It scans `.css` files in your workspace and provides:

- **Autocomplete** — class names appear as suggestions when typing inside `class="..."` attributes in HTML
- **Hover documentation** — hovering a class name shows its CSS property declarations

---

## How it works

The LSP server is a plain Rust binary that speaks the [Language Server Protocol](https://microsoft.github.io/language-server-protocol/) over stdio. It is downloaded automatically by the Zed extension at install time — you do not need to install it manually.

On startup it walks every `.css` file in the workspace root, parses class selectors, and builds an in-memory map. File changes are picked up incrementally via `workspace/didChangeWatchedFiles`.

---

## Building from source

Requires Rust installed via [rustup](https://rustup.rs).

```bash
git clone https://github.com/joshuaerney/css-class-mapper-lsp
cd css-class-mapper-lsp
cargo build --release
# binary is at target/release/css-class-mapper-lsp
```

### Cross-compilation targets

```bash
# macOS Apple Silicon
cargo build --release --target aarch64-apple-darwin

# macOS Intel
cargo build --release --target x86_64-apple-darwin

# Linux x86_64
cargo build --release --target x86_64-unknown-linux-gnu
```

---

## Release asset naming

GitHub release assets must be named exactly as follows for the Zed extension to find them:

| Platform | Asset filename |
|---|---|
| macOS Apple Silicon | `css-class-mapper-lsp-{version}-aarch64-apple-darwin.tar.gz` |
| macOS Intel | `css-class-mapper-lsp-{version}-x86_64-apple-darwin.tar.gz` |
| Linux x86_64 | `css-class-mapper-lsp-{version}-x86_64-unknown-linux-gnu.tar.gz` |

Each `.tar.gz` must contain a single executable named `css-class-mapper-lsp`.

---

## License

MIT — see [LICENSE](LICENSE).
