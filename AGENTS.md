# lib-lang-typecheck

`handl-plugin-lib-lang-typecheck` — the `typecheck` meta function as a
composable `plugin-lib-*` leaf crate.

## Layout

| path | role |
| --- | --- |
| `handl-packages/lang_typecheck/lang_typecheck.hnl` | the .hnl surface |
| `src/lib.rs`, `src/tests.rs` | the Rust crate |
| `pkg.hnl` | package manifest |
| `scripts/hnl-gate.sh` | shared hnl typecheck/lint/test gate |
| `ci.sh` | bupha entry → hnl-gate.sh |

## Contract

- One callable: `typecheck.typecheck(lang, ast)` — accepts a tagged
  `__ast__` value or raw JSON `Ast`, builds a sub-runtime via
  `RuntimeFactory`, typechecks, returns the synthesized type (types
  are values, ADR-0032).
- Pure-eval path (ADR-0054): type expressions evaluate via the bound
  typecheck engine without running effects; the CLI `typecheck`
  command calls this.
- Leaf crate: `handl-runtime`/`handl-language`/`handl-platform`/
  `handl-plugin-module` only — no engine impl crates, no `handl-kit-*`.
- Same `Rc<dyn RuntimeFactory>` wiring caveat as the other `lang-*`
  meta crates (not `Send + Sync`; see `src/lib.rs`).
- Sibling-repo deps are git deps (`branch = "main"`); `[patch]` tables
  resolve them from sibling checkouts.

## Verification

```bash
cargo test    # the Rust suite
workflows/gate.yaml    # the bupha gate — delegates to scripts/hnl-gate.sh
```

## License

MIT.

<!-- myco:agent-awareness -->

## Agent awareness

- Session start / any work discussion: run `myco status --prompt`
  before proposing next steps — know the board first.
- User describes new work → offer to capture it (`myco todo add`,
  `issue new`, `proposal new`). Don't wait to be asked.
- Picking up a task: `myco resume <ID>` is the briefing.
- Wrapping up: `myco handoff <ID>` anything resumable; keep statuses
  honest (claimed → in-progress → blocked/done).

<!-- /myco:agent-awareness -->
