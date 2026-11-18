# AGENTS.md — Recon Drone

## Contesto

Questa repository contiene il progetto **Recon Drone — Embedded & Robotics**, un robot terrestre a due ruote ispirato al drone da ricognizione standard di *Rainbow Six Siege*.

Il progetto è un hobby e un percorso di apprendimento per una persona che sta riprendendo la programmazione di sistemi e parte con conoscenze iniziali di elettronica e embedded.

## Fonti e priorità

1. Leggi \`docs/00_PROJECT_MASTER.md\` prima di discutere modifiche architetturali, scegliere componenti o proporre nuove funzionalità.
2. Considera **approvate** solo le decisioni indicate esplicitamente come tali nel documento principale.
3. Contrassegna tutte le altre idee come **proposta**, **ipotesi da verificare** oppure **questione aperta**.
4. Se trovi incoerenze fra documenti, segnala il conflitto: non modificarne silenziosamente il significato.
5. Non assumere che il contenuto delle altre conversazioni ChatGPT sia automaticamente aggiornato. Usa la versione presente su GitHub e, quando rilevante, indica il commit o la versione consultata.

## Metodo di progettazione

- Parti dai requisiti e dai criteri di verifica prima di scegliere un'implementazione.
- Spiega il perché delle decisioni e i principali compromessi tecnici.
- Preferisci piccoli esperimenti riproducibili e test indipendenti per ciascun sottosistema.
- Mantieni separati controllo motori, comunicazione di comando, acquisizione video e logica di sicurezza.
- Quando una modifica coinvolge più sottosistemi, esplicita le dipendenze.
- Evita di acquistare o selezionare componenti definitivi prima di averne verificato compatibilità elettrica, meccanica e software.
- Mantieni le spiegazioni didattiche e progressive, senza dare per scontata esperienza avanzata.

## Sicurezza

- Il robot deve fermare i motori alla perdita o scadenza dei comandi.
- Prova i motori inizialmente con le ruote sollevate e alimentazioni adeguate.
- Non alimentare i motori direttamente dai GPIO.
- Preferisci batterie e caricabatterie commerciali protetti e compatibili.
- Tratta il meccanismo di salto come un sottoprogetto da valutare e testare separatamente.
- Rispetta la privacy delle persone riprese dalla telecamera e le regole applicabili all'uso di apparati radio.

## Documentazione e modifiche

- Aggiorna i documenti pertinenti quando viene approvata una decisione.
- Mantieni stabili gli identificatori dei requisiti; se necessario, segnala deprecazioni e sostituzioni.
- Quando saranno necessari, crea ADR (*Architecture Decision Records*) in \`docs/decisions/\` per decisioni con alternative e compromessi significativi.
- Non riscrivere le decisioni passate come se fossero state approvate prima della loro effettiva conferma.
- Evita commit di credenziali, token, password, dati personali o altri segreti.
