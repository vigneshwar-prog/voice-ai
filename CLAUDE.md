# Voice AI Agent — Project Rules

## What this project is

A phase-by-phase, learn-by-building local-first voice AI agent, evolving into a
real-time multimodal voice agent using Pipecat. See `PLAN.md` for the full
22-phase roadmap and current status.

Source spec: `~/Downloads/Voice Agent — Phase-by-Phase Build Prompt.md`

## Non-negotiable working rules

1. **Explain before acting, every phase, no exceptions.**
   Before writing or editing any code for a phase, explain in depth:
   - What we're building in this phase and why it exists in the pipeline.
   - The architecture / data flow for this phase (draw it out in text/ASCII).
   - The key concepts involved (e.g. what is TTFT, why streaming, why
     backpressure matters, what a tool-calling schema is, etc.) — teach it,
     don't just namedrop it.
   - Trade-offs and alternatives (e.g. local vs. managed service, why this
     library over another).
   - What could go wrong / common failure modes for this phase.
   Only after this explanation is given (and, when the phase is a major or
   ambiguous one, after the user has confirmed) do we move to implementation.

2. **One phase at a time.** Do not skip ahead or pre-build later phases.
   Do not silently combine phases. Follow the phase list in `PLAN.md` in
   order unless the user explicitly asks to jump or reorder.

3. **Stop after every phase.** At the end of each phase, always provide:
   - What we built (summary)
   - Architecture/data flow
   - Files + complete runnable code
   - Install/run/test instructions
   - Important concepts explained
   - Common failures
   - Latency measurements where applicable
   - A short interview-style explanation of the phase
   - What comes next
   Then STOP and wait for the user to say "Continue" (or ask questions).

4. **Local-first, minimal deps, by design.** Prefer Python, Ollama,
   faster-whisper, Piper (or similar local TTS), FastAPI. Do NOT introduce
   LangChain, LangGraph, MCP, vector databases, Kubernetes, etc. until the
   plan explicitly reaches that phase and there is a clear pedagogical reason.
   Managed services (Deepgram, ElevenLabs) are introduced only in their
   designated later phases, explicitly as a comparison against the local
   approach — always explain the cost/latency/privacy trade-off when doing so.

5. **Optimize for understanding, not speed of delivery.** The goal is for
   the user to be able to explain and defend every architectural decision in
   a software engineering interview. When in doubt, favor a deeper
   explanation over a faster implementation.

6. **Existing RAG asset — reuse, but not as a shortcut for learning.**
   There is a production-grade RAG backend at
   `/Users/vigneshwar/Documents/AI/Rag_production` (FastAPI, Pinecone,
   sentence-transformers, Ollama provider, prompt-injection/PII safety
   services). Rules for using it:
   - Phase 9 (RAG fundamentals) must still be built from scratch, small and
     local (local embeddings + simple/in-memory or FAISS store) — the point
     is to learn retrieval fundamentals, not to wire up existing
     infrastructure.
   - From Phase 15 (full agent) and Phase 21 (production architecture)
     onward, explicitly revisit `Rag_production` as the "production-grade"
     option — reuse `rag_service.py`, the provider abstractions, and
     especially `safety_service.py` (prompt injection + PII) when we reach
     Phase 19 (security).
   - The voice agent should call the RAG backend as a **tool** via HTTP,
     consistent with the tool-calling model introduced in Phases 6–7, not by
     merging codebases.

7. **Hardware-aware model selection.** Recommend local model sizes
   (LLM/STT/TTS) based on the user's actual hardware. Ask for hardware specs
   in Phase 0 if not already known, and revisit model choice if performance
   is a problem in later phases.

8. **Track progress in `PLAN.md`.** After each phase is completed and the
   user confirms, update `PLAN.md`'s status table before moving on.
