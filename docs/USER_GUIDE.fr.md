# Elyvo Assist — Guide de l'utilisateur

> 🌐 Ce guide est également disponible en : [English](USER_GUIDE.md) · [Беларуская](USER_GUIDE.be.md) · [Deutsch](USER_GUIDE.de.md) · [Español](USER_GUIDE.es.md) · **Français** · [Italiano](USER_GUIDE.it.md) · [Português](USER_GUIDE.pt.md) · [Русский](USER_GUIDE.ru.md) · [Українська](USER_GUIDE.uk.md)

Elyvo Assist est un assistant IA de bureau pour les réunions, la recherche et le brainstorming. Il se présente sous la forme d'une superposition translucide au-dessus de n'importe quelle fenêtre, invoquée par un raccourci clavier. Il peut écouter votre microphone et l'audio système, transcrire en direct, observer votre écran et répondre à des questions en contexte — tout en restant invisible lors du partage et de l'enregistrement d'écran.

Ce guide couvre l'installation et présente un aperçu des principales fonctionnalités.

- [Installation](#installation)
- [Premier lancement](#premier-lancement)
- [Autorisations](#autorisations)
- [La superposition et les raccourcis clavier](#la-superposition-et-les-raccourcis-clavier)
- [Aperçu des fonctionnalités](#aperçu-des-fonctionnalités)
- [Paramètres](#paramètres)
- [Mise à jour](#mise-à-jour)
- [Désinstallation](#désinstallation)
- [Dépannage](#dépannage)

---

## Installation

Les installateurs et binaires sont publiés via [GitHub Releases](https://github.com/pdasilem/elyvo-assist/releases). Téléchargez le fichier correspondant à votre plateforme depuis la dernière version. Toutes les versions sont en 64 bits (`x86_64` / Apple Silicon).

Chaque version contient, pour la version `X.Y.Z` :

| Plateforme | Fichier |
|----------|------|
| Windows (recommandé) | `elyvo-assist-X.Y.Z-windows-x64-setup.exe` |
| Windows (MSI) | `elyvo-assist-X.Y.Z-windows-x64.msi` |
| macOS (Intel) | `elyvo-assist-X.Y.Z-macos-x64.dmg` |
| macOS (Apple Silicon) | `elyvo-assist-X.Y.Z-macos-arm64.dmg` |
| Debian / Ubuntu | `elyvo-assist-X.Y.Z-linux-x86_64.deb` |
| Arch / Manjaro | `elyvo-assist-X.Y.Z-1-x86_64.pkg.tar.zst` (+ `install.sh`) |

### Windows

1. Téléchargez l'installateur `...-setup.exe` (NSIS) — ou le `.msi` si votre organisation préfère un déploiement via MSI.
2. Exécutez-le et suivez les instructions. L'application s'installe dans `Program Files\Elyvo Assist`.
3. Lancez **Elyvo Assist** depuis le menu Démarrer.

### macOS

1. Téléchargez le `.dmg` correspondant à votre puce — `macos-x64` pour Intel, `macos-arm64` pour Apple Silicon (M1/M2/M3 et versions ultérieures).
2. Ouvrez l'image disque et faites glisser **Elyvo Assist** vers **Applications**.
3. Au premier lancement, macOS peut avertir que l'application provient d'un développeur non identifié. Faites un clic droit sur l'application → **Ouvrir** → **Ouvrir** pour l'autoriser.

> **Exigences Linux.** Elyvo Assist cible le bureau **KDE Plasma** sous **Wayland**. La protection contre la capture d'écran de la superposition est implémentée via KWin (le compositeur de KDE), donc le comportement de masquage lors du partage d'écran ne fonctionne que sous KDE/KWin. D'autres environnements de bureau (GNOME, etc.) peuvent exécuter l'application, mais les garanties de protection contre la capture ne s'appliquent pas. Vous avez également besoin d'une session **PipeWire** active pour la capture du microphone et de l'audio système.

### Linux — Debian / Ubuntu

```bash
sudo apt install ./elyvo-assist-X.Y.Z-linux-x86_64.deb
```

`apt` résout les dépendances d'exécution (WebKitGTK 4.1, OpenSSL 3, PipeWire). Sur les anciennes versions d'`apt`, utilisez `sudo dpkg -i ...` suivi de `sudo apt -f install` pour récupérer les dépendances manquantes.

### Linux — Arch / Manjaro

Le moyen le plus rapide est le script d'installation publié, qui télécharge le paquet, installe les bibliothèques système requises et exécute `pacman` pour vous :

```bash
curl -fsSL https://github.com/pdasilem/elyvo-assist/releases/latest/download/install.sh -o install.sh
bash install.sh
```

Le script ne prend en charge que les systèmes basés sur `pacman` et installera tous les paquets d'exécution manquants (GTK3, WebKit2GTK 4.1, PipeWire, libayatana-appindicator, etc.).

Vous préférez le faire manuellement ? Téléchargez le `.pkg.tar.zst` et installez-le directement :

```bash
sudo pacman -U elyvo-assist-X.Y.Z-1-x86_64.pkg.tar.zst
```

---

## Premier lancement

1. **Connexion.** Connectez-vous avec **e-mail et mot de passe**, un **code e-mail à usage unique**, ou **Google**. Les nouveaux comptes sont créés depuis le même écran (e-mail → code de vérification → définition d'un mot de passe).
2. **Intégration.** Un court assistant de configuration vous guide à travers quelques étapes — dont les **autorisations** et la **création de votre premier projet** — et se termine par une étape **À propos de vous** où vous pouvez éventuellement joindre un fichier (`.pdf`, `.doc`, `.docx`, `.md`, `.txt`) pour donner à l'assistant davantage de contexte à votre sujet. Vous pouvez modifier cela plus tard depuis votre **Profil**.
3. **Commencer à l'utiliser.** Une fois l'intégration terminée, le **Tableau de bord** s'ouvre. Invoquez la superposition de chat à tout moment avec le raccourci de bascule (par défaut `Ctrl+\`).

---

## Autorisations

Pour écouter et voir votre écran, Elyvo Assist a besoin de deux autorisations au niveau du système d'exploitation, demandées pendant l'intégration :

- **Microphone** — pour capturer ce que vous dites.
- **Capture d'écran** — pour que *Interroger mon écran* puisse voir la fenêtre active.

Sur **Windows** et **macOS**, celles-ci sont gérées via les invites habituelles du système. Sur **Linux**, accordez-les lorsqu'elles sont demandées ; si vous en refusez une par erreur, accordez-la depuis les paramètres de confidentialité de votre système d'exploitation.

Les paramètres audio et microphone eux-mêmes ne peuvent pas être configurés dans l'application — Elyvo utilise toujours le périphérique **par défaut** de votre système.

> Sur Linux, la capture du microphone et de l'audio système utilise PipeWire et le portail de bureau. Assurez-vous que PipeWire est en cours d'exécution (c'est le comportement par défaut sur les versions actuelles de Manjaro et Ubuntu).

---

## La superposition et les raccourcis clavier

Elyvo Assist se pilote presque entièrement au clavier afin que vous puissiez l'utiliser sans quitter votre réunion. La superposition de chat flotte au-dessus des autres fenêtres, est déplaçable, et est **masquée lors du partage et de l'enregistrement d'écran** (voir [protection de la fenêtre](../README.md#window-protection-from-screen-sharing)).

Raccourcis clavier par défaut (tous personnalisables dans **Paramètres → Raccourcis**) :

| Action | Par défaut | Ce qu'il fait |
|--------|---------|--------------|
| Basculer la visibilité | `Ctrl+\` | Afficher / masquer la superposition Elyvo |
| Interroger Elyvo | `Ctrl+Entrée` | Interroger votre écran ou l'audio en cours |
| Effacer le chat | `Ctrl+R` | Effacer la conversation en cours |
| Démarrer / arrêter la session | `Ctrl+Maj+\` | Démarrer ou terminer une session d'écoute |
| Déplacer la superposition | `Ctrl+↑ / ↓ / ← / →` | Repositionner la fenêtre à l'écran |
| Faire défiler la réponse | `Ctrl+Maj+↑ / ↓` | Faire défiler la réponse vers le haut / le bas |

Pour réattribuer un raccourci, ouvrez **Paramètres → Raccourcis**, cliquez sur un raccourci, puis appuyez sur la nouvelle combinaison.

---

## Aperçu des fonctionnalités

### Sessions

Une **session** correspond au moment où Elyvo écoute activement et conserve le contexte. Démarrez ou arrêtez une session avec `Ctrl+Maj+\`. Pendant une session, Elyvo capture votre microphone et l'audio système, transcrit en direct, et conserve la transcription en cours comme contexte pour vos questions. Elyvo utilise le périphérique d'entrée **par défaut** de votre système (vous ne pouvez pas le changer dans l'application) ; dans les Paramètres, vous pouvez voir le périphérique détecté et tester les niveaux de votre microphone et de l'audio système avec des indicateurs en direct.

### Interroger votre écran ou votre audio

Appuyez sur **Interroger Elyvo** (`Ctrl+Entrée`) et Elyvo répond en utilisant ce qui est actuellement à l'écran ainsi que l'audio/la transcription récents comme contexte — utile pour « résumer ce qui vient d'être dit », « qu'est-ce que cette erreur », ou « rédiger une réponse à ceci ». Vous pouvez également taper un message normal dans la zone de chat à tout moment.

### Modes IA

Les **Modes** vous permettent d'adapter le comportement de l'assistant selon les situations. Chaque mode dispose de son propre prompt système et d'un modèle de notes optionnel. Gérez-les sous **Modes** :

- Partez de la **Galerie de modèles** — ses modèles sont fournis par le serveur et évoluent avec le temps — ou créez un mode à partir de zéro.
- Modifiez le prompt système pour définir le ton, le rôle et les règles adaptés à cette situation.
- Joignez des **fichiers de mode** — du matériel de référence que l'assistant doit garder à l'esprit pour ce mode.
- Marquez un mode comme actif ; un mode général/par défaut est toujours disponible.

### Chat IA ambiant

Le chat ambiant est un chat léger, toujours disponible, qui vous suit dans toute l'application et peut être limité à un projet. Il fait partie de l'offre payante (voir **Paramètres → Facturation**).

### Projets

Les **Projets** regroupent des sessions liées et donnent à l'assistant un contexte partagé et persistant. Au sein d'un projet, vous pouvez gérer :

- **Membres** — voir qui fait partie du projet et inviter d'autres personnes par e-mail (chaque invité apparaît comme *en attente* jusqu'à ce qu'il accepte).
- **Mémoire** — des faits et du contexte que l'assistant doit retenir d'une session à l'autre dans ce projet.
- **Règles** — des consignes que l'assistant suit pour ce projet.
- **Paramètres** — un **mode**, une **langue de sortie** et une **langue de transcription** par projet, ainsi que **Enrichir le contexte** — un bouton (désactivé par défaut) qui permet à l'assistant de puiser du contexte pertinent dans vos *autres* sessions du même projet (rappel inter-sessions).

Lorsque quelqu'un vous invite à rejoindre son projet, l'invitation apparaît en haut de **Projets** avec des boutons **Accepter** / **Refuser**. Le chat ambiant peut être limité à un projet afin que les réponses s'appuient sur la mémoire et les règles de ce projet.

### Documents

Elyvo peut conserver une bibliothèque personnelle de documents de référence que vous pouvez afficher dans leur propre superposition pendant que vous travaillez — pratique pour garder des notes, un brief ou une checklist à portée de main pendant un appel.

- **Gérer vos documents.** Dans **Paramètres → Ressources**, ajoutez des fichiers Markdown (`.md`) — jusqu'à **1 Mo** chacun — sous *Vos documents*, ou supprimez ceux dont vous n'avez plus besoin. Les documents sont privés à votre compte.
- **Activer par projet.** Pour le projet actif, cochez les documents que vous voulez avoir sous la main. Les documents activés **s'ouvrent automatiquement en onglets** dans la visionneuse de documents chaque fois que vous l'ouvrez pour ce projet. Activer un document contrôle ce que la visionneuse affiche pour ce projet ; cela n'injecte pas le contenu du fichier dans les réponses de l'assistant.
- **Ouvrir la visionneuse.** Depuis le menu de session de la superposition de chat (le bouton `···`), choisissez **Documents**. Elle s'ouvre comme sa propre fenêtre déplaçable qui, comme la superposition principale, est **masquée lors du partage et de l'enregistrement d'écran**. Le même élément de menu permet de la refermer.
- **Lire et changer d'onglet.** Chaque document s'ouvre dans son propre onglet. Utilisez l'onglet **+** pour ouvrir n'importe lequel de vos documents, cliquez sur un onglet pour y basculer, et **×** pour le fermer. Le contenu s'affiche en Markdown formaté et suit le thème et la taille de police de votre chat.

### Calendrier et réunions

Connectez **Google Agenda** (depuis **Paramètres → Général**) pour voir vos réunions à venir dans Elyvo. Sur une carte de réunion, **« Rejoindre la réunion → »** se contente d'ouvrir le lien de l'appel (Zoom/Meet/Teams) dans votre navigateur, tandis que **« Prendre des notes »** démarre une session d'écoute. Peu avant une réunion, Elyvo affiche aussi un rappel dans l'application avec son propre bouton **« Prendre des notes »**, qui fait les deux à la fois — démarre la session et ouvre le lien de l'appel — afin que l'assistant écoute dès que vous rejoignez la réunion.

### Tableau de bord et historique

Le **Tableau de bord** est votre point de départ : il liste les sessions passées sous forme d'une liste consultable par recherche et regroupée par date (le champ de recherche se trouve dans l'en-tête de l'application) et vous permet d'ouvrir le détail d'une session, lequel comporte trois onglets — **Résumé** (le résumé de la réunion), **Transcription** (la transcription capturée) et **Utilisation** (les questions que vous avez posées à Elyvo pendant la session et ses réponses). Utilisez-le pour relire ou faire un suivi après une réunion.

### Mémoire et auto-apprentissage

Elyvo s'améliore avec l'usage. Dans votre **Profil**, vous pouvez consulter et modifier :

- **Mémoire utilisateur** — des faits durables vous concernant et vos préférences, que l'assistant applique partout.
- **Désambiguïsations** — des clarifications que l'assistant a apprises (par exemple, de quel « John » ou de quel projet vous parlez) afin qu'il cesse de mal deviner.

### Protection de la fenêtre contre le partage d'écran

La superposition est délibérément invisible à la capture afin que vous puissiez l'utiliser pendant un appel partagé sans qu'elle apparaisse dans le flux. La couverture diffère selon la plateforme — le [README principal](../README.md#window-protection-from-screen-sharing) fait foi pour la matrice complète. En résumé :

- **Windows 11** — masquée de tous les types de capture dès l'installation.
- **Windows 10** — même protection, mais **non garantie** : une limitation connue du système d'exploitation peut afficher la superposition sous forme de rectangle noir dans la capture au lieu de la masquer proprement.
- **Linux (KDE / KWin)** — masquée de l'*enregistrement et du partage* d'écran dès l'installation ; la masquer des *captures d'écran* statiques (Spectacle/PrintScreen) nécessite un correctif KWin ponctuel, à réappliquer après chaque mise à jour de KWin.
- **macOS** — utilise le même mécanisme natif de protection du contenu. Fiable sur **macOS 14 et versions antérieures** ; sur **macOS 15 et versions ultérieures**, la non-détectabilité n'est **pas garantie** et la superposition peut apparaître dans les captures.

---

## Paramètres

Ouvrez les Paramètres depuis le menu utilisateur. Les onglets sont :

- **Général** — préférences principales, périphérique d'entrée audio détecté et indicateurs de test du microphone / de l'audio système, connexion à Google Agenda, options de capture d'écran, et **Vérifier les mises à jour**.
- **Raccourcis** — consultez et réattribuez chaque raccourci clavier.
- **Profil** — vos réponses d'intégration, la mémoire utilisateur et les désambiguïsations.
- **Sécurité** — options de sécurité du compte.
- **Langue** — langue de l'interface / des réponses.
- **Ressources** — téléversez et gérez vos documents Markdown, et choisissez lesquels sont activés pour le projet actif (voir [Documents](#documents)).
- **Facturation** — votre abonnement et votre offre (conditionne les fonctionnalités payantes telles que le chat IA ambiant).

---

## Mise à jour

Elyvo Assist ne se met **pas** à jour lui-même, mais la vérification de version est bien automatique : le serveur interroge périodiquement GitHub (environ toutes les 8 heures, plus une fois au démarrage du serveur) à la recherche de nouvelles versions et, s'il en trouve une plus récente, envoie sur votre Tableau de bord une annonce que vous pouvez fermer, **« New version! »** (le titre reste en anglais), avec un lien de téléchargement. Vous pouvez aussi déclencher manuellement **Vérifier les mises à jour** dans **Paramètres → Général** à tout moment pour ouvrir directement la page [Releases](https://github.com/pdasilem/elyvo-assist/releases) dans votre navigateur.

Pour mettre à jour, téléchargez le dernier installateur pour votre plateforme depuis [Releases](https://github.com/pdasilem/elyvo-assist/releases) et exécutez-le par-dessus votre installation existante — les paramètres et la connexion sont conservés.

- **Arch / Manjaro :** relancez le `install.sh` de la dernière version, ou exécutez `sudo pacman -U` sur le nouveau `.pkg.tar.zst`.
- **Debian / Ubuntu :** `sudo apt install ./elyvo-assist-<nouvelle-version>-linux-x86_64.deb`.
- **Windows / macOS :** exécutez le nouvel installateur / ouvrez le nouveau DMG.

> Utilisateurs Linux KDE : réappliquez le correctif KWin pour les captures d'écran après une mise à jour système de KWin si vous comptez sur la protection des captures d'écran.

---

## Désinstallation

- **Windows** — *Paramètres → Applications → Applications installées → Elyvo Assist → Désinstaller*.
- **macOS** — faites glisser **Elyvo Assist** depuis *Applications* vers la Corbeille.
- **Debian / Ubuntu** — `sudo apt remove elyvo-assist`.
- **Arch / Manjaro** — `sudo pacman -R elyvo-assist`.

---

## Dépannage

**La superposition n'apparaît pas.** Assurez-vous que l'application est en cours d'exécution (vérifiez la barre système/la barre de menus) et appuyez sur le raccourci de bascule (`Ctrl+\`). Sur macOS, vérifiez que l'autorisation Accessibilité est accordée, sinon les raccourcis clavier globaux ne fonctionneront pas.

**Aucun audio n'est capturé.** Vérifiez l'accès au microphone et à la capture d'écran dans les paramètres de confidentialité de votre système d'exploitation, puis utilisez le test du microphone / de l'audio système dans **Paramètres → Général** pour confirmer les niveaux. Elyvo utilise le périphérique d'entrée par défaut de votre système, définissez donc le bon périphérique par défaut dans les paramètres audio de votre système d'exploitation. Sur Linux, vérifiez que PipeWire est en cours d'exécution.

**La superposition apparaît toujours dans les captures d'écran sous Linux.** L'*enregistrement/le partage* d'écran est masqué par défaut ; les captures d'écran statiques nécessitent le correctif KWin ponctuel décrit dans le [README](../README.md#window-protection-from-screen-sharing). Réappliquez-le après les mises à jour de KWin.

**Problèmes de connexion.** Essayez la méthode alternative (e-mail/mot de passe plutôt que Google), et assurez-vous que l'horloge de votre système est correcte — la validation OAuth et des jetons est sensible au temps.

Pour tout autre problème, ouvrez un ticket sur le [dépôt des versions](https://github.com/pdasilem/elyvo-assist/issues).
