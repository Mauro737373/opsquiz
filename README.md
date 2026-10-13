# OpsQuiz 1.1 - Question Quality Update

PWA statica per lo studio del capitolo 1 di *Operations Management* di Jacobs e Chase. Contiene 43 quesiti verificati sulla scansione del capitolo fornita dall'utente (pagine stampate 3-21). Domande, alternative e spiegazioni sono riformulazioni: nell'app sono marcate **Parafrasi del manuale** e ciascuna indica capitolo, sezione e pagina. Non sono incluse pagine del PDF.

## Pubblicare su GitHub Pages

1. Prima della sostituzione, apri la PWA attuale ed esporta i progressi dal riquadro **I tuoi dati**. È una copia di sicurezza, anche se l'aggiornamento mantiene lo stesso archivio locale.
2. Apri il repository [Mauro737373/opsquiz](https://github.com/Mauro737373/opsquiz) e vai alla radice del ramo che alimenta Pages (normalmente `main`).
3. Estrai questo ZIP sul computer. Carica **il contenuto della cartella `operations-quiz-pwa`**, non la cartella stessa, nella radice del repository. Sostituisci i file con lo stesso nome: `index.html`, `style.css`, `app.js`, `questions.json`, `sw.js`, `manifest.webmanifest`, `README.md` e `icons/`.
4. Registra le modifiche con **Commit changes**. Il repository dovrebbe già avere Pages attivo; controlla in **Settings > Pages** che la fonte punti al ramo e alla directory `/ (root)` corretti.
5. Dopo la pubblicazione, apri <https://mauro737373.github.io/opsquiz/> e ricarica la pagina. Se la PWA installata mostra ancora la versione precedente, chiudila e riaprila online; il service worker `opsquiz-static-v1.1` sostituirà la cache precedente. Aggiornare la pagina una seconda volta può essere necessario se la prima visita ha avviato l'installazione del nuovo service worker.
6. Controlla che l'intestazione mostri **1.1 · Offline**, che la libreria contenga **43 domande** e che, dopo una risposta in modalità studio, appaiano spiegazione, dicitura **Parafrasi del manuale** e riferimento a sezione e pagina.

Non caricare il PDF nel repository pubblico. GitHub Pages espone tutti i file del progetto.

## Avvio locale

Apri un terminale nella cartella `operations-quiz-pwa` ed esegui `python -m http.server 8000`, quindi visita `http://localhost:8000`. L'apertura diretta di `index.html` come file locale non consente il caricamento JSON o il service worker.

## Modalità e dati

- **Studio:** la spiegazione appare subito dopo ogni risposta, insieme al riferimento al manuale.
- **Esame:** le soluzioni e le spiegazioni appaiono nella revisione finale, per non rivelare la risposta durante la prova.
- Restano disponibili quiz casuali, per sezione, ripasso degli errori, statistiche locali, esportazione e importazione dei progressi e importazione di ulteriori set JSON.
- I risultati continuano a usare la chiave locale `opsquiz-v1` e gli stessi 43 ID. I punteggi precedenti sono conservati, ma non ricalcolati sulle domande aggiornate. Un avviso nella libreria segnala la presenza di risultati delle versioni precedenti. La cancellazione dei progressi elimina solo le statistiche e non le domande importate.
- L'app non invia risultati a un server e non sincronizza dispositivi diversi. Per trasferire i progressi, usa Esporta e Importa progressi.

## Verifica delle fonti

La scansione comprende le pagine 3-21, con pagina 5 duplicata. I 43 quesiti finali sono stati confrontati con le pagine visibili. La precedente **JC01-037** attribuiva il Just in Time a Toyota, ma la pagina 15 non fa questa attribuzione: il quesito è stato sostituito con uno sul rapporto fra JIT e controllo della qualità totale, documentato nella stessa pagina. **JC01-019** è stato rifatto sulla seconda differenza fra beni e servizi, leggibile a pagina 8. Per **JC01-027** il riferimento più preciso è pagina 12, che riporta l'esempio dello sportello bancario. Non rimangono quesiti segnalati come non verificati nel set finale.

## Formato di nuove domande

Il file JSON deve contenere un array `questions`. Ogni elemento deve avere almeno: `id` univoco, `chapter`, `section`, `page`, `question`, quattro `options` distinte, indice `correct` fra 0 e 3, `explanation`. `book`, `kind` e `status` sono facoltativi. Le spiegazioni importate sono mostrate come **Spiegazione importata**, poiché non sono state verificate insieme al set del capitolo 1.

Il progetto è un supporto personale allo studio e non un prodotto ufficiale dell'editore.
