# SKILL-WRITER — Convenzioni per la scrittura e modifica delle skill

**Carica prima di procedere:** [`SKILL-COMMON.md`](SKILL-COMMON.md) · [`SKILL-PIPELINE.md`](SKILL-PIPELINE.md) · [`SKILL-CONVERGENT.md`](SKILL-CONVERGENT.md)

## Quando usare questo file

Carica `SKILL-WRITER.md` ogni volta che il Director chiede di **creare una nuova skill** o **modificare una skill esistente** in `.agents/skills/<nome>/SKILL.md`.

## Struttura di una skill

Una skill Mind Weaver è un file markdown con:

1. **YAML frontmatter** in cima:
   ```yaml
   ---
   name: nome-skill
   description: >
     Una descrizione breve. Se contiene virgolette doppie interne, usa il blocco
     folded '>' così non rompe il parser YAML.
   ---
   ```
2. **Identificazione dello speaker** subito dopo il frontmatter:
   > `Inizia sempre la risposta con "nome-skill:" seguito da una riga vuota.`
3. **Sezione "Se stai modificando questa skill"** con il riferimento a `SKILL-WRITER.md`.
4. **Sezione "Carica prima di procedere"** con i file comuni rilevanti.
5. **Corpo della skill** — il workflow specifico. Non contiene governance (vive in `AGENTS.md`/`CANON.md`) né comportamenti condivisi (vivono in `SKILL-*.md`).

## Comportamenti comuni: non duplicarli

I file condivisi esistenti sono:

- `SKILL-COMMON.md` — principi condivisi: YAGNI/KISS/DRY, reuse-first, override di `CANON.md`.
- `SKILL-PIPELINE.md` — formato task e pipeline di esecuzione.
- `SKILL-CONVERGENT.md` — critica avversariale, dichiarare cosa resta aperto.
- `SKILL-REGRESSION.md` — prevenire regressioni quando si tocca codice esistente.

Se una sezione o un comportamento è utile per **più di una skill**, non copiarlo in ogni `SKILL.md`. Estrailo in un nuovo `SKILL-*.md` e riferiscilo con `**Carica prima di procedere:**` o `vedi ../SKILL-*.md`.

## Regole per la modifica di una skill

1. Carica `SKILL-WRITER.md`, `SKILL-COMMON.md`, `SKILL-PIPELINE.md` e `SKILL-CONVERGENT.md`.
2. Modifica solo la parte specifica del workflow della skill; non duplicare testo dai file comuni.
3. Se un comportamento condiviso deve cambiare, modifica il file comune e aggiorna i riferimenti nelle skill interessate.
4. Non inserire governance, metodologia o regole always-on nella skill. Le skill sono workflow invocabili; la governance vive in `AGENTS.md` e le decisioni in `CANON.md`.

## Esempio di header per una nuova skill

```markdown
---
name: example
description: >
  Breve descrizione della skill.
---

Inizia sempre la risposta con "example:" seguito da una riga vuota.

**Se stai modificando questa skill o creandone una nuova, carica [`../SKILL-WRITER.md`](../SKILL-WRITER.md).**

**Carica prima di procedere:** [`../SKILL-COMMON.md`](../SKILL-COMMON.md) · [`../SKILL-PIPELINE.md`](../SKILL-PIPELINE.md)
```
