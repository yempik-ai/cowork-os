> **EN —** How the knowledge base is organized and how to keep it tidy. Read this before adding files. The golden rule: don't duplicate; pick the most specific file.
> **IT —** Come è organizzata la knowledge base e come tenerla in ordine. Leggilo prima di aggiungere file. Regola d'oro: non duplicare; scegli il file più specifico.

---

# Project Structure

Quando lavori, usa questa struttura per leggere e aggiornare le informazioni.

Non duplicare contenuti tra file diversi. Se un'informazione potrebbe stare in più posti, scegli il file più specifico. Se non sei sicuro, aggiungila prima in `decisions/open_questions.md` o segnala il dubbio.

> **Questo file è il MANIFESTO dei moduli del workspace.** Le cartelle qui sotto sono un punto di partenza, non un elenco chiuso: il workspace **evolve** e può avere moduli che qui non compaiono. Due conseguenze operative:
> 1. **Crea moduli su bisogno.** Se il dominio richiede un modulo che non esiste (es. un'agenzia → `clients/`), crealo (vedi *Come aggiungere un modulo* in fondo) e **aggiungi la sua voce qui**.
> 2. **Le routine scoprono la struttura, non la assumono.** Manutenzione, review, audit e brief leggono le cartelle reali e/o questo manifesto: nessun percorso hardcodato. Tieni quindi questo file **in sync** a ogni aggiunta/rinomina/rimozione di un modulo.

---

## Root

- `PROJECT_INSTRUCTIONS.md` — il system prompt del Project (tono, obiettivi, vincoli, Memory Update). In Cowork vive nelle istruzioni del progetto; qui lo teniamo come file versionabile.
- `PROJECT_STRUCTURE.md` — questo file. Aggiornalo solo quando aggiungi, rimuovi o rinomini cartelle.
- `cowork.config.example.md` — glossario dei placeholder.

## `context/`

Informazioni fondamentali e relativamente stabili.

- `overview.md` — descrizione generale, cosa fa l'azienda, visione, mercato, stato attuale. Non usarlo per task temporanei o note settimanali.
- `positioning.md` — posizionamento, proposta di valore, messaggi chiave, differenziazione, categorie di mercato, problemi risolti.
- `services.md` — servizi offerti, descrizione, priorità, pacchetti, use case.
- `tone_of_voice.md` — tono di voce, parole da usare/evitare, esempi di copy buono e da evitare.
- `processes/` — come si eseguono **davvero** i processi operativi (uno per file), catturati con la skill `knowledge-transfer`: passi reali, punti di decisione, eccezioni, regole non scritte. È il **layer operativo** del company brain (il "come si lavora", non solo il "chi siamo"). Le regole estratte vanno anche in `decisions/decisions_log.md` con la fonte-intervista. `_TEMPLATE.md` è lo stampo.

## `marketing/`

Strategia, campagne, contenuti e insight.

- `strategy.md` — strategia generale, obiettivi trimestrali, canali prioritari, funnel, ICP/segmenti, roadmap marketing.
- `campaigns.md` — campagne attive/passate. Ogni campagna: nome, periodo, canale, obiettivo, dati principali, insight, prossime azioni.
- `content.md` — piano contenuti, idee, temi editoriali, calendario, angoli comunicativi.
- `monitoraggio/` — report di monitoraggio campagna datati (`monitoraggio_adv_YYYY-MM-DD.md`).

## `website/`

- `website_notes.md` — struttura del sito, pagine, osservazioni su copy/UX/SEO/conversione, note sulla repo.
- `backlog.md` — task concreti sul sito. Ogni task: titolo, priorità (Alta/Media/Bassa), area (Copy/SEO/UX/Conversione/Tecnico), descrizione, motivo, criterio di completamento, stato.
- `homepage_copy.md` — copy definitivo della homepage.

## `decisions/`

Il **Decision Lifecycle**: le decisioni hanno uno stato, non sono solo righe di log (vedi la sezione omonima in `PROJECT_INSTRUCTIONS.md`).

- `decision_candidates.md` — inbox delle decisioni: proposte rilevate (spesso dai `signals/`) in stato `proposed`, in attesa di conferma umana. Non autorevoli finché non confermate.
- `active_decisions.md` — vista viva: solo le decisioni `active` che guidano il lavoro oggi (owner + review date).
- `decisions_log.md` — storico completo, con motivazione e data. Non cancellare decisioni storiche.
- `decision_radar.md` — output settimanale generato dal task `decision-radar` (attive / da rivedere / conflitti / bloccanti / 3 da decidere). Sovrascritto a ogni run.
- `open_questions.md` — domande aperte, ipotesi da validare, bloccanti. Quando una domanda si chiude, registra la decisione in `decisions_log.md` e marca la voce come risolta (non eliminarla).

## `signals/`

Layer di **ingestione**: gli sweep (`daily-signal-sweep-am/pm`) leggono email, Slack e — se collegati — Notion e Google Drive (change-detection sui doc osservati), e li distillano in signal strutturati che alimentano i `decision_candidates`. `sync-state.md` tiene il watermark per fonte (idempotenza). **`email/`, `slack/`, `notion/` e `drive/` contengono contenuti privati e sono in `.gitignore`: mai committati.** Vedi `signals/README.md`.

## `reviews/`

Review operative ricorrenti, una per file datato:
- `weekly_review_YYYY-MM-DD.md` — pulse settimanale (dati + azioni).
- `maintenance_review_YYYY-MM-DD.md` — manutenzione della knowledge base.
- `founder-brief/brief_YYYY-MM-DD.md` — brief giornaliero del founder (routine `founder-daily-brief`).

I file `*.TEMPLATE.md` sono gli stampi da copiare.

## `workflows/`

Workflow trasversali — metodi che l'agente **esegue**, non cartelle da riempire: il **Relentless Outcome Workflow** (`workflows/relentless_outcome_workflow.md`, per le missioni) e il **Verification Gate** (`workflows/verification_gate.md`, la Definition of Done che verifica un deliverable prima del Memory Update). Il Verification Gate è opt-in: si attiva in setup.

## `missions/`

Missioni ambiziose gestite col **Relentless Outcome Workflow** (`workflows/relentless_outcome_workflow.md`): perseguono un *outcome*, non un task. Una sottocartella per missione; `_TEMPLATE/` è lo stampo.

## `products/`

Un workstream per ogni **prodotto proprio** con vita propria (roadmap, validazione, GTM), separato dalla memory marketing. `_TEMPLATE/` è lo stampo. Il codice dei prodotti vive nei rispettivi repo, non qui.

## `pipeline/`

Il **layer commerciale** per chi lavora su un CRM (es. Pipedrive). Contiene le **regole di vendita** catturate dalla persona (stadi reali, cosa è "fermo", soglia di silenzio prima di un follow-up), i **template di follow-up** nella sua voce, e l'**output del deal radar**. Alimenta la sezione "Pipeline" del `founder-daily-brief` così la persona legge una sola superficie. Le regole sono generate con la `knowledge-transfer` skill sul processo di vendita; le automazioni (`pipeline-deal-radar` + skill `pipeline-followup`) leggono questi file, non hardcodano nulla. Il CRM resta la fonte di verità sullo stato dei deal: qui vivono le *regole* e gli *output*, non una copia della pipeline.

- `rules.md` — regole del processo di vendita (stadi, definizione di "fermo", soglia no-reply, campi usati, criteri di priorità). Fonte: intervista KT.
- `deal_radar.md` — output rigenerato dal task `pipeline-deal-radar` (scaduti / fermi / da sistemare). Sovrascritto a ogni run.
- `followup_templates.md` — template di follow-up nella voce della persona, per tipo di situazione.

## `linkedin/`

Il **LinkedIn Growth OS**: distribuire il know-how in autorevolezza, conversazioni di qualità e opportunità commerciali. Profilo personale come motore. Vedi `linkedin/README.md`.

## `scheduled-tasks/`

Template dei task ricorrenti — "routine" (pulse, review, manutenzione, trend hunter, engagement radar, review missioni, brief founder…) + guida per ricrearli in Cowork. Vedi `scheduled-tasks/README.md`.

## `skills/`

Catalogo delle skill che si abbinano al kit (es. l'editor LinkedIn) + spazio per le tue (una sottocartella con `SKILL.md`). Vedi `skills/README.md`.

## `_inbox/`

Zona di scarico per materiale non ordinato. Butta qui file/note/export e di' *"processa l'inbox"*: Claude estrae i fatti e li archivia nei moduli giusti, in modo non distruttivo. Vedi `_inbox/README.md`.

## `examples/`

Un workspace reale, completo e **sanitizzato** (`examples/yempik/`): è lo *showcase* e il riferimento *few-shot* che l'installer usa come asticella di qualità. Non è il kit da compilare (quello è la root) — è la "soluzione".

---

## Convenzioni generali

- **Naming cartelle**: kebab-case.
- **File datati**: `nome_YYYY-MM-DD.md`.
- **Niente dati privati** nei file versionati pubblicamente: usa `{{placeholder}}` e tieni i contenuti reali fuori dal repo (vedi `.gitignore`).
- **Separare sempre** fatti, ipotesi e raccomandazioni.

## Come aggiungere un modulo

Quando un bisogno reale non ha casa in una cartella esistente, creane una nuova invece di forzarlo altrove:

1. **Cartella** kebab-case con nome chiaro (es. `clients/`, `menu/`, `events/`).
2. Un **`README.md`** breve: a cosa serve, cosa contiene, quando aggiornarlo.
3. Se è una **collezione** (molti elementi dello stesso tipo), un **`_TEMPLATE/`** come stampo e **una sottocartella per elemento** (es. `clients/<cliente>/`).
4. **Registra il modulo qui** in `PROJECT_STRUCTURE.md`: aggiungi una sezione `## \`nome/\`` con una riga di descrizione. Questo è ciò che rende il modulo visibile alle routine (che scoprono la struttura da qui e dall'elenco cartelle).
5. Se il modulo introduce un tipo di informazione nuovo per la **Memory Update**, aggiungi la riga corrispondente in `PROJECT_INSTRUCTIONS.md` (sezione "Dove aggiornare cosa").

> Regola: **il manifesto e la struttura reale non devono mai divergere.** Chi aggiunge/rinomina/rimuove una cartella aggiorna anche questo file.
