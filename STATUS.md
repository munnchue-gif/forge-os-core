# FORGE OS — CURRENT STATUS
**Updated:** 2026-08-11 (post-cleanup)
**Owner:** mancier / munnchue-gif

Any model: read this file first. It is the managed snapshot of where the project is.

---

## Where we are (locked)

| Item | Value |
|------|--------|
| Canonical PC tree | `~/the-forge` |
| Source of truth (code) | `munnchue-gif/the-forge` |
| Entry point for humans & models | `the-forge/START_HERE.md` |
| NPU | OpenVINO sees `CPU`, `GPU.0`, `GPU.1`, `NPU` |
| Bridge | **FIXED** — boots via `boot_forge()` (secret supplied). Old bare `ForgeKernel()` path removed. |
| Baseline tests | **62 passed** (simple fabric suite) |
| Internal ledger | **Simple** append log |
| Crypto boundary | **Gate + external adapters/sockets only** |
| Base44 | Optional glass only — **not the spine** |

### Frozen decisions
- Path: decoupled 2026-08-08
- NPU: OpenVINO **2026.3.0** + **libze1 1.17.44 held**
- Overseer: Watcher observe-only / Commander act-only via Gate
- Gate: one door, nonce per mint
- Secrets: client-side / env — never in DB as source of truth
- Finding: live shape in `fabric/types.py` (`id, organ, severity:str, title, detail`) + `make_finding` compatibility helper

---

## Multi-model protocol (enforced)

| Location | Role |
|----------|------|
| `the-forge/START_HERE.md` | Hard entry for every session |
| `forge-copilot/protocol/` | PRE_PROMPT + MASTER_PROMPT + AI NODE COMMIT LOG |
| `forge-copilot/node-logs/` | Append-only session logs |
| `forge-copilot/handoff/` | STATE / NEXT / RESUME |

**Any model session:** START_HERE → this STATUS → protocol absorb → AI NODE COMMIT LOG for every substantive reply → append node-logs when code changes.

---

## Test policy

**Baseline (must stay green):**
```bash
cd ~/the-forge && source .venv/bin/activate
export PYTHONPATH=$HOME/the-forge/forge
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

## Repo map (clean)

| Repo | Role |
|------|------|
| `munnchue-gif/the-forge` | **Source of truth** — live fabric code |
| `munnchue-gif/forge-os-core` | Status + lock docs |
| `munnchue-gif/forge-copilot` | Protocol + handoff + node-logs |
| `fabric-ui` / `the-forge-ui` / `git-concoctinating` | Glass / history — not spine |
| `forge-arena` / `sovereign-forge-v4` | Post-build / experimental |

---

## Next bricks (ordered)

1. On the live PC: prove `GET http://127.0.0.1:8787/health` → `booted: true`
2. Sweep any remaining old Finding constructors onto the live shape / `make_finding`
3. Bind real models (NPU brain + RTX capsules) using the scripts in `forge/bind/`
4. Keep the glass App thin and behind the contract

---

## How any model should work

1. Read **START_HERE.md** then **this file**.
2. Absorb `forge-copilot/protocol/PRE_PROMPT.md` + `MASTER_PROMPT.md`.
3. Use **AI NODE COMMIT LOG** for every substantive output.
4. Prefer small verifiable patches. Do not restart the architecture.
5. After changes: baseline tests + node-log + update this STATUS if numbers change.
