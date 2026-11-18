# 00 — Documento principale del progetto

**Progetto:** Recon Drone — Embedded & Robotics  
**Versione del documento:** 0.1  
**Stato:** definizione dei requisiti  
**Ultimo aggiornamento:** 2026-11-18

> Questa è la fonte di verità per **requisiti, decisioni e questioni aperte**. Le proposte non diventano decisioni finché non vengono esplicitamente approvate.
>
> Gli identificatori in questa prima versione sono **normalizzati** per evitare duplicazioni emerse durante la discussione preliminare. Da questa versione in poi restano stabili.

## 1. Visione

Progettare e realizzare un **robot terrestre mobile (UGV)** compatto, ispirato al drone standard di *Rainbow Six Siege*.

Il robot avrà **due ruote motrici laterali**, sarà alimentato a batteria, riceverà **comandi manuali a distanza** e trasmetterà **video in tempo reale**. Il controllo **FPV** (guida tramite le immagini della telecamera, senza necessità di vedere direttamente il robot) è un requisito obbligatorio.

Una versione finale avanzata dovrà includere un **salto controllato**. La navigazione autonoma rimane un possibile ampliamento futuro.

Il progetto ha inoltre uno scopo didattico: imparare programmazione embedded in C/C++, elettronica, protocolli di comunicazione, controllo motori, meccanica, integrazione e testing.

## 2. Ambito e priorità

| Fase | Traguardo | Stato |
| --- | --- | --- |
| M0 — Fondamenti | Sperimentazione al banco su I/O, controllo motori e comunicazioni | Pianificato |
| M1 — Rover manuale | Avanza, arretra, ruota e si arresta in sicurezza; controllo inizialmente a vista | Pianificato |
| M2 — Rover FPV | Trasmette video e può essere guidato guardando lo schermo | Pianificato |
| M3 — Replica meccanica | Corpo compatto a due ruote laterali con aspetto ispirato al gioco | Pianificato |
| M4 — Salto | Salto controllato e ripresa del funzionamento dopo l'atterraggio | Pianificato, avanzato |

La suddivisione in fasi non modifica i requisiti finali: serve a realizzarli e verificarli progressivamente.

## 3. Requisiti funzionali approvati

| ID | Requisito | Fase minima |
| --- | --- | --- |
| RF-01 | Il robot deve muoversi in avanti. | M1 |
| RF-02 | Il robot deve muoversi all'indietro. | M1 |
| RF-03 | Il robot deve poter ruotare sul posto in entrambe le direzioni. | M1 |
| RF-04 | Il robot deve ricevere comandi remoti tramite collegamento wireless, senza cavi verso l'operatore. | M1 |
| RF-05 | Il robot deve acquisire immagini tramite una telecamera integrata. | M2 |
| RF-06 | Il robot deve trasmettere immagini in tempo reale all'operatore. | M2 |
| RF-07 | Il robot deve operare con alimentazione a batteria. | M1 |
| RF-08 | In caso di perdita o scadenza dei comandi validi, il robot deve arrestare i motori entro un intervallo di sicurezza da definire. | M1 |
| RF-09 | Nella versione avanzata, il robot deve poter effettuare un salto controllato. | M4 |
| RF-10 | La guida ordinaria deve essere completamente manuale: i movimenti dipendono dai comandi dell'operatore. | M1 |
| RF-11 | Il robot deve poter essere guidato in modalità FPV, osservando il video e senza contatto visivo diretto. | M2 |

**Nota:** l'arresto automatico di sicurezza (RF-08) è consentito e obbligatorio anche nella modalità di guida manuale.

### Funzioni non ancora approvate come obbligatorie

- Controllo proporzionale di velocità e sterzata, anziché comandi a velocità fissa.
- Curve durante l'avanzamento o la retromarcia (auspicabili, ma da definire formalmente).
- Accelerazione e decelerazione progressive.
- Telemetria della batteria e qualità del collegamento.
- Navigazione autonoma, percorsi predefiniti ed evitamento automatico degli ostacoli: **possibili sviluppi successivi**, fuori dall'ambito iniziale.

## 4. Aspetti fisici concordati

| ID | Descrizione | Stato |
| --- | --- | --- |
| RM-01 | Corpo compatto e trasportabile. | Obiettivo confermato; dimensioni da definire |
| RM-02 | Due ruote motrici laterali. | Confermato |
| RM-03 | Telecamera integrata nel corpo. | Confermato |
| RM-04 | Elettronica e batteria a bordo. | Confermato |
| RM-05 | Aspetto finale riconoscibile e ispirato al drone del gioco. | Confermato; fedeltà estetica da specificare |
| RM-06 | Protezione di componenti ed elettronica durante l'uso previsto. | Obiettivo da dettagliare |

**Questione meccanica aperta:** due ruote laterali non garantiscono da sole la stabilità. Dovremo valutare geometria, eventuale punto di appoggio aggiuntivo e comportamento durante salto e atterraggio.

## 5. Scenario operativo

- **Ambienti:** interni ed esterni — **confermato**.
- **Terreno iniziale:** superfici generalmente regolari con piccole irregolarità — **ipotesi di progetto non bloccante**, da affinare nella fase meccanica.
- **Ostacoli maggiori, erba, ghiaia:** da valutare successivamente, non requisiti iniziali.
- **Pioggia, acqua, polvere e condizioni climatiche:** prestazioni ancora da specificare; non presumere impermeabilità.
- **Prove iniziali:** controllo a vista in ambiente controllato.
- **Uso finale:** controllo FPV obbligatorio.

## 6. Requisiti prestazionali ancora da concordare

**Nessuno dei valori nella tabella seguente è ancora un vincolo approvato.** Sono ipotesi discusse da confermare mediante analisi e prove.

| Metrica | Ipotesi iniziale | Stato |
| --- | --- | --- |
| Autonomia | Almeno 15 minuti | Non approvata |
| Portata di controllo | Almeno 10 metri | Non approvata |
| Risoluzione video | Almeno 640 × 480 | Non approvata |
| Fluidità video | Almeno 15 fps | Non approvata |
| Latenza video | Inferiore a 300 ms | Non approvata |
| Tempo massimo per arresto in assenza di comandi | 500 ms | Non approvata |
| Velocità massima | Da definire | Aperto |
| Dimensioni e massa | Da definire | Aperto |
| Altezza e ripetibilità del salto | Da definire | Aperto |

## 7. Decisioni tecniche aperte

| Tema | Decisione |
| --- | --- |
| Microcontrollore e processore | Da selezionare. ESP32-S3 discusso come piattaforma didattica, **non scelto definitivamente**. |
| Canale di controllo | Da valutare: Wi-Fi, ESP-NOW, radiocomando RC o altra soluzione. |
| Canale video | Da scegliere; può essere condiviso o separato dal controllo. |
| Dispositivo operatore | Da scegliere: PC, smartphone, gamepad, radiocomando o combinazione. |
| Motori, driver e ruote | Da dimensionare dopo i requisiti meccanici e prestazionali. |
| Camera e video | Da definire in base a latenza, ingombro, alimentazione e qualità. |
| Batteria e regolatori | Da dimensionare dopo la stima dei consumi. |
| Materiale e costruzione del telaio | Da valutare. |
| Meccanismo di salto | Da progettare come sottosistema avanzato. |

**Principio architetturale:** il protocollo radio è una **scelta implementativa**, non un requisito funzionale. Il software di controllo motori dovrebbe rimanere il più possibile indipendente dal canale di comunicazione.

## 8. Verifiche previste

| ID | Verifica |
| --- | --- |
| TV-01 | Il robot esegue avanti, indietro, rotazione in entrambi i versi e arresto sotto controllo manuale. |
| TV-02 | I comandi funzionano senza collegamento fisico all'operatore. |
| TV-03 | La perdita dei comandi provoca l'arresto entro la soglia che verrà approvata. |
| TV-04 | L'operatore può percorrere un tracciato semplice guardando solo il flusso video, in un'area di prova sicura. |
| TV-05 | L'alimentazione a batteria garantisce il funzionamento per il tempo minimo che verrà approvato. |
| TV-06 | La versione finale avanzata esegue un salto e rimane operativa dopo l'atterraggio. |

I test saranno completati con procedure e soglie quantitative quando i rispettivi requisiti saranno definiti.

## 9. Registro delle decisioni

| Data | Decisione / conferma | Stato |
| --- | --- | --- |
| 2026-11 | Progetto di un robot terrestre a due ruote laterali ispirato al drone standard del gioco. | Approvato |
| 2026-11 | Movimento avanti/indietro, rotazione sul posto e controllo remoto. | Approvato |
| 2026-11 | Acquisizione e trasmissione video; guida FPV obbligatoria nel risultato finale. | Approvato |
| 2026-11 | Guida completamente manuale; eventuale autonomia solo in futuro. | Approvato |
| 2026-11 | Uso previsto in interni ed esterni. | Approvato |
| 2026-11 | Piccole irregolarità del terreno come riferimento iniziale, non vincolo bloccante. | Provvisorio |
| 2026-11 | Salto come obiettivo della versione finale avanzata. | Approvato |
| 2026-11 | Wi-Fi e ESP32-S3 non sono ancora decisioni definitive. | Aperto |

## 10. Prossime decisioni

1. Definire **come l'operatore comanda movimento e velocità** (comandi discreti o proporzionali).
2. Concordare alcune **prestazioni minime misurabili**, soprattutto per FPV e autonomia.
3. Derivare le alternative architetturali dai requisiti, senza anticipare scelte di componenti.

---
**Manutenzione:** aggiornare questo documento quando una decisione viene approvata; registrare le scelte architetturali significative in documenti ADR dedicati quando necessario.
