Nexus TV v3.0.1

# NEXUS TV

**NEXUS TV v3.0.0 — made by nirupamjr!**

A lightweight, self-hosted TV entertainment interface designed for a Jio STB (or another TV browser) with a phone-based remote. Nexus combines a TV home screen, direct media playback, playlists, YouTube support, webpage mode, pairing by code/QR, and an experimental gyro cursor.

> Nexus is designed to control and display browser-playable or otherwise authorized media. It does not bypass DRM or protected playback systems.

---

## ✨ What Nexus TV does

### TV home screen

Nexus opens to an Android-TV-style home screen with app tiles. The current starter apps are:

- **Rivestream**
- **YouTube**
- **More apps** placeholder

The Nexus pointer is available on the home screen, and the selected tile gets a visible glass outline.

### Phone remote

Open the phone controller and pair it with the TV using the **4-character code** or the **QR code** shown on the TV.

The remote contains:

- Remote / navigation / playlist tabs
- Play / pause
- Seek controls
- Volume / mute
- Home / back
- Playlist controls
- Gyro cursor mode
- Gyro recenter

### Gyro cursor

The phone can act as an air mouse. Nexus reads device motion/orientation, smooths the input, throttles network updates, and moves a cursor overlay on the TV.

Gyro support depends on the browser/device. HTTPS is required by many mobile browsers before motion sensors can be exposed.

### Direct media playback

Nexus can play supported browser media such as:

- MP4
- WebM
- OGG
- HLS / `.m3u8` where the browser or HLS support allows it

For supported imported media, Nexus can manage its own playback UI, playlist state, subtitles, and next/previous navigation.

### YouTube

YouTube URLs are detected and handled through YouTube's supported embedded-player path for individual videos.

The full YouTube website is not forced into an iframe when browser/security policy prevents that. The Nexus home screen therefore opens a fast YouTube hub instead of waiting on an embed that the browser will reject.

### Webpage mode

For ordinary webpages, Nexus can display the page inside its TV shell where the target site permits embedding. Site security policies such as `X-Frame-Options` or CSP `frame-ancestors` can prevent embedding; Nexus does not bypass those policies.

### Playlists

Add one URL per line in the phone remote. Nexus keeps the playlist state in the room and can manage next/previous navigation for supported imported media and YouTube items.

---

## 🧭 Architecture

```text
                    ┌──────────────────────┐
                    │      NEXUS SERVER     │
                    │  Node.js + HTTP/SSE   │
                    └──────────┬───────────┘
                               │
                 ┌─────────────┴─────────────┐
                 │                           │
                 ▼                           ▼
        ┌─────────────────┐        ┌─────────────────┐
        │   TV / Jio STB  │        │  Phone Remote   │
        │ /tv             │        │ /               │
        │ Player + Home   │        │ Controls + Gyro │
        └─────────────────┘        └─────────────────┘
```

For screen mirroring, Nexus uses browser WebRTC capabilities where supported.

---

## 🚀 Run locally on Windows

### Requirements

- Windows
- Node.js **20+**
- A PC/laptop on the same LAN as the TV for local mode

### Start

1. Extract the Nexus TV folder.
2. Double-click `start.bat`.
3. The terminal detects active LAN IPv4 addresses and prints the local URLs.
4. Open the TV page on the Jio STB:

```text
http://YOUR-PC-IP:8787/tv
```

5. Open the phone remote on the phone:

```text
http://YOUR-PC-IP:8787/
```

6. Pair using the TV code or QR.

For gyro testing over a local network, use the HTTPS address printed by the server when available:

```text
https://YOUR-PC-IP:8788/
```

> The local HTTPS certificate is self-signed for development, so a browser warning is expected.

---

## ☁️ Run online

Nexus includes a `render.yaml` for Render Web Service deployment.

Basic flow:

```text
GitHub repository
       ↓
Render Web Service
       ↓
https://your-project.onrender.com
       ├── /tv  → TV
       └── /    → phone remote
```

### Render deployment

1. Put the project in a GitHub repository.
2. Create a new **Web Service** in Render.
3. Connect the repository.
4. Use the included `render.yaml` or equivalent settings.
5. Deploy.
6. Open the generated HTTPS URL:
   - TV: `/tv`
   - Phone: `/`

Online mode removes the need to keep your laptop running and removes LAN-IP editing from the normal workflow.

> Current room state lives in the running server process. Restarting/redeploying the service clears active rooms and pairing codes.

---

## 📁 Project structure

```text
nexus-tv/
├── public/
│   ├── index.html          # phone remote
│   ├── controller.js       # phone controls + pairing
│   ├── style.css           # glass UI
│   ├── tv.html             # TV interface
│   └── tv-player.js        # TV player + home + cursor
├── server/
│   ├── server.js           # Node server + room signaling
│   ├── cert.pem            # local HTTPS certificate
│   └── key.pem             # local HTTPS key
├── render.yaml             # Render configuration
├── start.bat               # Windows launcher
├── package.json
├── DEPLOY_ONLINE.md
├── README.md
└── CHANGELOG.md
```

---

## ⚡ v2.9 performance work

The v2.9 release focuses on reducing lag on low-power TV browsers and minimizing unnecessary network traffic.

- Gyro/cursor updates are throttled and coalesced.
- Video `timeupdate` state is not sent for every browser event.
- Static files use cache-busting versions for predictable refreshes.
- QR loading is deferred so TV startup is less blocked.
- Expensive blur effects can be reduced on weaker TV browsers.
- App opening uses a lightweight loading state.
- YouTube home avoids waiting on a full-site iframe that the browser will reject.
- YouTube video URLs still use the supported embedded-player flow.

---

## 🔐 Security and media limitations

Nexus is a browser application. That means it follows browser security rules.

Nexus does **not**:

- bypass DRM
- defeat `X-Frame-Options`
- defeat CSP `frame-ancestors`
- extract protected OTT streams
- inject arbitrary click events into cross-origin pages

Third-party pages control their own navigation, playback UI, and embedding permissions.

---

## 🛠 Troubleshooting

### TV cannot connect

- Make sure the TV and PC are on a network that can reach the server.
- Use the **LAN IP**, not `localhost`.
- Check Windows Firewall if another device cannot open the page.
- For online mode, use the public HTTPS URL instead of the LAN address.

### Phone pairs but commands lag

- Use a stable Wi-Fi/network connection.
- Disable battery-saving restrictions on the browser if they interfere with motion sensors.
- Recenter gyro before moving the cursor.

### Gyro does not activate

- Use HTTPS.
- Allow motion/sensor permissions if the browser asks.
- Some browsers/devices do not expose motion sensors to web pages.

### A streaming site is slow or does not open

The website itself may be slow, may block embedding, or may depend on browser features unavailable on the Jio STB. Nexus cannot remove those external limitations.

---

## 📜 Changelog

See **[CHANGELOG.md](CHANGELOG.md)** for the full release history.

---

## License / usage

This project is a personal/experimental media-controller project. Respect the terms of service, copyright, and access controls of the sites and media you use with it.


## v3.0.0 app loading changes
- Removed the restrictive iframe sandbox from the in-app web viewer to improve compatibility with sites that permit framing.
- App pages now start eagerly and get a paint before navigation to reduce blank transitions on slower TV browsers.
- Added a 4.5-second loading diagnostic for pages that appear to be blocked or slow.
- Nexus does not bypass `X-Frame-Options` or CSP `frame-ancestors` restrictions.
