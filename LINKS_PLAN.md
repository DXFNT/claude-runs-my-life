# Claude Runs My Life — plán odklikov (dual mode)

Cieľ: z každého slidu odklik na zdroj. **V** = verejný návod (DXFNT public, OK na školení).
**P** = privátny zdroj (DexfinityHUB org, len členovia). **V+P** = duál.

Bezpečnostný princíp: odkaz na privátny repo nič neprezradí (nečlen dostane 404).
Deck môže ostať verejný. Linkovať na privátne je OK.

Status: prechádzame slide po slide, Pavol dáva input ku kľúčovej lekcii a čo doplniť.

---

## Slide 1 — Príkaz "odpis mi"  [V+P]

**Kľúčová lekcia (Pavol):** Človek si autorizuje svojho VLASTNÉHO Clauda na čítanie
inboxu a vkladanie draftov, cez vlastnú Google Cloud OAuth app ("Desktop Ferisprav_bot").
Refine pre publikum = trust & safety model:
1. Vlastná OAuth app + vlastný token (odvolateľný prístup).
2. Draft only, nikdy auto-send — Send klikáš ty.
3. Token v Keychain, nie v iCloud.

**V — verejný návod:** "Ako autorizovať vlastného Clauda na drafty v Gmaili."
GCP projekt → enable Gmail API → OAuth Desktop creds → script → consent → token Keychain
→ draft-only guard → reply-in-thread cez threadId. Bez osobných dát.

**P — privátny zdroj:** reálny gmail_oauth.py setup, HTML pätička, reply-context, tracker.

Status: ✅ HOTOVO. Email téma rozdelená na 2 slidy (slide 1 = outcome, slide 1b/02 =
setup + trust/safety). Verejný návod + pamäťové pravidlo v `guides/email-draft-setup.md`.
Odkaz "Návod na stiahnutie ↗" v pätičke oboch slidov. Auto-číslovanie zapnuté (JS).

POZOR: vložením nového slidu sa hash posunul +1 od pôvodného slidu 2.
Mapovanie teraz: #1 odpis mi, #2 setup (nový), #3 review od, #4 account switch ...
#27 voice. (Pôvodné #2..#26 sú teraz #3..#27.)

---

## Slide 3 (pôv. 2) — Príkaz "review od"  [V+P]

**Kľúčová lekcia (Pavol):** Nie je to len "napíš review request". Je to pravidelná
RUTINA ktorá číta moje maily a HĽADÁ PRÍLEŽITOSTI — koho viem požiadať o Google recenziu.
Automatizovaný opportunity-finding systém. Recenzie podporujú vyhľadávanie aj AI
odporúčania. Claude navrhne koho osloviť.

**V — verejný návod:** ako postaviť recurring "find review opportunities" rutinu
(scheduled scan inboxu + ranking kandidátov). Bez osobných dát.
**P — privátny:** moje place IDs (BA/Praha), reviews-sent tracker, konkrétne kandidátky.

**Súvisiaca akcia:** obnoviť scheduled task `weekly-review-candidates-scan` (pondelok),
nech reálne pravidelne beží. → samostatný nový chat (brief pripravený).

Doplnené (Pavol): rutina v podstate beží. nové = týždenný WhatsApp ping s kandidátmi,
auto-navrhnutý text recenzie z kontextu, draft v Gmaili (otvorím, upravím, pošlem).

Status: ✅ HOTOVO. Slide #3 enrichnutý (punchline + krok 3 WhatsApp ping). Verejný
návod guides/review-opportunity-routine.md + footer odkaz. Rutina renewal = nový chat
(brief daný Pavlovi). Žiadny auto-send.
