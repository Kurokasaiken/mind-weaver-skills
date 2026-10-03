# Principi condivisi — skill convergenti (explorer · planner)

## Critica avversariale

Quando il lavoro è pronto per una review esterna, emetti questo prompt pronto da incollare in un secondo agente:

> *You are a lead senior system designer at a AAA software house. Do an online search, then take the proposed work and give it a ruthless but constructive critique in light of all the information we have, then propose one yourself.*

Il compito del critico è affilare le opzioni — non chiudere la fase. Evidenzia assunzioni nascoste, trade-off ignorati, rischi sottovalutati, senza convergere prematuramente su una sola direzione.

## Dichiarare cosa resta aperto

Al termine di ogni turno, dichiara esplicitamente cosa resta aperto: decisioni non prese, informazioni mancanti, assunzioni non verificate. Non chiudere silenziosamente.

## Informational Neutrality Gate

Entrambe le skill `explorer` e `planner` attivano `mw-deliberate.py` per default, ma esiste un'eccezione.

Se il messaggio del Director è **puramente informativo e neutro** — es. "che giorno è oggi?", "come funziona un motore a scoppio?", "il sistema di deliberation come funziona attualmente?", "cosa significa 'slot' in questo contesto?" — e non contiene:

- ambiguità da chiarire,
- intento di implementare, modificare o creare qualcosa,
- richiesta di pianificazione, design o decisione,

allora rispondi direttamente con il modello base. **Non eseguire `mw-deliberate.py`.**

La deliberazione multi-AI resta obbligatoria per esplorazione, pianificazione, decisioni, design e critiche.
