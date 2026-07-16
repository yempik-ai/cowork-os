# Capabilities catalog · Catalogo delle capacità

> **EN —** The catalog the installer reasons over. For every module, automation and skill: what it is in plain language, **when to set it up** (triggers from the interview), and what it creates. Claude reads this to *proactively* propose the right setup — because the average user doesn't know these features exist.
> **IT —** Il catalogo su cui ragiona l'installer. Per ogni modulo, automazione e skill: cos'è in parole semplici, **quando attivarlo** (trigger dall'intervista) e cosa crea. Claude legge questo per proporre *in modo proattivo* il setup giusto — perché l'utente medio non sa che queste funzioni esistono.

**How Claude should use this file:** during the interview, match the user's answers to the `Trigger` of each item below. Propose every match in plain language with a one-line *why it fits them*, grouped, and let them deselect. Default to "yes" for anything clearly relevant. Never wait for the user to ask for a capability they don't know exists.

**Two companions:** read **`examples/yempik/`** as the *quality bar* — a complete, real, sanitized workspace showing what "good" looks like. And remember the **`_inbox/`** drop-zone: if the user has unsorted material, have them dump it there and say *"process the inbox"* instead of answering everything by hand.

---

## 1. Core (always set up)

| Capability | What it is (plain language) | Creates |
|---|---|---|
| **Operating context** | The project keeps decisions, open questions, next actions and routines in files you can read and correct, so the workspace compounds week over week. | `context/`, `decisions/`, the **Memory Update** habit in `PROJECT_INSTRUCTIONS.md` |
| **Project Instructions** | The system prompt that makes Claude check sources, separate facts from assumptions, and update memory. | filled `PROJECT_INSTRUCTIONS.md` |
| **Structure guide** | Explains where everything lives so the workspace stays tidy. | `PROJECT_STRUCTURE.md` |

> Always generate these. Everything below is conditional on the interview.

---

## 2. Modules (set up by need)

### `marketing/`
- **What:** strategy, campaigns and content memory — turns data into prioritized actions.
- **Trigger:** the user does any marketing / content / lead-gen.
- **If they run NO paid ads:** generate `strategy.md` in *organic* shape (channels, funnel, referral, content) and keep `campaigns.md` + `monitoraggio/` as **dormant stubs** — don't fill the CPC/budget/RSA scaffolding.
- **Creates:** `marketing/strategy.md`, `marketing/campaigns.md`, `marketing/content.md`, `marketing/monitoraggio/`.

### `website/`
- **What:** a living audit + backlog of the site (copy, SEO, UX, conversion).
- **Trigger:** the user has (or is building) a website.
- **Creates:** `website/website_notes.md`, `website/backlog.md`, `website/homepage_copy.md`.

### 🚩 `linkedin/` — LinkedIn Growth OS
- **What:** a full system to turn know-how into authority and leads on a personal/founder profile — strategy, a content engine (6 formats + hook/CTA banks), a reputation engine, an engagement playbook, and a runnable 8-step editor.
- **Trigger:** the user is the face of the brand / wants to grow a personal or founder profile on LinkedIn.
- **Creates:** the `linkedin/` folder, filled with their angle, pillars and cadence.
- **Pairs with automations:** `trend-hunter-linkedin`, `engagement-radar-daily`, `linkedin-connection-batch`.
- ⚠️ **Rewrite the worked examples.** The engagement playbook, reputation People-Map hints and calendar occasions carry **illustrative examples in the prose** (not just `{{placeholders}}`). For a non-AI / different-domain business, **replace every concrete example with one from the user's domain** (keyword searches, comment voice, the worked comment, role hints). Leaving foreign-domain examples in is a correctness bug.

### 🚩 `missions/` — Relentless Outcome Workflow
- **What:** "mission mode" — for an ambitious goal Claude pursues an *outcome*, not a task (route maps, evidence logs, stop conditions). E.g. landing a partnership, breaking into named accounts.
- **Trigger:** the user names a big, hard goal (a partnership, a dream client, an ecosystem to break into).
- **Creates:** a `missions/<slug>/` from the template + `workflows/relentless_outcome_workflow.md`.
- **Pairs with:** `mission-weekly-review`.

### `products/`
- **What:** a separate workstream per owned product (roadmap, validation, GTM), kept apart from marketing memory.
- **Trigger:** the user has one or more of their own products (not just client work).
- **Creates:** a `products/<name>/` from the template.

### 🚩 `pipeline/` — CRM / sales layer (Pipedrive & co.)
- **What:** the sales layer for anyone who runs a deal pipeline in a CRM. Captures their **sales rules** (real stages, what "stuck" means, no-reply threshold, priority criteria), holds **follow-up templates** in their voice, and produces a **deal radar** (overdue follow-ups, stalled deals, hygiene). The radar **feeds the daily brief** so the person reads one surface, not a separate CRM screen.
- **Trigger:** the user manages deals/opportunities in a CRM (Pipedrive, HubSpot…), does outbound/inbound sales, says "deals go cold and I forget to follow up", or wants an assistant on their pipeline.
- **Set up via Knowledge Transfer.** Don't invent the rules: run a focused `knowledge-transfer` session on the sales-follow-up process, looking at the real pipeline, then write `pipeline/rules.md`. The automations read that file.
- **Creates:** `pipeline/rules.md`, `pipeline/deal_radar.md`, `pipeline/followup_templates.md`.
- **Pairs with:** the `pipeline-deal-radar` scheduled task (feeds the brief) + the on-demand `pipeline-followup` skill (drafts follow-ups). Both draft-only / read-only on the CRM.
- **Needs:** a CRM connector (read) — e.g. the Pipedrive MCP — and Gmail (read + drafts) for the follow-up skill. If the CRM isn't connected, the radar flags it and skips, without failing.

### 🚩 Knowledge Transfer, build the company brain from a person
- **What:** a guided, objective-first interview that captures what a person knows (exceptions, decision criteria, unwritten rules) and writes it into the workspace as processes, rules with a source, a glossary and open questions. This is how the company brain gets built from people, not only from files.
- **Trigger:** onboarding a new hire, a key person leaving or retiring, knowledge stuck in one head ("only Marco knows how"), or standardizing how a task is done.
- **Runs by itself** when the user describes that pain, or on demand via `/cowork-os:knowledge-transfer`.
- **Creates:** `context/processes/<process>.md`, updates to `decisions/decisions_log.md` (rules with source), `context/glossary.md`, `decisions/open_questions.md`.

### 🚩 Decision Lifecycle + Decision Radar
- **What:** stops the team from re-deciding and contradicting itself. Decisions become status-carrying records (`proposed → active → superseded/expired/rejected`, with owner + review date), fed by a daily **signal sweep** that reads email/Slack and captures the decisions/commitments made there. A weekly **Decision Radar** surfaces what's active, stale, conflicting, blocking, and the 3 decisions to make this week.
- **Trigger:** a **team (2+ people)** whose decisions scatter across channels — Slack/email/calls/heads — and who ask "wait, did we decide X or Y?"; small team with no PMO/chief-of-staff. For a **solo founder** the full lifecycle is usually overkill: offer a lighter "this week's 3 decisions to make / remember" instead. Note: the signal sweep reads **email + Slack** — if the team decides mostly on WhatsApp/calls/other channels, say so up front (don't imply full coverage).
- **Runs by itself** via the `daily-signal-sweep-am/pm` and `decision-radar` scheduled tasks; the lifecycle rule lives in `PROJECT_INSTRUCTIONS.md`.
- **Creates:** `decisions/decision_candidates.md`, `decisions/active_decisions.md`, `decisions/decision_radar.md`, the `signals/` folder (email/Slack/Notion/Drive ingestion, private/gitignored).
- **Needs:** email connector (read) + Slack connector (read) — both are full read sources. **Optional:** Notion (read) + Google Drive (read) add doc-change detection (the sweep flags edited pages/files in the pages/folders you tell it to watch, surfaced in the brief). If a connector isn't connected yet, the sweep skips it and flags it, without failing.

---

## 3. Scheduled automations (recurring — explain, then offer to set up)

> Most users don't know Claude can run on a schedule. Explain it simply: *"I can run this automatically every week and leave you a brief — want me to?"* Set up only the ones that match, with the suggested cadence (adjustable). Prompts live in `scheduled-tasks/`.

| Automation | Plain-language pitch | Trigger | Suggested cadence |
|---|---|---|---|
| **weekly-marketing-pulse** | A Monday brief on what your marketing did and the week's priorities. | does marketing | Mon 08:00 (`0 8 * * 1`) |
| **campaign-conversion-review** | Mid-week check on ad spend, conversions and what to fix. | runs paid ads | Wed 09:00 (`0 9 * * 3`) |
| **website-content-review** | Weekly look at site + content opportunities. | has a site/content | Fri 09:00 (`0 9 * * 5`) |
| **workspace-maintenance** | Keeps the knowledge base clean: de-dupes, resolves stale questions. | everyone | 1st & 15th 15:00 (`0 15 1,15 * *`) |
| **trend-hunter-linkedin** | Finds on-topic trends to post about, filtered to your category. | uses LinkedIn OS | Mon & Thu 07:30 (`30 7 * * 1,4`) |
| **engagement-radar-daily** | A daily list of in-target posts to comment on, in your voice (drafts only). | wants LinkedIn engagement | Mon–Fri 08:00 (`0 8 * * 1-5`) |
| **mission-weekly-review** | Weekly status + next routes for an active mission. | has a mission | Mon 08:30 (`30 8 * * 1`) |
| **linkedin-connection-batch** | Sends the queued, pre-approved connection requests. | does LinkedIn outreach | weekdays (`0 10 * * 1-5`) |
| **founder-weekly-review** | A Monday founder review across your CRM + workspace. | founder wants a weekly OS review | Mon 09:00 (`0 9 * * 1`) |
| **founder-daily-brief** | A short morning chief-of-staff brief: agenda + inbox/leads + pipeline + doc-changes + mission urgencies (read-only). | founder/salesperson wants a daily brief | weekdays 07:30 (`30 7 * * 1-5`) |
| **pipeline-deal-radar** | Reads the CRM + your sales rules → overdue follow-ups, stalled deals, hygiene. Feeds the daily brief (read-only on the CRM). | manages deals in a CRM (Pipedrive…) | weekdays 07:15 (`15 7 * * 1-5`) |
| **daily-signal-sweep-am** | Morning: reads email + Slack (+ optional Notion/Drive) since the watermark → signals → decision candidates (read-only). | decisions live in email/Slack; docs in Notion/Drive | weekdays 07:30 (`30 7 * * 1-5`) |
| **daily-signal-sweep-pm** | End-of-day: captures the decisions/commitments you made today (sent mail + your Slack) before they're forgotten. | same, capture-focused | weekdays 18:00 (`0 18 * * 1-5`) |
| **decision-radar** | Weekly decision governance: active / stale / conflicting / blocking + the 3 to decide this week. | team re-decides / contradicts itself | Mon 08:30 (`30 8 * * 1`) |

**Safety:** automations that touch the outside world **draft or propose** — with **one exception**: `linkedin-connection-batch` *sends* connection requests, but only from a queue you pre-approved (never pitch DMs, never emails). Everything else (comments, DMs, emails) is draft-only. Say this out loud when proposing them.

**Connector check:** several routines only pay off if a connector is linked — `weekly-marketing-pulse` / `campaign-conversion-review` need analytics/ads; the LinkedIn routines need Chrome; `founder-weekly-review` and `pipeline-deal-radar` need a CRM (e.g. Pipedrive); `founder-daily-brief` needs calendar/email (and, for its Pipeline line, the CRM). **Only propose a routine whose connector is actually connected** — otherwise offer to connect it, or a lighter alternative, rather than scheduling a run that comes back empty.

---

## 4. Skills (use if available; recommend if not)

> Skills are specialized capabilities Claude can invoke. The average user doesn't know they exist — surface them when relevant.

- **Built-in strategy skill (bundled):** `senior-strategy-architect` turns any vague strategy / plan / GTM / growth / pricing / "what should I do?" ask into decision-grade strategy — diagnosis → strategic choice → operating plan → metrics → risks, with 14 domain playbooks and an anti-fluff QA pass. Ships with the kit and fires on its own; use it whenever the user wants a *strategy*, not a list of tactics.
- **This kit's built-in "editor":** `linkedin/editor_workflow.md` works like a runnable LinkedIn editor ("esegui l'editor su [asset]") with no install. Mention it whenever the user wants to produce posts.
- **Bundled sales skill:** `pipeline-followup` prepares **draft** follow-up emails for CRM deals gone quiet — reads the deal's Gmail thread + `pipeline/rules.md`, writes a Gmail draft in the person's voice, never sends. On-demand ("controlla la pipeline e preparami i follow-up"). Pairs with the `pipeline/` module + `pipeline-deal-radar`.
- **Named skills the user may already have** (use them if installed, otherwise tell the user they exist — see `skills/README.md`):
  - `gtm-engineering-outbound` → ICP, signal maps, Clay-style list building, AI prospecting, cold email/LinkedIn, deliverability, reply handling, and weekly GTM review;
  - `clay-prospecting` → running the Clay MCP like a GTM engineer: targeted contact search, async enrichment, custom research data points, credit discipline, warm-path exclusion (the execution layer under `gtm-engineering-outbound`);
  - `document-data-extractor` → turning documents / invoices / receipts into a spreadsheet;
  - `validation-outreach` → cold messages to book discovery interviews;
  - `verification` → proving a technical task actually works before calling it done;
  - `youtube-transcript` → a YouTube link or a transcript request;
  - office builders `docx` / `pptx` / `xlsx` / `pdf` (and `html-presentations`) → a deliverable that should be a doc, deck, sheet or PDF;
  - `technical-decision-memory` → revisiting an architecture/tooling choice.
- **Rule:** if a relevant skill is installed, just use it. If it isn't, name it and point the user to where capabilities/plugins are managed — don't silently skip it.
- **Folder:** [`skills/README.md`](./skills/README.md) catalogs the skills that pair with cowork-os and is where the user keeps their own custom skills.

---

## 5. Mapping cheat-sheet (interview answer → propose)

- *"I'm the founder / the face of the brand"* → LinkedIn Growth OS + trend-hunter + engagement-radar.
- *"I run ads" (analytics/ads connected)* → marketing/ + weekly-marketing-pulse + campaign-conversion-review. *Organic-only* → marketing/ in organic shape + a lighter LinkedIn/content pulse; skip the ads routines.
- *"I have a website"* → website/ + website-content-review.
- *"I have my own product(s)"* → products/.
- *"I manage deals in a CRM / Pipedrive" / "deals go cold and I forget to follow up" / "I want an assistant on my pipeline"* → `pipeline/` + `pipeline-deal-radar` (feeds the daily brief) + the `pipeline-followup` skill. Set the rules via a focused `knowledge-transfer` session on the sales process — don't invent thresholds. Needs a CRM connector (read) + Gmail (drafts). **For a solo salesperson, don't stack three morning routines:** the `founder-daily-brief` already regenerates the pipeline inline from `pipeline/rules.md`, so scheduling *just the brief* is usually enough — add the standalone `pipeline-deal-radar` only if they want the fuller radar artifact or have heavy/multiple pipelines. And check first which channel their deals actually live in: if follow-ups happen mostly on WhatsApp/phone, say up front the skill (Gmail-only) can't see those — don't imply full coverage.
- *"I live in Google + Notion" / "tell me if a doc changed"* → founder-daily-brief + the signal sweep with Notion/Drive change-detection (tell it which pages/folders to watch).
- *"I want to land [big partner / dream client]"* → missions/ + mission-weekly-review.
- *"I do outbound / cold email / AI prospecting" / "I use Clay or Smartlead" / "I need ICP signals or deliverability"* → the `gtm-engineering-outbound` skill (strategy) + the `clay-prospecting` skill when the Clay MCP is connected (execution: enrichment runs, prospect lists, verified emails).
- *"I do outreach for discovery interviews"* → linkedin-connection-batch and/or the validation-outreach skill.
- *"I want a morning brief / a chief-of-staff"* → founder-daily-brief.
- *"I have a pile of unsorted material"* → the `_inbox/` intake flow ("process the inbox").
- *"Someone key is leaving" / "onboarding is slow" / "only one person knows how to do X"* → the **knowledge-transfer** interview (`/cowork-os:knowledge-transfer`).
- *"Give me a strategy / GTM / growth / pricing plan" / "what should I do?"* → the **senior-strategy-architect** skill (diagnosis-first, explicit trade-offs, operating plan with metrics and risks).
- *"We keep re-deciding / forgetting what we decided" / "decisions are all in email and Slack"* → Decision Lifecycle: `daily-signal-sweep-am/pm` + `decision-radar` (needs email read, ideally Slack read).
- *Always* → Core + workspace-maintenance + the Memory Update habit.
