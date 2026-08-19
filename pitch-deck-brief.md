# Pitch Deck Brief — Planning Development Accelerator

This is a content brief for a two-slide pitch deck section. Use it to generate:

- **Slide 1** — an introduction slide: what the tool is and what it does.
- **Slide 2** — an architecture/diagram slide: core components plus the AI pipeline (data
  ingested → processed → insights delivered).

Treat the text below as source material, not final slide copy — tighten, cut, and re-word for
slide density. Keep the tool itself unbranded (no vendor/product name beyond "Planning
Development Accelerator" and "the firm") — it's designed to be pitched as a firm-agnostic
capability, not a named commercial product.

---

## Slide 1 — Introduction

**Working title:** Planning Development Accelerator — stage-aware intelligence for every live
planning file

**One-line pitch:**
Map any planning approval to its lifecycle stage, know exactly who to bring in and when, track
feasibility as it happens, and generate the strategy notes and letters to back it up.

**The problem it solves:**
Property development approvals move through a long, high-stakes lifecycle — from site
identification through delivery and completion — and the knowledge needed to navigate each stage
well (who to engage, what signals matter, which plays work) usually lives in individual planners'
heads, scattered notes, and hard-won experience that isn't captured or reused. Firms re-learn the
same lessons project to project and file to file.

**What it does, in four capabilities:**

1. **Stage-by-stage intelligence** — an 8-stage lifecycle model (Stage 0–7, site identification
   through delivery/completion). At every stage, the tool surfaces the signals to track, the
   insights those signals produce, who to consult and when, and a codified strategic play for
   that moment in the file's life.
2. **Stakeholder sequencing** — a buy-in matrix mapping every stakeholder (client board, council
   planners, DA staff, councillors, state agencies, the local MP, the minister's office,
   community, media, future occupants) against the stage they matter at, what the firm wants from
   them, and what they want in return — with per-project engagement tracking.
3. **Feasibility & risk tracking** — a live kill-criteria checklist producing a computed
   Feasible / Watch / At-risk status, plus a record of key people on file (local MP, DPHI/DCA
   case officer, council assessment officer, panel chair) and strategic alignment against the
   state's own published targets (housing targets, TOD/precinct uplift, affordable housing,
   priority pathways).
4. **Auto-drafted strategy documents** — one click generates a stage strategy memo, a play brief
   for any codified playbook, or a stakeholder courtesy-briefing letter, pre-filled from the
   project's own data (people, alignment, feasibility status).

**The playbook library** — five codified, reusable plays sit behind the tool (e.g. *getting a
council to commit road upgrades*, *media & narrative campaigns*, *pressuring government to
support its own strategy*, *precedent farming*, *the coalition play*). Each is a named, structured
sequence — not folklore — that fires automatically when relevant to the stage being viewed.

**Positioning line for the slide footer:**
*Recommendations only — humans decide. Strategy analysis, not legal or financial advice.*

---

## Slide 2 — Core Components & AI Pipeline

**Slide goal:** one diagram showing (a) the core components of the tool today, and (b) the AI
pipeline layered on top — what data it would ingest, how it processes it, and what insights it
returns into the same components. Frame the AI layer explicitly as the **next stage of the
roadmap**: the current build ships a placeholder AI insights panel (clearly labelled
"Placeholder · not connected") that demonstrates the intended UX without being wired to a live
model — the diagram should represent the vision this placeholder points to, not a shipped
feature.

### Suggested diagram structure

Three horizontal bands, left to right: **Data ingested → AI processing → Insights delivered**,
with the processed insights flowing down into the core product components (which persist the
outcome per project).

```mermaid
flowchart LR
    subgraph ING["Data ingested"]
        direction TB
        I1["Project file data\n(people, alignment tags,\nfeasibility checklist)"]
        I2["Stage signals\n(amalgamation patterns, SPV\nregistrations, referral status,\nRFI timing, objection themes)"]
        I3["External planning records\n(council DA registers, panel\ndecisions, SEARs, precedent\napprovals, conditions imposed)"]
        I4["Stakeholder & political context\n(buy-in engagement log, MP /\nminister priorities, election\ncalendar, media coverage)"]
    end

    subgraph PROC["AI processing"]
        direction TB
        P1["Entity resolution &\npattern detection"]
        P2["Benchmarking against\nauthority's own record\n(RFI medians, condition\nlibrary, refusal rates)"]
        P3["Pathway & probability\nmodelling\n(CDC / DA / panel / HDA-SSD)"]
        P4["Playbook matching\nengine\n(stage + condition → play)"]
    end

    subgraph OUT["Insights delivered"]
        direction TB
        O1["Ranked leads &\nkill-criteria verdicts"]
        O2["Escalation triggers\n(\"agency X is 9 days past\nits own average\")"]
        O3["Stage-relevant playbook\nrecommendations"]
        O4["Auto-drafted memos,\nplay briefs & stakeholder\nletters"]
    end

    ING --> PROC --> OUT

    OUT --> CORE

    subgraph CORE["Core product components (today)"]
        direction LR
        C1["Stage dossier\n(Stage 0–7)"]
        C2["Buy-in matrix"]
        C3["Feasibility watch"]
        C4["Playbook library"]
        C5["Document generator"]
    end
```

### Component notes (for labelling the diagram / speaker notes)

**Core components (built today):**

| Component | What it holds |
|---|---|
| Stage dossier | The 8-stage lifecycle model; per-stage signals tracked, insights out, who to consult, the codified play |
| Buy-in matrix | 10 stakeholder rows × stage relevance × what-you-want / what-they-want × engagement status |
| Project intelligence | Key people on file, strategic alignment tags, feasibility kill-criteria + computed status |
| Playbook library | 5 codified plays (§4.1–4.5), each a structured, reusable sequence, auto-surfaced by stage |
| Document generator | Stage strategy memos, play briefs, and stakeholder courtesy letters, pre-filled from project data |

**AI pipeline (roadmap, represented today only as a placeholder panel):**

| Stage | What happens |
|---|---|
| Ingest | Project file data the firm has already entered, plus stage signals and — longer-term — external planning records (council registers, panel decisions, precedent approvals) and political/stakeholder context |
| Process | Entity resolution, benchmarking against the relevant authority's own historical behaviour, pathway/probability modelling, and matching live conditions to the right codified playbook |
| Deliver | Ranked leads, kill-criteria verdicts, escalation triggers, stage-relevant play recommendations, and drafted documents — surfaced back into the same panels a planner already works in, not a separate tool |

**Key framing for the deck:** the AI layer doesn't introduce a new interface — it makes the
existing stage dossier, buy-in matrix, feasibility watch, and document generator smarter and more
automatic, using the same categories of data the tool already asks a planner to capture by hand.
