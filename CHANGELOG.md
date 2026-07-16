# Changelog

All notable changes to cowork-os are documented here. Format loosely based on Keep a Changelog; versioning follows SemVer (pre-1.0, so minor versions add features).

## [0.5.0] - 2026-07-16 — The GTM execution layer

0.4.0 gave cowork-os a pipeline; 0.5.0 completes the commercial stack **upstream** of it. The GTM pair is now whole: `gtm-engineering-outbound` designs the outbound system (ICP, signals, messaging, deliverability), and the new **`clay-prospecting`** skill executes it on the **Clay MCP** — so prospecting runs are anchored to the company brain instead of improvised.

### Added
- **`clay-prospecting` skill (cataloged, Yempik standalone).** An operational runbook for running the Clay MCP like a GTM engineer: targeted contact search (domains + title keywords, low per-company limits), async waterfall enrichment with polling, Claygent-style custom research data points, credit discipline, and a hard **warm-path exclusion** rule — people you already know never get enriched or cold-messaged. Context-first: it reads the workspace ICP, decision log and existing lists before spending a single credit, and writes results to files, not chat. Published in [`yempik-skills`](https://github.com/yempik-ai/yempik-skills/tree/main/clay-prospecting).
- **`gtm-engineering-outbound` cataloged** in `skills/README.md` and `capabilities.md` as the strategy layer of the pair (published in [`yempik-skills`](https://github.com/yempik-ai/yempik-skills/tree/main/gtm-engineering-outbound)).

### Changed
- `capabilities.md` mapping: outbound / Clay / Smartlead asks now route to the strategy + execution pair (`gtm-engineering-outbound` → `clay-prospecting`), the latter when the Clay MCP is connected.
- SEO & AI-citation metadata improved across the repo (`AI-CITATION.md`, `CITATION.cff`, `codemeta.json`); new Decision Radar social preview image.
- Plugin manifest and marketplace entry bumped to `0.5.0`.

## [0.4.0] - 2026-07-08 — Decisions stop slipping through the cracks

cowork-os gains the two layers a growing team feels missing first: a **decision lifecycle** fed by your real communication, and a **sales pipeline** layer. Decisions get captured where they actually happen (email, Slack) instead of living in someone's head, and deals stop going cold because you forgot to follow up.

### Added
- **Decision Lifecycle + Decision Radar.** Decisions become status-carrying records (`proposed → active → superseded/expired/rejected`, with owner + review date). A weekly **Decision Radar** (`decision-radar` task, Mon 08:30) surfaces what's active, stale, conflicting, blocking, and the 3 decisions to make this week. New files: `decisions/decision_candidates.md`, `decisions/active_decisions.md`, `decisions/decision_radar.md`.
- **Signals — an ingestion layer.** Daily **signal sweeps** (`daily-signal-sweep-am` 07:30 / `daily-signal-sweep-pm` 18:00) read email + Slack (optional Notion + Google Drive) since a watermark and distill them into structured signals — decisions, commitments, questions, risks, deadlines — promoting real decisions/commitments to candidates. Read-only: captures and flags, never sends. Raw dumps are private and gitignored; only `signals/sync-state.md` (watermarks, no content) is tracked.
- **Pipeline — a sales/CRM layer.** New `pipeline/` module (`rules.md`, `followup_templates.md`, `deal_radar.md`), the `pipeline-deal-radar` task (weekdays 07:15) that reads the CRM + your sales rules for overdue follow-ups and stalled deals and feeds the daily brief, and a bundled **`pipeline-followup`** skill that drafts follow-up emails in your voice from the deal's Gmail thread (draft-only, never sends).
- **Mission template scaffolding:** `missions/_TEMPLATE/` now ships `target_accounts.md`, `people_map.md`, `outreach_assets.md`, `linkedin_queue.md`.
- **Worked example.** `examples/yempik/` gains decision + signal sample data.

### Changed
- **Scheduled tasks: 10 → 14** (added signal sweep AM/PM, decision radar, pipeline deal radar).
- **`founder-daily-brief`** now folds in the pipeline and doc-change lines, so it stays the single morning surface.
- Docs updated: README, `capabilities.md`, `PROJECT_INSTRUCTIONS.md`, `PROJECT_STRUCTURE.md`, `scheduled-tasks/README.md`. `.gitignore` now excludes private signal dumps and runtime `*_run.lock` files.
- Plugin manifest bumped to `0.4.0`; the marketplace entry was realigned from a stale `0.1.1` to `0.4.0`.

## [0.3.0] - 2026-07-07 — Decision-grade strategy on demand

### Added
- **`senior-strategy-architect` skill (bundled).** Turns any vague strategy / plan / GTM / growth / pricing / "what should I do?" ask into decision-grade strategy: diagnosis → strategic choice → coherent plan → metrics → risks. Ships 14 domain playbooks, an intake question bank, a framework library, a research protocol, and an anti-fluff QA rubric. Fires on its own.

### Changed
- `capabilities.md` and `skills/README.md` surface the new bundled skill and when it should trigger.

## [0.2.0] - 2026-07-01 — Build a company brain your team owns

cowork-os grows from "a Cowork workspace with memory" into what it was always for: a **company brain your team owns**, the decisions, context and processes your work runs on, in plain Markdown you can read, correct and govern. Not a memory engine, not a vendor you rent.

### Added
- **Knowledge Transfer skill** and `/cowork-os:knowledge-transfer` command: an objective-first interview that captures the tacit know-how in a person's head (the exceptions, the decision criteria, the unwritten rules) and writes it into the workspace as processes, rules with a source, a glossary and open questions. This is how the company brain gets built from people, not only from files.
- **A real elicitation engine, not a questionnaire.** After a few standard questions it generates each follow-up from your last answer: starts from a real case, pounces on hedge words ("usually", "it depends"), contrasts with a novice, separates the official process from the real one, and reconstructs the workflow for you to correct.
- **Process capture in onboarding.** `/cowork-os:install` now ends by offering to capture your most at-risk process with a bus-factor question ("if your most experienced person were away a week, what breaks first?"). About 15 minutes, skippable, and the brain grows over time.
- **`context/processes/`**, the home for how work actually gets done, with a template.
- **Proactive by default.** The core now offers to turn recurring work into a scheduled routine, and repeatable multi-step jobs into a reusable custom skill, because most users do not know these exist.

### Changed
- **Repositioned to "build a company brain you own":** README, banner, demo GIF, social preview, plugin description and topics.
- Plugin manifest bumped to `0.2.0`.

## [0.1.1] - 2026-06

- Plugin manifest fix and guided installer hardening (stop rule, inline routing, organic-marketing shape, connector checks).

## [0.1.0] - 2026-06

- Initial release: the cowork-os workspace (folder conventions + Memory Update protocol), Project Instructions, the Relentless Outcome Workflow, LinkedIn Growth OS, mission mode, and recurring scheduled routines.
