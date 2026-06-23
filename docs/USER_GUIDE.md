# Elyvo Assist — User Guide

> 🇷🇺 Это руководство также доступно на [русском](USER_GUIDE.ru.md).

Elyvo Assist is a desktop AI assistant for meetings, research, and brainstorming. It lives as a translucent overlay above any window, summoned with a hotkey. It can listen to your microphone and system audio, transcribe live, look at your screen, and answer questions in context — while staying hidden from screen sharing and screen recording.

This guide covers installation and an overview of the main features.

- [Installation](#installation)
- [First launch](#first-launch)
- [Permissions](#permissions)
- [The overlay and hotkeys](#the-overlay-and-hotkeys)
- [Features overview](#features-overview)
- [Settings](#settings)
- [Updating](#updating)
- [Uninstalling](#uninstalling)
- [Troubleshooting](#troubleshooting)

---

## Installation

Installers and binaries are published through [GitHub Releases](https://github.com/pdasilem/elyvo-assist/releases). Download the file that matches your platform from the latest release. All builds are 64-bit (`x86_64` / Apple Silicon).

Each release contains, per version `X.Y.Z`:

| Platform | File |
|----------|------|
| Windows (recommended) | `elyvo-assist-X.Y.Z-windows-x64-setup.exe` |
| Windows (MSI) | `elyvo-assist-X.Y.Z-windows-x64.msi` |
| macOS (Intel) | `elyvo-assist-X.Y.Z-macos-x64.dmg` |
| macOS (Apple Silicon) | `elyvo-assist-X.Y.Z-macos-arm64.dmg` |
| Debian / Ubuntu | `elyvo-assist-X.Y.Z-linux-x86_64.deb` |
| Arch / Manjaro | `elyvo-assist-X.Y.Z-1-x86_64.pkg.tar.zst` (+ `install.sh`) |

### Windows

1. Download the `...-setup.exe` (NSIS) installer — or the `.msi` if your organization prefers MSI deployment.
2. Run it and follow the prompts. The app installs to `Program Files\Elyvo Assist`.
3. Launch **Elyvo Assist** from the Start menu.

### macOS

1. Download the `.dmg` for your chip — `macos-x64` for Intel, `macos-arm64` for Apple Silicon (M1/M2/M3 and newer).
2. Open the disk image and drag **Elyvo Assist** into **Applications**.
3. On first launch, macOS may warn that the app is from an unidentified developer. Right-click the app → **Open** → **Open** to allow it.

> **Linux requirements.** Elyvo Assist targets the **KDE Plasma** desktop on **Wayland**. The overlay's screen-capture protection is implemented through KWin (KDE's compositor), so the hide-from-screen-sharing behavior works only under KDE/KWin. Other desktops (GNOME, etc.) can run the app, but the capture-protection guarantees do not apply. You also need a running **PipeWire** session for microphone and system-audio capture.

### Linux — Debian / Ubuntu

```bash
sudo apt install ./elyvo-assist-X.Y.Z-linux-x86_64.deb
```

`apt` resolves the runtime dependencies (WebKitGTK 4.1, OpenSSL 3, PipeWire). On older `apt` versions use `sudo dpkg -i ...` followed by `sudo apt -f install` to pull in missing dependencies.

### Linux — Arch / Manjaro

The fastest path is the published installer script, which downloads the package, installs the required system libraries, and runs `pacman` for you:

```bash
curl -fsSL https://github.com/pdasilem/elyvo-assist/releases/latest/download/install.sh -o install.sh
bash install.sh
```

The script only supports `pacman`-based systems and will install any missing runtime packages (GTK3, WebKit2GTK 4.1, PipeWire, libayatana-appindicator, and so on).

Prefer to do it by hand? Download the `.pkg.tar.zst` and install it directly:

```bash
sudo pacman -U elyvo-assist-X.Y.Z-1-x86_64.pkg.tar.zst
```

---

## First launch

1. **Sign in.** Elyvo Assist authenticates through your Elyvo account. You can sign in with **email and password** 
   or with available **OAuth2 Provider**. New users can create an account from the same screen.
2. **Onboarding.** A short wizard asks a few questions about you and what you do so the assistant can personalize 
   its answers. You can optionally attach any file describing you; it is used only to give the assistant more 
   context about you. You can revisit and edit these answers later from your profile.
3. **Splash → overlay.** After sign-in the app starts minimized into a small splash, then runs in the background. Bring up the chat overlay any time with the toggle hotkey (default `Ctrl+\`).

---

## Permissions

To listen and to see your screen, Elyvo Assist needs OS-level permissions. Open **Settings → Permissions** to review and grant them. The app requests:

- **Microphone** — to capture what you say.
- **System audio** — to capture the other side of a call (the audio coming out of your speakers).
- **Screen recording / capture** — so *Ask about my screen* can see the active window.
- **Accessibility** (macOS) — required for global hotkeys and overlay positioning.

Each permission shows a status of **Granted**, **Denied**, or **Not determined**, with a button to request it. If you deny a permission by mistake, grant it from your OS settings and reopen the panel.

> On Linux, system-audio capture uses PipeWire and the desktop portal. Make sure PipeWire is running (it is the default on current Manjaro and Ubuntu).

---

## The overlay and hotkeys

Elyvo Assist is driven almost entirely by the keyboard so you can use it without leaving your meeting. The chat overlay floats on top of other windows, is draggable, and is **hidden from screen sharing and recording** (see [window protection](../README.md#window-protection-from-screen-sharing)).

Default hotkeys (all rebindable in **Settings → Keybinds**):

| Action | Default | What it does |
|--------|---------|--------------|
| Toggle visibility | `Ctrl+\` | Show / hide the Elyvo overlay |
| Ask Elyvo | `Ctrl+Enter` | Ask about your screen or current audio |
| Clear chat | `Ctrl+R` | Clear the current conversation |
| Start / stop session | `Ctrl+Shift+\` | Begin or end a listening session |
| Move overlay | `Ctrl+↑ / ↓ / ← / →` | Reposition the window on screen |
| Scroll response | `Ctrl+Shift+↑ / ↓` | Scroll the answer up / down |

To rebind, open **Settings → Keybinds**, click a shortcut, and press the new combination.

---

## Features overview

### Sessions

A **session** is when Elyvo is actively listening and keeping context. Start or stop a session with `Ctrl+Shift+\`. During a session, Elyvo captures your microphone and (optionally) system audio, transcribes it live, and keeps the running transcript as context for your questions. You can choose which audio input device to use, and test your microphone and system audio levels, from Settings.

### Ask about your screen or audio

Press **Ask Elyvo** (`Ctrl+Enter`) and Elyvo answers using what's currently on your screen and the recent audio/transcript as context — useful for "summarize what was just said", "what's this error", or "draft a reply to this". You can also type a normal message into the chat box at any time.

### AI Modes

**Modes** let you tailor how the assistant behaves for different situations. Each mode has its own system prompt and an optional notes template. Manage them under **Modes**:

- Start from the **Template Gallery** or create a mode from scratch.
- Edit the system prompt to set tone, role, and rules (for example, a "Sales call" mode vs. a "Standup" mode).
- Attach **mode files** — reference material the assistant should keep in mind for that mode.
- Mark one mode active; there is always a general/default mode available.

### Ambient AI chat

Ambient chat is a lightweight, always-available chat that follows you across the app and can be scoped to a project. It is part of the paid plan (see **Settings → Billing**).

### Projects

**Projects** group related sessions and give the assistant shared, persistent context. Within a project you can manage:

- **Members** — see who's in the project and invite others by email (each invitee shows as *pending* until they accept).
- **Memory** — facts and context the assistant should remember across sessions in that project.
- **Rules** — guidance the assistant follows for that project.

When someone invites *you* to their project, the invitation appears at the top of **Projects** with **Accept** / **Reject** buttons. Ambient chat can be scoped to a project so answers draw on that project's memory and rules.

### Dashboard and history

The **Dashboard** is your home base: it lists past sessions as cards and lets you open a session's detail — its transcript, notes, and meeting summary. Use it to review or follow up after a meeting.

### Memory and self-learning

Elyvo improves with use. Under your **Profile** you can review and edit:

- **User memory** — long-lived facts about you and your preferences that the assistant applies everywhere.
- **Disambiguations** — clarifications the assistant has learned (for example, which "John" or which project you mean) so it stops guessing wrong.

### Window protection from screen sharing

The overlay is deliberately invisible to capture so you can use it during a shared call without it appearing in the stream. Coverage differs by platform — the [main README](../README.md#window-protection-from-screen-sharing) is the authoritative matrix. In short:

- **Windows** — hidden from all capture types out of the box.
- **Linux (KDE / KWin)** — hidden from screen *recording and sharing* out of the box; hiding it from static *screenshots* (Spectacle/PrintScreen) needs a one-time KWin patch, re-applied after KWin updates.
- **macOS** — uses the same native content-protection mechanism. Reliable on **macOS 14 and earlier**; on **macOS 15 and later** undetectability is **not guaranteed** and the overlay may appear in captures.

---

## Settings

Open Settings from the user menu. The tabs are:

- **General** — core preferences.
- **Keybinds** — view and rebind every hotkey.
- **Profile** — your onboarding answers, user memory, and disambiguations.
- **Security** — account security options.
- **Language** — interface / response language.
- **Billing** — your subscription and plan (gates paid features such as ambient AI chat).

---

## Updating

Download the newest installer for your platform from [Releases](https://github.com/pdasilem/elyvo-assist/releases) and run it over your existing install — settings and sign-in are preserved.

- **Arch / Manjaro:** re-run the `install.sh` from the latest release, or `sudo pacman -U` the new `.pkg.tar.zst`.
- **Debian / Ubuntu:** `sudo apt install ./elyvo-assist-<new-version>-linux-x86_64.deb`.
- **Windows / macOS:** run the new installer / open the new DMG.

> Linux KDE users: re-apply the KWin screenshot patch after a KWin system update if you rely on screenshot protection.

---

## Uninstalling

- **Windows** — *Settings → Apps → Installed apps → Elyvo Assist → Uninstall*.
- **macOS** — drag **Elyvo Assist** from *Applications* to the Trash.
- **Debian / Ubuntu** — `sudo apt remove elyvo-assist`.
- **Arch / Manjaro** — `sudo pacman -R elyvo-assist`.

---

## Troubleshooting

**The overlay won't appear.** Make sure the app is running (check the tray/menu bar) and press the toggle hotkey (`Ctrl+\`). On macOS, confirm Accessibility permission is granted, otherwise global hotkeys won't fire.

**No audio is captured.** Check **Settings → Permissions** for microphone and system-audio access, then pick the right input device and use the mic/system-audio test in Settings. On Linux, confirm PipeWire is running.

**The overlay still shows in screenshots on Linux.** Screen *recording/sharing* is hidden by default; static screenshots require the one-time KWin patch described in the [README](../README.md#window-protection-from-screen-sharing). Re-apply it after KWin updates.

**Sign-in problems.** Try the alternate method (email/password vs. Google), and make sure your system clock is correct — OAuth and token validation are time-sensitive.

For anything else, open an issue on the [releases repository](https://github.com/pdasilem/elyvo-assist/issues).