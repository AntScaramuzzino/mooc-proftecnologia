# ProfTecnologIA — piattaforma MOOC di Antonio Scaramuzzino

Catalogo statico in stile Coursera che raccoglie più MOOC sotto un unico dominio.
Zero backend, zero database: stessa filosofia del MOOC esistente e di `mooc-builder`.

## Cosa c'è in questa cartella

- `index.html` — la homepage-catalogo (self-contained, nessuna dipendenza esterna).
- `corsi.json` — il **registro dei corsi**: l'unica cosa da modificare per aggiungere/togliere un corso.
- `README.md` — questo file.

Apri `index.html` con doppio clic per vedere il prototipo. Funziona anche da `file://`
grazie a un fallback dei dati incorporato; quando è pubblicato online legge `corsi.json`.

## Architettura proposta per il repo "platform"

```
mooc-platform/                 ← un solo repo, un solo dominio
├── index.html                 ← catalogo (questo file)
├── corsi.json                 ← registro dei corsi
├── assets/                    ← logo, css/js condivisi del catalogo
├── ia-inclusiva/              ← corso 1 (output di mooc-builder)
├── valutazione-formativa/     ← corso 2
├── competenze-digitali/       ← corso 3
└── vercel.json                ← header di caching (riusa quello attuale)
```

Risultato sul dominio:
- `tuodominio.it/` → catalogo
- `tuodominio.it/ia-inclusiva/` → corso
- `tuodominio.it/valutazione-formativa/` → corso

## Come si aggiunge un nuovo corso

1. Genera lo scheletro: `mooc-builder new nuovo-corso --moduli 5`
2. Riempi i contenuti (dispense, quiz, flashcard, glossario…).
3. Builda: `mooc-builder build nuovo-corso`
4. Copia l'output in una sottocartella del repo platform: `nuovo-corso/`
5. Aggiungi un blocco a `corsi.json` (vedi schema sotto).
6. `git push` → Vercel pubblica. Il catalogo si aggiorna da solo.

## Schema di un corso in `corsi.json`

```json
{
  "id": "slug-univoco",
  "titolo": "Titolo del corso",
  "sottotitolo": "Una riga descrittiva",
  "descrizione": "2-3 frasi per la card del catalogo.",
  "autore": "Nome Cognome",
  "durata_ore": 6,
  "moduli": 5,
  "livello": "Base | Intermedio | Avanzato",
  "lingua": "it",
  "area": "Categoria (genera i filtri del catalogo)",
  "tag": ["parola", "chiave"],
  "colore": "#6B4FE0",
  "icona": "🤖",
  "stato": "pubblicato | in-arrivo",
  "url": "/slug-univoco/"
}
```

`area` alimenta automaticamente i filtri del catalogo. `stato: "in-arrivo"` mostra la card
come "in arrivo" senza link attivo — utile per annunciare corsi futuri.

## Limiti noti (scelta "catalogo statico")

- Nessun account utente unico: i progressi restano in `localStorage`, per-browser e per-corso.
- Niente sincronizzazione cross-device né iscrizioni centralizzate.
- Gli attestati restano gestiti dall'app Apps Script esistente.

Per superare questi limiti servirebbe un vero LMS con backend — fuori dallo scope attuale.
```
