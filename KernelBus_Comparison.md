# KernelBus — Two Historical Variants

## Variant A — Callback Fan-Out (has P0 isolation bug)

**Source**: baseline master.md / NPU_Repo dump  
**Style**: Immediate `asyncio.gather` to all subscribers + taps.

**Critical bug**: both `asyncio.gather` calls use `return_exceptions=False`.  
One crashing subscriber or tap kills the entire publish for everyone.

```python
# The broken lines (must change to return_exceptions=True if this variant is kept)
await asyncio.gather(*tap_tasks, return_exceptions=False)
await asyncio.gather(*sub_tasks, return_exceptions=False)
```

Pros: simple, low latency, zero-copy envelope.  
Cons: isolation failure is fatal; no back-pressure; no ordered processing.

---

## Variant B — Queue-Driven Worker (safer for multi-agent)

**Source**: (Forge)master.md / Kernel Review Module  
**Style**: Central `asyncio.Queue` + single background `_process_queue` task.  
Uses integer subscription tokens. Supports typed `Event` objects and wildcards.

Pros:
- Natural back-pressure (queue maxsize)
- Isolation is inherent (tasks are fire-and-forget with done callbacks)
- Easier to reason about ordering and draining on shutdown
- Token-based unsubscribe is clean

Cons:
- Slightly higher latency (queue hop)
- Requires `start()` / `stop()` lifecycle
- Callers must publish proper `Event` objects, not raw dicts

**Recommendation**: Prefer Variant B (or a cleaned hybrid) for production.  
If you keep Variant A, the first patch must be changing both gathers to `return_exceptions=True`.
