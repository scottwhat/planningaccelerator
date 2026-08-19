# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this directory is

- `meconebrainmastermind (1).md` — the original strategy spec this tool is derived from: a
  proposed stage-aware intelligence engine covering the entire property development lifecycle
  (site identification through delivery/completion). It defines a lifecycle state machine
  (Stage 0–7), a buy-in matrix of stakeholders to engage at each stage, and a playbook library of
  codified strategic plays. It is the source of truth for the *content* in the proof-of-concept
  site below (stage intelligence, buy-in matrix, playbooks, worked example) — when the spec
  changes, the corresponding data array in `docs/index.html` should be updated to match. The site
  itself is deliberately de-branded from the spec's "Mecone Brain" framing into a generic,
  firm-agnostic tool — do not reintroduce "Mecone" or "the Brain" as product names in the UI or
  generated documents; use "the firm" / "internal" phrasing instead so any consultancy could use it.
- `docs/index.html` — a single-file, no-build proof-of-concept web app: the **Planning Development
  Accelerator**. It lives in `docs/` (rather than `site/`) so it can be served directly by GitHub
  Pages with no build step — Pages is configured to deploy from the `main` branch's `/docs` folder.
  It lets a planning consultant create a project, step it through Stages 0–7 via a horizontal
  timeline strip under the project filebar, and at each stage see tracked signals, insights,
  who-to-consult list, and a codified play in the stage dossier. Below the dossier, Key people &
  alignment, Feasibility watch, the buy-in matrix, and the playbook library (§4.1–4.5 of the spec)
  flow into an evenly split two-column grid. A value-proposition strip under the masthead states
  what the tool delivers in one line. It also includes:
  - A **Project intelligence** section (spec §2–3): key people on file (local MP, DPHI/DCA case
    officer, council assessment officer, panel chair — name + notes, freeform per project),
    strategic alignment tags (which state targets the file is positioned against), and a
    feasibility watch checklist with a computed Feasible/Watch/At risk status plus freeform
    kill-criteria notes.
  - An **AI insights** popup — explicitly a non-functional placeholder (labelled "Placeholder ·
    not connected", input disabled to submit), opened via a masthead button rather than sitting
    inline on the page. It shows example prompts (e.g. "My project is blocked by DPHI — an RFI
    has gone quiet for three weeks. What can I do?"); clicking one fills the textarea to
    demonstrate the intended UX. Do not wire this up to a real model unless the user explicitly
    asks — it exists to communicate a future direction, not to be built out speculatively.
  - A document generator (modal with Copy / Download .txt): a strategy memo per stage that folds
    in key people, alignment, and feasibility status; a play brief per playbook; and a stakeholder
    courtesy-briefing letter per buy-in actor (pulls in the matching contact from Key people when
    one is on file). None of the generated documents are firm-branded — keep them generic.
  - A "Load worked example" action that seeds the Chatswood worked example from §6, including its
    people, alignment, and feasibility.
- `pitch-deck-brief.md` — source material for a two-slide pitch deck (intro slide + architecture/
  AI-pipeline diagram slide) covering this tool. Update it if the tool's capabilities or the AI
  roadmap framing change materially; it's a content brief, not app documentation.

There is no package manifest, build system, linter, or test suite. `docs/index.html` has no
dependencies beyond two Google Fonts stylesheets loaded via `<link>` — open it directly in a
browser, or serve it locally with e.g. `python3 -m http.server` from `docs/`. There is nothing to
build, lint, or test. The repo is published at https://github.com/scottwhat/planningaccelerator
and served live via GitHub Pages at https://scottwhat.github.io/planningaccelerator/ — pushing to
`main` redeploys the live page automatically.

## Architecture of `docs/index.html`

Everything lives in one file: inline `<style>`, inline `<script>`, no external JS/CSS besides
fonts. State model, defined at the top of the script:

- `STAGES` — array of 8 stage objects (spec §2), each with `tracks`, `insights`, `who`, `play`,
  and optional `lessons` fields.
- `BUYIN` — array of stakeholder rows (spec §3: actor, stage(s), what-you-want, what-they-want).
- `PLAYBOOKS` — array of the 5 codified plays (spec §4.1–4.5); each has a `type`
  (`ordered`/`unordered`/`prose`), a `lead` paragraph, and `items` (`{label, text}`) — this same
  structure drives both the on-page accordion and the generated play-brief text, so there's one
  source per play, not two.
- `ROLE_DEFS` / `ALIGNMENT_TAGS` / `FEASIBILITY_CHECKS` — the fixed field lists behind the Project
  intelligence panel (key-people roles, strategic alignment tags, kill-criteria checklist items).
- `AI_EXAMPLES` — the placeholder prompt strings shown in the AI insights panel (display only).
- `CHATSWOOD_EXAMPLE` — pre-filled project data mirroring the worked example (spec §6), including
  people/alignment/feasibility, used by "Load worked example."

Runtime project data (name/client/site/council, current stage pointer, buy-in checkboxes,
key people, strategic alignment, feasibility checklist + notes) is kept in a `projects` array and
persisted to `localStorage` under `planning-development-accelerator-v3` — there is no backend.
Multiple projects can exist side by side; switching projects re-renders the stage detail, buy-in
matrix, and intelligence panels from that project's saved state. `newProject()` is the single place
that initialises every field (including from a seed like `CHATSWOOD_EXAMPLE`) — extend it when
adding a new persisted field so both blank and seeded projects stay consistent.

## Working in this repository

- Treat requests to edit the spec markdown as document authoring, not software engineering.
- Treat requests to change the mapper as normal frontend work on `docs/index.html` — keep it a
  single dependency-free file unless the user asks for a real build setup.
- If a change adds a new stage field, buy-in row, or playbook, update both the spec markdown and
  the corresponding data array in `docs/index.html` so they stay in sync.
- This is a real git repository with a GitHub remote (`origin` → scottwhat/planningaccelerator).
  Follow the standard git safety rules: only commit/push when asked, never force-push without
  explicit confirmation, and don't rewrite published history.
