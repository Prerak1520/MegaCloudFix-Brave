# MegaCloudFix — Brave Edition

A browser extension that redirects all requests from `megacloud.blog` to `megacloud.tv`.

## Purpose

Some anime streaming sites reference megacloud.blog as their video host, which may be unavailable or blocked. This extension transparently rewrites those requests to megacloud.tv, both at the network level and inside the page itself.

## Files

- `manifest.json` — Extension manifest (Manifest V3, Brave/Chromium-compatible)
- `background.js` — Service worker that logs startup; network redirects are handled by declarativeNetRequest
- `content.js` — Patches fetch and XMLHttpRequest inside the page at document_start
- `rules.json` — Declarative redirect rules

## Installation (Brave)

1. Open Brave and go to `brave://extensions/`
2. Enable **Developer mode** (toggle in the top-right corner)
3. Click **Load unpacked**
4. Select the `MegaCloudFix-Brave` folder
5. The extension will appear in your extensions list — no restart needed

> **Note:** Brave's Shields may also block some requests independently. If you still have issues, try setting Shields to "Allow all" for the affected site, or adding an exception.

## How it works

Two layers of interception run simultaneously:

- `rules.json` uses the `declarativeNetRequest` API to redirect any network request to `megacloud.blog` before the browser connects — this is the primary, most reliable layer
- `content.js` patches `window.fetch` and `XMLHttpRequest.prototype.open` directly inside the page at `document_start`, catching requests that originate from iframes or player scripts before the network layer sees them

No data is collected or transmitted.

## Browser compatibility

This extension uses Manifest V3 and works on any Chromium-based browser:

| Browser | Install path |
|---|---|
| **Brave** | `brave://extensions/` |
| Chrome | `chrome://extensions/` |
| Edge | `edge://extensions/` |
| Opera | `opera://extensions/` |

For **Firefox**, see [RAELIE1/MegaCloudFixFireFox](https://github.com/RAELIE1/MegaCloudFixFireFox).
