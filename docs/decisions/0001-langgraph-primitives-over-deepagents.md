# ADR-0001: Build from LangGraph/LangChain primitives, not the deepagents package

**Status:** Accepted
**Date:** 2026-05-26
**Phase:** 0

## Context

This is a project for learning agent engineering and teaching it publicly (tutorial
notebooks + documented patterns). LangChain's `deepagents` package already bundles the
production patterns we care about — a middleware stack, sub-agent orchestration with context
isolation, virtual-filesystem backends, auto-summarization. Adopting it would yield a working
agent fast, but it abstracts away the exact mechanics we set out to understand.

## Decision

Do not import `deepagents`. Implement the equivalent patterns directly on **LangGraph 1.x**
and **LangChain 1.x** primitives (`StateGraph`, `create_agent`, middleware, `interrupt`,
`Send`, the Store) plus our own thin harness.

## Alternatives considered

- **Use `deepagents` directly** — fastest path to a working agent, but hides the middleware
  composition, sub-agent isolation, and summarization mechanics that are the whole point here.
- **Another agent framework (CrewAI, AutoGen, …)** — moves away from the LangGraph/LangChain
  runtime we want to learn and brings its own abstractions.
- **No harness, ad-hoc graph wiring per feature** — avoids a framework but never yields the
  reusable, production-shaped patterns the project is meant to teach.

## Consequences

- **+** Deep understanding of how a production agent harness actually works; able to explain
  and teach each pattern; full control to adapt patterns to the use case.
- **+** No coupling to `deepagents`' release cadence or design choices.
- **−** Slower to a first working agent; we maintain our own harness.
- **−** Risk of re-implementing bugs `deepagents` has already solved — mitigated by studying
  its source as a reference (read, don't copy) and by testing critical paths.

## References

- LangChain Deep Agents — architectural reference, studied not copied:
  https://github.com/langchain-ai/deepagents
- LangGraph docs (state, persistence, streaming, `interrupt`, subgraphs) and the LangChain v1
  middleware docs.
