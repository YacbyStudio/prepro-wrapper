# Předávka: O2 Wrapped – úpravy podle prepro (po připomínkách klienta)

Zadání pro Claude Code u vývojářů. Popisuje, co se v designu změnilo, a jak to přenést do aplikace. Referenční implementace je webová maketa v tomto repu (`index.html`), commit `ca6038c`.

## Zdroje pravdy
- **Design:** Figma *Wrapped-2*, stránka **„prepro verze“** – https://www.figma.com/design/IfriFOzqaYfNPSIKYtOQEh/Wrapped-2?node-id=154-986
  | Obrazovka | Figma node |
  |---|---|
  | Intro (7.17.1b) | `154:1746` |
  | Story 1 – hovory od začátku roku (7.17.1c) | `154:1798` |
  | Story 2 – hovory za 6 měsíců (7.17.1d) | `154:1860` |
  | Story 3 – data (7.17.1e) | `154:1917` |
  | Souhrn / sdílení (7.17.2a) | `154:1976` |
  | Díky (7.17.3) | `154:2043` |
- **Animace a chování:** maketa `index.html` (ve Figmě animace nejsou). Diff změn: `git show ca6038c`.
- Rozměry níže jsou v bodech rámce 375×844. Font On Air (`fonts/`).

## Pozor: výška řádku On Air
Figma počítá „line-height: auto“ u On Air jako ~1,4× velikosti písma. Prohlížeč (a pravděpodobně i iOS/Android) dává u stejného nastavení jen ~1,15×. **Výšky řádků proto nastavte explicitně podle tabulky níže**, jinak se celé rozvržení posune o několik bodů.

| Styl (Figma) | Písmo | Velikost / výška řádku |
|---|---|---|
| Black italic / Large text | On Air Black Italic | 36 / 44, tracking −0,4 |
| Black italic / Num Large | On Air Black Italic | 54 / 76, tracking −0,4 |
| Black italic / H1 | On Air Black Italic | 28 / 39, tracking −0,4 |
| Black italic / H3 | On Air Black Italic | 20 / 28 (citát), 20 / 24 (karta) |
| Black italic / Caption | On Air Black Italic | 12 / 16 |
| HL / H4 | On Air Bold | 18 / 25 |
| H5 (tlačítka) | On Air Bold | 16 |
| Body 1 | On Air Regular | 16 / 22 |
| Body 2 | On Air Regular | 14 / 22 |

## Změny po obrazovkách

### Intro (`154:1746`)
- Blok nadpis + podtitulek: x 32, **y 265**, šířka 311, centrováno, mezera 56.
- Nadpis: **Large text 36/44** (dřív 32). Zalamuje se do 3 řádků: „Podívejme se, jak / jste letos byli s O₂ / ve spojení!“.
- Podtitulek: **HL/H4 18/25** (dřív 15), šířka 219. Text **„Svůj mobil jsi používal↵celý rok 2026.“** (opraveno z „používali“, zalomení je vynucené).
- „Klepnutím pokračujete“: Body 2, y 764 – beze změny.

### Stories (`154:1798`, `154:1860`, `154:1917`)
- Popisek obrazovky (Body 1, 16): x 16, y 127.
- Progress bar: **16 bodů od okrajů** (dřív 11), mezera mezi segmenty 4, výška 3.
- Úvodní věta bloku: **HL/H4 18/25** (dřív 15), centrovaná. První blok y **237**.
- Řádek hodnot: o **16** níž (y 278), výška boxu 76.
  - Číslo **Num Large 54/76** (dřív 64), jednotka **H1 28/39** (dřív 22).
  - Mezera číslo → jednotka **10**, mezi dvěma hodnotami (32 h · 40 min) **20**.
  - Box jednotky končí 10 bodů nad spodkem boxu čísla → účaří čísla i jednotky lícují.
- Druhý blok: **40** pod koncem řádku hodnot (úvodní věta y 394, hodnoty y 435).
- **Jednotky zkráceny:** „spojených hovorů“ → **„hovorů“**, „telefonních čísel“ → **„čísel“**.
- Citát „To vás řadí mezi top x %…“: **Black Italic 20/28, kurzívou** (dřív bez kurzívy), tracking 0, šířka 248, centrováno, **y 591**.
- Story 3 (poslední): primární tlačítko „Pokračovat“ y 728 – beze změny.

### Souhrn (`154:1976`)
- Nadpis „Sdílejte váš rok s O₂↵s ostatními“: H1 28/39, **y 116** (dřív 124).
- Karta: **295 × 408** (dřív 270 × 370), y 226 (32 pod nadpisem), radius 30, centrovaná.
  - „Můj rok 2026 s O₂“: Caption 12/16, x 24, y 24.
  - Řádek hodnot y **88**, výška 66: číslo **54** (dřív 42), jednotka 28; číslo → jednotka **6**, mezi hodnotami **16**.
  - Popisek („volání“, „dat“): **H3 20/24** (dřív 16), 4 pod řádkem hodnot (y 158).
  - Druhá položka: hodnoty y 202 (20 pod popiskem), popisek y 272.
  - Logo O₂ 49 × 49, 24 od pravého a spodního okraje.
- **PNG karty pro sdílení** musí mít stejnou geometrii (295 × 408 @3x = 885 × 1224). V maketě viz `renderCardPng()`.
- Tlačítka „Sdílet“ (primární) + „Pokračovat“ (textové) – beze změny.

### Díky (`154:2043`)
- Logo O₂ 135 × 135: x 133, y 218 – beze změny.
- Nadpis „Díky, že jste s námi“: H1 28/39, **y 442** (dřív ~412).
- Podtitulek: Body 1 16/22, 16 pod nadpisem, text **„Chcete udělat radost svým blízkým,↵máme pro vás Voucher.“** (dřív „Chcete-li…“, zalomení je vynucené).
- Tlačítko „Zobrazit voucher“: spodní hrana 50 nad spodkem – beze změny.

## Animace (beze změny, pro úplnost)
Všechny texty nastupují stejně: průhlednost 0 → 1 za **480 ms (ease)** a posun 16 → 0 bodů za **620 ms, cubic-bezier(.2,.8,.2,1)**.

| Obrazovka | Časování od vstupu na obrazovku |
|---|---|
| Intro | nadpis 200 ms, podtitulek 900 ms |
| Story | blok *i*: úvodní věta 200 + i·1500 ms, hodnoty +350 ms; čísla se načítají od 0 za **900 ms** (easeOutCubic); citát po posledním bloku; tlačítko poslední story +700 ms po citátu |
| Souhrn | nadpis 100 ms, karta 350 ms (scale .92 → 1, rotace −4° → 0, posun 24 → 0), položky 700 + i·350 ms (s načítáním čísel), houpnutí karty v 1000 ms (2,2 s, rotateY ±16° + odlesk), tlačítka 700 + n·350 + 300 ms |
| Díky | logo O₂ (Lottie) 250 ms + rozostření 40 → 0 za 560 ms, nadpis 750 ms, podtitulek 950 ms, tlačítko 1250 ms; bubliny na pozadí v bezešvé 15s smyčce (`img/bubbles/bubbles.json`) |
| Pozadí | video smyčka na intru a stories, při vstupu rozostření 28 → 0 a scale 1,12 → 1 za 1,2 s; přechod mezi obrazovkami crossfade 350 ms |

**Nové u načítání čísel:** číslice jsou proporcionální (jako ve Figmě), ne tabulkové. Aby se řádek během načítání nehýbal, rezervujte číslu předem šířku jeho finální hodnoty a zarovnejte ho doprava (maketa: `animateCountUp()`, `min-width`).

`prefers-reduced-motion` / systémové omezení pohybu: bez posunů, jen krátké prolnutí (200 ms), čísla rovnou finální.

## Data (texty, které posílá backend)
Změněné výchozí texty (viz `DEFAULT_DATA` v `index.html`):
```js
intro.sub:                          'Svůj mobil jsi používal\ncelý rok 2026.'
stories[0].blocks[1].values[0].unit: 'hovorů'
stories[1].blocks[0].values[0].unit: 'čísel'
thanks.sub:                         'Chcete udělat radost svým blízkým,\nmáme pro vás Voucher.'
```
`\n` = vynucené zalomení (v maketě `white-space: pre-line`). Delší jednotky (např. „spojených hovorů“) se dál smí zalomit na 2 řádky – poslední řádek musí sedět na účaří čísla.

## Kontrola (akceptace)
- Každá obrazovka položená přes Figma rámec 375×844 sedí do ±2 bodů (texty, hodnoty, karta, tlačítka).
- Nadpis intra se zalamuje do 3 řádků jako ve Figmě, podtitulek do 2.
- Během načítání čísel se řádek hodnot horizontálně nehýbe; konečná šířka odpovídá Figmě.
- Sdílené PNG vypadá stejně jako karta na obrazovce.
- Citáty jsou kurzívou.

## Otevřené body
- **Pozadí share karty:** ve Figmě je (`wrapper_sharecard_bg_dark.webp` z CDN O2) o něco světlejší než `img/card-bg.jpg` v maketě. Do aplikace použijte asset z Figmy / CDN.
- **Lottie loga na obrazovce Díky:** maketa načítá `lottie/o2-logo-intro.json`, v pracovní složce je teď jen `lottie/o2-logo.json` – před nasazením sjednotit.
