# FORGE OS — CURRENT STATUS
**Updated:** 2026-08-11
**Owner:** mancier / munnchue-gif

Any model: read this file first. It is the managed snapshot of where the project is.

---

## Where we are (locked)

| Item | Value |
|------|--------|
| Canonical PC tree | `~/the-forge` |
| PC snapshot copy | `~/forge-os-locked-pc` (rsync, no .venv/.git) |
| NPU | OpenVINO sees `CPU`, `GPU.0`, `GPU.1`, `NPU` |
| Bridge code | `forge/bridge/server.py` (contract endpoints present) |
| Bridge boot gap | GitHub tree still has `ForgeKernel()` without `secret` — prefer `boot_forge()`; see forge-copilot `bridge-patch/BOOT_FIX.md` |
| Baseline tests | **62 passed** (simple fabric suite) |
| Internal ledger | **Simple** append log (no hash chain) |
| Crypto boundary | **Gate + external adapters/sockets only** |
| Base44 | Optional glass only — **not the spine** |

### Frozen decisions
- Path: decoupled 2026-08-08
- NPU: OpenVINO **2026.3.0** + **libze1 1.17.44 held**
- Overseer: Watcher observe-only / Commander act-only via Gate
- Gate: one door, nonce per mint
- Secrets: client-side / env — never in DB as source of truth

---

## Finding (canonical shape — live)

```text
Finding(
  id: str,
  organ: str,
  severity: str,   # not int
  title: str,
  detail: str,
  timestamp: float = auto,
  metadata: dict = auto,
)
```

Defined in `forge/fabric/types.py`.

**Old callers still use** `section_id=`, `kind=`, `severity=int`.  
Fix = map to the live signature. Do **not** reintroduce a second Finding type.

---

## Multi-model protocol

| Location | Role |
|----------|------|
| `forge-copilot/protocol/` | PRE_PROMPT, MASTER_PROMPT, AI NODE COMMIT LOG template |
| `forge-copilot/node-logs/` | Append-only session logs |
| `forge-copilot/handoff/` | STATE / NEXT / RESUME |

**Any model session:** STATUS (this file) → protocol absorb → AI NODE COMMIT LOG for every substantive reply → append node-logs when code changes.

---

## Test policy

**Baseline (must stay green):**
```bash
python -m pytest forge/fabric -q \
  --ignore=forge/fabric/test_ledger.py \
  --ignore=forge/fabric/test_kernel.py \
  --ignore=forge/fabric/test_judge.py \
  --ignore=forge/fabric/test_sandbox.py \
  --ignore=forge/fabric/test_sequence.py \
  --ignore=forge/fabric/test_overseer.py \
  --ignore=forge/fabric/test_conduit.py \
  --ignore=forge/fabric/test_bridge_accessors.py \
  --ignore=forge/fabric/bind/test_bind.py
# expect: 62 passed
```

---

## Repo map

| Repo | Role |
|------|------|
| `munnchue-gif/the-forge` (public) | Live fabric code |
| `munnchue-gif/forge-os-core` (private) | Status + lock docs |
| `munnchue-gif/forge-copilot` (private) | Protocol + handoff + node-logs |
| `forge-arena` / `sovereign-forge-v4` | Post-build |
| `git-concoctinating` / `the-forge-ui` | Base44 history — glass only |
| `fabric-ui` | Manifesto presentation — not core |

---

## Next bricks (ordered)

1. Fix bridge `_boot` to `boot_forge()` and prove `/health`.
2. Unify all `Finding(...)` construction to live fields.
3. Commit PC fabric deltas to `the-forge` if local is ahead.
4. Optional: thin Gate egress hash for external adapters only.
5. Do not pull hash-chain internal ledger unless product requires it.

---

## How any model should work

1. Read **this file**.
2. Absorb `forge-copilot/protocol/PRE_PROMPT.md` + `MASTER_PROMPT.md`.
3. Use **AI NODE COMMIT LOG** for substantive outputs.
4. Prefer `~/the-forge` / these repos over Drive dumps.
5. Do not mix Base44 into the fabric spine.
6. After changes: 62-test baseline; append `node-logs/`; update this STATUS if numbers change.
