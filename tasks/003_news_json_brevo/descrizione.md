# News: integrazione articoli da JSON e newsletter Brevo

## Mockup di riferimento

- Home con sezione news: https://gianpaologreco.github.io/GreenHub_MockUp/home.html

## Contesto

Le news della piattaforma vengono alimentate da un sistema esterno che produce file JSON aggiornati settimanalmente (ogni venerdi). I JSON sono ospitati su una pagina dedicata e accessibili via URL diretto (come un'API statica). In piu, va integrata la newsletter tramite Brevo (API gratuita) per l'invio del digest settimanale.

## Fonti dati JSON

L'endpoint base e una pagina web con i seguenti sotto-percorsi:
- `/articles.json` - Lista articoli normalizzati
- `/digest.json` - Digest settimanale completo
- `/newsletter.json` - Contenuto newsletter

Ogni articolo ha questo formato JSON (concordato con lo sviluppatore):

```json
{
  "title": "Titolo dell'articolo",
  "excerpt": "Breve descrizione / sottotitolo",
  "content": "<p>Contenuto formattato in HTML</p>",
  "category": "Normativa|Finanza Green|Energia|...",
  "image": "url_immagine (opzionale)",
  "link": "url_fonte_originale",
  "date": "2025-06-13",
  "tags": ["esg", "pmi", "normativa"]
}
```

## Flusso utente - Articoli/News

1. L'utente nella home vede le news nella sezione dedicata
2. Le news sono una griglia di card con: immagine (se disponibile), categoria, titolo, excerpt, data
3. Cliccando su una card si apre il dettaglio (pannello laterale o pagina dedicata) con il content formattato
4. In fondo al dettaglio: link alla fonte originale e tag
5. Pulsante "Load more" per caricare piu articoli (non mostrare tutti subito)
6. Le news sono visibili solo per utenti registrati/loggati

## Flusso utente - Digest

1. Il digest settimanale appare nel carosello della homepage (hero slider)
2. Cliccando si apre una pagina dedicata con il digest completo
3. Questa e la stessa pagina dove atterra chi clicca il link dalla newsletter email

## Flusso utente - Newsletter

1. L'utente puo iscriversi alla newsletter dal sito pubblico (pre-registrazione)
2. Ogni settimana il sistema prepara la newsletter dal digest JSON
3. La newsletter viene inviata tramite API Brevo
4. Il link nella newsletter porta alla pagina del digest sulla piattaforma
5. Se l'utente non e registrato, vede il titolo + contenuto sfumato + CTA per registrarsi (lead generation)
6. Se l'utente e gia registrato/loggato, vede il contenuto completo

## Integrazione Brevo

- Brevo (ex Sendinblue) ha API gratuite per l'invio newsletter
- Endpoint API: `https://api.brevo.com/v3/smtp/email`
- Serve: API key, lista contatti, template email
- Il contenuto della newsletter viene dal JSON `/newsletter.json`
- Lo sviluppatore deve integrare le API Brevo per:
  - Gestire la lista iscritti (aggiunta contatto su iscrizione)
  - Inviare la newsletter settimanale (cron o trigger manuale)

## Scope

- **Tocca**: `home.html` (sezione news, carosello digest), nuova pagina dettaglio articolo, nuova pagina digest, integrazione API Brevo
- **Non toccare**: percorso.html, certificato-impact.html, dashboard.html, gamification

## Criteri di accettazione

- [ ] Le news si popolano dal JSON remoto (`/articles.json`)
- [ ] Griglia news con card: titolo, excerpt, categoria, data, immagine (se presente)
- [ ] Dettaglio articolo con contenuto formattato e link alla fonte
- [ ] Pulsante "Load more" per paginazione
- [ ] Digest settimanale nel carosello homepage
- [ ] Pagina dedicata per il digest completo
- [ ] Iscrizione newsletter funzionante (API Brevo - aggiunta contatto)
- [ ] Invio newsletter via API Brevo con contenuto dal JSON
- [ ] Utente non registrato che atterra dal link newsletter vede contenuto sfumato + CTA registrazione
- [ ] Gestione errori: se il JSON non e disponibile, mostrare un messaggio di fallback

## Dipendenze

- Nessuna (indipendente dai task 001 e 002)
- Richiede: URL definitivo degli endpoint JSON (fornito da Gianpaolo)
- Richiede: API key Brevo (da configurare)

## Note

- I JSON vengono aggiornati settimanalmente (ogni venerdi). Non serve polling in tempo reale, basta un fetch al caricamento pagina.
- Il campo `image` degli articoli potrebbe essere vuoto. Prevedere un'immagine placeholder in quel caso.
- Il campo `content` e gia formattato in HTML. Va renderizzato cosi com'e (sanitizzare per XSS).
- La pagina del digest e strategica per la lead generation: chi arriva dalla newsletter e non e registrato deve essere invogliato a registrarsi.
- Il carosello homepage e gia esistente, il digest va aggiunto come slide.
