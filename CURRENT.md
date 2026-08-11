# CURRENT.md — Forge OS Live State
**Last updated:** 2026-08-10

## Active Reality (what is actually running / true right now)

- **Hardware**: MSI Vector, Intel Arrow Lake NPU + RTX 5080 16GB, Pop!_OS. NPU is visible and working in OpenVINO (`['CPU', 'GPU.0', 'GPU.1', 'NPU']`).
- **Live local tree**: `~/the-forge` (primary working copy). Bridge on `:8787`, Vite App on `:5173`.
- **Glass rule still in force**: App only requests; Forge decides. No secrets, no logic, no decisions in the App.
- **Mint path**: Still incomplete / erroring. request_action + full Gate + ledger wiring needed.
- **Base44**: Fully decoupled in intent. Old public repos are archive only.

## Repo Map (labels)

| Repo | Visibility | Role / Label | Status |
|------|------------|--------------|--------|
| **forge-os-core** | Private | PRODUCTION CORE — Overseer, Gate, NPU seat, INSTALL | Thin but correct home for finished core |
| **sovereign-forge-v4** | Private | ADAPTIVE / META PATH — Splicing, capsules, meta-router, VRAM keychain | Empty shell — future home for Meta-Forge |
| **forge-arena** | Private | CRITIQUE / INPUT ZONE — detached | Thin |
| **forge-copilot** | Private | CONTINUITY LAYER — CURRENT.md, LEDGER.md, recovery prompts | Thin — expand with this file |
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

## Immediate Priority Order

1. Finish mint / request_action so the glass works end-to-end.
2. Land CURRENT.md + LEDGER.md into forge-copilot and forge-os-core.
3. Integrate cleaned bridge panels into the live App.
4. Only then open the splicing / capsule / meta-router work in sovereign-forge-v4.
