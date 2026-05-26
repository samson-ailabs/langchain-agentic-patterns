# Contributing

This is a solo learning + build project (see [ROADMAP.md](ROADMAP.md)). The working
discipline below applies to the author and to any contributor.

## Working discipline

1. **Notebook-first.** Before writing `src/` code for a new module, draft the notebook
   explaining the concept. If you can't explain *why* a pattern exists, you don't
   understand it well enough to ship it.
2. **ADR before non-trivial decisions.** Write the Architecture Decision Record first;
   it forces you to articulate alternatives and consequences. Then choose.
3. **Read the source of any API you use heavily** (LangGraph / LangChain). AI-generated
   code often calls APIs in non-idiomatic ways.
4. **Manually run every feature you ship — once, end-to-end — before merging.**
5. **Commit small, commit often.** One logical unit per commit.
6. **No copy-paste from reference sources.** Read, internalize, then write from understanding.

## Quality gates (before a module merges to `main`)

- Linted (`ruff`), type-checked (`mypy`), formatted (`ruff format`)
- Critical paths tested; CI green
- Module section in `docs/ARCHITECTURE.md` updated
- Module notebook runs end-to-end without errors
- At least one ADR for the module's key decision
- A LangSmith trace link for a happy-path run in the PR description
- Author has personally used the feature end-to-end

## Dev setup

```bash
uv sync              # installs runtime + dev deps, and this project (editable)
uv run ruff check .
uv run mypy src
uv run pytest
```
