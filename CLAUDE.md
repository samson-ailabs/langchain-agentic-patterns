# CLAUDE.md — langchain-agentic-patterns

Working agreement for AI coding assistants on this repo. Keep it loaded; follow it per task.

## What this project is

A production deep research agent built from **LangGraph v1 + LangChain v1 primitives**,
with a voice-native interface. Solo learning build, 12 weeks, 3 public ships.

- **Current phase + what's in scope now:** `ROADMAP.md`
- **Architecture, stack, module map (M1–M11):** `docs/ARCHITECTURE.md`
- **Working discipline + quality gates:** `CONTRIBUTING.md`
- **Design decisions (the canonical "why"):** `docs/decisions/` (ADRs)

## Prime directive

This is a **learning project**. Depth of understanding > speed of delivery. Optimize every
task for *"the author can explain why this exists"*, not *"the code runs"*. If a faster path
skips understanding, it is the wrong path here.

## Step 0 — Orient (do this before every task)

1. **Check the phase** in `ROADMAP.md` and respect its constraints.
   - ⚠️ **Phase 0 (current): NO production code in `src/`.** Study, notes, and ADRs only.
2. **Identify the module** (M1–M11) the task belongs to; re-read its section in
   `docs/ARCHITECTURE.md`.
3. **Decide if an ADR is needed.** If the choice is non-obvious, hard to reverse, or has a
   real trade-off → yes. Required and accepted ADRs live in `docs/decisions/`.

## Per-task workflows

Pick the recipe that matches the task.

### A · New module or feature
`notebook-first → ADR → study the API → implement → test → verify → gate-check`
1. **Notebook-first** — draft the concept section (why before how) before any `src/` code.
   If you can't explain why the pattern exists, you don't understand it well enough to ship.
2. **ADR** — write it for the key design decision (see recipe B) before coding.
3. **Study the API** — consult the **Docs-langchain MCP** (see below) for any LangGraph/
   LangChain API used heavily; read the source when needed. Don't call APIs in non-idiomatic
   AI-generated ways.
4. **Implement** — complete, no stubs/TODOs/mocks; match existing conventions; small commits.
5. **Test** — write tests for critical paths *as you go*, not after.
6. **Verify** — run the notebook end-to-end; run module tests; trigger the feature manually
   end-to-end once; capture a LangSmith trace.
7. **Gate-check** — confirm all quality gates below before calling it done.

### B · A design decision / choosing between approaches
**Do not silently pick.** Draft an ADR first — `Context · Decision · Alternatives considered ·
Consequences · References`. Present it, then let the human choose. Diverging from a
deeply-understood pattern is engineering judgment; diverging from a poorly-understood one is
an anti-pattern.

### C · Bug / unexpected behavior
Root cause, never workaround. `Reproduce → hypothesis → fix → verify`. Never skip, disable,
or comment out a test to make things pass.

### D · Writing a notebook
Fixed structure, every code cell commented with the *why*:
What you'll learn · Why this matters · Concept · Implementation · Exploration ·
Common failure modes · Production considerations · References · Exercises.

## Quality gates (a module is NOT done until ALL pass)

- [ ] Linted (`ruff`), type-checked (`mypy`), formatted (`ruff format`)
- [ ] Critical paths tested; CI green
- [ ] Module section in `docs/ARCHITECTURE.md` updated
- [ ] Module notebook runs end-to-end without errors
- [ ] ≥1 ADR for the module's key decision
- [ ] LangSmith trace link for a happy-path run in the PR
- [ ] Author has personally used the feature end-to-end

## Where work is recorded (keep these in sync)

Clean division of labor so every doc stays trustworthy — don't pile everything into ROADMAP:

- **`ROADMAP.md`** — the plan + the **current phase**. Update *only at phase boundaries*: move the
  `Current phase` line, tick completed milestones. Step 0 reads this, so that line must stay
  accurate — and when the phase advances, update the Phase note in Step 0 above too.
- **`CHANGELOG.md`** — what actually shipped, recorded per Ship.
- **`docs/decisions/`** — one ADR per non-obvious decision, with rationale.
- **`docs/ARCHITECTURE.md`** — the relevant module section, updated as each module lands.
- **git commits + session todos** — granular task progress; never log fine-grained tasks in ROADMAP.

Rule of thumb: **done → CHANGELOG · decision → ADR · task → commit.** ROADMAP stays high-level.

## Hard rules (project-specific — never violate)

- **No `deepagents` import.** Implement equivalent patterns from primitives — this is a
  deliberate pedagogical choice (ADR-0001).
- **No copy-paste from reference sources.** Read → internalize → write from your own notes.
- **Sub-agent context isolation** is non-negotiable: the parent sees only the final result
  *string*, never a sub-agent's intermediate steps.
- **Two levels deep max** for sub-agents (orchestrator → sub-agents, no deeper).
- **Attribution placement:** README and notebooks lead with what the app does, not with any
  reference project; acknowledgments go in their own section.
- **Scope discipline:** build only what's planned for the current phase. Out-of-scope items
  (multi-tenancy, SSO/RBAC, Kubernetes, 40+ connectors, knowledge graph, i18n, billing,
  admin dashboards) are off-limits until an explicit post-MVP phase.
- **Cost budget** ≤ ~$30/month in dev. Prefer free tiers and cheap models for tests/smoke runs.

## How to collaborate here

- Surface choices as ADR drafts; don't decide architecture unilaterally.
- LangGraph/LangChain v1 are recent — verify APIs against the Docs-langchain MCP (below), not memory.
- Commit small, one logical unit; resist large generated diffs. Messages follow
  **Conventional Commits** — `type(scope): summary` (e.g. `feat:`, `fix:`, `docs:`, `chore:`,
  `refactor:`, `test:`). No Claude / `Co-Authored-By` signature.
- When two approaches are genuinely balanced, ask rather than guess.
- Pin library versions deliberately (see `pyproject.toml`) — don't let tooling choose them.
- Manage dependencies with `uv add` / `uv remove` (keeps `pyproject.toml` + `uv.lock` in sync).
  **Never use `uv pip`.** To inspect installed versions, use `uv tree` or read `uv.lock`.

## LangChain / LangGraph API — consult the Docs-langchain MCP

LangGraph v1 / LangChain v1 are recent and the API shifted (e.g. `create_react_agent` →
`create_agent`; pre/post-model hooks → middleware; `langgraph.prebuilt` → `langchain.agents`).
**Do not answer LangChain/LangGraph API questions from memory.** Before writing or reviewing
code that touches these libraries, query the **Docs-langchain** MCP server (official, current docs):

- `search_docs_by_lang_chain` — semantic search for concepts, guides, and API references. Start here.
- `query_docs_filesystem_docs_by_lang_chain` — read-only shell (`rg`, `tree`, `head`, `cat`) over
  the docs `.mdx` filesystem. Read a full page by appending `.mdx` to a path from search, e.g.
  `head -200 /oss/python/releases/langchain-v1.mdx`.

Scope to the Python OSS docs (`/oss/python/...`) for this project. Fall back to `context7` only if
the MCP is unavailable.
