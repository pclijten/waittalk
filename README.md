# WaitTalk 🗣️

> Praat met wie naast je staat — spontane gesprekken op de bushalte, het treinstation, of waar je ook wacht.

**Status:** Prototype in ontwikkeling  
**Platform:** Progressive Web App (geen app store nodig)

---

## 🚀 Stap 1 — Firebase instellen (eenmalig, ±15 minuten)

### 1.1 Firebase project aanmaken

1. Ga naar [https://console.firebase.google.com](https://console.firebase.google.com)
2. Klik **"Project toevoegen"**
3. Naam: `waittalk` → klik door (Analytics hoeft niet)
4. Wacht tot het project klaar is

### 1.2 Web-app registreren

1. Klik het `</>` icoontje ("Web")
2. App-naam: `waittalk-web` → klik **"App registreren"**
3. Je ziet nu een `firebaseConfig` object — kopieer dit!
4. Klik op **"Doorgaan naar console"**

### 1.3 Config in index.html plakken

Open `index.html` en zoek deze sectie (~regel 25):

```js
const firebaseConfig = {
  apiKey:            "JOUW_API_KEY",
  authDomain:        "JOUW_PROJECT.firebaseapp.com",
  ...
};
```

Vervang de hele `firebaseConfig` met jouw gekopieerde versie.

### 1.4 Realtime Database aanzetten

1. Ga in Firebase Console naar **"Build" → "Realtime Database"**
2. Klik **"Database aanmaken"**
3. Kies regio: **"Europe-west1 (Belgium)"** → klik "Volgende"
4. Kies **"Starten in testmodus"** → klik "Gereed"
5. Kopieer de database-URL (ziet eruit als `https://waittalk-xxx-default-rtdb.europe-west1.firebasedatabase.app`)
6. Plak deze URL in je `firebaseConfig` bij `databaseURL`

### 1.5 Security rules instellen

1. Ga in de Realtime Database naar het tabblad **"Rules"**
2. Vervang de bestaande regels met de inhoud van `database.rules.json`
3. Klik **"Publiceren"**

### 1.6 Anonieme authenticatie aanzetten

1. Ga naar **"Build" → "Authentication"**
2. Klik **"Aan de slag"**
3. Tabblad **"Sign-in method"** → klik op **"Anoniem"**
4. Zet het aan → klik **"Opslaan"**

---

## 🚀 Stap 2 — Deployen via GitHub Pages

### 2.1 Zet Service Worker aan

Voeg dit toe aan het einde van `index.html`, net voor de sluitende `</body>`:

```html
<script>
  if ("serviceWorker" in navigator) {
    navigator.serviceWorker.register("/sw.js");
  }
</script>
```

### 2.2 Push naar GitHub

```bash
git add .
git commit -m "feat: firebase integratie + PWA setup"
git push
```

### 2.3 GitHub Pages aanzetten

1. Ga naar je repository op GitHub
2. **Settings** → **Pages**
3. Source: **"Deploy from a branch"**
4. Branch: `main` / `master` → map: `/ (root)`
5. Klik **"Save"**
6. Na ±2 minuten is de app live op `https://JOUWGEBRUIKERSNAAM.github.io/waittalk/`

---

## 📁 Projectstructuur

```
waittalk/
├── index.html          ← Hoofd app (alle schermen)
├── manifest.json       ← PWA installatie-info
├── sw.js               ← Service Worker (offline support)
├── database.rules.json ← Firebase beveiligingsregels
├── icons/              ← App-iconen (zelf aanmaken of genereren)
│   ├── icon-192.png
│   └── icon-512.png
└── README.md
```

---

## 🔧 Iconen aanmaken

Je hebt twee PNG-iconen nodig voor de PWA. Snelste manier:

1. Ga naar [https://favicon.io/favicon-generator/](https://favicon.io/favicon-generator/)
2. Tekst: `W` · Achtergrond: `#1D9E75` · Tekst kleur: `#FFFFFF`
3. Download → hernoem naar `icon-192.png` en `icon-512.png`
4. Zet ze in de map `icons/`

---

## 🗺️ Roadmap

- [x] UX prototype
- [x] Firebase Auth (anoniem)
- [x] Profiel opslaan (localStorage)
- [x] Realtime Database koppeling
- [x] Match engine (interesse-overlap)
- [ ] Web Bluetooth nabijheidsdetectie
- [ ] Push-notificaties
- [ ] Gespreksopener AI-suggesties
- [ ] Rapporteer/blokkeer functie
- [ ] Statistieken dashboard

---

## ⚠️ Bekende beperkingen (prototype)

- **iOS Safari**: Web Bluetooth werkt nog niet op iOS. Alternatief in ontwikkeling (QR-code matching).
- **Nabijheid**: Nu op basis van "beiden online tegelijk". Echte BLE-detectie volgt.
- **Schaal**: Firebase gratis tier ondersteunt tot ±100 gelijktijdige gebruikers.

---

## 💬 Contact

Project door: jouw naam hier  
Gebouwd met: Firebase · Vanilla JS · GitHub Pages
