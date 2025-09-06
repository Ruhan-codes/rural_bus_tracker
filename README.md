# Rural Bus Tracker — Free Demo (No paid APIs)
Track a friend's live location (like a rural bus) and show it on a free map. Uses:
- **Leaflet + OpenStreetMap** (free, no map key needed)
- **Firebase Realtime Database** (free tier; API key is free and only identifies your project)

> ⚠️ For hackathon demo only. Do **not** keep the database open to the public after your demo.

---

## 1) Prerequisites
- A Google account (for Firebase).
- A code editor (e.g., **VS Code**).
- Internet connection.

## 2) Get the Code
- If you downloaded the ZIP, extract it.
- Folder contains: `driver.html`, `passenger.html`, `config.example.js`, `README.md`.

## 3) Create a Firebase Project (free)
1. Go to **https://console.firebase.google.com** → **Add project** → give it a name → continue (you can skip Google Analytics).
2. In left menu: **Build → Realtime Database** → **Create Database** → start in **test mode** (for demo).
3. Go to **Project Settings → General → Your apps → Web** → **Register app** (no hosting needed) → copy the **config**.

## 4) Add Your Firebase Config
1. In this folder, make a copy of `config.example.js` and rename to **`config.js`**.
2. Paste your Firebase config object inside `firebaseConfig = { ... }` in `config.js`.
   - This key is **free** and safe to expose for demos. It does not give admin access.

## 5) (Optional) Make Rules Public for the Demo
In **Realtime Database → Rules**, set temporarily (demo only):
```json
{
  "rules": {
    "bus": {
      ".read": true,
      ".write": true
    }
  }
}
```
Click **Publish**. After your demo, lock it down.

## 6) Run Locally (quick test)
- Open **passenger.html** in your browser on your laptop → it will load the map.
- Open **driver.html** in **the same laptop** (or another device). Click **Start Sharing** and allow location.
- Both default to `busId=demo`. You can change bus id by using a URL like:
  - `driver.html?busId=route1`
  - `passenger.html?busId=route1`

> Note: Geolocation requires **HTTPS** or **localhost**. On a **phone**, you must use HTTPS. See step 7 for GitHub Pages.

## 7) Put Online with HTTPS (for phone demo)
**GitHub Pages (free)**:
1. Create a GitHub account → New repository (e.g., `rural-bus-tracker`).
2. Upload **all files**, including your **`config.js`** (with your keys).
3. Repo **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main` → Folder: `/root` → Save.
4. Wait ~1–2 minutes; a public HTTPS URL appears under **Pages**.
5. Share these links with your friend:
   - `https://<your-username>.github.io/rural-bus-tracker/driver.html?busId=demo`
   - `https://<your-username>.github.io/rural-bus-tracker/passenger.html?busId=demo`

## 8) Use It
- On **driver’s phone**: open the **driver** link → tap **Start Sharing** → keep the page open and screen on.
- On **passenger’s phone**: open the **passenger** link → watch the marker move.
- You can change `busId` (e.g., `route1`) in both URLs to track multiple buses.

## 9) Cleanup / Security After Demo
- In Firebase **Rules**, restrict access or delete the project.
- Do not keep `.read/.write` public in production.
- Consider adding simple auth or write-only rules per busId if you continue the project.

## Troubleshooting
- **Map shows but no movement**: On driver page, ensure location permission is **Allowed** and **Start Sharing** is pressed.
- **Phone won’t share location**: Serve over **HTTPS** (GitHub Pages). Mobile browsers block geolocation on plain HTTP (non-localhost).
- **Marker jumps**: That’s normal with GPS. We show an accuracy circle.
- **Battery drains fast**: Tap **Stop Sharing** when not needed; GPS is power-hungry.

Good luck at your hackathon! 🚍
