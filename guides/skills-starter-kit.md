# Workshop zadanie: nahoď si Dexfinity Skills Starter Kit

Návod k slidu **"Skills Starter Kit"** z decku *Claude Runs My Life*.

Cieľ: tvoj Claude Code je za pár minút nabitý všetkým čo v Dexfinity používame. 60+ custom
skillov a 3 memory packy. Audity, Google Ads, SEO, social, sales playbook, CEO rozsekni,
Lovable setup, práca s hubom a tímom.

> Toto je verejný návod. Skilly žijú v privátnom internom repe (treba DXFNT prístup).
> Memory packy sú verejné a čisté. Žiadne emaily, faktúry, sumy ani klientske dáta.

---

## Workshop zadanie (toto si spravte)

1. Nainštaluj si skilly z `DXFNT/claude-skills`.
2. Nainštaluj si 3 memory packy.
3. Over že to funguje. V novom chate napíš *„Aké skilly mám k dispozícii?"*.
4. Skús jeden naživo. Napríklad *„sprav audit jednej stránky"* alebo *„daj mi pripomienku zajtra o 10"*.

Hotové za 10 minút. Kto má problém s prístupom, krok 1 nižšie to rieši.

---

## Čo potrebuješ pred štartom

1. **Claude Code nainštalovaný.** Ak ešte nemáš, [návod tu](https://docs.claude.com/claude-code).
   Rýchlo: `npm install -g @anthropic-ai/claude-code`.
2. **GitHub účet + DXFNT prístup.** Bez toho `git clone` privátneho repa zlyhá (404).
   Rieši krok 1.

---

## Krok 1. GitHub prístup

1. Nemáš GitHub účet? Založ si ho na [github.com/signup](https://github.com/signup).
2. Napíš **Palimu** svoj GitHub username alebo `@dexfinity.com` email. Pridá ťa do
   organizácie a do tímu, ktorý má prístup k skillom.
3. Keď ti príde pozvánka do organizácie, **klikni Accept**. Až potom `git clone` prejde.

> Test či máš prístup: otvor [github.com/DXFNT/claude-skills](https://github.com/DXFNT/claude-skills).
> Ak vidíš repo, si dnu. Ak vidíš 404, ešte nie si pridaný, ozvi sa Palimu.

---

## Krok 2. Nainštaluj skilly (60+)

Jeden príkaz. Naklonuje repo a spustí inštalačný skript, ktorý skilly nakopíruje do
`~/.claude/skills/`.

```bash
git clone https://github.com/DXFNT/claude-skills.git
cd claude-skills
./install.sh
cd ..
```

Inštalátor si pred prepísaním spraví zálohu tvojich existujúcich skillov, takže oň
neprídeš. Po dobehnutí máš v `~/.claude/skills/` všetko.

---

## Krok 3. Nainštaluj memory packy (3, verejné)

Memory packy dodávajú Claudovi kontext a pravidlá, ktoré si pamätá medzi konverzáciami.
Brand poskytuje jazyk, UX gramatiku, audit pack celé odseky.

```bash
mkdir -p ~/.claude/memory
for repo in dexfinity-ai-audit-memory dexfinity-brand-memory dexfinity-ux-memory; do
  git clone https://github.com/DXFNT/$repo.git /tmp/$repo
  cp /tmp/$repo/memory/*.md ~/.claude/memory/
done
```

| Pack | Čo robí | Kedy sa zíde |
|---|---|---|
| `dexfinity-brand-memory` | Farby, fonty, logo, min veľkosti | Vždy keď Claude robí vizuál (web, email, deck, social) |
| `dexfinity-ai-audit-memory` | Celý AI Ads Audit playbook (gold standard) | Pri auditoch (`ai-audit`, `ai-audit-deep`) |
| `dexfinity-ux-memory` | UX patterns z reálnych auditov | Pri landing page, pricing, interaktívnom UI |

---

## Krok 4. Over že to sedí

1. Spusti nový Claude Code session (`claude` v termináli).
2. Napíš: *„Aké custom skilly mám k dispozícii?"*. Claude by mal vymenovať veci ako
   `ai-audit`, `dex-design`, `gads-copy-doctor`, `rozsekni`, `dex-sales-pro`.
3. Skús jeden naživo. Napríklad:
   - *„daj mi pripomienku zajtra o 10 zavolať klientovi"* → spustí `reminder`
   - *„sprav audit tejto stránky [url]"* → spustí `audit-page`

Funguje? Hotovo. Si nabitý rovnakým arzenálom ako zvyšok tímu.

---

## Ako sa skilly volajú

- **Väčšina sa spúšťa automaticky** keď Claude detekuje trigger. Nemusíš si pamätať
  názvy. Napíš čo chceš (*„sprav audit pre Oxalis"*) a Claude vyberie správny skill sám.
- **Vieš ich volať aj priamo** cez `/názov-skillu`, aj keď sa nezobrazujú v autocomplete.
- **Každý skill má vlastný `SKILL.md`** v `~/.claude/skills/<name>/` s popisom triggerov.

---

## Checklist

- [ ] Mám GitHub účet a prijatú pozvánku do DXFNT
- [ ] `github.com/DXFNT/claude-skills` mi nezobrazuje 404
- [ ] `./install.sh` dobehol, skilly sú v `~/.claude/skills/`
- [ ] Memory packy sú v `~/.claude/memory/`
- [ ] V novom session Claude vymenuje skilly a jeden naživo zafungoval

---

*Súčasť decku [Claude Runs My Life](https://dxfnt.github.io/claude-runs-my-life/). Go Beyond.*
