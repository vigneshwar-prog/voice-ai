# Voice AI Agent — Build Plan

Learn-by-building, phase-by-phase local-first voice AI agent, evolving into a
real-time multimodal agent with Pipecat. Rules for how we work through this
plan are in `CLAUDE.md` — most importantly: **explain in depth before any
action, one phase at a time, stop after each phase.**

Related asset: `/Users/vigneshwar/Documents/AI/Rag_production` (existing
production RAG backend — reused starting Phase 9 discussion / Phase 15 /
Phase 21, see `CLAUDE.md` rule 6).

## Status legend
⬜ Not started · 🟨 In progress · ✅ Done

## Phases

| # | Phase | Goal | Status |
|---|-------|------|--------|
| 0 | Environment + architecture | Hardware assessment, install Ollama/Whisper/TTS, overall architecture diagram | ⬜ |
| 1 | Ollama | Text → local LLM → response | ⬜ |
| 2 | Whisper/faster-whisper | Microphone → speech → text | ⬜ |
| 3 | Voice + Ollama | Mic → STT → Ollama → text response | ⬜ |
| 4 | Local TTS | STT → Ollama → TTS → speaker (full local voice loop) | ⬜ |
| 5 | Agent + tool calling | LLM decides when to call tools (calculator/time/weather) | ⬜ |
| 6 | Reliable tools | Schemas, validation, authorization, timeout, retries, failure handling | ⬜ |
| 7 | Memory + conversation state | Multi-turn context management | ⬜ |
| 8 | RAG (local) | Local embeddings + retrieval, built from scratch | ⬜ |
| 9 | Real-time fundamentals | Streaming, WebSockets/WebRTC, latency, buffering, backpressure, cancellation | ⬜ |
| 10 | Latency engineering | Measure STT/LLM TTFT/tool/TTS TTFA/end-to-end; build a latency budget | ⬜ |
| 11 | Pipecat | Rebuild pipeline on Pipecat — processors, frames, transports, orchestration | ⬜ |
| 12 | Streaming ASR (Deepgram, optional) | Integrate + compare vs local Whisper | ⬜ |
| 13 | Streaming TTS (ElevenLabs, optional) | Integrate + compare vs local TTS | ⬜ |
| 14 | Full real-time voice agent | Pipecat + streaming STT + Ollama + tools/RAG + streaming TTS | ⬜ |
| 15 | Graceful degradation | Timeouts, retries, fallbacks, cancellation, service failure handling | ⬜ |
| 16 | Barge-in / interruption | User can interrupt agent mid-speech | ⬜ |
| 17 | Observability | Structured logs, latency metrics, TTFT/TTFA, errors, retries, fallbacks | ⬜ |
| 18 | Security | Prompt injection (direct/indirect), malicious RAG data, tool authz, RBAC, input/output validation, sandboxing | ⬜ |
| 19 | MCP | Introduce MCP after understanding plain tool calling; explain where it fits | ⬜ |
| 20 | Production architecture | Scalability, WebRTC/WebSockets, sessions, GPUs, cost, reliability, monitoring | ⬜ |
| 21 | Interview preparation | Full architecture walkthrough + engineering trade-offs | ⬜ |

*(Numbering here is 0-indexed to match the source prompt's "Phase 0" start;
the source prompt's phases 1–22 map to rows 0–21 above.)*

## Technology baseline (local-first, per CLAUDE.md rule 4)

- Language: Python
- LLM: Ollama (local model, size TBD in Phase 0 based on hardware)
- STT: faster-whisper
- TTS: Piper (or comparable local TTS)
- Backend: FastAPI (once needed)
- Frontend: minimal, kept simple until real-time phases
- Real-time orchestration: Pipecat (from Phase 11)
- Optional managed comparisons: Deepgram (ASR, Phase 12), ElevenLabs (TTS, Phase 13)
- Explicitly deferred until their designated phase: LangChain, LangGraph,
  MCP (Phase 19), vector databases (beyond a minimal local one in Phase 8),
  Kubernetes

## Current status

**Next up: Phase 0 — Environment + architecture.**
Nothing has been built yet. Waiting to begin Phase 0 with hardware
assessment and an in-depth explanation before any installation/code.

## Learning notes

`learning.html` — a standalone, sidebar-navigable HTML page logging every
phase's notes and every Q&A doubt raised during the build. Open it directly
in a browser (`open learning.html`). New entries are appended to the
`ENTRIES` array in the file's script; each phase gets a "PHASE" entry when
completed, and each ad-hoc question gets a "Q&A" entry. Sidebar supports
search and filtering by type.

## Change log

- Project created. `CLAUDE.md` and `PLAN.md` established. Ready to start Phase 0.
- Added `learning.html` (sidebar-navigable notes log) with first Q&A entry: STT/TTS explainer + popular models comparison.
