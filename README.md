# PCT Canonical Snapshot — Supreme Program Rules (2025-12-06)

**Authority:** Program Control Tower V1 (PCT) — account-wide, single source of truth.  
**Write access:** PCT only. Departments & builder threads: read-only.

## Routing & Budgets
- Order: Apple → SLM → Azure (Perplexity only for shopping).  
- Default today: **Azure** until SLM-ONLY R1–R4 pass.  
- Per-turn budgets: ≤1 search / ≤3 reads / ≤30 s.

## ID Canon & Cancel (P4.1)
- One **turnId** per send → reuse as **X-Request-Id** (cloud) and **requestId** (SLM).  
- SSE must drop stray/late chunks (requestId mismatch).  
- **Cancel ≤500 ms**; allow partial billing for streamed tokens.

## SLM-ONLY — Phase Order (current)
Place **after T5–T12** and **before DEG**:
- **R1:** Contract & Diagnostics (lock BrainClient I/O; per-call logs).  
- **R2:** Context Lifecycle & Latency (context/Metal reuse; caps; A17 Quick ≤2 s, Think ≤6 s).  
- **R3:** Streaming + Auto-Continuation (TTFB ≤0.7 s warm / ≤1.5 s cold; segmented decode; continue on length).  
- **R4:** Language/Tone + Repetition Clamp (strict header; 1 retry on LID miss; 3–4-gram clamp; Quick/Think skeletons).

## Dept 5 — iOS Host App
- **Conversation Mode removed** (owned by Conversation Mode Team).  
- Keeps: Insert-Mode, cloud SSE + Cancel, Safe Thinking Overlay.  
- Terminal phase: **DinoVoice (XTTS-v2) runtime + Clone Voice** (on-device; consent/purge; Apple TTS fallback).  
- Start DinoVoice **after SLM-ONLY R1–R4** are green.

## SLM Training — Dino-4B
- **Status:** DONE (Prod V1.1); maintenance-only.  
- Keep Azure default while SLM repairs land.  
- **Do not retrain 7B now**; reconsider only if post-R1–R4 gates still fail (e.g., Quick >3 s / Think >10 s typical, or lang/tone <90%/80%).

## Azure Backend — Guards
- Honor cancel; stop generation on disconnect; record partial tokens for canceled streams.  
- `/v1/model/manifest`: SAS (5-min) + sha256 enforced.  
- Audits: ≤1 cloud bill & ≤1 SLM usage per `(userId, requestId)`; join on requestId to catch double-billing.

**Consumption Rule:** All departments must link to this file as “PCT Canonical Snapshot”. When in doubt, this wins.
