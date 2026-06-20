# NotebookLM priamo z kódu (a z nahrávky rovno tasky)

Návod k slidom **"NotebookLM priamo z kódu"** a **"Z nahrávky rovno tasky v Basecampe"** z decku *Claude Runs My Life*.

Cieľ má dve úrovne:

1. **Základ.** Prestaneš klikať v NotebookLM webe. Máš jeden priečinok `notebooklm-sources/` v projekte. Hodíš tam PDF, poznámku, prepis alebo zoznam URL. Jeden príkaz to celé nahrá do tvojho notebooku. Potom sa notebooku pýtaš priamo z kódu.
2. **Combo.** Z nahrávky porady vytiahneš s Claudom čo treba spraviť a tie úlohy ti rovno založí ako tasky do Basecampu. Z porady do to-do bez prepisovania.

> Toto je verejný návod. Nie sú v ňom žiadne osobné tokeny ani dáta. Funguje s tvojím vlastným Google účtom a tvojím NotebookLM.

---

## Prečo to robiť takto

Web NotebookLM je fajn na pozeranie. Ale keď chceš pracovať so zdrojmi opakovane a hlavne z nich niečo spraviť, klikanie ťa zdržuje. Toto je tá istá sila, len z kódu, a napojená na ďalšie nástroje.

1. **Jeden priečinok = pravda.** Čo je v `notebooklm-sources/`, to je v notebooku. Žiadne ručné uploady jeden po druhom.
2. **Tvoj Claude Code to postaví za teba.** Nemusíš písať kód. Vložíš mu prompt nižšie a on nainštaluje CLI, naviguje ťa cez prihlásenie a vyrobí sync skript.
3. **Tvoj účet, tvoj token.** Prihlásiš sa svojím Google účtom. Token žije lokálne na tvojom Macu, nie v cudzej službe.

---

## Najrýchlejšia cesta. Vlož toto svojmu Claude Code

Skopíruj celý blok nižšie a pošli ho svojmu Claude Code. Ono spraví zvyšok.

```
Napoj ma na NotebookLM tak, aby som vedel pracovať priamo z kódu. Konkrétne:

1. Nainštaluj NotebookLM CLI: pip install notebooklm-py a potom notebooklm skill install.

2. Naveď ma cez prihlásenie. Spustím notebooklm login v mojom Termináli (ja, nie ty,
   lebo to čaká na Enter). Prihlásim sa Google účtom, počkám na homepage NotebookLM,
   prepnem sa do Terminálu a stlačím Enter. Potom over notebooklm list, či token funguje.

3. Vytvor mi v tomto projekte priečinok notebooklm-sources/ a malý sync skript
   notebooklm_sync.py, ktorý:
   - prejde všetky súbory v notebooklm-sources/ (pdf, txt, md, docx)
   - prečíta aj urls.txt v tom priečinku (jedna URL alebo YouTube link na riadok)
   - nahrá každý zdroj do zvoleného notebooku cez notebooklm source add
   - vedie si .synced.json so zoznamom toho, čo už bolo nahraté, aby nevznikali duplikáty
   - vypíše čo pridal a čo preskočil

4. Ukáž mi jeden príkaz na pridanie všetkého (python notebooklm_sync.py --notebook <id>)
   a jeden príklad ako sa potom notebooku spýtam otázku z kódu (notebooklm ask "...").

Token nedávaj nikam do cloudu. Audio rieš podľa sekcie nižšie, zvyšok z kódu.
```

Tvoj Claude Code z toho vyrobí appku na mieru tvojho projektu. Keď niečo padne, povedz mu chybu a on to doladí.

---

## Audio: dve cesty

NotebookLM CLI **audio nahrať nevie**, audio sa do notebooku dá pridať len cez web UI. Máš preto dve možnosti, vyber podľa toho či ti vadí jeden web klik.

**Cesta A. NotebookLM si audio prepíše sám.** Nahrávku nahráš cez web (notebooklm.google.com → Add source → upload). NotebookLM ju interne prepíše a obsah je hneď queryovateľný z kódu cez `notebooklm ask`. Žiadny Whisper netreba. Jediný háčik je ten jeden manuálny upload.

**Cesta B. Whisper a ostávaš v kóde.** Nahrávku prepíšeš lokálne cez Whisper, prepis ako `.txt` alebo `.md` hodíš do `notebooklm-sources/` a sync ho nahrá automaticky. Žiadny web. Bonus: máš surový prepis ako súbor, vieš ho grepovať aj dať Claudovi priamo.

Prompt na Whisper cestu pre tvoj Claude Code:

```
Pridaj mi do projektu prepis audia cez Whisper. Keď do notebooklm-sources/ hodím
audio súbor (m4a, mp3, wav), skript ho najprv prepíše lokálne cez Whisper do .txt
vedľa neho a až ten .txt sa nahrá do NotebookLM. Audio súbor sám sa nenahráva.
```

---

## Combo. Z nahrávky rovno tasky v Basecampe

Keď už máš obsah nahrávky v NotebookLM (alebo ako prepis), toto je tá najsilnejšia časť. Z porady spravíš rozdanú prácu.

Reťazec:

1. **Daj zdroj.** Nahrávka alebo prepis je v NotebookLM.
2. **Pochop.** Spýtaš sa `notebooklm ask "kto má čo spraviť do kedy, vráť ako zoznam s vlastníkom a termínom"`. Claude vytiahne jasné action items aj s citáciami.
3. **Založ tasky.** Claude ti tasky najprv navrhne, po tvojom OK ich rovno vytvorí v Basecampe (priradí, dá termín).

Prompt pre tvoj Claude Code:

```
Z môjho NotebookLM notebooku (nahrávka/prepis porady) vytiahni action items: kto,
čo, do kedy. Najprv mi ich ukáž ako zoznam na schválenie. Po mojom OK ich založ ako
tasky do Basecampu do projektu <názov>. Priraď vlastníkov a termíny. Nič nezakladaj
bez môjho OK.
```

> **Pozor.** Tasky sa nikdy nezakladajú potichu. Claude vždy najprv navrhne, ty potvrdíš, až potom vznikajú. Rovnaký safety pattern ako pri emailoch.

Toto u nás beží cez Basecamp. Funguje to rovnako aj s Asana, Linear, Notion či ClickUp, ak má tvoj Claude Code napojený ich connector. Pre Basecamp treba mať nastavený Basecamp prístup, NotebookLM časť je univerzálna.

---

## Čo dostaneš

Po dobehnutí máš:

```
tvoj-projekt/
  notebooklm-sources/        ← sem hádžeš zdroje
    klient-brief.pdf
    porada.txt               ← prepis (z Whisperu alebo ručný)
    urls.txt                 ← URL a YouTube linky, jeden na riadok
  notebooklm_sync.py         ← jeden príkaz nahrá všetko
  .synced.json               ← pamätá si čo už je nahraté
```

Workflow odvtedy:

1. Hodíš nový súbor alebo URL do `notebooklm-sources/`.
2. `python notebooklm_sync.py --notebook <id>` nahrá len to nové.
3. `notebooklm ask "konkrétna otázka, daj mi SK štruktúrovanú odpoveď s číslami"`.
4. Pri porade. „vytiahni action items a po mojom OK založ tasky do Basecampu".

---

## Čo CLI vie a nevie

- **Vie** pridať: PDF, text, Markdown, Word, URL, YouTube, Google Doc/Slides/Sheets.
- **Nevie** nahrať audio. Audio cez web UI (Cesta A), alebo prepis cez Whisper (Cesta B).
- `notebooklm ask` drží konverzáciu, takže sa dá pýtať follow-up.

---

## Keď prihlásenie zlobí

Najčastejší problém je zaseknutý profil prehliadača. Príznak: `Authentication expired or invalid` aj keď si prihlásený, alebo `Opening in existing browser session`. Riešenie: zavri okno Chrome for Testing (Cmd+Q) a spusti `notebooklm login` znova. Tvoj Claude Code ti s tým poradí, len mu povedz tú hlášku z Terminálu.

---

*Súčasť decku [Claude Runs My Life](https://dxfnt.github.io/claude-runs-my-life/). Go Beyond.*
