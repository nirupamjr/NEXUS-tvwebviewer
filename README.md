Nexus TV v2.9.0 — made by nirupamjr!

# Nexus TV v2.9.0

Nexus TV is a lightweight TV player + phone remote with local LAN mode and an online hosted mode.

## Online mode (recommended for using it without your laptop)

This project is prepared for a Render Web Service. Render provides a public `onrender.com` URL and HTTPS for web services, so the TV and phone can use the same public URL from different networks. Render also supports real-time WebSocket connections; Nexus TV currently uses HTTP + Server-Sent Events for room signaling.

### Deploy

1. Extract this ZIP.
2. Put the contents of the `nexus-tv` folder into a GitHub repository (the `render.yaml` should be at the repository root).
3. In Render, choose **New → Web Service** and connect that repository.
4. The included `render.yaml` is configured for the free plan with:
   - Build: `npm install`
   - Start: `npm start`
   - Health check: `/api/health`
5. Deploy. Render will assign a public URL such as `https://your-service.onrender.com`.

### Use

On the Jio STB browser open:

`https://your-service.onrender.com/tv`

On the phone open:

`https://your-service.onrender.com/`

The TV generates a four-character code. Enter it on the phone or scan the QR code.

No local IP editing is needed in online mode. The server automatically uses Render's `RENDER_EXTERNAL_URL` when it exists.

## Local mode

Double-click `start.bat` on Windows. It automatically detects the laptop's LAN IPv4 address and prints the TV, phone, and local HTTPS mirror URLs.

## Features

- TV player
- Phone remote
- Pairing code + QR
- Direct MP4/WebM/OGG/M3U8 playback
- YouTube embedded playback
- Webpage mode with Nexus-controlled navigation
- Nexus playlists with Next/Previous and automatic advance for direct media and YouTube
- Subtitles via VTT
- Local screen mirroring via HTTPS + WebRTC
- Online screen mirroring via HTTPS + WebRTC (browser/network support varies)

## Notes

Online room state is kept in the running server process, so a service restart clears current rooms/codes. This is fine for a lightweight personal/experimental setup.

Free Render web services can spin down after 15 minutes without qualifying activity. Nexus TV sends a lightweight HTTP heartbeat while a TV/controller session is open to help keep the online service active during use; an idle service can still take longer to respond when first opened again.

Screen mirroring uses a direct peer-to-peer WebRTC connection with a public STUN server. Some networks require a TURN relay; a future release can add configurable TURN support for more reliable cross-network mirroring.

Protected/DRM content is not bypassed.


## v2.6 home screen
The TV now opens to an Android-TV-style Nexus home screen with glass app tiles for Rivestream and YouTube. Selecting a streaming tile opens the service directly in the TV browser so its own navigation and controls remain intact. The Nexus pointer is retained on the Nexus home screen; third-party streaming pages use their native UI. A placeholder tile is included for future apps. The Nexus Remote Home/Back action returns to this home screen.

Note: third-party sites may block iframe/web embedding or control their own navigation. Nexus does not bypass those restrictions.


## v2.9 performance and fast app shell
- TV performance mode reduces expensive blur effects on weaker STB browsers.
- Gyro/cursor commands are throttled to reduce network chatter and pointer lag.
- Static assets use cache-busting query versions and the QR script is deferred.
- YouTube home uses a fast Nexus hub because the full YouTube site cannot be embedded; specific videos still use the official player.

## v2.8 in-app apps
Home-screen apps now open inside the Nexus TV shell where the target service permits iframe embedding. The Nexus glass header remains visible so Home is always one click away. YouTube uses its supported embedded-player path for video playback; a full YouTube homepage cannot be embedded when YouTube/browser security policies disallow it.
