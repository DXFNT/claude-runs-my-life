# Ako napojíš NotebookLM priamo do kódu

Návod k slidu **"NotebookLM priamo z kódu"** z decku *Claude Runs My Life*.

Cieľ: prestaneš klikať v NotebookLM webe. Máš jeden priečinok `notebooklm-sources/` v projekte. Hodíš tam PDF, poznámku, prepis alebo zoznam URL. Jeden príkaz to celé nahrá do tvojho notebooku. Potom sa notebooku pýtaš priamo z kódu.

> Toto je verejný návod. Nie sú v ňom žiadne osobné tokeny ani dáta. Funguje s tvojím vlastným Google účtom a tvojím NotebookLM.

---

## Prečo to robiť takto

Web NotebookLM je fajn na pozeranie. Ale keď chceš pracovať so zdrojmi opakovane, klikanie ťa zdržuje. Toto je tá istá sila, len z kódu.

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

Token nedávaj nikam do cloudu. Audio sa cez CLI nahrať nedá, to ostáva na web UI,
zvyšok rieš z kódu.
```

Tvoj Claude Code z toho vyrobí appku na mieru tvojho projektu. Keď niečo padne, povedz mu chybu a on to doladí.

---

## Čo dostaneš

Po dobehnutí máš:

```
tvoj-projekt/
  notebooklm-sources/        ← sem hádžeš zdroje
    klient-brief.pdf
    poznamky.md
    urls.txt                 ← URL a YouTube linky, jeden na riadok
  notebooklm_sync.py         ← jeden príkaz nahrá všetko
  .synced.json               ← pamätá si čo už je nahraté
```

Workflow odvtedy:

1. Hodíš nový súbor alebo URL do `notebooklm-sources/`.
2. `python notebooklm_sync.py --notebook <id>` nahrá len to nové.
3. `notebooklm ask "konkrétna otázka, daj mi SK štruktúrovanú odpoveď s číslami"`.

---

## Čo CLI vie a nevie

- **Vie** pridať: PDF, text, Markdown, Word, URL, YouTube, Google Doc/Slides/Sheets.
- **Nevie** nahrať audio. Audio nahrávky pridávaš cez web UI (notebooklm.google.com → Add source). Zvyšok rieši kód.
- `notebooklm ask` drží konverzáciu, takže sa dá pýtať follow-up.

---

## Keď prihlásenie zlobí

Najčastejší problém je zaseknutý profil prehliadača. Príznak: `Authentication expired or invalid` aj keď si prihlásený, alebo `Opening in existing browser session`. Riešenie: zavri okno Chrome for Testing (Cmd+Q) a spusti `notebooklm login` znova. Tvoj Claude Code ti s tým poradí, len mu povedz tú hlášku z Terminálu.

---

*Súčasť decku [Claude Runs My Life](https://dxfnt.github.io/claude-runs-my-life/). Go Beyond.*
