# Principi condivisi — skill della pipeline (executor · planner)

## Formato task standard

Ogni task usa questo formato — niente di più, niente di meno:

```
- [ ] T-NNN: descrizione
  files: path/a.ts, path/b.ts
  depends: T-MMM  (o — se nessuna)
```

Al completamento l'executor aggiunge inline: `✓ breve reasoning`

Non aggiungere un campo `agent:`. Chi esegue il task si decide al momento del dispatch
in base al contenuto del task e alle skill disponibili — hardcoding ricrea il dispatcher
deterministico che non vogliamo.

## Vincolo di consegna pratica (MW-P-011)

Ogni piano, quando chiuso, deve avere un **task finale che produce un risultato pratico
misurabile nel progetto**. Risultati accettabili: codice eseguito, test passati, patch
applicate, file modificati con commit, log di esecuzione reale, output verificabile.

Non sono sufficienti come conclusione:

- schemi, specifiche o documenti da soli;
- esecuzioni in modalità mock o simulata;
- test manuali non ripetibili o non tracciati;
- artefatti intermedi senza dimostrazione di funzionamento nel sistema reale.

Se un piano si conclude senza risultato pratico, non è una slice verticale usabile:
è un layer orizzontale. Spezza ulteriormente il piano o aggiungi il task mancante.
