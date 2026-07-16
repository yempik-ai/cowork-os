> **EN —** A pre-"done" gate for any deliverable that goes to a client or drives a decision: prove it before you ship it. Every fact reconciled to a real source, every number cited, every `{{placeholder}}` resolved, the unverified declared out loud. Runs right before the Memory Update.
> **IT —** Un gate pre-"done" per ogni deliverable che va a un cliente o guida una decisione: dimostralo prima di consegnarlo. Ogni fatto ricondotto a una fonte reale, ogni numero citato, ogni `{{placeholder}}` risolto, il non-verificato dichiarato. Gira subito prima del Memory Update.

---

# Verification Gate — Definition of Done

> Quando conta, "sembra pronto" non basta. Prima di dichiarare un deliverable *done*, deve passare il gate. È la Definition of Done del lavoro di conoscenza: post, proposte, report, deck, brief, liste di invio.

## Principio fondamentale

Non produrre. Verifica.

- Prodotto: "Ho scritto il post / la proposta / il report."
- Done: "L'ho verificato e posso mostrare su cosa si regge ogni affermazione."

Un output che non passa il gate è una **bozza**, non un deliverable.

## Quando gira

- **Su richiesta:** *"esegui il verification gate su [deliverable]"*.
- **Sempre (se abilitato in setup):** prima di dichiarare *done* qualunque deliverable importante — vedi *Attivazione*.
- **Non serve** per micro-task interni (una risposta in chat, un brainstorming). Serve quando l'output **esce** o **decide**.

## Il gate — 7 controlli

1. **Ricondotto alla fonte.** Ogni fatto e ogni numero è tracciabile a una fonte reale collegata (file di memoria, analytics, CRM, repo). Niente dati inventati (regola di Project).
2. **Citazioni.** Ogni metrica/claim porta la sua fonte. Senza fonte → marcalo `[da verificare]`, mai presentato come `[DATO REALE]`.
3. **Placeholder risolti.** Nessun `{{placeholder}}` residuo. Ogni nome, cifra, destinatario, link è reale oppure marcato `[illustrativo]`.
4. **Fatti / ipotesi / raccomandazioni separati.** L'output distingue `[DATO REALE]` · `[IPOTESI]` · `[RACCOMANDAZIONE]` (convenzione di Project).
5. **Completezza vs richiesta.** L'output copre tutto ciò che il task chiedeva. Ciò che manca è **dichiarato**, non nascosto.
6. **Azioni esterne = bozza.** Nulla è "inviato/pubblicato". Ogni comunicazione verso l'esterno resta bozza in attesa di approvazione umana (posture di Project).
7. **Dichiarazione del non-verificato.** Una riga esplicita: *"Non verificato: …"*. Se è tutto verificato, dillo.

## Verdetto

- **PASS** → il deliverable è *done*. Procedi al Memory Update.
- **BLOCK** → elenca cosa manca, correggi, ri-verifica. Non consegnare, non dichiarare *done*.

⛔ **Regola madre: non dichiarare "done" ciò che non passa il gate.** Meglio un BLOCK onesto con la lista dei buchi che un deliverable che *sembra* pronto e non lo è.

## Blocco output obbligatorio (precede il Memory Update)

```
Verification
- Ricondotto alla fonte: ✅/❌  · Dati citati: ✅/❌  · Placeholder risolti: ✅/❌
- Fatti/ipotesi/racc. separati: ✅/❌  · Completezza vs richiesta: ✅/❌  · Azioni esterne solo bozza: ✅/❌
- Non verificato: [elenco, oppure "niente"]
Verdetto: PASS | BLOCK — [motivo in una riga]
```

Poi, se **PASS**, esegui il **Memory Update** (`PROJECT_INSTRUCTIONS.md`). Il gate verifica il *deliverable*; il Memory Update aggiorna il *company brain*. Sono due fasi diverse: prima si verifica, poi si scrive la memoria.

## Esempio (breve)

Deliverable: bozza di post LinkedIn.

```
Verification
- Ricondotto alla fonte: ❌ ("il 73% delle PMI…" non ha fonte)
- Dati citati: ❌  · Placeholder risolti: ❌ ({{CTA}} ancora nel testo)
- Fatti/ipotesi/racc. separati: ✅  · Completezza: ✅  · Azioni esterne solo bozza: ✅
- Non verificato: la statistica del 73%, il claim "gli studi dimostrano"
Verdetto: BLOCK — statistica inventata + {{CTA}} non risolto. Rimuovo o cito, risolvo la CTA, poi ri-verifico.
```

Esempio completo e compilato: [`examples/yempik/reviews/verification-linkedin-post.md`](../examples/yempik/reviews/verification-linkedin-post.md).

## Attivazione (opt-in, chiesto in setup)

Il gate è **disattivo di default**. In fase di installazione l'agente **chiede**: *"Vuoi un passaggio di verifica prima che i deliverable siano dichiarati done?"*

- **Sì** → aggiungi **una riga** alle regole operative del **tuo** `PROJECT_INSTRUCTIONS.md` (la tua copia, non il template del kit): *"Prima di dichiarare done un deliverable importante, esegui `workflows/verification_gate.md` e riporta il blocco Verification prima del Memory Update."*
- **No** → resta on-demand: invocalo con *"esegui il verification gate su [deliverable]"* quando serve.

Non forzarlo nel system prompt del kit: è una scelta dell'utente, non un default imposto.

## Relazione con la skill `verification` (il gemello di codice)

La skill `verification` (in code-os, o qualunque skill di verifica del codice) prova che un task **tecnico** è davvero *done*. La sua regola madre: **«No green output, no done» — "done" è una prova, non una sensazione.** Questo gate applica lo **stesso principio ai deliverable di business** (prosa, deck, proposte, post, liste), senza installazione. Ogni controllo del gate ha il suo gemello di ingegneria — stessa disciplina, superficie diversa:

| Skill `verification` (codice) | Verification Gate (deliverable) |
|---|---|
| *Evidence, not assertion* — mostra l'output di test/build, non un'affermazione | **1. Ricondotto alla fonte** — ogni fatto ha la sua evidenza, non è un'asserzione |
| *Anchor every claim to a source* — se non puoi ancorarlo, non spedirlo | **2. Citazioni** — ogni claim porta la sua fonte; senza fonte → `[da verificare]` |
| *Verify the blast radius* prima del commit | **3. Placeholder risolti** — nessuno scope residuo (`{{…}}`, destinatario) non risolto |
| *Separate facts from assumptions* | **4. Fatti / ipotesi / raccomandazioni separati** |
| *Run the tests* — esercita la modifica end-to-end | **5. Completezza vs richiesta** — l'output copre davvero ciò che il task chiedeva |
| *Refuse destructive/irreversible commands* senza approvazione | **6. Azioni esterne = bozza** — niente inviato/pubblicato senza approvazione umana |
| *Record blockers, don't push past them* | **7. Dichiarazione del non-verificato** |

Il verdetto **PASS/BLOCK** è l'equivalente di *"No green output, no done"*: la skill fa girare i test, il gate fa girare i sette controlli. Usa la **skill** per il codice, il **gate** per tutto il resto.

## Frase guida

"Done" non è un sentimento. È una fonte per ogni numero, un destinatario per ogni `{{placeholder}}`, e una riga onesta su ciò che ancora non sai.
