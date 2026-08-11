# CURRENT.md — Forge OS Live State
**Last updated:** 2026-08-10 (evening)

## Active Reality (what is actually running / true right now)

- **Hardware**: MSI Vector, Intel Arrow Lake NPU + RTX 5080 16GB, Pop!_OS. NPU is visible and working in OpenVINO (`['CPU', 'GPU.0', 'GPU.1', 'NPU']`).
- **Live local tree**: `~/the-forge` (primary working copy). Bridge on `:8787`, Vite App on `:5173`.
- **Glass rule still in force**: App only requests; Forge decides. No secrets, no logic, no decisions in the App.
- **Mint path**: IN PROGRESS — request_action + full Gate + ledger wiring is the active work item.
- **Base44**: Fully decoupled in intent. Old public repos are archive only.

## Repo Map (labels)

| Repo | Visibility | Role / Label | Status |
|------|------------|--------------|--------|
| **forge-os-core** | Private | PRODUCTION CORE — Overseer, Gate, NPU seat, INSTALL | Thin but correct home for finished core |
| **sovereign-forge-v4** | Private | ADAPTIVE / META PATH — Splicing, capsules, meta-router, VRAM keychain | Empty shell — future home for Meta-Forge |
| **forge-arena** | Private | CRITIQUE / INPUT ZONE — detached | Thin |
| **forge-copilot** | Private | CONTINUITY LAYER — CURRENT.md, LEDGER.md, recovery prompts | Active continuity home |
| **the-forge** (public) | Public | Historical / early | Archive |
| **the-forge-ui** (public) | Public | Early UI liberation attempt | Archive |
| **git-concoctinating** (public) | Public | Original Base44 Command Board | Archive only — never source of truth |

## Salvaged from forge-board-core.zip (2026-08-10)

Cleaned bridge panels live in `/home/workdir/artifacts/salvaged_bridge/`:
- MintPanel.jsx (glass language, correct ops)
- LiveFeed.jsx, HealthPanel.jsx, LedgerPanel.jsx, WrapsPanel.jsx, ConcoctPanel.jsx
- PanelShell, TroubleshootPanel, BridgeSettings, ConnectionGuide, TaskRow
- forgeBridge.js (localStorage config + bridgeFetch + SSE openFeed — still has CF headers, easy to strip)

These are the best App-layer pieces. Use them; discard Base44 entities/auth.

## New material classified (2026-08-10 evening)

**Thread 1 — Fabric / Forge-NG core (security-first Python fabric)**
- SELF_GROWING_ADAPTER_WHITEPAPER.md + INSTALL.md → design draft only. adapter.py not written. Sits on Gate/Bus/Overseer/WrapStore. Do not implement until mint is green.
- Master Whitesheet + kimi assessments → historical validation of security model (macaroons, judge, ledger, burn). Hardware concerns largely resolved by NPU fix.

**Thread 2 — Practical Forge Platform (Ollama + Docker + capsules)**
- Fedora Migration Guide (full React/Vite app + guideData.ts) → polished, self-contained operator guide for Pop!_OS → Fedora move. Park as finished deliverable.
- Long kimi chat history → evolution of rooms/corridors, hot-swappable models, Overseer risk scoring, auto-dissolving capsules. Valuable context, not live code.

**Noise**
- Pasted document.txt → unrelated NSFW roleplay. Quarantine / ignore.

## Immediate Priority Order

1. **Finish mint / request_action** so the glass works end-to-end. (ACTIVE)
2. Integrate cleaned bridge panels into the live App.
3. Only then open the Self-Growing Adapter or splicing / meta-router work.
4. Fedora migration is a separate, later decision.
