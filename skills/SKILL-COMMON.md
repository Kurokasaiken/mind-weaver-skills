# Principi condivisi — tutte le skill Mind Weaver

## Contesto Mind Weaver

Se stai lavorando su questo repo (Mind Weaver come progetto), leggi [`CONTEXT-MINDWEAVER.md`](../../CONTEXT-MINDWEAVER.md) prima di procedere.

## Aggiungi solo ciò che serve (MW-P-010)

Aggiungi solo ciò che il task richiede esplicitamente (YAGNI). Tra due soluzioni ugualmente valide, scegli la più semplice (KISS). Se la logica esiste già, riusala invece di riscriverla (DRY).

## Reuse-first

Prima di costruire qualcosa di nuovo, verifica:
1. Esiste già nel progetto?
2. Una dipendenza già installata lo fa?

Se non sai, cerca prima di costruire. Se la risposta è sì, riusa — non ricostruire.

## Condizionali come segnale di esplorazione

Frasi come "dovrei", "vorrei", "dovrebbe", "potrei", "potremmo", "se" sono segnali di
esplorazione, non di esecuzione. Se il Director usa il condizionale, l'AI deve attivare o
rimandare all'`explorer`. `executor` e `planner` non eseguono: chiedono se il
Director vuole passare all'`explorer` o riformulare il messaggio in modo imperativo.

## Correzione trigger da feedback del Director

Quando il Director segnala che hai usato la skill o lo strumento sbagliato:

1. Fermati e chiedi: "Quale parola o formula avresti dovuto individuare per attivare la skill/strumento corretto?"
2. Aspetta la risposta del Director.
3. Proponi la modifica specifica (testo esatto) allo skill o al file comune interessato.
4. Aspetta un avallo esplicito del Director ("sì", "ok", "scrivilo") prima di applicare.
5. Dopo l'avallo, carica `SKILL-WRITER.md` e applica la modifica.

Le piccole correzioni di trigger non richiedono tracciabilità formale in `PROPOSALS.md`.

## CANON.md è autoritativo

Non scrivere in `CANON.md` senza approvazione esplicita dell'utente. Se devi deviare da una regola di `CANON.md`, dichiaralo prima di procedere — non dopo. L'override va registrato in `ATTRITI.md`.
