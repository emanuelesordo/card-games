# Tavolo — Card Games

Web app mobile-first per giochi di carte italiani, destinata a GitHub Pages.

## Stato reale

- **Briscola locale giocabile**: 2, 3 o 4 partecipanti totali (un umano e avversari CPU); mazzo italiano di 40 carte, versione 3 giocatori con 39 carte rimuovendo un due; 4 giocatori a squadre alternate; assegnazione prese e 120 punti complessivi.
- **Carte trevigiane**: in questa prima versione le carte sono *segnaposto tipografici* per i semi italiani, non illustrazioni originali trevigiane.
- **Burraco**: presente come voce della home ma **non ancora giocabile**.
- **Lobby multiplayer, partite private e codice di accesso**: **non implementati**, richiedono il backend.
- **Briscola CPU**: avversari basilari, non un'IA avanzata.
- **Partite locali**: non vengono salvate e si perdono ricaricando la pagina.

## Avvio e pubblicazione

Non servono dipendenze: `index.html` si apre direttamente nel browser. Per GitHub Pages: Settings > Pages > Deploy from a branch > `main`, root `/`. L'URL previsto, dopo l'attivazione di Pages, è https://emanuelesordo.github.io/card-games/.

## Architettura online prevista

GitHub Pages ospita solo il frontend. Utilizzare Supabase Auth anonima, database PostgreSQL, Realtime per notifiche e funzioni RPC/Edge Functions come autorità esclusiva sulle mosse.

Schema concettuale:
- `rooms`: identificativo, nome, visibilità, codice privato memorizzato in forma non reversibile, gioco, posti, stato.
- `room_players`: stanza, identità anonima autenticata, nickname, posto, presenza e squadra.
- `matches`: stato autoritativo, mazzo e mani segrete, turno, punteggio.
- `match_events`: storico delle azioni con numero progressivo e controllo anti-replay.

Requisiti di sicurezza: **non pubblicare le mani avversarie**, non fidarsi delle mosse calcolate dal browser, RLS, accesso privato ai codici, turni atomici lato server, riconnessione basata su sessione autenticata e protezione da doppie azioni.

## Passi successivi

1. Configurare il progetto Supabase dedicato e implementare autenticazione anonima, lobby pubblica/privata e sincronizzazione in tempo reale.
2. Spostare il motore della Briscola sul backend; validare mosse, prese e rientro da disconnessione; aggiungere illustrazioni originali del mazzo trevigiano con licenza adatta.
3. Realizzare il Burraco italiano completo con configurazione 2/4, pozzetti, combinazioni, burraco pulito/semipulito/sporco, pinelle, jolly, chiusure e punteggi; testare separatamente le varianti regolamentari.
4. Aggiungere test automatici, persistenza delle partite, feedback accessibili e controlli touch per tablet.

## Limitazioni e test

La verifica automatizzata end-to-end dei diversi dispositivi, della pubblicazione GitHub Pages e del multiplayer **non è ancora stata effettuata**. Questo repository è un prototipo iniziale, non una release multiplayer completa.
