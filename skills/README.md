> **EN —** Skills are specialized capabilities Claude can invoke (a LinkedIn editor, a document→spreadsheet extractor, office-file builders…). Most people don't know they exist — this folder catalogs the ones that pair with the kit and is where you keep your own. The installer proposes the relevant ones automatically.
> **IT —** Le skill sono capacità specializzate che Claude può invocare (un editor LinkedIn, un estrattore documenti→Excel, generatori di file Office…). Quasi nessuno sa che esistono — questa cartella cataloga quelle che si abbinano al kit ed è dove tieni le tue. L'installer propone in automatico quelle utili.

---

> **Where the bundled skills live.** The skills that ship with cowork-os (`cowork-os-core`, `knowledge-transfer`, `senior-strategy-architect`, `pipeline-followup`) are inside the plugin at [`plugins/cowork-os/skills/`](../plugins/cowork-os/skills/) and load automatically. **This `skills/` folder is the catalog plus room for your own custom skills**, which is why it is mostly just this README.

## Skills that pair with cowork-os · Skill che si abbinano

These are named so Claude can invoke them precisely. **Most are not bundled in this repo** (the first-party `knowledge-transfer`, `senior-strategy-architect` and `pipeline-followup` skills ship with the kit); the rest are separate Cowork skills. Claude uses whichever are installed; if a useful one is missing, it names it and points you to **Settings → Capabilities**.

| Skill | What it does | Claude reaches for it when |
|---|---|---|
| `senior-strategy-architect` *(bundled)* | Turns any vague strategy/plan/GTM/growth/pricing ask into decision-grade strategy: diagnosis → strategic choice → coherent plan → metrics → risks, with 14 domain playbooks and anti-fluff QA. Fires on its own. | the user wants a *strategy*, not a list of tactics ("fammi una strategia", "growth ideas", "GTM plan", "what should I do?") |
| `gtm-engineering-outbound` *(Yempik standalone)* | Builds and audits GTM engineering outbound systems: ICP, signals, Clay-style list building, AI prospecting, cold email/LinkedIn, deliverability, reply handling, and weekly review. Published in [`yempik-skills`](https://github.com/yempik-ai/yempik-skills/tree/main/gtm-engineering-outbound). | the user wants founder-led outbound, cold email, Clay/Smartlead workflows, ICP signal maps, list enrichment, deliverability, or a repeatable commercial system |
| `clay-prospecting` *(Yempik standalone)* | The **execution layer** under `gtm-engineering-outbound`: an operational runbook for the **Clay MCP** — targeted contact search, async waterfall enrichment, Claygent-style custom research data points, credit discipline, warm-path exclusion, file-based outputs. Reads the workspace (ICP, decision log, existing lists) before spending a credit. Published in [`yempik-skills`](https://github.com/yempik-ai/yempik-skills/tree/main/clay-prospecting). | the user wants to run Clay: enrich contacts/companies, find decision makers, build a prospect list, get verified direct emails via the Clay MCP |
| `knowledge-transfer` *(bundled)* | Interviews a person and builds the company brain (processes, rules with source, glossary) into the workspace. Runs on its own or via `/cowork-os:knowledge-transfer`. | onboarding, a key person leaving, standardizing a process |
| `pipeline-followup` *(bundled)* | Prepares **draft** follow-up emails for CRM deals gone quiet: reads the deal's Gmail thread + `pipeline/rules.md`, writes a Gmail draft in your voice, never sends. On-demand. | "controlla la pipeline e preparami i follow-up", "chi non mi ha risposto?", chasing stalled deals |
| `linkedin-editor` | Turns any asset into ready-to-publish LinkedIn posts (8-step workflow). Also shipped here as a no-install workflow in `../linkedin/editor_workflow.md`. | "esegui l'editor su [asset]" |
| `document-data-extractor` | Pulls receipts / invoices / docs into a clean Excel table. | you want document data tabulated |
| `validation-outreach` | Cold messages that book *discovery* interviews (learning, not selling). | you want to talk to potential customers |
| `verification` | Proves code/work actually works before claiming it's done. | a technical task whose success is checkable |
| `youtube-transcript` | Clean transcript of a YouTube video. | you paste a video link / want its text |
| `docx` · `pptx` · `xlsx` · `pdf` | Build Word / PowerPoint / Excel / PDF deliverables. | a deliverable should be a doc / deck / sheet / PDF |
| `html-presentations` | High-end HTML slide decks with custom diagrams. | you want a designed presentation |
| `technical-decision-memory` | Institutional memory of past technical decisions. | revisiting an architecture/tooling choice |

> **Why not bundled:** third-party skills aren't ours to redistribute, and they evolve on their own. Cataloging + invoking them keeps the kit lightweight and always current.
>
> **Yempik's own skills** (e.g. `gtm-engineering-outbound`, `linkedin-editor`, `verification`) are published as standalone skills in the companion repo **[`yempik-skills`](https://github.com/yempik-ai/yempik-skills)** — cross-link them there rather than copying them here.

## Bring your own · Porta le tue

Keep a custom skill as its own subfolder with a `SKILL.md` inside — for example a folder `my-skill/` containing `SKILL.md`. Then either tell Claude when to use it, or add a row for it in `../capabilities.md` so the installer can propose it too.

> **Rule for Claude:** if a relevant skill is installed, just use it. If it isn't, name it and point the user to where capabilities are managed — never silently skip a capability the user doesn't know exists.
