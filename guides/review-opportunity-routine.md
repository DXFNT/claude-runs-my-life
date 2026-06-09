# Týždenná rutina: nájdi koho požiadať o Google recenziu

Návod k slidu **"Príkaz review od"** z decku *Claude Runs My Life*.

Cieľ: raz týždenne automaticky prejsť inbox, nájsť ľudí ktorých sa oplatí požiadať
o Google recenziu, poslať si **WhatsApp ping** so zoznamom a návrhom textu recenzie.
Draft čaká v Gmaili. **Send klikáš ty.**

> Verejný, sanitizovaný návod. Bez osobných tokenov a klientskych dát.

---

## Kľúčová lekcia

Nie je to "napíš mi review request". Je to **opportunity-finding rutina**. Systém
ktorý za teba pravidelne číta komunikáciu a sám navrhne príležitosti. Ty len rozhoduješ.

Recenzie majú dvojitú hodnotu: podporujú **klasické vyhľadávanie** aj **AI odporúčania**
(LLM-y citujú miesta s dobrými recenziami).

---

## Ako to funguje

1. **Scheduled scan (1x týždenne).** Pondelok ráno prejde poslednú komunikáciu
   (default okno 14 dní).
2. **Filtre.** Vyhodí interné maily, transakčné/automatické, cold outreach,
   recruiterov, personal admin, a ľudí už požiadaných za posledných 6 mesiacov.
3. **Ranking + dôvod.** Zoradí kandidátov podľa pozitívneho momentu (dodaný projekt,
   poďakovanie, vyriešený problém) a ku každému dá dôvod a suggested angle.
4. **Návrh textu recenzie.** Z kontextu konverzácie navrhne citát, aby človek nemusel
   premýšľať čo napísať.
5. **WhatsApp ping.** Zoznam kandidátov ti príde na WhatsApp (alebo macOS notifikáciu).
6. **Ty otvoríš draft v Gmaili, upravíš, pošleš.** Žiadny auto-send.

---

## Stavebné bloky

- **Scheduled task** (macOS launchd alebo scheduler). Reliabilita: hourly catch-up
  okno + lock file, lebo launchd nespúšťa zmeškané joby po sleepe. Skript drž mimo
  iCloud priečinka (sandbox).
- **Inbox scan** cez Gmail API (readonly scope), targeted query s `newer_than:14d`.
- **WhatsApp ping** napr. cez CallMeBot (`https://api.callmebot.com/whatsapp.php`),
  API key v Keychain. Posiela sa len krátky zoznam, žiadne citlivé telo mailu.
- **Draft only.** Rutina NEPOSIELA emaily. Len pripraví zoznam a (voliteľne) draft.

---

## Bezpečnosť

- [ ] Scan má readonly Gmail scope (nečíta viac než treba)
- [ ] WhatsApp/notifikácia obsahuje len mená a dôvod, nie celé telá mailov
- [ ] Žiadny auto-send: review request draft otváraš a posielaš ty
- [ ] API kľúče (Gmail token, CallMeBot key) v Keychain, nie na disku

---

*Súčasť decku [Claude Runs My Life](https://dxfnt.github.io/claude-runs-my-life/). Go Beyond.*
