---
applyTo: "static/**"
description: "Use when editing the vanilla-JS frontend, CSS, templates, message rendering, panels, or workspace UI."
---

# Frontend instructions

- Preserve the no-build, no-framework structure. Extend the current `static/*.js` modules instead of adding framework state layers, bundlers, or parallel abstractions.
- `static/index.html` and `static/boot.js` own first-paint, restore, and panel-state preload behavior. Changes around sidebar/workspace state, bfcache, or reconnect flows must avoid refresh flicker and stale running-state UI.
- Reuse established helpers and escaping patterns such as `S`, `esc()`, and the existing render helpers before adding new global state or raw `innerHTML` paths.
- Keep desktop, mobile, and PWA behavior aligned. Responsive or interaction changes should follow `TESTING.md`, and UI-facing changes still need before/after evidence per `CONTRIBUTING.md`.
- If you touch service worker, auth, manifest, or session-prefixed route behavior, preserve the existing auth-sensitive cache rules and installability behavior.
- For markdown or message rendering changes, prefer the existing renderer pipeline and add regression coverage for the exact output contract you are changing.
- For theme or appearance work, stay within the existing CSS variable and locale-aware settings patterns instead of introducing parallel styling systems.