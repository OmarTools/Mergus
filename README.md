<div align="center">
  <img width="120" height="120" alt="Untitled design (4)" src="https://github.com/user-attachments/assets/cd1083ee-52e8-41b7-bfd2-52db6bc16b2d" />

  <h1>Mergus</h1>
  <p><strong>A fast, private, multi-profile browser for Windows — designed and built from the ground up.</strong></p>
  <p>Tabbed browsing · Isolated profiles + incognito · Built-in ad blocking · Download manager · Local AI · Chrome/Edge import</p>
</div>
<img width="1093" height="748" alt="image" src="https://github.com/user-attachments/assets/e15b09b3-d7b4-4289-8fcb-8a67053be948" />

---

## Overview

**Mergus** is a complete desktop web browser for Windows, independently designed and developed as an end-to-end product exercise: a polished user experience on top of a carefully hardened Chromium foundation. It targets users who juggle multiple identities online (personal, work, clients) and want tracking protection and everyday power tools built in — no extension hunting required.

**Status:** stable release · **Platform:** Windows 10/11 (x64) · **License:** proprietary — see [LICENSE](LICENSE)

---

## ✨ Features

### Browsing essentials
- **Multi-tab engine** — every tab runs in its own view with independent navigation, history-aware back/forward, reload/stop, and smart URL bar (URLs, domains, and search queries all resolve from one input)
- **Drag-to-reorder tabs**, duplicate, pin, sleep inactive tabs automatically (configurable timeout), "keep awake" override
- **Split view** — two pages side by side in one window with adjustable ratio; survives resizes and sidebar toggles
- **Find in page** (`Ctrl+F`) with live match counts, **page zoom** with % indicator, **printing**
- **Session restore** — picks up exactly where you left off (toggleable in Settings)
- **Private start page** — instant, offline, zero tracking: search box + quick tiles, no network calls
- **Styled error pages** instead of blank views when a site fails to load

### Profiles & privacy separation
- **Unlimited color-coded profiles**, each with fully **isolated cookies, storage, cache, and extensions** (separate Chromium partitions)
- **Incognito profiles** — pure in-memory sessions; nothing touches disk, everything vanishes on close
- **Per-site permission memory** — camera, microphone, location, notifications, clipboard and more, remembered per origin
- **Chrome-style permission bubble** anchored to the address-bar lock icon — small, dismissible, no fullscreen interruption
- **Local favicon cache** — site icons are fetched from the site itself and cached on disk; unlike most browsers, Mergus never phones a third party (e.g. Google's icon service) with your browsing history
- **Built-in ad & tracker blocking** — a native request-level engine covering major ad networks, trackers, and analytics, with a live blocked-counter; no extension required, works in every profile including incognito

### Productivity
- **Command palette** (`Ctrl+K`) — every action at your fingertips
- **3-dot main menu** unifying tabs, downloads, library, AI, import, and settings
- **Library** — bookmarks, page likes with address-bar auto-suggest, and full searchable **history**
- **Real download manager** — every download asks where to save, with progress, open/reveal-in-folder, and cancel
- **Sidebar apps** — dock Gmail, YouTube, WhatsApp, Spotify… one click away, with per-app context actions
- **Import in seconds** — one-click bookmarks import from Chrome, Edge, and Brave, plus any bookmarks HTML file

### Local AI 🤖
- **Page summarization 100% on-device** — page text is extracted locally and sent only to a model running on your own PC (via [Ollama](https://ollama.com)); nothing ever goes to the cloud
- **Model manager** — list installed models, download new ones with live progress, delete, and one-click browsing of Hugging Face
- **Honest capability check** — Mergus reads your RAM/CPU and tells you which model sizes your PC can actually handle before you download gigabytes

### Craft
- **Glassmorphism UI** with per-profile theme hues, dark aesthetic, collapsible sidebar, custom frameless window controls
- **Full keyboard control** — see shortcuts below; shortcuts work even while a page has focus

---

## 🔒 Security engineering

Mergus treats the browser as hostile-input software, not a CRUD app:

| Area | What was done |
|---|---|
| Site permissions | Allow/Block prompt per origin with remember list — nothing auto-granted, camera/mic included |
| Downloads | Save-dialog confirmation for every file, visible progress, no silent drops |
| Navigation | Non-HTTP(S) top-level redirects (e.g. `file://` phishing) blocked at the view layer |
| Renderer hardening | `sandbox`, `contextIsolation`, no Node in pages, strict CSP on the browser UI |
| Extension installs | Unpacked extensions show a full permission manifest for approval before receiving file access; auto-downloaded components are hash-pinned and tamper-checked |
| Code protection | Shipped binary is obfuscated and packed (asar + integrity checks), DevTools disabled in release builds |
| Process model | Single-instance lock eliminates Chromium cache-lock corruption |

---

## 🛠 Tech stack & architecture

- **Runtime:** Electron 35 (Chromium) · Node.js · Windows x64 (NSIS installer + portable)
- **Tab engine:** one `WebContentsView` per tab, bounds-managed against a custom frameless chrome window
- **State & IPC:** main-process managers (tabs, profiles/sessions, extensions, downloads, AI, history store) bridged to the UI over a typed `contextBridge` API
- **Local services:** on-disk favicon cache served over a privileged custom scheme; private `mergus://` pages (start, error); Ollama REST integration for AI
- **Build:** obfuscated + asar-packaged release pipeline producing signed-layout installer and portable EXE

---

## ⌨️ Keyboard shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl+T` / `Ctrl+W` | New tab / close tab |
| `Ctrl+L` | Focus address bar |
| `Ctrl+F` / `Ctrl+K` / `Ctrl+P` | Find · Command palette · Print |
| `Ctrl +` / `Ctrl -` / `Ctrl 0` | Zoom in / out / reset |
| `Ctrl+1…9`, `Ctrl+Tab` | Jump to tab / cycle tabs |
| `Ctrl+R`, `F5` | Reload |

---

## 📥 Download & install

1. Download **`Mergus-Setup-1.0.0.exe`** (installer) or **`Mergus-Portable-1.0.0.exe`** (no install, runs anywhere) from this repository.
2. Run it — no account, no telemetry, no setup wizard questions.
3. Optional: install [Ollama](https://ollama.com) to unlock page summarization and the model manager; one-click import your Chrome/Edge bookmarks from the ⋮ menu.

> _Note: the release is unsigned, so Windows SmartScreen may ask for confirmation on first run — click “More info → Run anyway”._

---

## 🗺 Roadmap

Auto-updater · password manager with OS-keyring encryption · extension store · tab groups · cross-device profile sync · macOS/Linux builds.

---

## 📄 License

© Mergus. All rights reserved. This software is proprietary freeware — see [LICENSE](LICENSE) for the terms. Third-party components (Chromium, Electron, Ollama) remain property of their respective owners and are governed by their own licenses.

## 👤 Author

Built solo, end to end — product design, UI, browser engineering, security model, and release pipeline.

Omar Elhifny - Omar.a.elhifny@gmail.com - Linkedin.com/in/omar-elhifny/
