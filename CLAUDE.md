# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running Locally

Static files — no build step:

```bash
python -m http.server 3000   # then open http://localhost:3000
# or: right-click index.html → "Open with Live Server" in VS Code
```

## Architecture

**`CONTEXT.md` is the authoritative design reference** — read it before modifying any page. It contains CSS variable definitions, exact component patterns, PseInt syntax, and the full rule set.

### Project Structure

```
index.html          → root hub
clase1/             → Módulo 1: Problem Solving (Polya model, flowcharts)
clase2/             → Módulo 2: PseInt pseudocode
clase3/             → Módulo 3: Python (includes Pyodide REPL)
clase4/             → Módulo 4: VS Code
sugerencias.html    → standalone feedback page (Firebase)
```

Each `clase*/claseN.html` is the module hub; lesson pages live alongside it in the same folder.

### Key Constraints

- Every `.html` file is **fully self-contained** — all CSS and JS are inline (`<style>` / `<script>`). No external files.
- No CSS frameworks, no JS libraries (Pyodide in `python-consola.html` is the only CDN dependency).
- All `href`/`src` use **relative paths only**.
- Every page must include the theme toggle with `localStorage` (exact pattern in `CONTEXT.md §4.1`).

### Module 2 (PseInt) Dual-Panel Pattern

`pseint-*.html` pages use a 50/50 grid: left terminal panel + right flowchart panel. Code lines carry `data-target="shape-id"` and shapes carry matching `id` — JavaScript syncs hover highlights between them. When editing these pages, keep `data-target` ↔ `id` pairs in sync.

### Module 3 (Python)

`python-consola.html` loads Pyodide v0.29.3 from jsDelivr — it runs a Python 3 REPL + Matplotlib in WebAssembly. This file is significantly larger than others (~41 KB); its async initialization pattern differs from the rest of the codebase.

### Adding New Pages

- New PseInt lesson → copy any `pseint-*.html`, then add a `.content-card` in `clase2/clase2.html`.
- New Python lesson → copy any `python-*.html`, then add a `.content-card` in `clase3/clase3.html`.
- New module → add to `index.html` hub.
- Always update `README.md` when adding pages.
