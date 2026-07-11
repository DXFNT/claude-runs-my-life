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
| 1 | Príkaz `odpis mi`. Claude pripraví draft, ja klikám Send |
| 2 | Príkaz `review od`. Claude pýta Google recenzie z reálnych konverzácií |
| 3 | Personal → team licencia. Pamäť ostáva, connectors si pýtajú handshake |
| 4 | Dexguide content boost. Collabim Holy Grail gap → pipeline článkov |
| 5 | 3 prompty, 1 case study. Raw materiály → live Dexfinity deck |
| 6 | Tomáš pingne, faktúry píšu seba. Full-auto monthly billing pipeline |
| 7 | Kedy Chrome nestačí. Google Docs API namiesto browser automation |
| 8 | Keď klient odchádza, otvor väčšie dvere. Nebshop → Nebbia premium partner |
| 9 | Public repo s vašimi emailmi je trojkrokový problém. GitHub security |
| 10 | Keď audit povie pauznúť, my sa pýtame prečo. DexIQ #27 root cause |
| 11 | Sekrety bez pomlčiek. Bootstrap secrets pipeline za 41 sek |
| 31 | Claude počúva tvoje porady. NotebookLM nahrávka → obohatí dokument |
| 32 | Príprava na budget call za pár minút. Ponuka vs timetrack + stratégia z nahrávky |
| 33 | Druhá firma, druhý tajomník. Samostatný OAuth bot pre ďalší účet za pár minút |
| 34 | Návod: postav si vlastného bota (1/2). Príprava na strane Googlu |
| 35 | Návod: postav si vlastného bota (2/2). Prepojenie s Macom a bezpečnosť |
| 36 | NotebookLM priamo z kódu. Jeden priečinok → sync skript → pýtaš sa z kódu (setup k #31) |
| 37 | Z nahrávky rovno tasky v Basecampe. NotebookLM × Basecamp combo, action items → BC todos |
| 38 | Skills Starter Kit. 60+ skillov + 3 memory packy na jeden install, DXFNT/claude-skills |
| 39 | Z Drivu po schválenie klientom. Fotky → interaktívny deck, klient sám odklikne + notifikácia (BC / WhatsApp) |
| 40 | Redirect gap zachytený. Shopify API + GSC DWD odhalili chýbajúcu vzdelávaciu vrstvu, 142 CSV riadkov pred cutoverom (vino.sk) |
| 41 | Inzerát prepísaný z chatu. WordPress cez API, záloha → prepis → cache purge, web nespadol (dexfinity.com kariéra) |
| 42 | Z rozbitej zmluvy podpis-ready dokument. Reformát na brand štandard, právne porovnanie so vzorom, doplnené ochranné ustanovenia, footer opravený v šablóne |
| 43 | Kde web padá na hubu. 404 audit po migrácii e-shopu cez firemné Google napojenie, HTTP overenie každej adresy, verdikt a task za pár minút |
| 44 | Prierez projektu za 5 minút. Skill project-map zladí objednávku z Drive, tasky z Basecampu a dokumenty na jednu os, nájde objednané služby bez taskov |
| 45 | Prečo lacnie remarketing? Stopa viedla do Googlu. Meta leady za 1,4 € prepojené cez tri platformy, zdroj je podcast kampaň na Googli čo plní pool |
| 46 | Karta #multisport a je vybavené. Mesačný benefit pre celý tím zbalený do jedného triggera v kalendári, náhľad na odsúhlasenie, zvyšok dobehne rutina |
| 47 | Jeden dokument, celý projekt. Klientsky projekt má v Basecampe interný index s linkami na Drive, prezentácie, výstupy aj notebook. Jedno miesto pravdy |
| 48 | Plaud po slovensky, ako sa patrí. Addon je len mikrofón, mozog je nastavenie účtu. Jazyk na Slovak, vlastná šablóna a AI inštrukcie, vypnúť zdieľanie dát |
| 49 | Slovník teraz hovorí aj po česky. 49 chýbajúcich Dexguide hesiel doplnených cez WPML + DeepL za popoludnie, celý glosár 112/112 dvojjazyčný. Nájdi gap, nechaj preložiť, publikuj a over |

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
