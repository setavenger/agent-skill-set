# Initiative description format

Initiatives are the **top-level container** in Linear for this workspace: one initiative holds an overarching scope (a customer engagement, a product suite, a long-lived surface area). Projects roll into it over time. They are **not** a closed program with every project listed up front, and they are **not** Goal / Reasoning / Effect tickets at a bigger scale.

Copy the template below into the initiative `description` when calling `save_initiative`. Prefer substance over emptiness — a one-line stub after a richer description was wiped is a regression. Do **not** force the project/issue section set here.

## What an initiative is

| Layer | Name | Example |
|-------|------|---------|
| **Initiative** | Overarching scope being built or sustained | "Run Records", "Acme Nursery Ops", "Billing Suite" |
| **Project** | Feature or delivery effort inside that scope | "Harvest log export", "Subscription digests" |
| **Issue** | One unit of work in one primary repo | "Add harvest CSV endpoint" |

- Name the initiative after the **thing contained** (engagement, suite, surface) — not after a single feature.
- Do **not** require nested initiatives. Flat only unless the user explicitly asks otherwise.
- Adding projects later is expected. Do not treat a missing future project as a planning failure.

## Tone — mission, not milestone plan

The description answers: **what overarching thing is contained and being built here?**

It should orient a new reader (human or agent) so they know whether a new project belongs under this initiative. It should **not**:

- Pretend the full project roster is known
- Require every future feature to be listed before work starts
- Mirror project/issue templates (Goal · Reasoning · Effect · Design · Implementation · …)
- Sound like a sprint plan or a "definition of done" for the whole container

`summary` (Linear field, ≤255 chars) = one-line orientation. `description` = the real substance.

## Preferred sections

Use these headings when they fit. Merge, reorder, or skip with a short note when a section would be empty noise — unlike projects/issues, omitted headings are OK here if the prose still covers the mission.

```md
## Mission

{What this container is for. 1–3 short paragraphs: the overarching thing being built or sustained, in plain language. Not a feature list.}

## Context

{World this lives in: who it serves, what operational or product reality it sits in, why it exists as a separate container. Avoid forcing the words "client" or "product" unless they help.}

## What belongs here

{Kinds of work that belong under this initiative. Boundaries vs adjacent initiatives if useful. Keep loose — examples of themes, not a locked backlog.}

## How this evolves

{Explicit: projects are added on a rolling basis as needs appear (e.g. requested features). Scope is not cleared in advance. Do not rewrite Mission into a closed checklist when a new project lands — add the project and, if useful, a line under Landscape.}

## Landscape

{Optional living snapshot of notable active or recent projects — orientation only, not completion criteria. OK to be incomplete. Or: "See linked projects in Linear."}

## Notes

{Links, stakeholders, contracts, repos at suite level, or N/A. Historical docs welcome. Not a substitute for project-level ADRs.}
```

## Section ideas (pick what helps)

Not mandatory. Use when they add signal:

| Idea | When it helps |
|------|----------------|
| **Mission** | Always — core of the description |
| **Context** | External party, domain jargon, or multi-repo suite needs grounding |
| **What belongs here** | Risk of dumping unrelated work into the wrong initiative |
| **How this evolves** | Agents keep trying to "finish" the initiative by listing all projects |
| **Landscape** | Several projects already exist and readers need a map |
| **Stakeholders / contacts** | Non-obvious owners or external points of contact |
| **Systems at a glance** | Suite spans many repos; one short list, detail stays on projects |
| **Non-goals for the container** | Whole classes of work live elsewhere (another initiative) |
| **History** | Migrated from a mega-project or docs dump; pointer to old material |

## Anti-patterns

- Overwriting a rich description with a one-line summary
- Copying [PROJECT-FORMAT.md](./PROJECT-FORMAT.md) wholesale onto the initiative
- "Goal: complete all projects listed below" + a checklist that must stay exhaustive
- Treating initiative status **Completed** as soon as one project ships (initiative outlives individual features)
- Creating one initiative per feature (that is a **project**)

## Example — long-lived engagement / surface

```md
## Mission

Run Records is the software surface for day-to-day nursery run logging: what was done, where, by whom, and what needs follow-up. This initiative collects that work as it grows — not a single release train.

## Context

Built for a plant-nursery operation that needs reliable records across crews and seasons. Domain language and workflows show up across multiple features; keeping them in one initiative preserves shared context without forcing unrelated suites into the same bucket.

## What belongs here

Features and fixes that advance run logging, related operational records, and the supporting apps/services for this surface. Generic platform work that many suites will share belongs in its own initiative or project, linked from here when needed.

## How this evolves

New projects appear as needs are requested or discovered. There is no requirement to pre-declare every project. When a new feature is large enough to outgrow a single issue (and its sub-issues), add a **project** under this initiative.

## Landscape

See linked projects in Linear. Snapshot when useful; not a closed roadmap.

## Notes

Prior planning notes may live in older docs or the former mega-project description — prefer linked projects + ADRs for active technical truth.
```

## Example — product suite

```md
## Mission

Billing Suite covers how money moves through our apps: invoicing, payments, and the operator tools around them. Individual billing features ship as projects inside this initiative.

## Context

Multiple apps touch billing data. This initiative is the home for that theme so feature projects stay findable without stuffing every billing ticket into one giant project.

## What belongs here

Invoicing, payment capture, billing admin, and billing-specific integrations. Unrelated growth/marketing work stays out.

## How this evolves

Projects are added when a feature is scoped. The initiative does not need a fixed end-state project list.

## Landscape

- Invoice line-item correctness (api-service)
- (add rows as projects appear)

## Notes

Cross-repo contracts live on the relevant **project** as Linear Documents, not on this initiative.
```

## Validation (lightweight)

Before `save_initiative` (create or major rewrite):

1. **Mission** (or equivalent prose) explains the overarching container — not one feature.
2. Description is richer than `summary` alone when prior context exists; do not clobber richer text without user intent.
3. No forced Goal / Reasoning / Effect / Implementation scaffold unless the user asks for it.
4. Evolution is acknowledged: rolling projects, not a pre-cleared checklist.
5. Flat: no parent initiative unless the user explicitly wants nesting.
