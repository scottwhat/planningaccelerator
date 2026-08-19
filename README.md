# Planning Development Accelerator

A single-file, no-build proof-of-concept web app that maps any planning approval to its lifecycle
stage (Stage 0–7), tracks who to engage and when, watches feasibility as it happens, and
auto-drafts the strategy notes and letters to back it up.

**Live app:** https://scottwhat.github.io/planningaccelerator/

## What's in this repo

- `index.html` — the app itself. Served directly by GitHub Pages (Pages is configured to
  deploy from the `main` branch's root) — there is no build step.
- `meconebrainmastermind (1).md` — the original strategy spec the tool's content is derived from
  (lifecycle stages, buy-in matrix, playbook library, worked example).
- `pitch-deck-brief.md` — source material for a two-slide pitch deck introducing the tool and its
  architecture / AI-pipeline roadmap.
- `CLAUDE.md` — guidance for working on this repo with Claude Code.

## Running it locally

No dependencies beyond two Google Fonts stylesheets. Either open `index.html` directly in a
browser, or serve it locally:

```
python3 -m http.server
```

Then visit `http://localhost:8000`.
