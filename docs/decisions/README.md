# Architecture Decision Records (ADRs)

Every significant, non-obvious design decision gets one ADR here. This is mandatory per the
quality gates (see [CONTRIBUTING.md](../../CONTRIBUTING.md)): a module is not done without at
least one ADR for its key decision.

## Naming

`NNNN-short-kebab-title.md` — e.g. `0001-langgraph-over-deepagents.md`. Numbers are sequential
and never reused.

## Template

```markdown
# ADR-NNNN: <decision title>

**Status:** Proposed | Accepted | Superseded by ADR-XXXX | Deprecated
**Date:** YYYY-MM-DD
**Phase:** 0 | 1 | 2 | 3

## Context
What problem we're solving; the constraints that apply.

## Decision
What we decided. One paragraph.

## Alternatives considered
Each alternative, with one line on why it was not chosen.

## Consequences
Positive outcomes, negative outcomes, and the trade-offs accepted.

## References
Sources that informed the decision (cite by file:line where applicable).
```

## Index

- [ADR-0001](0001-langgraph-primitives-over-deepagents.md) — Build from LangGraph/LangChain primitives, not `deepagents` · **Accepted**

Written when their decisions become real (not upfront): middleware execution order (when
building M1), sub-agent isolation mechanics (when building M4).
