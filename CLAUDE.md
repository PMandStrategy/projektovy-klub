# Projektový klub — Statický web

## O projektu

Statický web pro **Projektový klub** (projektovyklub.cz) — nezávislou diskuzní platformu o řízení projektů, kterou od roku 2010 organizuje Mira Vlach.

Web je hostovaný na **GitHub Pages**. Žádný build krok, žádný framework — čisté HTML + CSS.

## Struktura

```
├── index.html          # Úvod (homepage) — hero, benefity, příští termíny, bootcamp, OKR
├── praha.html          # Setkání v Praze — termíny, archiv
├── ostrava.html        # Setkání v Ostravě — termíny, archiv
├── online.html         # Online webináře — aktuální + archiv
├── o-nas.html          # O klubu, pravidla, historie, seznam 106 proběhlých setkání
├── kontakt.html        # Kontakt + SmartEmailing formulář pro odběr pozvánek
└── css/
    └── style.css       # Veškeré styly (CSS proměnné, responzivita, formulář)
```

## Důležité technické detaily

### SmartEmailing formulář (kontakt.html)

Formulář na kontaktní stránce odesílá data **přímo na SmartEmailing** servery. Klíčové údaje:

- **Action URL:** `https://app.smartemailing.cz/public/web-forms-v2/display-form/676293-pz82grjhw5m6copas0gkx02xqtptvxxocfm0b859zkbeqabinp8morokcibjm8idnpuqn9nham2w5znbnmkomrtr8qu48ud4qznc`
- **Account ID:** 676293
- **Pole:** `fields[df_name]`, `fields[df_surname]`, `fields[df_emailaddress]`, `fields[cf_1][]` (checkboxy: Praha=1, Ostrava=4, Online=7)
- **Hidden fieldy:** `referrer`, `sessionid`, `sessionUid`, `_do`

⚠️ **Neměnit action URL, názvy polí ani hodnoty checkboxů** — jsou navázané na SmartEmailing konfiguraci.

### Design systém (css/style.css)

- **Fonty:** Plus Jakarta Sans (body) + DM Serif Display (nadpisy) z Google Fonts
- **Barvy:** definované jako CSS proměnné v `:root` — `--color-primary` (tmavě modrá #1a3a5c), `--color-accent` (červená #e8443a)
- **Responzivita:** breakpoint 768px pro mobilní navigaci
- **Navigace:** sticky header, hamburger menu na mobilu (čistý JS onclick)

### Externí odkazy

Tyto URL se na webu používají a měly by zůstat aktuální:

- `www.strategickybootcamp.cz` — Strategický bootcamp
- `www.okrmastermind.cz` — OKR Mastermind
- `www.skolenipm.cz` — Školení PM (Mira Vlach)
- `www.banka-projektu.cz` — Banka projektů
- `linkedin.com/company/projektovy-klub/` — LinkedIn profil klubu
- GDPR dokument: `docs.google.com/document/d/1GPNy4386yZ_0MS69yGr_9smS4S6Z56MGbb0OvNmY8_Q`

### Obrázek Miry Vlacha

Aktuálně načítaný z Weebly CDN (`projektovyklub.weebly.com/uploads/...`). Ideálně stáhnout lokálně do `img/` a aktualizovat cestu v `o-nas.html`.

## Typické úpravy

### Přidání nového setkání

1. Aktualizovat příslušnou stránku (`online.html`, `praha.html` nebo `ostrava.html`) — přepsat obsah karty
2. Aktualizovat sekci "Příští setkání" na `index.html`
3. Po proběhnutí akce přidat do seznamu na `o-nas.html` (číslo setkání + 1, na začátek `<ol>`)

### Úprava kontaktních údajů

Kontaktní údaje jsou na `kontakt.html` v `.contact-grid` a ve footeru všech stránek.

### Změna stylů

Vše v jednom souboru `css/style.css`. Barvy, fonty a rozměry měnit přes CSS proměnné v `:root`.

## Jazyk

Web je celý v **češtině**. Veškerý obsah i commity pište česky.
