# Raspored — Dizajn tim

Web aplikacija za vođenje rasporeda dizajn tima. Frontend se spaja direktno na Supabase (shema `raspored`, izolirana od postojećih tablica za godišnji odmor u istom projektu).

## Sadržaj paketa

- `index.html` — cijela aplikacija
- `favicon.svg`, `favicon.ico`, `apple-touch-icon.png`, `icon-192.png`, `icon-512.png` — ikone
- `site.webmanifest`
- `netlify.toml` — sigurnosni headeri, caching

## Deploy na Netlify (drag & drop)

1. app.netlify.com → **Add new site → Deploy manually**
2. Povuci SVE datoteke iz ovog zipa (raspakirane) u prozor za upload
3. Gotovo — dobiješ link odmah

Nema build koraka, nema environment varijabli.

## Prikazi

- **Dan** — precizan raspored po pola sata, zaposlenici kao stupci, povlačenje/razvlačenje stavki
- **3 dana / Tjedan** — zaposlenici kao redovi, dani kao stupci, brzi pregled i povlačenje stavki između dana/zaposlenika
- Filter zaposlenika iznad prikaza (klik na chip uključuje/isključuje)
- Dashboard odmah pri otvaranju prikazuje tjedni raspored (bez dodatnih klikova)

## Lozinka

Lozinka se provjerava usporedbom SHA-256 otiska protiv vrijednosti u tablici `raspored.app_config`. Ovo je "meka" zaštita (odvraća slučajne posjetitelje), a stvarna zaštita podataka je Supabase Row Level Security nad shemom `raspored` — anon ključ u kodu ima pristup samo toj shemi, ne i `public` (godišnji).

### Promjena lozinke

Treba je ažurirati u bazi (Supabase SQL Editor):
```sql
update raspored.app_config
set value = '<novi_sha256_hex>'
where key = 'password_hash';
```
(SHA-256 heš možeš izračunati npr. u terminalu: `echo -n "nova_lozinka" | shasum -a 256`)
