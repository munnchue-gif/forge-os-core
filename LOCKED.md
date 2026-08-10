# FORGE OS — LOCKED RECORD
**Date locked:** 2026-08-10  
**Canonical PC:** `~/the-forge`  
**Snapshot:** `~/forge-os-locked-pc`  
**Live status:** see `STATUS.md`

Do not mix with Base44-coupled entity models as spine.

---

## Frozen decisions

| Decision | Locked value |
|----------|----------------|
| Active path | Decoupled 2026-08-08 |
| NPU | OpenVINO **2026.3.0** + **libze1=1.17.44 held** |
| Overseer | Watcher observe-only + Commander act-only via Gate |
| Gate | One door; nonce per mint |
| Internal ledger | **Simple** event log |
| Crypto | Gate + external adapters/sockets only |
| Secrets | Client-side / env |
| Baseline tests | **62 passed** (design suite deferred) |
| Finding | `id, organ, severity:str, title, detail` in `types.py` |

---

## Baseline test command

```bash
cd ~/the-forge && source .venv/bin/activate
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
```

---

## Change control

- Gate, nonce, libze1/OpenVINO version, or ledger policy changes require updating this file + STATUS.md.
- Watcher must never gain act methods; Commander must never gain observe methods.
