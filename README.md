# Claude runs my life

Interný (a možno aj externý) Dexfinity training deck. Reálne workflowy, ktoré
Pavol Adamčák každý deň používa s Claude. **Jeden chat = jeden slide.**

## Live

https://dxfnt.github.io/claude-runs-my-life/

## Navigácia

- `←` `→` alebo `Space` — ďalší / predchádzajúci slide
- `F` — fullscreen
- `Home` / `End` — na prvý / posledný
- URL hash `#0`, `#1`, … — direct link na konkrétny slide

## Slidy

| # | Téma |
|---|---|
| 0 | Cover |
| 1 | Príkaz `odpis mi` — Claude pripraví draft, ja klikám Send |
| 2 | Príkaz `review od` — Claude pýta Google recenzie z reálnych konverzácií |

## Pridanie nového slidu

1. Edit `index.html`
2. Skopíruj posledný `<section class="slide">` blok ako šablónu
3. Zvýš `data-id` atribút a `Slide NN` v hlavičke
4. Commit + push, GitHub Pages sa updatne za pár sekúnd

## Branding

Dexfinity brand. Navy `#05024E`, blue `#0065F7`, teal `#16AB8B`.
Fonty Questrial (headings) + Poppins (body).
Žiadne semafory, žiadne em pomlčky, žiadny bold-bullet pattern.

## Licencia

Dexfinity internal. Public repo na zdieľanie deck-u, kód je MIT-style reusable.
