# Deploy — mooc-proftecnologia

Il catalogo ProfTecnologIA è statico (index.html + corsi.json + vercel.json).
Pubblicazione su GitHub + Vercel, da lanciare **dal Mac** (terminale).

> ⚠️ Da Cowork è stata creata una cartella `.git` incompleta che non era rimovibile
> in cloud. **Primo passo: cancellala e reinizializza git localmente** (comandi sotto).

## 1. GitHub

```bash
cd ~/"Library/CloudStorage/GoogleDrive-antonio.scaramuzzino@coopinrete.it/Drive condivisi/Antonio Scaramuzzino/Corsi/Corso IA come co-pilota nella progettazione della didattica inclusiva/MOOC/mooc-proftecnologia"

rm -rf .git                # rimuove il .git parziale creato in cloud
git init -b main
git add .
git commit -m "feat: catalogo MOOC ProfTecnologIA (2 corsi pubblicati + 3 in arrivo)"
```

Crea il repo remoto. Con GitHub CLI (consigliato, un comando):

```bash
gh repo create mooc-proftecnologia --public --source=. --remote=origin --push
```

Oppure a mano: crea un repo vuoto `mooc-proftecnologia` su github.com, poi:

```bash
git remote add origin https://github.com/AntScaramuzzino/mooc-proftecnologia.git
git push -u origin main
```

## 2. Vercel

**Via web (più semplice):**
1. vercel.com → *Add New…* → *Project*
2. *Import* del repo `mooc-proftecnologia`
3. Framework Preset: **Other** (sito statico, nessuna build)
4. *Deploy*

**Via CLI:**

```bash
npm i -g vercel        # se non già installato
vercel --prod
```

Da qui in poi ogni `git push` su `main` ripubblica automaticamente.

## 3. Aggiungere un corso in futuro

Modifica solo `corsi.json` (vedi schema nel `README.md`), poi `git commit && git push`.
Il catalogo si aggiorna da solo. I singoli corsi restano i loro deploy Vercel separati;
qui si linkano tramite il campo `url`.
