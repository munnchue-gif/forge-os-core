# FORGE OS — CURRENT STATUS
**Updated:** 2026-08-10
**Owner:** mancier / munnchue-gif

Any model: read this file first. It is the managed snapshot of where the project is.

---

## Where we are (locked)

| Item | Value |
|------|--------|
| Canonical PC tree | `~/the-forge` |
| PC snapshot copy | `~/forge-os-locked-pc` (rsync, no .venv/.git) |
| NPU | OpenVINO sees `CPU`, `GPU.0`, `GPU.1`, `NPU` |
| Bridge | `http://127.0.0.1:8787` (uvicorn) |
| Baseline tests | **62 passed** (simple fabric suite) |
| Internal ledger | **Simple** append log (no hash chain) |
| Crypto boundary | **Gate + external adapters/sockets only** |
| Base44 | Optional glass only — not the spine |

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
That is the main source of remaining test failures. Fix = map to the live signature (or a small `make_finding()` helper). Do **not** reintroduce a second Finding type.

### Severity mapping (recommended)
- int `0` → `"info"` or `"0"`
- int `1` → `"low"` or `"1"`
- int `2` → `"medium"` or `"2"`
- int `3` → `"critical"` or `"3"`

Pick one scheme and stick to it in STATUS updates.

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

**Design suite (deferred):** chained audit ledger, rich Finding/judge/conduit/bind tests. Re-enable only after Finding callers are unified and ledger policy is explicit.

---

## Repo map

| Repo | Role |
|------|------|
| `munnchue-gif/the-forge` (public) | Live fabric code on master |
| `munnchue-gif/forge-os-core` (private) | **Status + lock docs + production path** |
| `munnchue-gif/forge-copilot` (private) | Prompts so any model can see state |
| `forge-arena` / `sovereign-forge-v4` | Arena / V4 architecture — not this baseline |
| `git-concoctinating` | Base44 board — archive/glass only |

---

## Next bricks (ordered)

1. Unify all `Finding(...)` construction to live fields (types.py).
2. Commit `~/the-forge` fabric (incl. isolation/sequence) and push `the-forge` + mirror docs here.
3. Optional: thin Gate egress hash for external adapters only.
4. Do not pull hash-chain internal ledger unless product requires tamper-evidence.

---

## How any model should work

1. Read **this file** (`STATUS.md`).
2. Read `LOCKED.md` / NPU notes if changing Gate or NPU.
3. Prefer `~/the-forge` / this repo over Drive dumps and `ALLFORGE` copies.
4. Do not mix Base44 entities into the fabric spine.
5. After changes: re-run the 62-test baseline; update this STATUS date and numbers.
