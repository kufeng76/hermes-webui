---
applyTo: "tests/**/*.py"
description: "Use when editing or adding pytest coverage, regression tests, fixtures, or browser-contract tests."
---

# Test instructions

- Prefer focused regression tests named for the issue or behavior being fixed. This repo already uses many issue-pinned tests, so extend the closest existing coverage before creating a broad new umbrella test.
- Reuse fixtures from `tests/conftest.py` before adding ad hoc setup. The shared fixtures already isolate ports, state directories, workspaces, and network access.
- Keep tests hermetic. Avoid real `~/.hermes` state, external network access, and timing-heavy assertions when a narrower contract can be pinned.
- When UI behavior changes, update the smallest relevant regression tests and use `TESTING.md` for the visible browser contract.
- Run the narrowest relevant `pytest` target first; the broad fallback remains `pytest tests/ -v --timeout=60`.