# LEDGER.md — Append-Only Evolution Log
**Rule**: Never edit previous entries. Only append. Date every entry. This is the uneditable handoff for any model.

---

### 2026-08-10 evening — New material intake + mint start

- Received large dump: Self-Growing Adapter whitepaper + INSTALL, kimi deep-dive assessments, Master Whitesheet, long architecture chat history, complete Fedora Migration Guide React app.
- Classified into two threads that must stay separate:
  - Thread 1 (Fabric core): Adapter whitepaper is design-only; do not code until mint is solid.
  - Thread 2 (Practical Platform): Fedora guide is a finished operator deliverable; park it.
- Noise (NSFW paste) quarantined.
- Decision confirmed: start mint / request_action now as the highest-leverage unfinished piece.
- Updated CURRENT.md with classification and new priority.

### 2026-08-10 — Session handoff & salvage

- Confirmed NPU is permanently fixed and visible in OpenVINO.
- Reviewed forge-board-core.zip (Base44-era App). Salvaged all bridge/* panels + forgeBridge.js into artifacts/salvaged_bridge/. They already speak correct glass language.
- Identified two KernelBus variants in historical material (callback fan-out with isolation bug vs queue-driven worker). Neither is yet the live production bus.
- GitHub layout is intentionally split but currently thin. Labels applied in CURRENT.md.
- Decision: finish glass + mint first. Do not force Meta-Forge / splicing code until the door is solid.
- Created this LEDGER + CURRENT.md as the permanent continuity mechanism.
- Pushed CURRENT.md, LEDGER.md, KernelBus_Comparison.md into forge-copilot and forge-os-core.

### 2026-08-09 and earlier (summary from prior sessions)

- NPU driver stack (libze1, ICD, ZE_* env) fixed after multiple attempts.
- Bridge server on 8787 with /health, /sections, /wraps live; /mint and /concoct/preview incomplete.
- Private repos created: forge-os-core, sovereign-forge-v4, forge-arena, forge-copilot.
- Explicit decoupling from Base44 ordered and in progress.
- Capsule / Confetti Snips / Model Splicing (Tri-part Memory Sink) designed in detail but not implemented in live tree.
