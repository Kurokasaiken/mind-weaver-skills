# SKILL-REGRESSION — Prevenire regressioni nelle modifiche

## Quando si tocca codice esistente

1. Carica `.mw/regression/INDEX.md` e i `REG-NNN.md` pertinenti al componente che stai per modificare.
2. Descrivi il comportamento attuale reale del file/componente.
3. Elenca le decisioni passate (`CANON.md`, `LOGBOOK.md`, `ATTRITI.md`, piani completati) che lo vincolano.
4. Identifica esplicitamente quali parti modificherai e perché.
5. Se una modifica sovrascrive un `Must-not-change` di un `REG` o una decisione in `CANON`, ferma e segnala invece di procedere.

## Dopo la modifica

- Esegui lo smoke test sul componente toccato.
- Verifica che i `Must-not-change` siano ancora rispettati.
- Se la modifica corregge o aggiorna una regressione, aggiorna `.mw/regression/INDEX.md` e il relativo `REG-NNN.md`.
