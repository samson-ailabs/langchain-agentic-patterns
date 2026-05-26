# langchain-agentic-patterns

> **Faber** — a production AI agent built from LangGraph v1 and LangChain v1 primitives. Deep research, voice, RAG, and MCP tools, composed on a custom middleware harness.

<!-- Hero gif / screenshot goes here once Ship 1 is live -->

> **Status:** 🚧 Phase 0 (Study). No production code yet. See [ROADMAP.md](ROADMAP.md).

## What it does

- **Text or voice research queries** — ask a question by chat or by speaking
- **Plan generation with clarification** — the agent scopes the question, asking for clarification when needed (human-in-the-loop)
- **Parallel multi-agent research** — an orchestrator dispatches isolated sub-agents for web search and document retrieval
- **Synthesis with citations** — a writer agent composes a grounded report with inline source citations
- **Persistent memory** — user preferences and prior topics carry across sessions
- **Extensible via MCP** — any Model Context Protocol server becomes a connector

## Quick start

> 🚧 **Not runnable yet — Phase 0 (study).** There is no application code or container setup
> in the repo. The one-command start below is the *target* for **Ship 1** (Week 5), when
> `docker-compose.yml`, the API, and the UI land.

```bash
# Planned for Ship 1 — does not work yet:
cp .env.example .env   # fill in your API keys
docker compose up
```

## Architecture

A three-layer stack — LangGraph v1 (runtime), LangChain v1 (framework), and a custom agent harness assembled from primitives. The harness composes a middleware stack (planning, memory, filesystem, sub-agents, summarization, HITL, tool-call patching, guardrails) over a set of specialized agents.

See [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) for the full overview and module map.

## Tutorial notebooks

Eleven notebooks are **planned** — one per module, each explaining *why* a pattern exists
before *how* to build it. None are published yet (Phase 0); see [ROADMAP.md](ROADMAP.md) for the schedule.

| # | Notebook | Module(s) |
|---|----------|-----------|
| 01 | `01_agent_core.ipynb` | Agent Core |
| 02 | `02_rag_pipeline.ipynb` | RAG Pipeline |
| 03 | `03_web_search.ipynb` | Web Search |
| 04 | `04_multi_agent_research.ipynb` | Multi-Agent Deep Research |
| 05 | `05_mcp_integration.ipynb` | MCP Integration |
| 06 | `06_hitl_and_memory.ipynb` | HITL + Memory |
| 07 | `07_code_execution.ipynb` | Code Interpreter |
| 08 | `08_full_research_system.ipynb` | End-to-end integration |
| 09 | `09_api_and_streaming.ipynb` | API + Streaming |
| 10 | `10_evaluation_and_deployment.ipynb` | Evaluation + Deployment |
| 11 | `11_voice_interface.ipynb` | Voice Interface |

## Benchmarks

| Benchmark | Score | Model | Date |
|-----------|-------|-------|------|
| Deep Research Bench | _pending (Ship 2)_ | — | — |
| Internal eval (30q) | _pending (Ship 2)_ | — | — |

## Deployment

Planned for Ship 1 / Ship 3: a Docker Compose setup and a hosted demo, to be documented in
`docs/DEPLOYMENT.md` (not written yet — Phase 0).

## Tech stack (planned)

Target stack for the full build. Phase 0 has only **LangGraph + LangChain** installed; the rest lands per [ROADMAP.md](ROADMAP.md).

| Layer | Component |
|-------|-----------|
| Runtime | LangGraph v1 (1.x) |
| Framework | LangChain v1 (1.x) |
| Language | Python 3.12 |
| Package manager | uv |
| Vector DB | ChromaDB (dev) → pgvector (prod) |
| Web search | Tavily |
| API | FastAPI |
| Frontend | Web app (framework TBD — decided later via ADR) |
| Voice | Deepgram (STT) + ElevenLabs (TTS) |
| Tracing | LangSmith |

## Acknowledgments

This project draws on two canonical references in agent engineering:

- **Architectural reference — [LangChain Deep Agents](https://github.com/langchain-ai/deepagents)**: middleware stack,
  BackendProtocol abstraction, sub-agent isolation, auto-summarization patterns.

- **Product reference — [Onyx](https://www.onyx.app/)**: deep research workflow design, citation UX, feature scope.
  Studied via blog posts and product docs; no code copied.

Implementation in this repository is the author's own, built directly on LangGraph and
LangChain v1 primitives. Patterns are derived from internalized study, not from copied code.

## License

Apache 2.0 — see [LICENSE](LICENSE).
