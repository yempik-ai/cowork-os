> **EN —** Filled example (sanitized): the Verification Gate run on a Yempik LinkedIn post draft. Shows two real catches (a fabricated stat, an unresolved `{{CTA}}`) → BLOCK → fixes → PASS → Memory Update. Post copy is illustrative.
> **IT —** Esempio compilato (sanitizzato): il Verification Gate eseguito su una bozza di post LinkedIn di Yempik. Mostra due catch reali (una statistica inventata, una `{{CTA}}` non risolta) → BLOCK → correzioni → PASS → Memory Update. Il testo del post è illustrativo.

---

# Verification Gate — esempio: bozza post LinkedIn

**Data:** 2026-06-18 · **Deliverable:** bozza post LinkedIn (tema: AI Adoption nelle PMI) · **Esecuzione:** on-demand (*"esegui il verification gate su questo post"*)

> Metodo: [`workflows/verification_gate.md`](../../../workflows/verification_gate.md). Convenzione tag: `[DATO REALE]` = verificato da fonte · `[IPOTESI]` = lettura non provata · `[da verificare]` = claim senza fonte · `[illustrativo]` = esempio sanitizzato.

---

## Deliverable in ingresso (bozza)

> Il **73% delle PMI italiane** ha già adottato l'AI nei processi. Gli studi dimostrano che chi non lo fa resta indietro. In Yempik abbiamo aiutato decine di aziende a partire dai processi giusti. {{CTA}}

## Passaggio 1 — Gate (prima esecuzione)

```
Verification
- Ricondotto alla fonte: ❌  — "il 73% delle PMI italiane" non ha fonte collegata; nessun dato di questo tipo nei file di memoria.
- Dati citati: ❌  — "gli studi dimostrano" senza alcuno studio citato.
- Placeholder risolti: ❌  — {{CTA}} ancora nel testo.
- Fatti/ipotesi/racc. separati: ❌  — la statistica è presentata come un fatto ma è [da verificare].
- Completezza vs richiesta: ✅  — lunghezza e tema ok.
- Azioni esterne solo bozza: ✅  — è una bozza, non pubblicata.
- Non verificato: la statistica del 73%; il claim "gli studi dimostrano"; la CTA.
Verdetto: BLOCK — due claim inventati + placeholder non risolto. Non pubblicabile sotto il nome del founder.
```

## Passaggio 2 — Correzioni

- **Statistica 73%** → *rimossa* (nessuna fonte). Sostituita con un'osservazione qualitativa vera: *"Sempre più PMI ci chiedono di partire dai processi, non dagli strumenti."*
- **"Gli studi dimostrano"** → *rimosso*; sostituito con un'evidenza di prima mano (`[DATO REALE]`, dal lavoro Yempik): *"Nei nostri progetti il collo di bottiglia non è mai il modello: è il processo intorno."*
- **`{{CTA}}`** → risolto: *"Se stai valutando dove l'AI conviene davvero nei tuoi processi, scrivimi: ti mando la nostra checklist di adoption."*

## Passaggio 3 — Gate (ri-esecuzione)

```
Verification
- Ricondotto alla fonte: ✅  — nessun numero non verificato; le affermazioni sono esperienza di prima mano marcata [DATO REALE].
- Dati citati: ✅  · Placeholder risolti: ✅  · Fatti/ipotesi/racc. separati: ✅
- Completezza vs richiesta: ✅  · Azioni esterne solo bozza: ✅
- Non verificato: niente.
Verdetto: PASS — pubblicabile previa approvazione umana.
```

## Memory Update

```
Memory Update
- File aggiornati: linkedin/post_tracker.md (riga bozza post "AI Adoption PMI")
- Decisioni aggiunte: nessuna
- Domande aperte aggiunte: "Serve una fonte reale sul tasso di adozione AI nelle PMI IT? Se sì, quale?" → decisions/open_questions.md
- Task aggiunti: nessuno
- Rischi aggiunti: nessuno
- Opportunità aggiunte: nessuna
- Prossime azioni: approvazione umana → pubblicazione
```

---

> **Lezione.** Il gate ha intercettato *prima* della pubblicazione ciò che avrebbe danneggiato la credibilità del founder — una statistica inventata sotto il suo nome. Costo: 3 minuti. È esattamente il tipo di errore che passa quando un output "sembra pronto".
