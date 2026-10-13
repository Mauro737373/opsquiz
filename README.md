# OpsQuiz — MVP PWA

Applicazione statica, offline-ready, per quiz di Operations Management. Nessun account, nessun backend e nessun tracker. Progressi salvati nel `localStorage` del browser. Include 43 domande preliminari del capitolo 1 di *Operations Management* (Jacobs & Chase, edizione italiana) derivate dalle schede tratte dalla scansione del libro (pagine 3–21).

## Avvio e installazione

Non basta aprire `index.html` direttamente dalla cartella: le fetch JSON e il service worker richiedono un server.

### Prova locale su PC

Da questa cartella esegui:

```bash
python -m http.server 8000
```

Apri `http://localhost:8000`. Per installare la PWA su PC, usa l'opzione *Installa app* del browser Chromium/Edge, se disponibile.

### Pubblicazione gratuita via GitHub Pages (HTTPS)

1. Crea un repository GitHub (per semplicità `opsquiz`).
2. Carica **il contenuto** di questa cartella nella radice del repository (`index.html`, `questions.json`, `app.js`, ecc.).
3. Vai in **Settings → Pages → Build and deployment → Deploy from a branch**.
4. Seleziona il branch `main` e la directory `/ (root)` e salva.
5. Visita l'URL HTTPS di GitHub Pages che GitHub mostra (di solito `https://<utente>.github.io/opsquiz/`).
6. Da iPhone, apri l'URL in Safari, usa **Condividi → Aggiungi alla schermata Home**. Per le funzioni offline, apri l'app una volta mentre sei online.

**Nota sulla privacy e il copyright:** GitHub Pages pubblica i dati del sito. Questo pacchetto include domande rielaborate, non il PDF integrale. Non caricare scansioni di manuali o dati riservati nel repository pubblico. La PWA non invia i tuoi progressi a GitHub o a un server applicativo.

## Funzioni incluse

- Libreria per argomenti/sottocapitoli.
- Quiz a risposta multipla con quattro opzioni, una corretta.
- Feedback immediato e modalità esame.
- Correzione e risultato finale con pagina del libro.
- Modalità errori da ripassare, fino a risposta corretta successiva.
- Statistiche locali.
- Salvataggio locale persistente ed esportazione/importazione progressi JSON.
- Importazione di set di domande in JSON con controllo minimo dello schema.
- Cache offline con Service Worker (dopo il primo accesso online).

## Limiti del primo MVP

- **Non genera automaticamente quiz dai PDF dentro il browser.** Le scansioni vanno elaborate separatamente e convertite in `questions.json`; il file JSON può essere importato dall'interfaccia. Questa scelta serve anche a controllare le citazioni e gli errori nelle scansioni.
- Domande e risposte corrette del primo set derivano da una versione precedente delle schede di studio, ma **non sono state verificate una a una con trascrizione OCR e confronto editoriale formale**. La pagina originale è sempre indicata. Le alternative scorrette sono formulate appositamente; non sono citazioni dirette.
- Nessuna sincronizzazione automatica tra iPhone e PC: per spostare i risultati, usare Esporta/Importa progressi.
- Se cambi i file JS/JSON dopo la pubblicazione, incrementa `CACHE` in `sw.js` affinché il nuovo contenuto offline venga riscaricato.

## Schema di importazione nuove domande

```json
{
  "questions": [
    {
      "id": "JC02-001",
      "book": "Jacobs & Chase · Operations Management",
      "chapter": "Capitolo 2",
      "section": "2.1 - Titolo nel libro",
      "page": 24,
      "question": "Domanda controllata sul PDF?",
      "options": ["Risposta corretta", "Distrattore A", "Distrattore B", "Distrattore C"],
      "correct": 0,
      "explanation": "Risposta corretta, coerente con il testo e verificabile alla pagina indicata.",
      "kind": "Concetto",
      "status": "Verificata"
    }
  ]
}
```

`correct` è l'indice della risposta giusta (0–3). Ogni ID deve essere univoco. Dopo aver importato un JSON nell'app, i quiz si aggiungono alla libreria **del browser corrente**. Per distribuire gli stessi nuovi quiz su tutti i dispositivi, unisci le nuove domande al file `questions.json` e pubblica una nuova versione con cache aggiornata.

## Struttura

- `index.html`: pagina iniziale.
- `style.css`: grafica responsive.
- `app.js`: quiz, salvataggio, report, import/export.
- `questions.json`: banca dati iniziale.
- `sw.js`: cache offline.
- `manifest.webmanifest` e `icons/`: installazione come PWA.

Questo progetto è un prototipo personale di studio, non un prodotto ufficiale degli editori dei manuali.
