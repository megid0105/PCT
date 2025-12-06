# PCT — Codex-Max Strategy & Rules (Account-Wide)

**Authority:** Program Control Tower V1 (PCT)  
**Scope:** All departments & builder threads (read & obey). PCT is the only writer of project memory.

---

## 1) Purpose
Codex-Max standardizes how CTs/builders apply phases, generate QC, run audits, and publish updates. It eliminates desync by reading the **PCT Canonical Snapshot** on every run and enforcing guardrails.

## 2) Non-Negotiable Guardrails (Law)
1. **PCT memory is write-protected.** Codex-Max must never write/modify PCT memory; it only opens PRs or pushes MD to dept boards.
2. **ID Canon:** Every command requires `--request-id` (UUID). The same ID appears in logs, artifacts, and PR titles.
3. **Dry-Run First:** Default `--dry-run`; `--apply` requires a signed role token (least-priv).
4. **RBAC:** Roles — PCT (approves), Dept CT (merges), Builders (run). Everything auditable.
5. **Budgets:** ≤1 search / ≤3 reads / ≤30s of networked tool time per command/turn.
6. **Allowlist-only:** Codex-Max talks only to approved repos/services; no arbitrary URLs.
7. **Snapshot Check:** Refuse if local PCT snapshot is older than upstream. Always run `codex snapshot sync` first.
8. **Artifacts Required:** Phase changes must ship the **QC trio** (PhasePropertyList.md, HostWiring-Sketch.md, QC_Report.md) + `codex-manifest.json` (requestId + snapshotDate).
9. **Dept 5 guards:** Verify **Cancel ≤500 ms** and SSE requestId guards in CI.
10. **Billing/Usage audits:** Weekly join audit on `(userId, requestId)` across cloud billing & SLM usage; zero double-bill anomalies.

## 3) Does / Does Not
**Does:** read snapshot; generate MD; open PRs; run audits; pin deltas; verify guards in CI.  
**Does not:** write PCT memory; change schemas; bypass rate limits; run unlimited network/tools.

## 4) Required Outputs per Phase
- `SLM-<Phase>-<Feature>-PhasePropertyList.md`  
- `SLM-<Phase>-<Feature>-HostWiring-Sketch.md`  
- `SLM-<Phase>-<Feature>-QC_Report.md`  
- `codex-manifest.json` (requestId, snapshotDate, dept, phase, artifacts[])

## 5) Enforcement
CI/PR fails if snapshot stale, QC trio missing, Cancel/SSE tests fail, or audits detect multi-billing. Violations page Dept CT + PCT.

## 6) Pilot Scope & Acceptance
**Departments:** SLM-ONLY, Dept 5.  
**Acceptance:** (a) 100% PRs include QC trio with current snapshot date; (b) Cancel ≤500 ms verified; (c) zero double-bill anomalies for 7 days; (d) no Codex-Max writes to PCT memory.

---

### Canonical Expectations (today)
- Routing: Apple → SLM → Azure (Azure default until SLM R1–R4 pass)  
- SLM-ONLY: **R1, R2, R3, R4** before DEG  
- Dept 5: Conversation Mode external; terminal phase **DinoVoice (XTTS-v2)**
— PCT V1
