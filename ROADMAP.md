# Roadmap

12 weeks, full-time. Three public ships. No silent stretch longer than 4 weeks.

> **Current phase: Phase 1 — Foundation MVP (Weeks 3–5).** Move this line at each phase boundary.

## Phase 0 — Study (Weeks 1–2) · ✅ closed

Repo skeleton + founding decision in place. Understanding is built by doing from Phase 1 on
(no separate study-notes deliverable).

- [x] Public repo created with skeleton (README, LICENSE, ROADMAP, .gitignore, pyproject)
- [x] ADR-0001 — LangGraph primitives over `deepagents`
- [x] Deep Agents + Onyx cloned locally under `refs/` (gitignored) for reference
- [x] Accounts (LangSmith, Tavily, OpenAI, Anthropic, host)
- [x] First public post

> ADR-0002 (middleware order) & ADR-0003 (sub-agent isolation) get written when building M1 / M4.

## Phase 1 — Foundation MVP (Weeks 3–5) → **Ship 1**

**Goal:** Working RAG agent with web search, accessible via API and a basic UI, deployed publicly.
**Modules:** M1 (Agent Core), M2 (RAG), M3 (Web Search), partial M9 (basic API).

- Week 3: M1 + M2 partial (ingestion, vector store). Notebooks 01, 02.
- Week 4: M2 (retrieval, citations) + M3 (web search). Notebook 03.
- Week 5: partial M9 (FastAPI chat + upload), basic Streamlit UI, deploy. **Ship 1.**

**Ship 1:** hosted demo URL; notebooks 01–03; blog "Building a Production RAG Agent from LangGraph Primitives"; ADRs through 0006.

## Phase 2 — Deep Research Signature (Weeks 6–9) → **Ship 2**

**Goal:** The signature multi-agent deep research feature, benchmarked publicly.
**Modules:** M4 (Deep Research), M6 (HITL), M7 (Memory), partial M10 (Evaluation).

- Week 6: M4 Phase A (scoping + clarification HITL) + Phase B (orchestrator + search agent). Notebook 04.
- Week 7: M4 Phase B (RAG sub-agent, parallel) + Phase C (writer). Notebook 04.
- Week 8: M6 (HITL patterns) + M7 (memory + summarization). Notebook 06.
- Week 9: M10 partial (eval + Deep Research Bench). Notebook 08. **Ship 2.**

**Ship 2:** demo with deep research; notebooks 04, 06, 08; **Deep Research Bench score in README**; benchmark blog post; ADRs through 0010.

## Phase 3 — Production Polish + Voice (Weeks 10–12) → **Ship 3**

**Goal:** Production-grade with the voice differentiator.
**Modules:** M5 (MCP), M8 (Code Interpreter), full M9, full M10, M11 (Voice).

- Week 10: M5 + M8. Notebooks 05, 07. M11 STT/TTS setup, voice chat working.
- Week 11: M11 voice + research integration. Full M9 streaming. Notebook 11.
- Week 12: full M10 (observability, deployment hardening). Notebooks 09, 10. Docs polish. **Ship 3.**

**Ship 3:** demo with voice; all 11 notebooks; full benchmark report; finalized README + architecture docs; voice blog post; all ADRs.

## Out of scope (until a post-MVP Phase 4)

Multi-tenancy, SSO/RBAC, Kubernetes, 40+ connectors, enterprise vector DBs, mobile/desktop apps, distributed execution, fine-tuning, billing, admin dashboards, i18n, knowledge graphs.
