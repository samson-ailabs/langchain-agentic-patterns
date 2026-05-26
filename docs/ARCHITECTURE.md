# Architecture

> Living document. Each module's section is filled in as the module ships.

## Three-layer stack

- **LangGraph v1 (runtime)** — state machine execution, persistence, streaming,
  checkpointing, interrupts. Foundational dependency; everything sits on top.
- **LangChain v1 (framework)** — `create_agent`, `init_chat_model`, middleware
  abstraction, model/tool abstractions. Used directly where it fits, bypassed where
  custom behavior is required.
- **Custom harness (this project — the `faber` package)** — opinionated assembly of middleware,
  sub-agents, backends, and tools for production agent workflows.

This project does **not** import `deepagents`. Equivalent patterns are implemented from
primitives, deliberately, for learning depth (see ADR-0001 when written).

## High-level layers

```
Frontend (Web app + Voice)
   │  HTTP / SSE / WebSocket
API layer (FastAPI)
   │
Agent orchestration (LangGraph v1)
   ├─ Chat agent · Research orchestrator · Voice agent
   ├─ Sub-agents: Search · RAG · Writer
   └─ Middleware stack
Tool layer (Web search · Doc parser · Code sandbox · MCP · Voice I/O)
Data layer (ChromaDB · PostgreSQL · File storage · LangGraph Store)
```

## Middleware execution order

Order matters — each middleware can inject tools, modify the system prompt, or transform
messages around the LLM call.

1. `PlanningMiddleware` — `write_research_plan` tool + planning instructions
2. `MemoryMiddleware` — load user preferences / prior context into the prompt
3. `FilesystemMiddleware` — bind `ls`/`read_file`/`write_file`/`edit_file` to the backend
4. `SubAgentMiddleware` — `delegate_task` tool, sub-agent spawning with context isolation
5. `SummarizationMiddleware` — compact older messages, offload full history to backend
6. `HITLMiddleware` — wrap configured tools with `interrupt()` approval
7. `PatchToolCallsMiddleware` — repair malformed tool calls before execution
8. `GuardrailsMiddleware` — output filtering; runs last so it sees the final response

## Modules (planned)

| # | Module | Phase | Notebook |
|---|--------|-------|----------|
| M1 | Agent Core (base agent, registry, config, planning + patch middleware) | 1 | 01 |
| M2 | RAG Pipeline (loaders, chunking, hybrid retrieval, citations, backends) | 1 | 02 |
| M3 | Web Search (provider abstraction, Tavily, scraper, summarizer) | 1 | 03 |
| M4 | Multi-Agent Deep Research (scope → research → write) — signature feature | 2 | 04 |
| M5 | MCP Integration (universal connector protocol) | 3 | 05 |
| M6 | Human-in-the-Loop (approve / review / sensitive tool gating) | 2 | 06 |
| M7 | Memory (short-term + long-term, auto-summarization) | 2 | 06 |
| M8 | Code Interpreter (sandboxed Python) | 3 | 07 |
| M9 | API + Streaming (FastAPI, SSE) | 1/3 | 09 |
| M10 | Evaluation + Deployment (LLM-as-judge, Deep Research Bench, Docker) | 2/3 | 10 |
| M11 | Voice Interface (STT/TTS) — differentiator | 3 | 11 |

## Core design rules (non-negotiable)

- **Sub-agent context isolation** — the parent sees only a sub-agent's final result string,
  never its intermediate steps. Prevents context pollution at scale.
- **Two levels deep maximum** — orchestrator → sub-agents. No sub-agent spawns sub-agents.
- **Orchestrator does not transform findings** — it routes and aggregates; transformation
  happens in the writer.
- **Parallel by default** — sub-agents dispatch via `Send()`; sequential only on strict
  dependency.

## Decision records

Significant design choices are recorded as ADRs in `docs/decisions/` — ADR-0001 onward.
