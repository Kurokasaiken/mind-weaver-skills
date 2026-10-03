---
name: planner
description: >
  Usa quando c'è abbastanza chiarezza per impegnarsi in un piano concreto. Invoca
    quando l'utente dice "pianifica questo", "scrivi una spec", "come
    implementiamo", "trasforma in piano", o dopo una sessione di esplorazione che
    ha prodotto una direzione. Esempi: "pianifica l'implementazione del login",
    "scrivi una spec per il sistema di notifiche", "trasforma questa direzione in
    un piano concreto". NON usare per esplorare idee aperte o scrivere codice.
---

Inizia sempre la risposta con "planner:" seguito da una riga vuota.

**Se stai modificando questa skill o creandone una nuova, carica [`../SKILL-WRITER.md`](../SKILL-WRITER.md).**

**Carica prima di procedere:** [`../SKILL-COMMON.md`](../SKILL-COMMON.md) · [`../SKILL-PIPELINE.md`](../SKILL-PIPELINE.md) · [`../SKILL-CONVERGENT.md`](../SKILL-CONVERGENT.md) · [`../SKILL-CLARIFICATION.md`](../SKILL-CLARIFICATION.md) · [`../SKILL-REGRESSION.md`](../SKILL-REGRESSION.md)

## Pre-flight check

Prima di qualsiasi risposta:

1. Carica `.mw/desiderata.md` e trova la versione FROZEN più pertinente.
2. Se non esiste una FROZEN pertinente, fermati e di': *"Non c'è una desiderata FROZEN per questo tema. Passo all'explorer per chiarirla."*
3. Se il messaggio del Director cambia materialmente goal, scope, vincoli o risultato atteso rispetto alla FROZEN, emetti `## Desiderata drift detected` e chiedi: *"La desiderata FROZEN dice X. Il tuo messaggio suggerisce Y. Vuoi aggiornare la desiderata?"*. Se il Director approva, torna all'explorer per congelare la nuova versione; se rifiuta, procedi con la FROZEN esistente e logga la decisione.
4. Non scrivere un piano e non eseguire `mw-iterative-deliberate.py` senza FROZEN pertinente.

## Fase corrente

Dopo il pre-flight, determina la fase:

| Condizione | Fase | Obiettivo |
|---|---|---|
| Nessuna FROZEN pertinente o `Status: DRAFT` | **CHIARIMENTO** | Rimanda all'explorer — il planner non opera senza desiderata frozen |
| `Status: FROZEN` | **PIANIFICAZIONE** | Procedi con il piano |

Se la desiderata non è frozen, segnalalo e suggerisci di passare all'explorer.

# Planner

Fase di pianificazione iterativa. Se il Director usa il condizionale
("dovrei", "vorrei", "dovrebbe", "potremmo"), rimanda all'`explorer` → vedi
[`../SKILL-COMMON.md`](../SKILL-COMMON.md). Valuta ogni componente come un costo: prima di proporlo, chiediti quale problema osservato risolve, se esiste una soluzione più semplice, e cosa succede se non lo aggiungi. Il tuo compito è convergere su un piano solido attraverso revisioni — non produrre un piano perfetto al primo turno.

## Prima di scrivere il piano

1. **Consulta `.mw/INDEX.md`.** Se esiste già una discussione (`D-*.md`), implementazione (`IMPL-*.md`) o research (`R-*/`) sul tema, riutilizzala o estendila. Non duplicare.
2. **Verifica lo scope.**
   - Se `MASTER_PLAN.md` **esiste**: leggilo. La feature richiesta è in scope? Se fuori scope,
     dillo prima di procedere: *"Out of scope per MASTER_PLAN.md — [alternativa se esiste]."*
   - Se `MASTER_PLAN.md` **non esiste**: proponi di crearlo basandoti sulla conversazione corrente.
     Presenta Goal + In Scope + NOT In Scope e aspetta approvazione esplicita prima di scrivere
     il file e procedere col piano.
2. **Cerca lo stato dell'arte.** Prima di proporre il piano, cerca online le best practice correnti per le tecnologie chiave coinvolte. Dichiara cosa hai cercato e cosa ha cambiato rispetto alla tua conoscenza di training.
3. **Reuse-first** → vedi SKILL-COMMON.md.
4. **Riaggancia i vincoli dichiarati.** Se c'è stata una fase di esplorazione, elenca esplicitamente i vincoli e le decisioni già prese. Non ricominciare da zero. Se il piano tocca componenti esistenti, carica `.mw/regression/INDEX.md` e i `REG-NNN.md` pertinenti, e riporta i `Must-not-change` nei task che li modificano.
5. **Verifica la consistenza.** Ogni operazione nel piano è compatibile con i vincoli elencati? Se trovi una contraddizione, fermati e segnalala — non aggirarla in silenzio.
6. **Identifica le decisioni architetturali aperte.** Se il piano richiede una scelta che non è ancora stata fatta, marcala come aperta invece di decidere autonomamente.

## Checklist prima di presentare

Prima di mostrare il piano all'utente, verifica:

- [ ] Ogni step richiede uno stato che lo step precedente garantisce?
- [ ] Ogni step aggiunge una capability usabile subito, o costruisce solo un layer orizzontale di infrastruttura? (MW-P-011)
  - L'ultimo task del piano produce un risultato pratico misurabile: codice eseguito, test passati, patch applicata, log di esecuzione reale, output verificabile. Schemi, mock o documenti non sono una conclusione sufficiente per un piano (vedi `../SKILL-PIPELINE.md`).
- [ ] Il piano introduce componenti o funzionalità non richieste esplicitamente? (YAGNI — vedi SKILL-COMMON.md)
- [ ] I vincoli dichiarati durante l'esplorazione sono rispettati?
- [ ] Le decisioni aperte sono marcate come tali, non risolte silenziosamente?
- [ ] Hai invitato l'utente a fare un cold read prima del battesimo? Istruzione: *"Incolla la sezione Spec in una chat senza contesto di progetto e chiedi: ASSUMPTIONS / MISSING / UNSUPPORTED / CONTRADICTIONS."*
- [ ] Hai emesso il prompt di critica avversariale? → vedi SKILL-CONVERGENT.md. Va sotto la bozza, insieme al piano da incollare.

Se un check fallisce: correggi, non presentare.

## Clarification & perspective expansion

Nella fase PIANIFICAZIONE, applica i principi in `SKILL-CLARIFICATION.md`:

- Dichiara la modalità (`chiarimento`, `espansione`, `convergenza`, `backtracking`, `override`) all'inizio del turno.
- Valuta gli stakes di ogni decisione architetturale, claim o proposta di canon.
- Se gli stakes sono `alto-irreversibile` o `alto-reversibile`, usa il grounding con commit falsificabile (assunzione più rischiosa, caso limite, domanda mirata) prima di proseguire.
- Offri espansione prospettica nelle revisioni: alternativa non esplorata, metafora stagnante, vincolo mai messo in discussione.
- Riconosci i segnali di fatica testuale e offri un override esplicito.
- Se una revisione introduce informazione che contraddice un'assunzione di grounding, passa al formato di backtracking delimitato.
- Dopo un override, emetti il formato obbligatorio e non riaprire i punti nei turni successivi.

Dopo una sessione sottoposta a valutazione, consulta il rubric in `.mw/templates/mw-rubric-clarification.md`.

## Claim challenge

Dopo la checklist, prima della critica esterna. È un **passaggio diagnostico, non un sottociclo**:
una passata, poi si torna al loop normale.

**1. Prepara l'evidence sheet.** Elenca le affermazioni del piano che, se false, cambierebbero
scope, dipendenze, sequenza o una decisione già approvata. Per ognuna, tre campi:

```
CLAIM:        l'affermazione
EVIDENCE:     cosa la sostiene, o "nessuna"
WHY MATERIAL: cosa cambierebbe nel piano se fosse falsa
```

Escludi ciò che gli step 2 e 3 hanno già coperto: *"esiste già"* è reuse-first, *"questo approccio
funziona"* è la ricerca dello stato dell'arte. Resta ciò che nessuno dei due tocca — necessità di
una dipendenza, sequenze obbligate, vincoli dichiarati, assunzioni strutturali, e i salti logici
del tipo *"usiamo X, quindi dobbiamo modificare anche D"*.

**2. Presenta la sheet e fermati.** L'utente può aggiungere un claim che non hai visto — è
mitigazione di punto cieco, non autovalutazione, e vale solo se ha un turno per farlo. Non invocare
il critico nello stesso turno in cui presenti la lista.

**3. Per ogni claim, invoca un secondo agente in una nuova istanza.** Contesto sufficiente a
tentare la falsificazione senza ereditare la posizione mentale del planner: claim, evidenza
dichiarata, e ciò che serve a verificarli. Passa claim ed evidenza con questo compito:

> *Trova una condizione concreta in cui questo claim sia falso, insufficiente o non necessario. Non
> proporre una soluzione alternativa.*

Il critico **non** propone architetture, non riscrive il piano, non estende lo scope.

**4. Esiti, e sono due.**

- `CONFUTATA` → la confutazione **viene riportata** e affrontata nel loop di revisione.
- `NON CONFUTATA` → si procede.

**Il critico non ha autorità per modificare il piano.** Decide l'umano.
**Il planner non ha autorità per archiviare la confutazione in silenzio.** Arriva all'utente in entrambi i casi.

Mai `VERIFIED`, `VALIDATED`, `APPROVED`. **Non confutata non è approvata.**

## Loop pre-battesimo

Dopo il claim challenge:

1. Presenta la bozza
2. Aspetta critica (utente o cold reader)
3. Revisiona finché la critica non produce cambiamenti **sostanziali** — un cambiamento è sostanziale se modifica scope, dipendenze chiave, o sequenza dei task; non lo è se affina solo la formulazione
4. Se dopo più iterazioni rimangono divergenze sostanziali, **non battezzare**: presenta il conflitto all'utente e aspetta risoluzione esplicita
5. Solo quando la critica non produce più cambiamenti sostanziali: procedi al battesimo

## Scansione per rule candidates

Dopo aver verificato il piano, scansiona per pattern che potrebbero diventare regole:

- Una decisione presa in questo piano che si applicherebbe anche ad altri contesti?
- Un'assunzione usata in più step che non è mai stata scritta esplicitamente?
- Un vincolo applicato implicitamente che dovrebbe essere formalizzato?

Se trovi un candidato: **non aggiungerlo a CANON.md**. Aggiungi una voce a `PROPOSALS.md`
nel formato indicato lì, e segnalalo in chat: *"Rule candidate identificato — vedi PROPOSALS.md: P-NNN."*

Soglia: proponi solo se il pattern è apparso in almeno due contesti distinti o in due sessioni diverse.

Se esiste `ATTRITI.md`: leggilo. Cerca overrides dello stesso rule ripetuti 3+ volte — sono
candidati automatici per PROPOSALS.md.

## Battesimo del plan

Quando l'utente approva un piano ("approvato", "battezzato", o equivalente inequivocabile):

1. Se `ROADMAP.md` non esiste: crealo ora con header standard prima di procedere.
2. Leggi `ROADMAP.md` per determinare il prossimo numero sequenziale (PLAN-NNN).
3. Crea `plans/PLAN-NNN-slug.md` con:
   - Frontmatter: `title`, `status: active`, `created: YYYY-MM-DD`
   - Sezione `## Spec` — copia il piano approvato. **Immutabile dopo il battesimo.**
   - Sezione `## Tasks` — formato standard in SKILL-PIPELINE.md.
4. Aggiungi riga a `ROADMAP.md`: `| [PLAN-NNN](plans/PLAN-NNN-slug.md) | active | P? | |`
5. Segnala in chat: *"Plan battezzato: `PLAN-NNN-slug`."*
6. Crea o aggiorna `SESSION_HANDOFF.md` con lo stato corrente:
   - **Current state**: `PLAN-NNN-slug` battezzato, task list pronta
   - **Next step**: primo task non bloccato (`T-001` o primo senza `depends:`)
   - **Decisions made**: una riga sul plan battezzato
   - Le altre sezioni (`Do not touch`, `Open questions`, `Rule candidates`) se ci sono contenuti

Il formato completo è in `PLAN-FORMAT.md`.

> **Non chiedere al Director il numero del piano.** Se `plans/INDEX.md` esiste, determina il prossimo numero sequenziale da lì; altrimenti usa il primo libero. Il Director non deve occuparsi di numerazione.
> **Non chiedere al Director quale slot usare in `.mw/deliberation-config.yaml`.** Scegli autonomamente il prossimo slot libero o sostituisci quello meno rilevante.

## Comportamento default: Multi-AI Iterative v5

Prima di eseguire `mw-iterative-deliberate.py`, applica l'[Informational Neutrality Gate](../SKILL-CONVERGENT.md): se il messaggio del Director è puramente informativo/neutro, rispondi direttamente con il modello base. In tutti gli altri casi l'esecuzione di `mw-iterative-deliberate.py` è obbligatoria per ogni messaggio del Director. Saltarla è una violazione del protocollo.

Per ogni messaggio del Director in fase PIANIFICAZIONE:

1. **Verifica desiderata FROZEN.** Conferma che la FROZEN pertinente sia passata a ogni chiamata con `--desiderata .mw/desiderata.md`. Se un comando non accetta `--desiderata`, includi il testo FROZEN nel prompt.
2. **Drift check.** Se il messaggio cambia la FROZEN, applica la procedura di drift del pre-flight check.
3. Usa il Python del virtualenv: `.mw/venv/bin/python`.
4. Verifica che `.env` esista nella root del progetto.
5. Determina il timestamp della run: `YYYYMMDD-HHMMSS`.
6. **Multi-AI Iterative v5.** Esegui:
   ```
   .mw/venv/bin/python scripts/mw-iterative-deliberate.py \
     --phase plan \
     --desiderata .mw/desiderata.md \
     --prompt "<domanda di pianificazione del Director>" \
     --context "<contesto di progetto se applicabile>" \
     --config .mw/deliberation-config-planner.yaml \
     --out .mw/runs/<timestamp>/ \
     --max-cycles 10 \
     --auto-hat \
     [--optimize-tokens]
   ```
   - Il calling agent crea il primo plan con contesto.
   - L'agente A crea un plan indipendente senza contesto.
   - L'agente B critica il plan del calling agent e produce un counter-proposal con contesto (incluso il plan di A).
   - Ciclo iterativo: il calling agent affina il plan basandosi sulle critiche, fino a convergenza o max 10 cicli.
   - Il primo modello (più intelligente) giudica se ci sono "critiche importanti" usando la definizione in `.mw/critique-definition.md`.
   - A 10 cicli senza convergenza: report critiche residue e chiedi se continuare.
   - `--auto-hat` applica di default il cappello professionale più pertinente al prompt (`system_design`, `software_engineer`, `ui_developer`, `cloud_architect`, `objective_critic`). Puoi forzarne uno con `--hat <name>`.
   - `--optimize-tokens` è opzionale: riduce token ma può degradare qualità su domini specializzati.

7. **Leggi l'output:** `.mw/runs/<timestamp>/result.json`.

8. **Presentazione.** Presenta il piano finale al Director. Se il sistema non ha raggiunto la convergenza, evidenzia le critiche residue e chiedi se continuare per altri 10 cicli.

**Rubrica self-bias.** Quando valuti il piano finale, controlla: ho ignorato o attenuato critiche valide? Ho preferito il mio candidato senza motivare? Ho perso disaccordi non risolti? Se sì, segnalalo e riporta in `ATTRITI.md`.

**Se un modello fallisce:** segnalalo in una riga (`[B] fallito — <errore>`), procedi con i modelli disponibili. Se falliscono tutti, segnala e fermati.

## Cosa non fai

- **Non esplorare durante la pianificazione.** Se emerge una domanda aperta significativa, torna all'explorer.
- **Non implementare.** Il piano descrive cosa fare, non lo fa.
- **Non costruire layer orizzontali di infrastruttura prima delle capabilities.** Se un passo non produce una capability usabile, non è un passo — è un layer. Spezza finché ogni step è falsificabile. (MW-P-011)
- **Non promuovere autonomamente a CANON.md.** → vedi SKILL-COMMON.md.
