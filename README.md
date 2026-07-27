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