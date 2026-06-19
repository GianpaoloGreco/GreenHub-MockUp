# Percorso IMPACT: flusso step sequenziali per sblocco certificato livello 1

## Mockup di riferimento

- Percorso IMPACT (pagina step): https://gianpaologreco.github.io/GreenHub_MockUp/percorso.html
- Certificato IMPACT (pagina certificato): https://gianpaologreco.github.io/GreenHub_MockUp/certificato-impact.html

## Contesto

Quando un utente si registra a GreenHub, ottiene un certificato di **livello 0** (membro registrato). Per passare a **livello 1** (certificato attivo, comunicabile all'esterno), deve completare il Percorso IMPACT: una sequenza di 4 contenuti con domande di riflessione.

Il certificato di livello 0 ha molte sezioni bloccate/limitate. Solo dopo il completamento del percorso l'utente puo comunicare il certificato e vedere gli attestati della gamification agganciati.

## Flusso utente

1. L'utente arriva sulla pagina del certificato (`certificato-impact.html`)
2. Vede il certificato in stato "livello 0" con un invito a completare il percorso
3. Clicca "Inizia il percorso" e atterra su `percorso.html`
4. Vede 4 step in sequenza (lo step N+1 e bloccato finche N non e completato):
   - **Step 1**: Leggi il Report ESG 2025 (report PDF, 15 min)
   - **Step 2**: Guarda il Webinar "ESG per PMI: da dove iniziare" (video, 45 min)
   - **Step 3**: Completa il corso "Fondamenti ESG" (4 moduli, ~3 ore)
   - **Step 4**: Guarda "Come misurare l'impatto ESG nella tua PMI" (video, 18 min)
5. Per ogni step:
   - Clicca sulla card, si apre un pannello laterale (slide panel da destra)
   - Vede: descrizione del contenuto, dettagli (formato, durata, relatori), CTA per fruire il contenuto
   - Sotto il contenuto, c'e una **domanda di riflessione** (NON un quiz)
   - Le domande non hanno risposta giusta/sbagliata, servono a mappare le preferenze dell'utente
   - L'utente deve selezionare una risposta per poter cliccare "Segna come completato"
6. Completati tutti e 4 gli step, la vista cambia automaticamente alla **vista completamento**:
   - Banner "Certificato IMPACT sbloccato" con CTA verso la pagina certificato
   - Sezione "GreenHub ha piantato 100 alberi certificati" (azione collettiva)
   - Due opzioni "Vuoi fare di piu?":
     a. **Dona al traguardo collettivo** (importi 10/25/50/altro EUR, certificazione aggiuntiva)
     b. **Azione personalizzata dal Marketplace** (link a marketplace.html)
7. Da questo momento il certificato passa a livello 1

## Dettagli tecnici importanti

- **Stato percorso**: salvato in localStorage (`gh_percorso` = array di indici completati, `gh_preferences` = oggetto con risposte)
- **Sblocco sequenziale**: lo step N si sblocca solo se tutti gli step precedenti sono completati
- **Card layout**: colonna singola, immagine a sinistra + testo a destra (su desktop), impilate su mobile
- **Pannello laterale**: slide panel fisso a destra (520px, max 92vw), con overlay scuro
- **Domande di riflessione**: 4 opzioni per step, nessuna risposta giusta, testo e opzioni forniti dal backend
- **I contenuti dei 4 step** (testi, descrizioni, domande) verranno forniti come dati statici nel primo rilascio

## Scope

- **Tocca**: `percorso.html` (nuova pagina), `certificato-impact.html` (aggiungere stato livello 0 e link al percorso)
- **Non toccare**: dashboard.html, gamification, news, marketplace

## Criteri di accettazione

- [ ] La pagina percorso mostra 4 step in sequenza, con blocco/sblocco corretto
- [ ] Ogni step apre un pannello laterale con contenuto + domanda di riflessione
- [ ] L'utente non puo completare uno step senza selezionare una risposta alla domanda
- [ ] Il progresso persiste (localStorage) tra sessioni
- [ ] Al completamento di tutti gli step, la vista cambia in "completato" con banner + azioni
- [ ] La pagina certificato mostra stato livello 0 pre-percorso e livello 1 post-percorso
- [ ] Le card degli step rispettano il design system (bg-black, card #1A1A1A, primary #10B981, font Inter)
- [ ] Il pannello laterale si chiude con click sull'overlay o tasto Escape

## Dipendenze

- Nessuna

## Note

- Le domande di riflessione NON sono test di competenza. Non ci sono risposte giuste/sbagliate. Servono a mappare l'orientamento dell'utente per proporgli contenuti e opportunita piu rilevanti in futuro.
- La donazione e il marketplace appaiono SOLO dopo il completamento, mai durante il percorso.
- L'azione collettiva ("GreenHub ha piantato 100 alberi") e un dato condiviso tra tutti gli utenti, non personale. Quando l'azione avviene, compare nel certificato di tutti.
- Il concetto si chiama "Epic Meaning": l'utente partecipa a qualcosa di piu grande facendo la sua parte.
