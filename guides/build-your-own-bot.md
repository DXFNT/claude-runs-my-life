# Workshop zadanie: postav si vlastného Google bota

Návod k slidom **"Postav si vlastného bota (1/2 a 2/2)"** z decku *Claude Runs My Life*.

Cieľ: samostatná inštancia, ktorá tvojmu Claudovi dovolí **čítať a spravovať tvoj vlastný
Google účet** (Gmail, Drive, Docs, Sheets, Calendar). Vlastná OAuth aplikácia, vlastný kľúč,
token v trezore. **Odosielanie vždy klikáš ty.** Žiadny auto-send.

> Toto je verejný, sanitizovaný návod. Staviaš bota pre **svoj vlastný** účet. Nie sú v ňom
> žiadne cudzie tokeny ani prístupy. Tie ostávajú v privátnom internom repe.

---

## Workshop zadanie (toto si spravte)

1. Rozhodni typ účtu (osobný Gmail vs firemný Workspace).
2. Sprav prípravu na strane Googlu (projekt, služby, súhlas).
3. Vytvor prístupový kľúč a ulož ho do Keychain.
4. Odklikni súhlas a otestuj že bot vidí tvoj účet.

Prvá polovica je Google (raz a navždy), druhá polovica je tvoj Mac (pár klikov).

---

## Časť 1 — strana Googlu (slide 1/2)

### Krok 1. Rozhodni typ účtu

Typ účtu určuje celý postup, najmä **expiráciu prístupu**:

| Účet | Súhlas (consent) | Dôsledok |
|---|---|---|
| **Firemný Workspace, kde si admin** | **Internal** | Token nevyprší po 7 dňoch, žiadna verifikácia. Produkčne stabilné. Odporúčané. |
| **Osobný @gmail.com** | External + Testing | Funguje, ale refresh token v Testing režime vyprší po 7 dňoch. Treba občas re-auth. |

> Kľúčová lekcia: ak môžeš ísť cez **Internal** (si admin domény), choď. Inak ti bot po
> týždni odhlási sám seba.

### Krok 2. Založ projekt a zapni služby

1. Vytvor **Google Cloud projekt** ([console.cloud.google.com/projectcreate](https://console.cloud.google.com/projectcreate)).
   Pri Workspace botovi ho zakladaj **pod cieľovou organizáciou**, nie pod osobným účtom.
2. **Enable** API, ktoré bot bude používať. Cez gcloud je to rýchlejšie než klikať:
   ```bash
   # Pozor: názov projektu ≠ project ID. Najprv zisti reálne ID:
   gcloud projects list
   gcloud config set project <PROJECT_ID>
   for api in gmail drive docs sheets calendar-json people tasks; do
     gcloud services enable $api.googleapis.com
   done
   ```
   (Pridaj ďalšie podľa potreby: `slides`, `forms`, `script`, `admin` pre Workspace admin veci.)

### Krok 3. Nastav súhlas na Internal

1. Otvor consent screen: `console.cloud.google.com/auth/overview?project=<PROJECT_ID>`.
2. Pri Workspace admin účte vyber **Internal**. Žiadna Google verifikácia, žiadna 7-dňová expirácia.
3. Osobný Gmail: zostane External + Testing, pridaj svoj email do **Test users**.

---

## Časť 2 — tvoj Mac (slide 2/2)

### Krok 4. Vytvor prístupový kľúč (OAuth Desktop client)

1. APIs & Services → **Clients** → Create → **Desktop app**:
   `console.cloud.google.com/auth/clients?project=<PROJECT_ID>`.
   (Desktop client sa **nedá** vytvoriť cez gcloud, iba cez Console UI.)
2. **Download JSON** (`client_secret_*.json`). Drž ho len dočasne, o chvíľu ide do Keychain a zmažeš ho.

### Krok 5. Ulož do trezoru (Keychain, nie na disk)

Secret nikdy do iCloud-synced priečinka (`~/Documents` na Macu býva iCloud). Patrí do Keychain:

```bash
security add-generic-password -s "mybot_oauth_credentials" -a "me@mydomain.com" \
  -w "$(cat ~/Downloads/client_secret_*.json)" -U
rm ~/Downloads/client_secret_*.json   # zmaž disk kópiu
```

### Krok 6. Odklikni súhlas (prvý beh)

Prvé spustenie skriptu otvorí prehliadač na prihlásenie. Dve veci pre bezpečnosť:

1. Auth otvor v **Safari** (oddelene od Chrome, kde máš bežne prihlásený iný účet), aby si
   sa neprihlásil omylom zlým účtom.
2. Skript **over že prihlásený email = ten očakávaný** ešte pred uložením tokenu:
   ```python
   prof = svc.users().getProfile(userId="me").execute()
   assert prof["emailAddress"] == "me@mydomain.com", "Zlý účet, token neukladám"
   # token ulož do Keychain, nie do .json na disk
   ```
3. Ak Google ukáže "app not verified" (osobný Gmail v Testing), Advanced → Go to (unsafe) → Allow.

Otestuj: vypýtaj si profil a posledných pár mailov. Vidí to? Bot žije.

---

## Bezpečnosť (vždy)

1. **Token a credentials v Keychain**, nie v `.json` na disku, nie v iCloud priečinku.
2. **Send guard, draft only.** Default akcia je draft. Odosielanie za zámkom, ktorý sa
   nedá omylom prejsť:
   ```python
   class SendNotAllowedError(Exception): pass
   def send_email(svc, raw, allow_send=False):
       if not allow_send:
           raise SendNotAllowedError("Draft only. Send klikáš ty.")
       # ... messages().send() ...
   ```
3. **Auth v Safari + kontrola emailu** pred uložením tokenu (krok 6).
4. **Kill switch.** Prístup zrušíš za 5 sekúnd: [myaccount.google.com/permissions](https://myaccount.google.com/permissions)
   (ako daný účet) → tvoja app → Remove access.
5. **Audit log** akcií do `~/Library/Logs/<tvoj-bot>/`, mimo iCloud.

---

## Checklist

- [ ] Viem typ účtu a podľa toho consent (Internal vs External+Testing)
- [ ] GCP projekt založený, potrebné API enabled (over `gcloud services list --enabled`)
- [ ] Consent screen nastavený (Internal ak si admin)
- [ ] Desktop OAuth client vytvorený, JSON stiahnutý
- [ ] Credentials v Keychain, disk kópia zmazaná
- [ ] Prvý `--auth` prešiel v Safari, email overený, token v Keychain
- [ ] Send guard `allow_send=False` je default
- [ ] Viem kde prístup zrušiť (myaccount.google.com/permissions)

---

*Súčasť decku [Claude Runs My Life](https://dxfnt.github.io/claude-runs-my-life/). Go Beyond.*
