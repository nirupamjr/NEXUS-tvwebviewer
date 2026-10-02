# Changelog

All notable Nexus TV changes are documented here.

---

## v2.9.0 — Performance pass

### Added
- Lightweight fast app-opening state.
- TV performance mode for weaker STB browsers.
- More aggressive asset caching/busting strategy.
- Deferred QR-code script loading.

### Improved
- Gyro cursor updates are throttled/coalesced to reduce network traffic.
- Video time/state synchronization no longer fires on every `timeupdate` event.
- Home-screen cursor selection performs less DOM work during movement.
- YouTube home avoids attempting to load the full YouTube website in an iframe.
- Direct YouTube video URLs continue to use the supported embedded player.
- General startup and repeat-load responsiveness was improved.

### Notes
- Third-party site response time is still outside Nexus's control.
- Some TV browsers remain constrained by CPU, memory, and browser-engine limitations.

---

## v2.8.0 — Nexus shell navigation

### Added
- Nexus app-shell header for supported embedded webpages.
- Home navigation from the Nexus shell.
- Improved separation between Nexus-controlled UI and third-party site UI.

### Changed
- Home-screen app launches attempt to stay inside Nexus where embedding is allowed.
- Unsupported/blocked embeds can still require a direct full-page browser view.

---

## v2.7.1 — Pairing modal fix

### Fixed
- Corrected the TV home-screen pairing modal rendering.
- Restored the liquid-glass pairing overlay above the Nexus home screen.
- Pairing modal disappears automatically after remote connection.

---

## v2.7.0 — Liquid-glass remote pairing

### Added
- Liquid-glass TV pairing modal.
- 4-character pairing code display.
- QR pairing link for the phone remote.
- Manual pairing flow when a phone is not immediately available.

---

## v2.6.0 — Faster interaction + YouTube launch handling

### Added
- Cursor support on the Nexus home screen.
- Visible selected-app outline/glow.
- Gyro cursor with motion/orientation fallback.
- Gyro recenter control.
- Useful Nexus TV home/back behavior.

### Improved
- YouTube is no longer treated like a generic webpage embed.
- YouTube home uses a faster Nexus path when the full YouTube site cannot be embedded.
- General home/app loading behavior improved.

---

## v2.5.0 — Android-TV-style home screen

### Added
- Nexus home screen with app tiles.
- Rivestream tile.
- YouTube tile.
- More-apps placeholder.
- Home-screen app navigation.

---

## v2.4.0 — Liquid-glass UI + remote redesign

### Added
- Liquid-glass-inspired Nexus TV interface.
- Remote / Navigation / Playlist / Settings sections.
- Large glass clickpad.
- Volume controls.
- Navigation controls.
- Experimental gyro cursor mode.

### Design direction
- Dark cinematic surfaces.
- Translucent glass panels.
- Large touch targets for TV use.
- TV-focused minimal animations.

---

## v2.3.0 — Nexus playlists

### Added
- Multi-item playlist input.
- Next / Previous controls.
- Playlist position/state in the paired room.
- Automatic advancement for supported direct media and YouTube items.

### Improved
- Playlist navigation remains inside Nexus instead of relying on a site's own "next" tab/window behavior for Nexus-managed media.

---

## v2.2.x — Online-ready builds

### Added
- Render Web Service configuration.
- Public online deployment workflow.
- Online room signaling for phone ↔ TV control.
- Public HTTPS usage for remote/controller access.

### Notes
- Online room state is process-local.
- Restarting the service clears active rooms.

---

## v2.1.0 — NEXUS logo cleanup

### Changed
- Corrected the terminal ASCII branding to clearly spell **NEXUS**.
- Added the `made by nirupamjr!` credit beside/below the logo area.

---

## v2.0.0 — Server/UI refresh

### Added
- Cleaner Nexus TV server terminal branding.
- Improved startup output.
- Expanded TV/home UI foundation.

---

## v1.9.0 — Terminal banner alignment

### Changed
- Improved placement of the creator credit in the terminal banner.
- Refined the Nexus server startup presentation.

---

## v1.8.0 — Startup UI cleanup

### Changed
- Removed duplicated startup information.
- Simplified terminal startup output.
- Refined Nexus TV server banner.

---

## v1.7.0 — Terminal branding

### Added
- Large Nexus TV ASCII startup logo.
- Creator credit: `made by nirupamjr!`.

---

## v1.6.0 — Automatic IP detection + online preparation

### Added
- Automatic active LAN IPv4 detection.
- Printed TV, phone, and HTTPS mirror URLs.
- Render deployment configuration.

### Goal
- Move Nexus away from hard-coded local IPs so the same project can be moved to another laptop without manually editing addresses.

---

## v1.5.0 — Screen mirroring prototype

### Added
- Browser-based screen mirroring prototype using WebRTC.
- HTTPS local mode for browser features requiring secure contexts.

### Notes
- Browser/device support varies.
- Some networks require TURN relays for reliable cross-network WebRTC.

---

## v1.4.0 — Webpage mode

### Added
- Ability to send a webpage URL to the TV browser shell.
- Separate webpage-open flow from direct media playback.

### Notes
- Nexus does not extract or bypass protected streams from arbitrary pages.

---

## v1.3.0 — YouTube support

### Added
- YouTube URL detection.
- YouTube embedded-player mode.
- Remote play/pause and seek behavior for supported YouTube playback.

---

## v1.2.0 — Direct player fixes

### Fixed
- HLS/player initialization issues.
- Direct-media loading errors.
- Better user-visible player error states.

---

## v1.1.0 — Direct media playback fix

### Fixed
- Direct MP4 playback pipeline.
- Player command routing between phone and TV.
- Clearer handling for unsupported webpage URLs.

---

## v1.0.0 — First working build

### Added
- Node.js server.
- TV player page.
- Phone controller page.
- 4-character pairing system.
- WebSocket/SSE-style room signaling foundation.
- Play/pause and basic playback controls.
- Direct media URL loading.
- Basic subtitle/quality controls.
