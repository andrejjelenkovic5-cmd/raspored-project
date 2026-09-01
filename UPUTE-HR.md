# Raspored — projekt (web + desktop)

Ovaj repozitorij sadrži **dvije odvojene verzije** iste aplikacije:

```
raspored-project/
├── web/        <- ovo se rucno drag&drop-a na Netlify (kao i do sad)
├── desktop/    <- ovo GitHub Actions gradi u macOS .app/.dmg
└── .github/    <- automatika za gradnju desktop verzije
```

**Ove dvije verzije su potpuno neovisne.** Možeš graditi/mijenjati
jednu bez da diraš drugu. Obje se spajaju na istu Supabase bazu.

---

## Web verzija (`web/`)

Ništa se ne mijenja u tvom dosadašnjem radnom toku:
1. Netlify → drag & drop cijeli sadržaj `web/` foldera (kao i do sad)
2. Gotovo — link ostaje isti (dizajn-raspored.mmtim.com)

Ovaj folder možeš i ignorirati na GitHubu ako želiš — GitHub Actions
ga ne dira, ne gradi ga, samo je ovdje kao arhiva/pregled izvornog koda.

---

## Desktop verzija (`desktop/`) — macOS aplikacija

### Korak 1 — napravi repo na GitHubu (samo prvi put)

1. https://github.com/new → ime npr. `raspored-project` → **Private**
2. Ne dodaji README/gitignore (već imamo)
3. "Create repository"

### Korak 2 — pošalji kod na GitHub (samo prvi put)

U Terminalu, unutar ovog foldera (`raspored-project`):

```bash
git init
git add .
git commit -m "Prva verzija - web + desktop"
git branch -M main
git remote add origin https://github.com/TVOJ-USERNAME/raspored-project.git
git push -u origin main
```

(Zamijeni `TVOJ-USERNAME` — vidjet ćeš točnu adresu na GitHub stranici
tvog novog repozitorija, kopiraj je odande da budeš siguran da je točna.)

### Korak 3 — pokreni gradnju macOS app-a

1. Na GitHubu, u repozitoriju, otvori tab **"Actions"**
2. Klikni **"Build macOS App (desktop/)"** na lijevoj listi
3. Klikni **"Run workflow"** (desno) → zeleni gumb **"Run workflow"**
4. Pričekaj 5-10 minuta — vidjet ćeš žuti krug (u tijeku), pa zelenu
   kvačicu (gotovo) ili crveni X (greška — pošalji mi log ako se desi)

### Korak 4 — preuzmi gotov `.app`

1. Klikni na završeni "run" (onaj sa zelenom kvačicom)
2. Skrolaj do dna → **"Artifacts"** → **"raspored-desktop-macos"**
3. Preuzmi (zip), otpakiraj
4. Prvi put: **desni klik na app → Open** (zbog "nepoznat programer"
   upozorenja). Nakon toga, obican dvoklik radi normalno.

**Da — nakon ovoga imaš pravi `.app` fajl koji instaliraš/pokrećeš na
Macu kao svaku drugu aplikaciju.** Možeš ga staviti u Applications
folder kao i bilo koji drugi program.

---

## Kad god poželiš noviju verziju desktop app-a

1. Zamijeni `desktop/src/index.html` novijom verzijom (istom kao i
   `web/index.html` — obje bi trebale biti identične nakon svakog
   ažuriranja)
2. `git add . && git commit -m "update" && git push`
3. Ponovi Korak 3 i 4 gore

## Napomena

Zbog `paths: ["desktop/**"]` u workflow fajlu, gradnja se **automatski**
pokrene i pri svakom pushu koji mijenja nešto unutar `desktop/` foldera
(ne treba ručno kliktati "Run workflow" svaki put ako ne želiš — samo
pushaš i pričekaš, gradnja krene sama). Promjene samo u `web/` folderu
NE pokreću desktop gradnju (jer se ništa u desktop/ nije promijenilo).
