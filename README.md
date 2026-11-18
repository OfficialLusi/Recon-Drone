# Recon Drone — Embedded & Robotics

Progetto hobbistico e didattico per progettare e costruire un **robot terrestre da ricognizione a due ruote**, ispirato al drone standard di *Rainbow Six Siege*.

> **Stato:** definizione dei requisiti. Non sono ancora stati scelti hardware, protocolli radio o componenti definitivi.

## Obiettivo

Realizzare un piccolo robot alimentato a batteria, capace di:

- avanzare, arretrare e ruotare sul posto;
- ricevere comandi manuali a distanza, senza cavi;
- acquisire e trasmettere immagini in tempo reale;
- essere guidato anche in **FPV** (*First Person View*), usando il video della telecamera;
- integrare due ruote motrici laterali e un telaio compatto;
- effettuare, nella versione avanzata, un salto controllato.

Il progetto è anche un percorso di apprendimento di programmazione embedded, elettronica, comunicazioni, meccanica e testing.

## Scopo e fasi

1. **Fondamenti e prototipo da banco:** esperimenti su GPIO, PWM, motori e comunicazioni.
2. **Rover controllato a vista:** guida manuale e arresto sicuro alla perdita del comando.
3. **Rover FPV:** telecamera, trasmissione video e guida osservando lo schermo.
4. **Replica meccanica:** carrozzeria compatta ispirata al gioco.
5. **Versione avanzata:** meccanismo di salto, dopo la validazione del rover.

La navigazione autonoma e l'evitamento automatico degli ostacoli sono possibili evoluzioni, **non requisiti della prima versione**.

## Documentazione

- [Documento principale](docs/00_PROJECT_MASTER.md): requisiti approvati, ipotesi, questioni aperte e stato del progetto.
- [Istruzioni per gli agenti](AGENTS.md): come utilizzare la repository durante le attività assistite.
- Documenti di architettura, hardware, firmware e test verranno aggiunti quando saranno necessari.

## Regola di lavoro

**Una decisione proposta non è automaticamente una decisione approvata.**

La repository è la fonte di verità del progetto. Le discussioni in chat possono produrre proposte, ma le decisioni definitive devono essere registrate nei documenti versionati con Git.

## Stato corrente

- [x] Definita la visione generale.
- [x] Confermata la guida manuale e l'integrazione FPV.
- [x] Previsto l'uso in interni ed esterni.
- [ ] Completare i requisiti di controllo e le prestazioni misurabili.
- [ ] Confrontare le architetture hardware e di comunicazione.
- [ ] Costruire il primo prototipo.

## Avvertenza

Il dispositivo è pensato per uso hobbistico e ricognizione non invasiva. Durante le prove, utilizzare un'area controllata, rispettare la privacy altrui e progettare sempre un comportamento sicuro in caso di perdita del collegamento.

---
**Ispirazione:** *Tom Clancy's Rainbow Six Siege* di Ubisoft. Progetto indipendente, non affiliato a Ubisoft.
