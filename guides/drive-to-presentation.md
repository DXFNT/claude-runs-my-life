# Z Drive priečinka fotiek po klikateľnú prezentáciu

Návod k slidu **„Fotky na vstupe, schválené na výstupe"** z decku *Claude Runs My Life*.

Cieľ: od kolegu dostaneš priečinok fotiek na Google Drive a o pár minút z toho máš
brandovaný klikateľný deck. Fotky skoro na celú obrazovku, klient si to preklikne
a rovno odklikne schválenie. Žiadny dizajnér, žiadny kóder, spravíš to aj ty sám.

> Toto je verejný návod. Konkrétne tokeny, účty a napojenia (Drive, Cloudflare, notifikácie)
> sú interné. Na prvotný setup ti pomôže Pali. Potom to už spustíš jednou vetou.

---

## Čo potrebuješ

1. Zdieľaný **Google Drive priečinok** s fotkami (pokojne aj viac priečinkov, napríklad po kolekciách).
2. **Claude Code** s napojeným Drive a Cloudflare (interný setup, raz nastavený, potom funguje stále).

---

## Postup (jedna veta a zvyšok dorobí Claude)

1. **Hodíš link na Drive.**
   Napíš Claudovi napríklad: *„Z týchto Drive priečinkov urob webovú prezentáciu, nech sa to dá ľahko preklikať a ukázať klientovi"* a vložíš linky.
   Claude fotky stiahne, pomenuje a roztriedi po kolekciách a rozmeroch sám. Ty netriediš nič.

2. **Claude postaví Dexfinity deck.**
   Plný brand (navy, modrá, Poppins, logo, Go Beyond), fotky na celú obrazovku, listovanie šípkami,
   na konci slide „všetko pokope" so súhrnom všetkých fotiek. Stačí povedať *„v Dexfinity dizajne"*
   a aktivuje sa `dex-design`.

3. **Nasadí a vráti link.**
   Žije na webe (Cloudflare Pages) za pár sekúnd. Pošleš link klientovi, on si to preklikne.

4. **Notifikuj zodpovedného (dve možnosti).**
   Povedz Claudovi nech po nasadení (alebo keď klient odklikne schválenie) pošle notifikáciu:
   - **Basecamp task** komentár na danom projekte, alebo
   - **WhatsApp ping** cez CallMeBot.
   Claude pošle notifikáciu sám. Zodpovedný už len otvorí link.

---

## Tipy

- **Schválenie klientom.** Vieš pridať ku každej fotke odklik ✓ / ✕ a komentár. Voľby sa ukladajú,
  a keď klient dokončí, padne notifikácia. Stačí povedať *„pridaj klientovi schvaľovanie a notifikáciu"*.
- **Landscape ostáva landscape.** Široké fotky nestláčaj do portrétu. Claude to rieši sám podľa brand pravidiel.
- **Redeploy.** Keď pribudnú nové fotky, len ich hoď do priečinka a povedz *„aktualizuj prezentáciu"*.
- **Login brána.** Ak má byť prezentácia chránená heslom, povedz to. Default je verejný link na ľahké zdieľanie.

---

## Príklad naživo

Reálny výstup tohto workflowu: produktové AI fotky regálov rozdelené do troch kolekcií,
deck s preklikávaním a súhrnom. Pozri **[živý príklad](https://mamutex-regaly.pages.dev)**.

---

*Súčasť decku [Claude Runs My Life](https://dxfnt.github.io/claude-runs-my-life/). Go Beyond.*
