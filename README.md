# Covert Calculator Vault

A stealth Progressive Web App (PWA) disguised as an iOS-style calculator, concealing an encrypted private notes vault accessed via a passcode sequence.

---

## Overview

The application functions outwardly as a standard arithmetic calculator. Entering a designated numeric passcode and pressing the equals sign (`=`) swaps the interface to an encrypted markdown/plain-text scratchpad.

### Key Capabilities

* **Stealth Camouflage:** Styled after the native iOS dark-mode calculator.
* **Passcode Gateway:** Access triggered by entering the code and evaluating (`=`).
* **Hardware Emergency Lock:** Uses the `devicemotion` API to trigger an immediate interface reload upon detecting physical phone shaking.
* **Client-Side Obfuscation:** XOR-based byte masking combined with Base64 encoding for local note storage.
* **Auto-Draft:** Local retention of in-progress drafts prior to manual commit.
* **Data Portability:** Flat CSV export and import mechanics for offline backups.
* **Offline Operation:** Registers an inline Service Worker caching application shell assets.

---

## Vault Access Mechanics

* **Lockout:** Pressing the **Lock** button in the header or shaking the physical device forces an immediate session flush (`location.reload()`).

---

## Architecture & Code Structure

The entire application is self-contained within a single HTML file:

| Component | Implementation | Function |
|---|---|---|
| **Styling** | Vanilla CSS (CSS Grid, Variables) | Emulates native mobile interfaces with safe-area spacing and dynamic display resizing. |
| **Logic** | Vanilla JavaScript | State management for basic four-function arithmetic and vault display toggle. |
| **Storage** | `localStorage` | Persists note objects under key `mg_notes_v4` and drafts under `mg_draft_secure`. |
| **Obfuscation** | Bitwise XOR + `btoa`/`atob` | Basic client-side string obfuscation using a fixed salt string. |
| **PWA Cache** | Dynamic Blob URL Service Worker | Intercepts fetch requests to serve cached assets offline (`mg-vault-v3`). |

---

## Deployment & Setup

### Requirements

* HTTPS environment (required for Service Worker registration and iOS `DeviceMotionEvent` permissions).
* Any static hosting provider (GitHub Pages, Cloudflare Pages, Vercel, Netlify) or standard web server (Nginx, Caddy, Apache).

### Local Execution
