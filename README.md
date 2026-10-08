# 🔊 Lettore Vocale eBook

Web app statica (un solo file `index.html`) che importa un eBook e lo legge ad alta voce
con la sintesi vocale del browser, controllabile con **comandi vocali**:

| Dici | Effetto |
|---|---|
| **"stop"**, ferma, fermati, pausa, basta | si ferma e resta sulla frase corrente |
| **"evidenzia"**, sottolinea, segna | evidenzia in giallo la frase in lettura |
| **"riprendi"**, continua, riparti, leggi | riparte dalla stessa frase |
| avanti / indietro | frase successiva / precedente |
| più veloce / più lento | varia la velocità di 0,2× |

## Caratteristiche

- Import **TXT**, **EPUB** (spine OPF, manuale, via JSZip) e **PDF** (supporto opzionale via pdf.js).
- Nessun server, nessun build step, nessuna dipendenza da installare: solo HTML + CSS + JS.
- Lettura a **frasi singole** (evita il troncamento delle utterance lunghe in Chrome) con
  punto di ripresa sempre preciso.
- **Anti-eco**: ignora i comandi se il microfono capta la voce sintetica in riproduzione.
- **Memoria locale** (`localStorage`): posizione, evidenziazioni, voce e velocità.
- Interfaccia **mobile-first** con tema scuro e controlli grandi; scorciatoie da tastiera
  (`Spazio` = play/pausa, `H` = evidenzia).

## Requisiti

- **Browser: Chrome o Edge.** Il riconoscimento vocale usa `SpeechRecognition`, disponibile
  solo su Chromium. Su Firefox e Safari l'ascolto funziona, ma i comandi vocali no
  (restano i pulsanti Stop / Evidenzia / Riprendi).
- **HTTPS o localhost obbligatori** per il microfono. Pubblicando su Vercel o GitHub Pages
  il problema non si pone: il dominio è già HTTPS.

## Pubblicazione su Vercel

1. Crea un repository su GitHub e carica `index.html` (più questo README).
2. Su [vercel.com](https://vercel.com) → **Add New… → Project → Import Git Repository**.
3. Framework Preset: **Other**. Build Command e Output Directory: **lasciare vuoti**.
4. **Deploy**. Ogni `git push` genera automaticamente un nuovo deploy.

Senza GitHub: `npx vercel` dalla cartella del progetto (deploy diretto).

## Pubblicazione su GitHub Pages

Settings → Pages → Source: *Deploy from a branch* → branch `main`, cartella `/ (root)`.
L'app sarà su `https://<utente>.github.io/<repo>/`.

## Prova in locale

```bash
python3 -m http.server 8000
# apri http://localhost:8000
```

## Note legali

Aprire file EPUB/PDF **protetti da DRM non è possibile**: l'app mostra un messaggio di errore.
Usa solo libri di cui hai il diritto di accesso.
