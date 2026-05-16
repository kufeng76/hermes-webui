---
applyTo: "api/**/*.py"
description: "Use when editing Python backend modules for routes, session state, onboarding, providers, uploads, or streaming."
---

# Backend/API instructions

- Keep `server.py` thin. New HTTP behavior usually belongs in `api/routes.py` or a focused helper module under `api/`.
- Preserve session and streaming contracts. Disk-backed session JSON, sidebar/session metadata projection, pending-turn state, SSE payloads, and replay/journal behavior are coupled surfaces.
- Do not change SSE event names or payload shapes casually. For streaming, replay, recovery, or run-journal work, read `ARCHITECTURE.md`, `docs/rfcs/hermes-run-adapter-contract.md`, and `docs/rfcs/webui-run-state-consistency-contract.md` first.
- Keep multipart upload paths ahead of generic request-body parsing. Consuming `rfile` before the upload handler will break `/api/upload`.
- Process-global env overrides such as `TERMINAL_CWD`, `HERMES_HOME`, and `HERMES_SESSION_KEY` are part of the current single-user runtime model. Do not make partial concurrency changes without tracing the whole request lifecycle.
- Prefer existing config surfaces over new ad hoc keys. Provider/model work should stay compatible with `api/config.py`, profile scoping, and existing auxiliary routing conventions.
- For onboarding, bootstrap, or provider-readiness changes, link to or defer to `docs/onboarding-agent-checklist.md`, `docs/onboarding.md`, and `docs/troubleshooting.md` instead of re-embedding that guidance.
- Validate with the narrowest relevant `pytest` target first. Use `pytest tests/ -v --timeout=60` only when the slice truly needs broad coverage.