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
├── css/
│   └── style.css       # Veškeré styly (CSS proměnné, responzivita, formulář)
└── img/
    ├── mira-vlach.jpg   # Fotka organizátora Miry Vlacha (používá o-nas.html)
    └── galerie/         # 31 fotek ze setkání klubu (responzivní grid na o-nas.html)
```

## Důležité technické detaily

### SmartEmailing formulář (kontakt.html)

Formulář na kontaktní stránce odesílá data **přímo na SmartEmailing** servery — slouží k odběru pozvánek. Klíčové údaje:

- **Action URL:** `https://app.smartemailing.cz/public/web-forms-v2/display-form/676293-pz82grjhw5m6copas0gkx02xqtptvxxocfm0b859zkbeqabinp8morokcibjm8idnpuqn9nham2w5znbnmkomrtr8qu48ud4qznc`
- **Account ID:** 676293
- **Pole:** `fields[df_name]`, `fields[df_surname]`, `fields[df_emailaddress]`, `fields[cf_1][]` (checkboxy: Praha=1, Ostrava=4, Online=7)
- **Hidden fieldy:** `referrer`, `sessionid`, `sessionUid`, `_do`

⚠️ **Neměnit action URL, názvy polí ani hodnoty checkboxů** — jsou navázané na SmartEmailing konfiguraci.

### FAPI platební formulář (online.html)

Na stránce online.html je embed **FAPI** formulář pro placenou registraci na webináře:

```html
<script type="text/javascript" src="https://form.fapi.cz/script.php?id=4619387c-121b-4730-b55f-bc7c3ff9aa24"></script>
```

- **FAPI** (form.fapi.cz) = český platební/registrační systém
- Formulář se načítá dynamicky přes JS, generuje platbu + fakturu
- **ID formuláře se mění s každou novou akcí** — při vypisování nového webináře je potřeba od organizátora získat nové FAPI ID a aktualizovat `src` URL ve scriptu
- Formulář není potřeba stylovat — FAPI si renderuje vlastní UI

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

### Obrázky

- **Fotka Miry Vlacha:** `img/mira-vlach.jpg` — stažena z Weebly CDN, cesta v `o-nas.html` ukazuje na lokální soubor
- **Fotogalerie:** `img/galerie/` — 31 fotek ze setkání klubu, zobrazené jako CSS grid na stránce `o-nas.html` (mezi sekcí „Historie klubu" a „Proběhlá setkání")

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
