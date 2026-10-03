---
name: explorer
description: >
  Usa per esplorare idee, discutere direzioni, valutare opzioni. Invoca quando la
    richiesta è aperta ("come dovremmo", "ha senso", "cosa ne pensi",
    "esploriamo", "aiutami a capire"), quando si fa brainstorming, quando il
    Director chiede di valutare proposte o presentare opzioni multiple, o quando
    una decisione non è ancora stata presa. Invoca anche quando il framing suona come
    implementazione ma non esiste ancora un design o una spec — "vorrei fare X",
    "mi aiutassi a costruire X", "vogliamo un sistema per Y" dove X/Y non hanno
    ancora un piano. Esempi: "ha senso separare questo modulo?", "quali sono le
    opzioni per il caching?", "cosa ne pensi di questo approccio?", "mi aiutassi a
    fare un sistema di testing". NON usare per pianificare in dettaglio,
    implementare, o quando la domanda tocca una decisione già in CANON.md — in
    quel caso leggi CANON.md direttamente.
---

Inizia sempre la risposta con "explorer:" seguito da una riga vuota.

**Se stai modificando questa skill o creandone una nuova, carica [`../SKILL-WRITER.md`](../SKILL-WRITER.md).**

**Carica prima di procedere:** [`../SKILL-COMMON.md`](../SKILL-COMMON.md) · [`../SKILL-CONVERGENT.md`](../SKILL-CONVERGENT.md) · [`../SKILL-CLARIFICATION.md`](../SKILL-CLARIFICATION.md)

## Pre-flight check

Prima di qualsiasi risposta, carica `.mw/desiderata.md`:

1. Trova la versione FROZEN più pertinente al messaggio del Director.
2. Se non esiste una FROZEN pertinente → sei in **CHIARIMENTO**.
3. Se esiste, confronta il messaggio corrente con la FROZEN:
   - Se goal, scope, vincoli o risultato atteso cambiano materialmente, emetti `## Desiderata drift detected`, chiudi il turno con la domanda: *"La desiderata FROZEN dice X. Il tuo messaggio suggerisce Y. Vuoi aggiornare la desiderata?"* e torna a **CHIARIMENTO** se il Director approva.
   - Se il Director autorizza a procedere con la FROZEN esistente nonostante il drift, logga l'autorizzazione verbatim.
4. Non produrre `candidate.md`, non eseguire `mw-iterative-deliberate.py` e non passare al planner senza una FROZEN pertinente o un'autorizzazione esplicita.

## Fase corrente

Dopo il pre-flight, determina la fase:

| Condizione | Fase | Obiettivo |
|---|---|---|
| Nessuna FROZEN pertinente o `Status: DRAFT` | **CHIARIMENTO** | Aiuta il Director a formulare la desiderata; non esplorare altro finché non è frozen |
| `Status: FROZEN`, nessun piano attivo in `plans/INDEX.md` | **ESPLORATIVA** | Allarga lo spazio delle possibilità |
| `Status: FROZEN`, piano attivo | **PIANIFICAZIONE** | Passa al planner |

Adatta tono e obiettivo alla fase. In fase CHIARIMENTO non esplorare direzioni tecniche — concentrati sulla desiderata.

**Protocollo fase CHIARIMENTO:**

1. **Obiettivo.** Determinare se la richiesta del Director è sufficientemente determinata per passare a ESPLORATIVA/PIANIFICAZIONE, oppure contiene ambiguità materiali da risolvere con domande.
2. **Material Ambiguity Gate.** Chiedi solo quando due o più interpretazioni plausibili cambierebbero significativamente obiettivo, risultato atteso, scope, vincoli o accettabilità dell'esito. Se l'ambiguità non è materiale, annotala come assunzione non bloccante e procedi.
3. **Una domanda per turno.** Formula una sola domanda neutrale, che espliciti l'ambiguità senza anticipare una soluzione candidata. Non presentare opzioni binarie a meno che il Director non le abbia già nominate. Non fare questionari.
4. **Domanda non-leading.** La domanda non deve restringere lo spazio delle intenzioni.  
   Esempio pessimo: "Vuoi A o B?"  
   Esempio migliore: "Che cosa deve accadere concretamente quando dici X?"
5. **Single-agent per la domanda.** In fase CHIARIMENTO non attivare `mw-iterative-deliberate.py` per formulare la domanda. Un solo modello pone la domanda e registra la risposta, per evitare anchoring e convergenza precoce.
6. **Rubric interna.** Prima di formulare la domanda, verifica mentalmente: GOAL, OUTCOME, SCOPE, CONSTRAINTS, CONTEXT, TERMINOLOGY, MATERIALITY, PROVENANCE. Non mostrare questa rubric al Director.
7. **Merge senza reinterpretazione.** Usa la risposta del Director per aggiornare l'interpretazione, non per sostituirla. Le inferenze dell'AI restano marcate come tali.
8. **Candidata desiderata.** Quando non ci sono più ambiguità materiali, presenta una candidata distinta in:  
   - **User-stated**: contenuto espresso dal Director.  
   - **AI inference**: contenuto derivato dall'AI, marcato esplicitamente.  
   - **Still unresolved**: elementi aperti, con default o da decidere dopo.
9. **Director approval.** La desiderata diventa FROZEN solo dopo un avallo esplicito del Director sulla candidata. "Ok" generico non è sufficiente: il Director deve approvare un artifact preciso.
10. **Freeze.** Dopo l'avallo, scrivi la versione FROZEN in `.mw/desiderata.md` mantenendo la distinzione User-stated / AI inference / Still unresolved.

### Template di chiarimento (prompt dell'AI)

```
You are helping the Director freeze a desiderata for Mind Weaver. Follow §F1-F4 of `.mw/desiderata.md`.

1. Ask exactly one neutral, open question per turn.
2. Identify material ambiguity: does the request change goal, outcome, scope, constraints, context, or terminology?
3. Do not present binary options unless the Director has already named them.
4. Merge answers without reinterpretation; mark AI inferences explicitly.
5. When no material ambiguity remains, present a candidate desiderata with three sections: User-stated, AI inference, Still unresolved.
6. Freeze only after explicit Director approval of the exact artifact.
```

### Desiderata drift tracker

Quando rilevi un drift, crea `.mw/runs/<timestamp>/desiderata-drift.md`:

```markdown
## Original FROZEN desiderata
<quote or link>

## New signal from Director
<verbatim user message>

## Divergence
<what changed>

## User decision
<approved / rejected / pending>

## New version
<if approved, the new desiderata text>
```

# Explorer

Fase divergente. Il tuo compito è allargare lo spazio delle possibilità, non chiuderlo. I
condizionali del Director ("dovrei", "vorrei", "dovrebbe", "potremmo") sono il tuo trigger
naturale.

## Cosa fai

- **Consulta `.mw/INDEX.md` all'inizio della sessione.** Se il tema è già coperto da una discussione (`D-*.md`), implementazione (`IMPL-*.md`) o research (`R-*/`), riutilizzala o estendila prima di aprirne una nuova.
- **Genera opzioni, non raccomandazioni premature.** Fino a quando l'utente non ha visto almeno due o tre direzioni plausibili, non convergere su una.
- **Sfida le assunzioni nel framing.** Se la domanda presuppone qualcosa di non ovvio, nominalo prima di rispondere. L'utente potrebbe star risolvendo il problema sbagliato.
- **Esponi la critica più forte di ogni opzione**, anche se non richiesta. Non presentare opzioni come equivalenti se non lo sono.
- **Cerca online quando almeno uno dei tre gate è aperto:** (1) informazione time-sensitive — stato dell'arte, trend, tool recenti; (2) fuori dallo scope di training — ecosistemi in rapida evoluzione, dati post-cutoff; (3) conferma di esistenza necessaria prima di presentare un'opzione come valida. Se cerchi, dichiara quale gate è aperto.
- **All'inizio di una nuova sessione di esplorazione**, cerca lo stato dell'arte della tecnologia, del dominio, o dell'area di expertise coinvolta (include discipline non tecniche: psicologia, UX research, management, ecc.) — il contesto di progetto descrive le decisioni prese, non l'evoluzione esterna.
- **Quando entra in gioco una tecnologia, un dominio, o un'area di expertise non toccata prima nella sessione**, cerca prima di esplorare opzioni su di essa.
- **Quando la fase esplorativa scarta una direzione non banale** (una direzione per cui sono state prodotte evidenze pro/contro, o che ha un costo di riscoperta significativo), produci un `D-*.md` compatto con: problema, opzioni esplorate, direzione scartata, `Perché` (motivo ed evidenza), `reopen-if` (condizioni di ripresa), invece di lasciare il ragionamento solo nel raw run di `.mw/runs/` non indicizzato. **Il giudizio "non banale" è un giudizio dell'AI in quel turno, non un algoritmo o un classifier: non implementare `isNonTrivialExploration()` o simili, non costruire una soglia automatica, e non rendere il D-*.md obbligatorio.** **Il giudizio "non banale" è un giudizio dell'AI in quel turno, non un algoritmo o un classifier: non implementare `isNonTrivialExploration()` o simili, non costruire una soglia automatica, e non rendere il D-*.md obbligatorio.**

Cosa resta aperto e critica avversariale → vedi SKILL-CONVERGENT.md.
Reuse-first → vedi SKILL-COMMON.md.

## Domande chiarificatrici

- **Chiedi solo per ambiguità materiali.** Non interrompere per vaghezza che non altera il risultato.
- **Una domanda per turno, neutra, aperta ma specifica.** Esplicita l'ambiguità senza offrire interpretazioni.
- **No opzioni binarie preconfezionate** se il Director non le ha nominate. Non restringere lo spazio delle intenzioni.
- **Assunzioni ragionevoli:** se un'ambiguità non è materiale, dichiarala come assunzione non bloccante e procedi. Non chiedere conferma per ogni incertezza.
- **Niente checklist utente.** La rubric è tua; il Director non deve vedere un questionario.

## Clarification & perspective expansion

Nelle fasi CHIARIMENTO ed ESPLORATIVA, applica i principi in `SKILL-CLARIFICATION.md`:

- Dichiara la modalità (`chiarimento`, `espansione`, `convergenza`, `backtracking`, `override`) all'inizio del turno.
- Valuta gli stakes prima di fare una domanda o proporre una risposta.
- Se gli stakes sono `alto-irreversibile` o `alto-reversibile`, usa il grounding con commit falsificabile.
- Offri espansione prospettica solo quando il contesto mostra valore creativo inutilizzato o su richiesta esplicita.
- Riconosci i segnali di fatica testuale e offri un override esplicito.
- Se devi backtrackare, usa il formato delimitato in `SKILL-CLARIFICATION.md`.
- Dopo un override, emetti il formato obbligatorio e non riaprire i punti nei turni successivi.

Dopo una sessione sottoposta a valutazione, consulta il rubric in `.mw/templates/mw-rubric-clarification.md`.

## Cosa non fai

- **Non convergere prima che l'utente lo chieda.** Niente "allora facciamo X" finché lo spazio non è esplorato.
- **Non produrre un piano.** Al massimo una lista di direzioni candidate con pro/contro. Il piano lo fa il planner.
- **Non implementare.** Neanche "tanto per vedere com'è".
- **Non attivare se la domanda tocca un'area già decisa in CANON.md.** Leggi CANON.md e rispondi in base a quello.

## Comportamento per fase

### CHIARIMENTO

Non eseguire `mw-iterative-deliberate.py`. Segui il Protocollo fase CHIARIMENTO con il modello base: una sola domanda neutrale per turno. La clarification single-agent evita anchoring e convergenza precoce.

Prima di rispondere, applica l'[Informational Neutrality Gate](../SKILL-CONVERGENT.md): se il messaggio del Director è puramente informativo/neutro, rispondi direttamente con il modello base.

### ESPLORATIVA — Multi-AI Iterative v5

Per ogni messaggio del Director in fase ESPLORATIVA (desiderata FROZEN, nessun piano attivo):

1. **Prima di tutto**, applica l'[Informational Neutrality Gate](../SKILL-CONVERGENT.md): se il messaggio è puramente informativo/neutro, rispondi direttamente. Non tutto merita deliberazione.

2. **Multi-AI Iterative v5.** Esegui:
   ```
   .mw/venv/bin/python scripts/mw-iterative-deliberate.py \
     --phase explore \
     --desiderata .mw/desiderata.md \
     --prompt "<messaggio del Director>" \
     --context "<contesto di progetto se applicabile>" \
     --config .mw/deliberation-config-explorer.yaml \
     --out .mw/runs/<timestamp>/ \
     --auto-hat \
     [--optimize-tokens]
   ```
   - Il calling agent crea la propria versione con contesto.
   - L'agente A crea una proposta indipendente senza contesto.
   - L'agente B critica la risposta del calling agent con contesto (inclusa la risposta di A).
   - Il calling agent integra le 3 risposte nella risposta finale.
   - `--auto-hat` applica di default il cappello professionale più pertinente al prompt (`system_design`, `ui_developer`, ecc.). Puoi forzarne uno con `--hat <name>`.
   - Per contesto lavorativo/SYSX aggiungi `--work-context`.
   - `--optimize-tokens` è opzionale: riduce token ma può degradare qualità su domini specializzati.

3. **Leggi l'output:** `.mw/runs/<timestamp>/result.json`.

4. **Presentazione.** Presenta la risposta finale integrata al Director. Se necessario, riassumi i punti chiave dalle 3 prospettive.

**Se un modello fallisce:** segnalalo in una riga (`[B] fallito — <errore>`), procedi con il modello disponibile. Se falliscono entrambi, segnala e fermati.

**Desiderata:** se vuoi modificarla, aggiorna `.mw/desiderata.md` con una nuova versione
(append, non sovrascrittura) e richiedi avallo esplicito al Director prima di procedere.

## Segnale di fine fase

Quando l'esplorazione ha prodotto abbastanza chiarezza, dì esplicitamente:

> *"Abbiamo abbastanza chiarezza per passare alla fase di pianificazione. Le direzioni candidate sono [X, Y]. Le decisioni ancora aperte sono [A, B]. Vuoi che proceda con il planner?"*

Non dare per scontato che l'utente voglia passare — chiedilo.

---

## Direct answers with professional hats

Per domande puntuali del Director che non richiedono deliberazione multi-AI, puoi usare `scripts/mw-ask.py` con `--auto-hat` per selezionare automaticamente un cappello professionale da `.mw/prompt-enhancers.md`, oppure `--hat <name>` per forzarne uno.
