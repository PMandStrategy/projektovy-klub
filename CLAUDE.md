# Projektový klub — Statický web

## O projektu

Statický web pro **Projektový klub** (projektovyklub.cz) — nezávislou diskuzní platformu o řízení projektů, kterou od roku 2010 organizuje Mira Vlach.

Web je hostovaný na **GitHub Pages** s vlastní doménou **https://projektovyklub.cz**. Žádný build krok, žádný framework — čisté HTML + CSS.

Soubor `CNAME` v kořenu repozitáře obsahuje doménu `projektovyklub.cz`. Nesmí se mazat — GitHub Pages ho potřebuje pro nasměrování vlastní domény.

## Struktura

```
├── index.html          # Úvod (homepage) — benefity, příští termíny, bootcamp, OKR
├── praha.html          # Setkání v Praze — termíny, archiv
├── ostrava.html        # Setkání v Ostravě — termíny, archiv
├── online.html         # Online webináře — aktuální + archiv
├── o-nas.html          # O klubu, pravidla, historie, galerie, seznam 106 proběhlých setkání
├── kontakt.html        # Kontakt + SmartEmailing formulář pro odběr pozvánek
├── js/
│   └── main.js         # Hamburger menu animace (linkován na všech stránkách)
├── css/
│   └── style.css       # Veškeré styly (CSS proměnné, responzivita, formulář)
└── img/
    ├── logo-basic-PK-min.png  # Logo klubu (v navigaci na všech stránkách)
    ├── mira-vlach.jpg         # Fotka organizátora Miry Vlacha (o-nas.html)
    └── galerie/               # 31 fotek ze setkání klubu (CSS grid + GLightbox na o-nas.html)
```

## Designový systém

### Princip

Web je primárně **černobílý** — bílé pozadí, tmavý text. Barvy z loga se používají jen jako střídmé akcenty:
- **Zelená (--teal #3DB88C)** — odkazy, aktivní stavy v navigaci, CTA tlačítka, badge „Online", accent-line, tečky u programu
- **Fialová (--purple #7B6BAA)** — JEŠTĚ střídměji: border u druhého řečníka, tečka u programu, badge pro Prahu

**Nikdy** nepoužívej plnobarevné hero bannery ani velké barevné plochy.

### Barevná paleta (CSS proměnné v :root)

```
--teal: #3DB88C           (z loga — P)
--teal-light: #E1F5EE     (zesvětlená zelená pro pozadí)
--teal-dark: #085041      (tmavá zelená pro text)
--purple: #7B6BAA         (z loga — K)
--purple-light: #F5F4FA   (zesvětlená fialová)
--purple-dark: #3C3489    (tmavá fialová pro text)
--ink: #111               (hlavní text)
--ink-mid: #444           (sekundární text)
--ink-soft: #777          (terciární text, labely)
--ink-faint: #aaa         (hints, placeholdery)
--border: #e8e8e8         (hlavní bordery)
--border-light: #f2f2f2   (jemné oddělovače)
--surface: #fafafa        (pozadí karet, sekcí)
--white: #fff             (pozadí stránky)
```

### Fonty

- **Instrument Sans** (body) + **Newsreader** (nadpisy, serifový) z Google Fonts
- Google Fonts link: `https://fonts.googleapis.com/css2?family=Instrument+Sans:wght@400;500;600;700&family=Newsreader:opsz,wght@6..72,400;6..72,500;6..72,600&display=swap`

### Typografická hierarchie

- **h1 (název stránky/akce):** font-display, 2.4rem, weight 500, letter-spacing -0.02em
- **Eyebrow label (.eyebrow):** 0.72rem, uppercase, letter-spacing 0.08em, --ink-faint, weight 600
- **Section label (.section-label):** totéž jako eyebrow, + border-top pro oddělení sekcí
- **Tělo textu:** 0.9rem, --ink-mid, line-height 1.65
- **Odkazy:** barva --ink, podtržení barvou --teal, text-underline-offset 3px

### Navigace

- Sticky header, bílé pozadí, spodní border
- Logo jako `<img>` tag (`img/logo-basic-PK-min.png`, height="32")
- Aktivní odkaz: barva --ink, spodní border 2px --teal
- Neaktivní: barva --ink-soft, hover → --ink + background --surface
- Mobilní hamburger: animace z `js/main.js`, plynulé rozbalení přes max-height

### Stránky bez hero bannerů

Žádné hero bannery. Místo toho:
1. `<hr class="accent-line">` (zelená linka 36px)
2. `<p class="eyebrow">` (uppercase label)
3. `<h1>` (velký serifový nadpis)
4. Volitelně `.lede` odstavec a `.chips` (badge/chipy)

## Konvence pro stránky akcí (online.html, praha.html, ostrava.html)

Při vypisování nové akce se obsah stránky aktualizuje podle následujících pravidel:

### 1. Záhlaví akce

Vždy obsahuje:
- Eyebrow label („Příští setkání")
- Název tématu (velký serifový nadpis, h1)
- Stručný popis (1-2 věty, `.lede`)
- Chipy: typ akce (Online/Praha/Ostrava), datum a čas, cena

### 2. Flexibilní sekce

Ne každá akce má stejnou strukturu. CC rozhodne na základě vstupního textu, které sekce zahrnout:

- **Řečníci** (.speakers-grid) — jen pokud jsou konkrétní řečníci. Počet karet odpovídá počtu řečníků. Pokud je jen diskuze bez řečníků, sekci vynech.
- **Program** (.program-list) — jen pokud je konkrétní program. Pro volnou diskuzi stačí zmínka v popisu.
- **Témata** (.topic-tags) — flex wrap tag chipy. Vždy zahrnout, pokud jsou známá témata.
- **Praktické informace** (.info-table) — vždy zahrnout (datum, místo, kapacita, cena, požadavky).
- **Medailonky** (.bio) — jen pokud jsou řečníci s podrobnějším bio. Volitelné.

### 3. Registrace

Vždy zahrnout:
- Tmavý CTA blok (.cta-block) s textem
- FAPI formulář (script přímo v toku HTML)
- Podpis Miry Vlacha pod formulářem

### 4. Po proběhnutí akce

1. Aktualizovat stránku akce (přepsat na novou, nebo zobrazit `.no-event` s „aktuálně není vypsáno žádné téma")
2. Přidat záznam o proběhlé akci do `o-nas.html` (číslo +1, na začátek seznamu `<ol>`)
3. Aktualizovat sekci „Příští setkání" na `index.html`

⚠️ CC by měl **VŽDY** připomenout/zkontrolovat, zda byl záznam přidán do `o-nas.html`.

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

⚠️ **FAPI `<script>` nesmí být obalený v žádném `<div>`** — musí být přímo v toku HTML. Pokud je obalený, FAPI nedokáže detekovat svou vlastní URL a formulář se nenačte.

### Logo

- Soubor: `img/logo-basic-PK-min.png`
- Použití: `<a href="index.html" class="site-logo"><img src="img/logo-basic-PK-min.png" alt="Projektový klub" height="32"></a>`
- Linkováno v navigaci na všech 6 stránkách

### JavaScript

- **`js/main.js`** — hamburger menu animace, používá se na všech 6 stránkách (linkován před `</body>`)
- **GLightbox 3.3.0** z CDN — lightbox pro fotogalerii, pouze na `o-nas.html`

⚠️ **Při přidávání nových stránek nezapomenout linkovat `js/main.js` před `</body>` a Google Fonts v `<head>`.**

### Obrázky

- **Logo:** `img/logo-basic-PK-min.png` — v navigaci na všech stránkách
- **Fotka Miry Vlacha:** `img/mira-vlach.jpg` — na `o-nas.html` v person-card
- **Fotogalerie:** `img/galerie/` — 31 fotek ze setkání, CSS grid + GLightbox na `o-nas.html`

### Externí odkazy

Tyto URL se na webu používají a měly by zůstat aktuální:

- `www.strategickybootcamp.cz` — Strategický bootcamp
- `www.okrmastermind.cz` — OKR Mastermind
- `www.skolenipm.cz` — Školení PM (Mira Vlach)
- `www.banka-projektu.cz` — Banka projektů
- `linkedin.com/company/projektovy-klub/` — LinkedIn profil klubu
- GDPR dokument: `docs.google.com/document/d/1GPNy4386yZ_0MS69yGr_9smS4S6Z56MGbb0OvNmY8_Q`

## Typické úpravy

### Přidání nového setkání

1. Aktualizovat příslušnou stránku (`online.html`, `praha.html` nebo `ostrava.html`) — přepsat obsah stránky podle konvencí výše
2. Aktualizovat sekci „Příští setkání" na `index.html`
3. Po proběhnutí akce přidat do seznamu na `o-nas.html` (číslo setkání + 1, na začátek `<ol>`)

### Úprava kontaktních údajů

Kontaktní údaje jsou na `kontakt.html` v `.info-table` a ve footeru všech stránek.

### Změna stylů

Vše v jednom souboru `css/style.css`. Barvy, fonty a rozměry měnit přes CSS proměnné v `:root`.

## Jazyk

Web je celý v **češtině**. Veškerý obsah i commity pište česky.
