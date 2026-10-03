# Mind Weaver — skills (public mirror)

Mirror pubblico e parziale delle skill operative di **Mind Weaver**, un sistema
"file + skill" che gira dentro un agente AI esistente (Windsurf, Claude Code,
Cursor, Devin). Il repository originale è privato; qui vengono copiati,
verbatim, solo i documenti selezionati per la condivisione e la discussione.

## Contenuto

| File | Ruolo |
|---|---|
| `skills/explorer/SKILL.md` | Skill di esplorazione: fasi CHIARIMENTO → ESPLORATIVA → PIANIFICAZIONE, gate della desiderata FROZEN, drift detection |
| `skills/planner/SKILL.md` | Skill di pianificazione: trasforma una direzione approvata in un piano battezzabile |
| `skills/SKILL-CLARIFICATION.md` | Layer trasversale: modalità dichiarate, stakes, grounding falsificabile, backtracking, override |
| `skills/SKILL-CONVERGENT.md` | Regole della fase convergente (critica avversariale, Informational Neutrality Gate) |
| `skills/SKILL-COMMON.md` | Comportamenti comuni (reuse-first, convenzioni) |
| `skills/SKILL-PIPELINE.md` | Come le skill si passano il lavoro nella pipeline |
| `skills/SKILL-REGRESSION.md` | Anti-pattern e regressioni note da non reintrodurre |
| `skills/SKILL-WRITER.md` | Convenzioni per scrivere/modificare le skill |

## Contesto minimo per leggere questi file

- Lo stato "cosa vuole l'utente" vive in `.mw/desiderata.md` (non incluso):
  versioni incrementali con `Status: DRAFT | FROZEN`. Solo una FROZEN approvata
  esplicitamente dal Director autorizza il lavoro operativo.
- Le skill si riferiscono a script locali (`scripts/mw-iterative-deliberate.py`,
  `scripts/mw-ask.py`) e a file di progetto (`plans/INDEX.md`, `CANON.md`)
  che non fanno parte di questo mirror.
- I documenti sono in italiano; i template di prompt interni in inglese.
