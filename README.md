# Elyvo Assist

Desktop AI assistant for meetings, research, and brainstorming sessions. Runs as an overlay above any window, triggered by a hotkey. Communicates with the backend for session management, AI modes, and chat processing.

This repository hosts public releases. Client source code is in `elyvo-assist-src`. Installers and binaries are published through GitHub Releases.

## Window protection from screen sharing

The chat window is hidden from screenshots, screen recording, and screen sharing (Zoom, Google Meet, Discord, OBS).

- **macOS / Windows** — native `set_content_protected`, works out of the box for all capture types.
- **Linux (KDE / KWin)** — screen recording / sharing works out of the box via `excludeFromCapture`. Static screenshots (Spectacle, PrintScreen) are **NOT** hidden without a KWin patch — see `elyvo-server/scripts/kwin-screenshot-patch.sh`.
- **Browser-based Zoom/Meet** — the OS window picker may show a preview, but the window content is hidden during the stream.

> **Manjaro / Ubuntu** — full screenshot protection requires patching KWin (see the script above). The patch must be reapplied after every KWin update.

## Roadmap

- [x] OAuth2 providers — sign-in via OAuth2 (in addition to email/password)
- [x] Projects — a `Project` entity for grouping sessions, project-scoped ambient chat
- [ ] Add MCP or tool for cross-session and per project memory using RAG or similar tool
- [x] Make it self-learning assistant
- [ ] Move from local render to server render
- [ ] Context saving tool
- [ ] Add centralized theme management to overlay chats