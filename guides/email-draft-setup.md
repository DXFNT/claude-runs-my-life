# Ako si autorizuješ vlastného Clauda na drafty v Gmaili

Návod k slidu **"Príkaz odpis mi"** z decku *Claude Runs My Life*.

Cieľ: tvoj Claude vie prečítať tvoj inbox, pochopiť kontext a **vložiť draft odpovede**
priamo do správneho threadu. **Send klikáš vždy ty.** Žiadny auto-send.

> Toto je verejný, sanitizovaný návod. Nie sú v ňom žiadne osobné tokeny, podpisy ani
> klientske dáta. Tie ostávajú v privátnom internom repe.

---

## Kľúčová lekcia (prečo to robiť takto)

Nie je to "AI mi píše emaily". Je to **trust & safety model**, ktorý z toho robí
bezpečnú vec, nie risk:

1. **Vlastná OAuth aplikácia, vlastný token.** Nie cudzia služba. Ty vlastníš Google
   Cloud projekt aj credentials. Prístup vieš kedykoľvek jedným klikom odvolať.
2. **Draft only, nikdy auto-send.** Claude píše drafty do tvojho inboxu. Tlačidlo
   Send stláčaš ty, po prečítaní. V kóde je technický guard, ktorý odoslanie blokuje.
3. **Token v Keychain, nie v cloude.** Secret nikdy do iCloud-synced priečinka
   (`~/Documents` na Macu je často iCloud). Patrí do macOS Keychain.
4. **Audit log + kill switch.** Každá akcia sa loguje, prístup sa dá zrušiť v Google
   účte za 5 sekúnd.

---

## Setup krok po kroku

### 1. Google Cloud projekt + Gmail API
1. Otvor [Google Cloud Console](https://console.cloud.google.com/) a vytvor projekt.
2. **Enable** Gmail API:
   `https://console.developers.google.com/apis/api/gmail.googleapis.com/overview?project=<TVOJ_PROJECT_ID>`

### 2. OAuth credentials (Desktop)
1. APIs & Services → **Credentials** → Create Credentials → **OAuth client ID**.
2. Typ aplikácie: **Desktop app**. Daj jej názov (napr. `Claude Email Bot`).
3. Stiahni `credentials.json`. **Nedávaj ho do iCloud priečinka** — drž ho dočasne
   a po prvom spustení ho presuň/zmaž (token aj credentials pôjdu do Keychain).

### 3. Scopes
Pre čítanie + drafty stačí:
```
https://www.googleapis.com/auth/gmail.compose
https://www.googleapis.com/auth/gmail.readonly
```
(Pre štítkovanie/úpravy pridaj `gmail.modify`. Pre odosielanie `gmail.send` — ale
ak chceš zachovať draft-only bezpečnosť, `gmail.send` **nepridávaj**.)

### 4. Prvý beh = browser consent
```python
from google_auth_oauthlib.flow import InstalledAppFlow
SCOPES = [
    "https://www.googleapis.com/auth/gmail.compose",
    "https://www.googleapis.com/auth/gmail.readonly",
]
flow = InstalledAppFlow.from_client_secrets_file("credentials.json", SCOPES)
creds = flow.run_local_server(port=0)   # otvorí prehliadač, prihlásiš sa
# creds.to_json() ulož do Keychain, nie na disk
```

### 5. Token do Keychain (nie na disk)
```bash
# Ulož
security add-generic-password -s "my_gmail_oauth_token" -a "ja@mojadomena.sk" -w "$TOKEN_JSON" -U
# Načítaj v skripte
security find-generic-password -s "my_gmail_oauth_token" -a "ja@mojadomena.sk" -w
```

### 6. Draft-only guard (povinné)
V skripte maj odosielanie za zámkom, ktorý sa nedá omylom prejsť:
```python
class SendNotAllowedError(Exception): pass

def send_email(svc, raw, allow_send=False):
    if not allow_send:
        raise SendNotAllowedError("Draft only. Send klikáš ty v Gmaili.")
    # ... users().messages().send() ...
```
Default akcia = `users().drafts().create()`. `send()` sa nevolá nikdy automaticky.

### 7. Draft ako reply do existujúceho threadu
Aby draft pristál ako odpoveď pod správny mail (nie nový thread):
```python
svc.users().drafts().create(userId="me", body={
    "message": {"raw": raw, "threadId": THREAD_ID}   # threadId je povinné
}).execute()
# MIME headers: In-Reply-To a References = Message-ID posledného mailu v threade
```

---

## Pamäťové pravidlo na skopírovanie (CLAUDE.md)

Vlož do svojho `~/.claude/CLAUDE.md`, nech tvoj Claude pozná workflow:

```markdown
## Shortcut: "odpis mi [meno]" = dvojkrokový reply workflow v Gmaili

Krok 1. Nájdi osobu v Gmaili, prečítaj posledný relevantný thread, v chate napíš
NÁVRH odpovede (plain text preview). Žiadny draft v Gmaili v tomto kroku.

Krok 2. Po mojom "OK" vytvor Gmail DRAFT ako reply do originálu threadu
(drafts().create s threadId + In-Reply-To/References headers). Pripoj moju pätičku.
Vráť draftId. NEODOSIELAJ — Send klikám ja.

HARD RULE: NIKDY messages.send() bez môjho explicit OK v aktuálnom turne.
Token v Keychain. Audit log každého send_blocked/send_executed.
```

---

## Bezpečnostný checklist pred použitím

- [ ] `credentials.json` nie je v iCloud-synced priečinku
- [ ] Token je v Keychain, nie v `.json` na disku
- [ ] Scopes neobsahujú `gmail.send` (ak chceš draft-only)
- [ ] `allow_send=False` je default, `send()` sa nevolá automaticky
- [ ] Vieš kde prístup odvolať: Google účet → Security → Third-party access

---

*Súčasť decku [Claude Runs My Life](https://dxfnt.github.io/claude-runs-my-life/). Go Beyond.*
