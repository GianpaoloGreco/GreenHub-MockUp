# Gamification: ristrutturazione con Punti GH e traguardi collettivi

## Mockup di riferimento

- Dashboard gamification: https://gianpaologreco.github.io/GreenHub_MockUp/dashboard.html

## Contesto

La gamification attuale ha XP, badge, streak e livelli individuali. Questo sistema va ristrutturato completamente. I badge e i livelli individuali creano confusione con il sistema dei livelli del certificato IMPACT. Il nuovo modello si basa su azioni collettive (Epic Meaning): le azioni di tutti gli utenti alimentano una barra condivisa che sblocca traguardi reali (es. piantumazione alberi, pulizia spiagge) che diventano attestati nel certificato personale.

## Cosa rimuovere

- XP individuali (sostituiti da Punti GH)
- Badge individuali
- Streak giornaliero
- Livelli individuali (il livello e solo quello del certificato)
- Classifica/leaderboard individuale

## Cosa aggiungere/modificare

### Punti GH (GreenHub Points)
- I punti si chiamano "Punti GH" o "GH"
- Sono punti collettivi: le azioni di TUTTI gli utenti alimentano un contatore globale
- Ogni azione (leggere un articolo, scaricare un documento, partecipare a un evento, completare una missione) genera punti GH
- Il totale e visibile nella dashboard come barra di progresso condivisa

### Barra collettiva con roadmap traguardi
- Una barra di progresso che mostra il totale punti GH di tutti gli utenti
- Sotto la barra, una roadmap visuale con milestone:
  - 500 GH, 1.000 GH, 2.000 GH, 5.000 GH, 10.000 GH (valori di esempio)
  - Ogni milestone ha un traguardo associato (es. "GreenHub piantera 200 alberi certificati")
  - I milestone raggiunti si vedono come completati, quelli futuri come bloccati
- Questa barra e UGUALE per tutti gli utenti (dato globale)

### Missioni
- Le missioni restano, ma danno Punti GH invece di XP
- Ogni missione ha un valore in GH e un link alla pagina dove completarla
- Le missioni completate appaiono con opacita ridotta e check verde

### Attestati nel certificato
- Quando un traguardo collettivo viene raggiunto, genera un attestato
- L'attestato e visibile nella pagina del certificato dell'utente
- MA SOLO se l'utente ha un certificato attivo (livello 1+)
- Se l'utente non ha ancora fatto il percorso (livello 0), gli attestati sono accumulati ma non visibili nel certificato
- Nella dashboard c'e una sezione "Nel tuo certificato" che mostra gli attestati sbloccati

### Donazione
- CTA per donare verso il prossimo traguardo collettivo
- La donazione e opzionale, mai obbligatoria
- Chi dona riceve una certificazione aggiuntiva nel proprio certificato

## Flusso utente

1. L'utente apre la dashboard
2. Vede 3 stat card in alto: Punti GH totali, Missioni (completate/totali), stato certificato
3. Sotto, la barra collettiva con il progresso globale e la roadmap dei traguardi
4. CTA "Dona ora" per contribuire al prossimo traguardo
5. Lista missioni attive e completate
6. Sidebar "Nel tuo certificato": mostra gli attestati collettivi sbloccati
7. In basso: riepilogo attivita (articoli letti, documenti scaricati, eventi seguiti, opportunita salvate) e scadenze

## Scope

- **Tocca**: `dashboard.html` (ristrutturazione completa sezione gamification)
- **Non toccare**: percorso.html, certificato-impact.html, news, marketplace

## Criteri di accettazione

- [ ] Rimossi completamente: XP, badge, streak, livelli individuali
- [ ] Stat card mostrano: Punti GH, Missioni, Certificato
- [ ] Barra collettiva con totale globale e percentuale verso il prossimo traguardo
- [ ] Roadmap visuale con milestone e stato (completato/in corso/bloccato)
- [ ] Missioni funzionanti con punti GH e link alle pagine rilevanti
- [ ] Sezione "Nel tuo certificato" con attestati collettivi (visibili solo con certificato attivo)
- [ ] CTA donazione presente e non invasiva
- [ ] La barra collettiva e i traguardi sono dati globali (non per singolo utente)
- [ ] Prossime scadenze e riepilogo attivita mantenuti

## Dipendenze

- Task 001 (Percorso IMPACT): il certificato deve avere livello 0/1 perche gli attestati della gamification si vedono solo con certificato attivo (livello 1+). Si puo sviluppare in parallelo, ma il collegamento "attestati visibili solo con certificato attivo" va coordinato.

## Note

- Due barre separate: una per i certificati rilasciati (nella pagina certificato/percorso), una per le azioni gamification (nella dashboard). NON mescolarle.
- Il punteggio della gamification NON fa salire il livello del certificato. Sono due sistemi separati che si incrociano solo sugli attestati.
- I traguardi non devono essere necessariamente costosi per GreenHub. Es. "giornata pulizia spiagge" costa alla GreenHub ATS, non costa 5.000 EUR reali, ma il valore percepito e alto.
- I valori dei punti e dei traguardi nel mockup sono di esempio. Il backend definira i valori reali.
