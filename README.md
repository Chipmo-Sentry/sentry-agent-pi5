# sentry-agent-pi5

The **premium edge-AI** camera agent for **Chipmo Sentry**, targeting the **Orange Pi 5** and its **RK3588
NPU** (6 TOPS). Unlike the other agents, this one is designed to run a real Stage-1 model **on the board**,
so only candidate events travel to the cloud — cutting uplink bandwidth and central GPU load for stores
with many cameras or weak internet.

> **Status: planned (M3+) — not started.** This repo is a placeholder, scheduled after
> [sentry-agent-pizero2w](https://github.com/Chipmo-Sentry/sentry-agent-pizero2w). It needs its own
> proof-of-concept: YOLO11n converted to **RKNN** running on the RK3588 NPU at a usable frame rate.

Planned stack: **Go** (relay + pairing, shared design with the Pi Zero agent) · **RKNN-Toolkit-Lite2**
(NPU inference) · cross-compiled ARM `.img` · published on GitHub Releases.

---

## Intended role

- **Edge filter, cloud decision.** The on-board NPU runs a lightweight person/motion + shelf-zone filter
  (a *bandwidth* filter), then pushes only candidate clips to
  [sentry-ingest](https://github.com/Chipmo-Sentry/sentry-ingest). The full behaviour engine + VLM verdict
  still happen on [sentry-ai](https://github.com/Chipmo-Sentry/sentry-ai) — the architectural rule that AI
  *decisions* live on the AI host holds even here ([docs/07-DECISIONS.md](../docs/07-DECISIONS.md)).
- **Same pairing + relay contract** as the other agents (6-digit code → agent JWT → `/api/v1/agent/*`),
  with a Go client generated from the backend OpenAPI spec.

## Where it sits in the lineup

| Tier | Agent | Hardware | AI on device |
|---|---|---|---|
| Free | [sentry-agent-pc](https://github.com/Chipmo-Sentry/sentry-agent-pc) | store's own Windows PC | none |
| Mid | [sentry-agent-pizero2w](https://github.com/Chipmo-Sentry/sentry-agent-pizero2w) | Orange Pi Zero 2W | none (relay only) |
| **Premium** | **sentry-agent-pi5** | Orange Pi 5 + RK3588 NPU | **Stage-1 bandwidth filter** |

Target retail price ~$199–299 (M3+ plan).

---

## Related repos

- [sentry-agent-pizero2w](https://github.com/Chipmo-Sentry/sentry-agent-pizero2w) — the relay-only sibling (shares the Go core)
- [sentry-agent-pc](https://github.com/Chipmo-Sentry/sentry-agent-pc) — the shipping reference agent
- [sentry-ai](https://github.com/Chipmo-Sentry/sentry-ai) — cloud behaviour engine + VLM verdict

Platform overview: [Sentry-v.3 README](../README.md).
