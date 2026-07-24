# Elyvo Assist

Desktop AI assistant for meetings, research, and brainstorming sessions. Runs as an overlay above any window, triggered by a hotkey. Communicates with the backend for session management, AI modes, and chat processing.

This repository hosts public releases. Client source code is in `elyvo-assist-src`. Installers and binaries are published through GitHub Releases.

📖 **User Guide** — installation per platform and a full features overview, available in every language the app's interface supports:

| Language | Guide |
|----------|-------|
| English | [USER_GUIDE.md](docs/USER_GUIDE.md) |
| Беларуская (Belarusian) | [USER_GUIDE.be.md](docs/USER_GUIDE.be.md) |
| Deutsch (German) | [USER_GUIDE.de.md](docs/USER_GUIDE.de.md) |
| Español (Spanish) | [USER_GUIDE.es.md](docs/USER_GUIDE.es.md) |
| Français (French) | [USER_GUIDE.fr.md](docs/USER_GUIDE.fr.md) |
| Italiano (Italian) | [USER_GUIDE.it.md](docs/USER_GUIDE.it.md) |
| Português (Portuguese) | [USER_GUIDE.pt.md](docs/USER_GUIDE.pt.md) |
| Русский (Russian) | [USER_GUIDE.ru.md](docs/USER_GUIDE.ru.md) |
| Українська (Ukrainian) | [USER_GUIDE.uk.md](docs/USER_GUIDE.uk.md) |

## Window protection from screen sharing

The chat window is hidden from screenshots, screen recording, and screen sharing (Zoom, Google Meet, Discord, OBS).

- **Windows 11** — native `set_content_protected`, works out of the box for all capture types.
- **Windows 10** — same mechanism, but **NOT guaranteed**: a known Windows/DWM limitation can make the window appear as a solid black rectangle in the capture instead of being cleanly excluded (varies by build and by the screen-sharing/recording tool used).
- **macOS** — native `set_content_protected`; reliable on macOS 14 and earlier. On macOS 15+ undetectability is **NOT** guaranteed and the window may appear in captures.
- **Linux (KDE / KWin)** — screen recording / sharing works out of the box via `excludeFromCapture`. On **KWin 6.7.0+ (Plasma 6.7+)** static screenshots are also hidden out of the box — no patch needed. On older KWin (≤ 6.6.x) static screenshots (Spectacle, PrintScreen) are **NOT** hidden without a KWin patch — see `elyvo-assist-src/scripts/kwin/kwin-screenshot-patch.sh`.
- **Browser-based Zoom/Meet** — the OS window picker may show a preview, but the window content is hidden during the stream.

> **Manjaro / Ubuntu** — on KWin older than 6.7.0, full screenshot protection requires patching KWin (see the script above); the patch must be reapplied after every KWin update. From KWin 6.7.0+ the protection is built in and no patch is needed.

## Roadmap

- [x] OAuth2 providers — sign-in via OAuth2 (in addition to email/password)
- [x] Projects — a `Project` entity for grouping sessions, project-scoped ambient chat
- [x] Add tool for cross-session and per project memory using RAG or similar tool
- [x] Make it self-learning assistant
- [ ] Move from local render to server render
- [x] Context saving tool
- [x] Add centralized theme management to overlay chats
- [ ] Add mobile app
- [x] Add web-search tool
- [x] Add centralized message overlay
- [x] Add doc viewer
- [ ] Add calendar and meeting creator
- [ ] Add small menu bar to manage chat/resources
- [x] Add interface translation  