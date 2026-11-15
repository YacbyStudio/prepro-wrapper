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

## Animace a časování

Všechny časy jsou v ms **od vstupu na obrazovku** (t = 0). Zdroj: `index.html` (konstanty `BLOCK_GAP`, `LEAD_TO_VALUE`, `COUNT_UP_MS`, `CARD_ITEM_GAP`, `READ_HOLD`, funkce `buildIntro/buildStory/buildSummary/buildThanks`).

**Nástup každého prvku** (texty, řádky hodnot, citát, tlačítka): průhlednost 0 → 1 za **480 ms (ease)** a zároveň posun nahoru za **620 ms, cubic-bezier(.2,.8,.2,1)**. Výchozí posun: nadpisy a úvodní věty 16 bodů, řádky hodnot 20, citát 12, nadpis souhrnu a texty Díky 14, tlačítka 16.

**Načítání čísel:** začne současně s nástupem řádku hodnot, běží **900 ms** z 0 na finální hodnotu, easing easeOutCubic (`1 − (1 − p)³`), zaokrouhleno na celá čísla, formát cs-CZ (mezera jako oddělovač tisíců). Číslice jsou proporcionální (jako ve Figmě), proto číslu předem rezervujte šířku finální hodnoty a zarovnejte ho doprava, aby se řádek nehýbal (maketa: `animateCountUp()`, `min-width`).

### Intro
| Čas | Co se stane |
|---|---|
| 200 | nadpis |
| 900 | podtitulek |
| 1 580 | „Klepnutím pokračujete“ |
| — | **čeká na tap** (žádný automatický posun) |

### Story (obecně, blok *i* = 0, 1, …)
| Čas | Co se stane |
|---|---|
| 200 + i·1500 | úvodní věta bloku |
| 550 + i·1500 | řádek hodnot + start načítání čísel (900 ms) |
| 200 + n·1500 | citát (n = počet bloků) |
| konec nástupu | s citátem: 200 + n·1500 + 700 + 400; bez citátu: 200 + n·1500 + 100 + 400 |
| konec nástupu + **2 500** | **automatický posun** na další story (čas na čtení `READ_HOLD`) |

Progress bar: aktivní dílek se plní lineárně od 0 do 100 % po celou dobu story (nástup + čas na čtení).

### Story – konkrétně s aktuálními daty
| | Story 1 (2 bloky + citát) | Story 2 (2 bloky) | Story 3 (1 blok + citát, poslední) |
|---|---|---|---|
| úvodní věta 1 | 200 | 200 | 200 |
| čísla 1 (načítání) | 550 → 1 450 | 550 → 1 450 | 550 → 1 450 |
| úvodní věta 2 | 1 700 | 1 700 | – |
| čísla 2 (načítání) | 2 050 → 2 950 | 2 050 → 2 950 | – |
| citát | 3 200 | – | 1 700 |
| tlačítko Pokračovat | – | – | 2 400 |
| konec nástupu | 4 300 | 3 700 | 2 800 |
| **posun na další obrazovku** | **6 800** (auto) | **6 200** (auto) | **čeká na tlačítko** |

### Souhrn
| Čas | Co se stane |
|---|---|
| 100 | nadpis |
| 350 | karta (scale .92 → 1, rotace −4° → 0, posun 24 → 0) |
| 700 | položka 1 + načítání čísel (900 ms) |
| 1 000 | houpnutí karty: 2 200 ms, rotateY 0 → −16° → +13° → −4° → 0 (+ odlesk), jednou |
| 1 050 | položka 2 + načítání čísel |
| 1 750 | tlačítka Sdílet / Pokračovat |
| — | čeká na tlačítko (žádný automatický posun) |

### Díky
| Čas | Co se stane |
|---|---|
| 0 | bubliny na pozadí: prolnutí 1 200 ms, pak bezešvá 15s smyčka (`img/bubbles/bubbles.json`) |
| 250 | logo O₂ – Lottie `lottie/o2-logo.json` (O hotové ve snímku 22, „2“ ve snímku 36 @ 60 fps = 600 ms), web navíc rozostření 40 → 0 za 560 ms |
| 750 | nadpis |
| 950 | podtitulek |
| 1 250 | tlačítko Zobrazit voucher |

### Pozadí (intro + stories)
- Video ve smyčce, při každém vstupu na obrazovku se spustí od začátku s rozostřením 28 → 0 a scale 1,12 → 1 za **1 200 ms** (cubic-bezier(.2,.7,.2,1)).
- Přechod mezi obrazovkami: crossfade **350 ms** (linear).

### Ovládání
- **Tap vpravo** (60 % šířky): na intru a story okamžitě další obrazovka (i během nástupu). Na souhrnu a Díky jen dokončí nástup.
- **Tap vlevo** (40 % šířky): předchozí obrazovka od začátku (ne dál než intro).
- **Podržení** déle než **220 ms**: pauza – zastaví progress bar, odpočet do automatického posunu, video na pozadí i animace; po puštění pokračuje, nepřepíná. (Desktop maketa: i mezerník.)
- **×**: zpět na vstupní obrazovku.

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
- ~~**Lottie loga na obrazovce Díky:** sjednotit název souboru~~ – vyřešeno: maketa i předávka používají `lottie/o2-logo.json` (obsah beze změny proti dřívějšímu `o2-logo-intro.json`).
