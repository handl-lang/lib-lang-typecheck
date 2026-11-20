# lib-lang-typecheck

`handl-plugin-lib-lang-typecheck` — the `typecheck` meta function as a
composable `plugin-lib-*` leaf crate.

## Layout

```text
handl-packages/lang_typecheck/lang_typecheck.hnl   the .hnl surface
src/lib.rs, src/tests.rs                           the Rust crate
scripts/hnl-gate.sh                                the shared hnl typecheck/lint/test gate
ci.sh                                              bupha entry — delegates to hnl-gate.sh
```

Sibling-repo deps are git dependencies (`branch = "main"`); `[patch]`
tables resolve them from sibling checkouts.

## Gate

```bash
cargo test    # the Rust suite
bash ci.sh    # the bupha gate — delegates to scripts/hnl-gate.sh
```

## License

MIT.
