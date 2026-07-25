# Elyvo Assist — Benutzerhandbuch

> 🌐 Dieser Leitfaden ist auch verfügbar auf: [English](USER_GUIDE.md) · [Беларуская](USER_GUIDE.be.md) · **Deutsch** · [Español](USER_GUIDE.es.md) · [Français](USER_GUIDE.fr.md) · [Italiano](USER_GUIDE.it.md) · [Português](USER_GUIDE.pt.md) · [Русский](USER_GUIDE.ru.md) · [Українська](USER_GUIDE.uk.md)

Elyvo Assist ist ein Desktop-KI-Assistent für Meetings, Recherchen und Brainstormings. Er läuft als durchscheinendes Overlay über jedem Fenster und wird per Tastenkombination aufgerufen. Er kann dein Mikrofon und den Systemton mithören, live transkribieren, deinen Bildschirm sehen und Fragen im Kontext beantworten — und bleibt dabei vor Bildschirmfreigabe und Bildschirmaufnahme verborgen.

Dieser Leitfaden behandelt die Installation und einen Überblick über die wichtigsten Funktionen.

- [Installation](#installation)
- [Erster Start](#erster-start)
- [Berechtigungen](#berechtigungen)
- [Das Overlay und die Tastenkombinationen](#das-overlay-und-die-tastenkombinationen)
- [Funktionsübersicht](#funktionsübersicht)
- [Einstellungen](#einstellungen)
- [Aktualisieren](#aktualisieren)
- [Deinstallieren](#deinstallieren)
- [Fehlerbehebung](#fehlerbehebung)

---

## Installation

Installationsprogramme und Binärdateien werden über [GitHub Releases](https://github.com/pdasilem/elyvo-assist/releases) veröffentlicht. Lade die zu deiner Plattform passende Datei aus dem neuesten Release herunter. Alle Builds sind 64-Bit (`x86_64` / Apple Silicon).

Jedes Release enthält, pro Version `X.Y.Z`:

| Plattform | Datei |
|----------|------|
| Windows | `elyvo-assist-X.Y.Z-windows-x64-setup.exe` |
| macOS (Intel) | `elyvo-assist-X.Y.Z-macos-x64.dmg` |
| macOS (Apple Silicon) | `elyvo-assist-X.Y.Z-macos-arm64.dmg` |
| Debian / Ubuntu | `elyvo-assist-X.Y.Z-linux-x86_64.deb` |
| Arch / Manjaro | `elyvo-assist-X.Y.Z-1-x86_64.pkg.tar.zst` (+ `install.sh`) |

### Windows

1. Lade das Installationsprogramm `...-setup.exe` (NSIS) herunter.
2. Führe es aus und folge den Anweisungen. Die App wird unter `Program Files\Elyvo Assist` installiert.
3. Starte **Elyvo Assist** über das Startmenü.

### macOS

1. Lade die `.dmg`-Datei für deinen Chip herunter — `macos-x64` für Intel, `macos-arm64` für Apple Silicon (M1/M2/M3 und neuer).
2. Öffne das Disk-Image und ziehe **Elyvo Assist** in den Ordner **Programme**.
3. Beim ersten Start warnt macOS möglicherweise, dass die App von einem nicht identifizierten Entwickler stammt. Klicke mit der rechten Maustaste auf die App → **Öffnen** → **Öffnen**, um sie zuzulassen.

> **Linux-Anforderungen.** Elyvo Assist ist auf die Desktop-Umgebung **KDE Plasma** unter **Wayland** ausgerichtet. Der Bildschirmaufnahmeschutz des Overlays ist über KWin (den Compositor von KDE) implementiert, daher funktioniert das Verbergen vor Bildschirmfreigabe nur unter KDE/KWin. Andere Desktop-Umgebungen (GNOME usw.) können die App ausführen, aber die Garantien zum Aufnahmeschutz gelten dort nicht. Außerdem benötigst du eine laufende **PipeWire**-Sitzung für die Mikrofon- und Systemton-Aufnahme.

### Linux — Debian / Ubuntu

```bash
sudo apt install ./elyvo-assist-X.Y.Z-linux-x86_64.deb
```

`apt` löst die Laufzeitabhängigkeiten auf (WebKitGTK 4.1, OpenSSL 3, PipeWire). Bei älteren `apt`-Versionen verwende `sudo dpkg -i ...`, gefolgt von `sudo apt -f install`, um fehlende Abhängigkeiten nachzuladen.

### Linux — Arch / Manjaro

Der schnellste Weg ist das veröffentlichte Installationsskript, das das Paket herunterlädt, die erforderlichen Systembibliotheken installiert und `pacman` für dich ausführt:

```bash
curl -fsSL https://github.com/pdasilem/elyvo-assist/releases/latest/download/install.sh -o install.sh
bash install.sh
```

Das Skript unterstützt nur `pacman`-basierte Systeme und installiert alle fehlenden Laufzeitpakete (GTK3, WebKit2GTK 4.1, PipeWire, libayatana-appindicator und so weiter).

Möchtest du es lieber manuell erledigen? Lade die `.pkg.tar.zst`-Datei herunter und installiere sie direkt:

```bash
sudo pacman -U elyvo-assist-X.Y.Z-1-x86_64.pkg.tar.zst
```

---

## Erster Start

1. **Anmelden.** Melde dich mit **E-Mail und Passwort**, einem **einmaligen E-Mail-Code** oder mit **Google** an. Neue Konten werden über denselben Bildschirm erstellt (E-Mail → Bestätigungscode → Passwort festlegen).
2. **Onboarding.** Ein kurzer Einrichtungsassistent führt dich durch einige Schritte — einschließlich der **Berechtigungen** und dem **Anlegen deines ersten Projekts** — und endet mit einem Schritt **Über dich**, in dem du optional eine Datei (`.pdf`, `.doc`, `.docx`, `.md`, `.txt`) anhängen kannst, um dem Assistenten mehr Kontext über dich zu geben. Du kannst dies später in deinem **Profil** bearbeiten.
3. **Loslegen.** Nach dem Onboarding öffnet sich das **Dashboard**. Rufe das Chat-Overlay jederzeit mit der Umschalt-Tastenkombination auf (Standard `Ctrl+\`).

---

## Berechtigungen

Um mitzuhören und deinen Bildschirm zu sehen, benötigt Elyvo Assist zwei Berechtigungen auf Betriebssystemebene, die während des Onboardings angefragt werden:

- **Mikrofon** — um aufzuzeichnen, was du sagst.
- **Bildschirmaufnahme** — damit *Frage zu meinem Bildschirm* das aktive Fenster sehen kann.

Unter **Windows** und **macOS** werden diese über die normalen Systemabfragen gehandhabt. Unter **Linux** erteilst du sie, wenn danach gefragt wird; falls du eine versehentlich verweigerst, erteile sie stattdessen in den Datenschutzeinstellungen deines Betriebssystems.

Die Audio- und Mikrofoneinstellungen selbst lassen sich nicht in der App konfigurieren — Elyvo verwendet immer das **Standardgerät** deines Systems.

> Unter Linux verwenden die Mikrofon- und Systemton-Aufnahme PipeWire und das Desktop-Portal. Stelle sicher, dass PipeWire läuft (es ist auf aktuellen Manjaro- und Ubuntu-Systemen der Standard).

---

## Das Overlay und die Tastenkombinationen

Elyvo Assist wird fast ausschließlich über die Tastatur gesteuert, sodass du es benutzen kannst, ohne dein Meeting zu verlassen. Das Chat-Overlay schwebt über anderen Fenstern, lässt sich verschieben und ist **vor Bildschirmfreigabe und -aufnahme verborgen** (siehe [Fensterschutz](../README.md#window-protection-from-screen-sharing)).

Standard-Tastenkombinationen (alle unter **Einstellungen → Tastenkombinationen** neu belegbar):

| Aktion | Standard | Was sie bewirkt |
|--------|---------|--------------|
| Sichtbarkeit umschalten | `Ctrl+\` | Elyvo-Overlay anzeigen / ausblenden |
| Elyvo fragen | `Ctrl+Enter` | Frage zu deinem Bildschirm oder dem aktuellen Audio stellen |
| Chat leeren | `Ctrl+R` | Die aktuelle Unterhaltung löschen |
| Sitzung starten / beenden | `Ctrl+Shift+\` | Eine Zuhör-Sitzung beginnen oder beenden |
| Overlay verschieben | `Ctrl+↑ / ↓ / ← / →` | Das Fenster auf dem Bildschirm neu positionieren |
| Antwort scrollen | `Ctrl+Shift+↑ / ↓` | Die Antwort nach oben / unten scrollen |

Um eine Tastenkombination neu zu belegen, öffne **Einstellungen → Tastenkombinationen**, klicke auf einen Shortcut und drücke die neue Kombination.

---

## Funktionsübersicht

### Sitzungen

Eine **Sitzung** ist der Zeitraum, in dem Elyvo aktiv zuhört und den Kontext behält. Starte oder beende eine Sitzung mit `Ctrl+Shift+\`. Während einer Sitzung nimmt Elyvo dein Mikrofon und den Systemton auf, transkribiert live und behält das laufende Transkript als Kontext für deine Fragen bei. Elyvo verwendet das **Standard**-Eingabegerät deines Systems (du kannst es in der App nicht ändern); in den Einstellungen siehst du das erkannte Gerät und kannst deine Mikrofon- und Systemton-Pegel mit Live-Anzeigen testen.

### Frage zu deinem Bildschirm oder Audio stellen

Drücke **Elyvo fragen** (`Ctrl+Enter`), und Elyvo antwortet anhand dessen, was gerade auf deinem Bildschirm zu sehen ist, sowie des jüngsten Audios/Transkripts als Kontext — nützlich für „Fasse zusammen, was gerade gesagt wurde", „Was bedeutet dieser Fehler" oder „Entwirf eine Antwort darauf". Du kannst jederzeit auch eine normale Nachricht in das Chat-Feld eingeben.

### Schnellaktionen

Während einer Sitzung bietet der Chat fünf Ein-Klick-Aktionen. Sie sind **rollenbewusst**: Jede bezieht ihre Bedeutung aus Situation und Ziel des aktiven Modus — dieselbe Schaltfläche hilft also anders, je nachdem, ob du antwortest, bewertest, verhandelst oder lernst.

- **Assist** — die Substanz, die der Moment verlangt: die Antwort auf das, was dich gerade gefragt wurde; eine Referenzantwort oder eine schnelle Einschätzung, wenn *du* bewertest; die vollständige Lösung, wenn der Screenshot eine Aufgabe enthält. Material zum Denken, keine Worte zum Aussprechen.
- **What should I say?** — der eine nächste Satz, den du laut sagen solltest, in deiner Stimme, direkt verwendbar.
- **Follow-up questions** — ein Satz von 3–4 Fragen, die du als Nächstes stellen könntest, um dein Ziel voranzubringen: ein Menü zur Auswahl, nicht eine einzelne Zeile.
- **What did they mean?** — entschlüsselt die letzte Äußerung der Gegenseite: ihre Aussage, ihre Absicht und unausgesprochene Bedenken.
- **Recap** — bis zu drei Stichpunkte dazu, was sich seit deinem letzten Blick geändert hat, entschieden oder gefragt wurde.

So funktioniert die Rotation: In einem Kandidaten-Modus beantwortet Assist die an dich gerichtete Frage; in einem Prüfer-Modus liefert es die Referenzantwort, an der du eine Antwort messen kannst; in einem Verhandlungs-Modus werden Follow-up questions zu Sondierungsfragen. In einem Vorlesungs- oder Webinar-Modus, in dem du hauptsächlich zuhörst, erklärt Assist den gerade gemachten Punkt einfacher, Follow-up questions werden zu Fragen an den Vortragenden oder zu Verständnischecks, und Recap bringt dich nach einer Ablenkung wieder auf Stand. Gesteuert wird das vom Systemprompt des aktiven Modus — die Schaltflächen bleiben dieselben (siehe **KI-Modi** unten).

### KI-Modi

Mit **Modi** kannst du das Verhalten des Assistenten für verschiedene Situationen anpassen. Jeder Modus hat seinen eigenen System-Prompt und optional eine Notizvorlage. Verwalte sie unter **Modi**:

- Starte mit der **Vorlagen-Galerie** — ihre Vorlagen werden vom Server bereitgestellt und ändern sich mit der Zeit — oder erstelle einen Modus von Grund auf.
- Bearbeite den System-Prompt, um Tonfall, Rolle und Regeln für diese Situation festzulegen.
- Hänge **Modus-Dateien** an — Referenzmaterial, das der Assistent für diesen Modus berücksichtigen soll.
- Markiere einen Modus als aktiv; es gibt immer einen allgemeinen Standardmodus.

### Ambient-KI-Chat

Der Ambient-Chat ist ein schlanker, jederzeit verfügbarer Chat, der dich durch die gesamte App begleitet und auf ein Projekt eingegrenzt werden kann. Er ist Teil des kostenpflichtigen Plans (siehe **Einstellungen → Abrechnung**).

### Projekte

**Projekte** fassen zusammengehörige Sitzungen zusammen und geben dem Assistenten einen gemeinsamen, dauerhaften Kontext. Innerhalb eines Projekts kannst du verwalten:

- **Mitglieder** — sehen, wer im Projekt ist, und andere per E-Mail einladen (jede eingeladene Person wird bis zur Annahme als *ausstehend* angezeigt).
- **Gedächtnis** — Fakten und Kontext, an die sich der Assistent über Sitzungen hinweg in diesem Projekt erinnern soll.
- **Regeln** — Vorgaben, an die sich der Assistent für dieses Projekt hält.
- **Einstellungen** — ein projektspezifischer **Modus**, eine **Ausgabesprache** und eine **Transkriptsprache**, sowie **Kontext anreichern** — ein Umschalter (standardmäßig deaktiviert), mit dem der Assistent relevanten Kontext aus deinen *anderen* Sitzungen im selben Projekt heranziehen kann (sitzungsübergreifender Rückgriff).

Wenn dich jemand in sein Projekt einlädt, erscheint die Einladung oben in **Projekte** mit den Schaltflächen **Annehmen** / **Ablehnen**. Der Ambient-Chat kann auf ein Projekt eingegrenzt werden, sodass Antworten auf dem Gedächtnis und den Regeln dieses Projekts basieren.

### Dokumente

Elyvo kann eine persönliche Bibliothek mit Referenzdokumenten führen, die du dir während der Arbeit als eigenes Overlay aufrufen kannst — praktisch, um Notizen, ein Briefing oder eine Checkliste während eines Anrufs griffbereit zu haben.

- **Deine Dokumente verwalten.** Füge unter **Einstellungen → Ressourcen** Markdown-Dateien (`.md`) — jeweils bis zu **1 MB** — unter *Deine Dokumente* hinzu oder lösche nicht mehr benötigte. Dokumente sind privat für dein Konto.
- **Pro Projekt aktivieren.** Hake für das aktive Projekt die Dokumente ab, die griffbereit sein sollen. Aktivierte Dokumente **öffnen sich automatisch als Tabs** im Dokumenten-Viewer, sobald du ihn für dieses Projekt öffnest. Das Aktivieren eines Dokuments steuert, was der Viewer für dieses Projekt anzeigt; es speist den Inhalt der Datei nicht in die Antworten des Assistenten ein.
- **Den Viewer öffnen.** Wähle im Sitzungsmenü des Chat-Overlays (die Schaltfläche `···`) **Dokumente**. Es öffnet sich als eigenes, verschiebbares Fenster, das wie das Haupt-Overlay **vor Bildschirmfreigabe und -aufnahme verborgen** ist. Derselbe Menüpunkt schließt es wieder.
- **Lesen und wechseln.** Jedes Dokument öffnet sich in einem eigenen Tab. Nutze den **+**-Tab, um eines deiner Dokumente zu öffnen, klicke auf einen Tab zum Wechseln und auf **×**, um ihn zu schließen. Der Inhalt wird als formatiertes Markdown dargestellt und folgt deinem Chat-Theme und deiner Schriftgröße.

### Kalender und Meetings

Verbinde **Google Kalender** (unter **Einstellungen → Allgemein**), um deine anstehenden Meetings in Elyvo zu sehen. Auf einer Meeting-Karte öffnet **„Meeting beitreten →"** lediglich den Anruflink (Zoom/Meet/Teams) in deinem Browser, während **„Notizen aufnehmen"** eine Zuhör-Sitzung startet. Kurz vor einem Meeting zeigt Elyvo außerdem eine In-App-Erinnerung mit einer eigenen Schaltfläche **„Notizen aufnehmen"**, die beides zugleich erledigt — die Sitzung startet und den Anruflink öffnet —, sodass der Assistent ab dem Moment mithört, in dem du beitrittst.

### Dashboard und Verlauf

Das **Dashboard** ist deine Startzentrale: Es listet vergangene Sitzungen als durchsuchbare, nach Datum gruppierte Liste auf (das Suchfeld befindet sich in der App-Kopfzeile) und lässt dich die Detailansicht einer Sitzung öffnen, die drei Tabs hat — **Zusammenfassung** (die Meeting-Zusammenfassung), **Transkript** (das aufgezeichnete Transkript) und **Nutzung** (die Fragen, die du Elyvo während der Sitzung gestellt hast, und dessen Antworten). Nutze es, um ein Meeting nachzubereiten oder nachzuverfolgen.

### Gedächtnis und Selbstlernen

Elyvo verbessert sich mit der Nutzung. Unter deinem **Profil** kannst du Folgendes einsehen und bearbeiten:

- **Benutzergedächtnis** — dauerhafte Fakten über dich und deine Präferenzen, die der Assistent überall anwendet.
- **Begriffsklärungen** — Klarstellungen, die der Assistent gelernt hat (zum Beispiel, welchen „John" oder welches Projekt du meinst), damit er nicht mehr falsch rät.

### Fensterschutz vor Bildschirmfreigabe

Das Overlay ist bewusst für Aufnahmen unsichtbar, sodass du es während eines geteilten Anrufs nutzen kannst, ohne dass es im Stream erscheint. Der Umfang unterscheidet sich je nach Plattform — die [Haupt-README](../README.md#window-protection-from-screen-sharing) ist die maßgebliche Übersicht. Kurz zusammengefasst:

- **Windows 11** — standardmäßig vor allen Aufnahmearten verborgen.
- **Windows 10** — derselbe Schutz, aber **nicht garantiert**: Eine bekannte Einschränkung des Betriebssystems kann dazu führen, dass das Overlay in der Aufnahme als schwarzes Rechteck erscheint, statt sauber verborgen zu werden.
- **Linux (KDE / KWin)** — standardmäßig vor Bildschirm*aufnahme und -freigabe* verborgen. Auf **KWin 6.7.0+ (Plasma 6.7+)** sind auch statische *Screenshots* standardmäßig verborgen — kein Patch nötig. Auf älterem KWin (≤ 6.6.x) ist, um es vor statischen *Screenshots* (Spectacle/PrintScreen) zu verbergen, einmalig ein KWin-Patch nötig, der nach KWin-Updates erneut angewendet werden muss.
- **macOS** — verwendet denselben nativen Inhaltsschutzmechanismus. Zuverlässig auf **macOS 14 und früher**; auf **macOS 15 und neuer** ist die Unerkennbarkeit **nicht garantiert**, und das Overlay kann in Aufnahmen erscheinen.

---

## Einstellungen

Öffne die Einstellungen über das Benutzermenü. Die Tabs sind:

- **Allgemein** — grundlegende Einstellungen, das erkannte Audioeingabegerät sowie die Test-Anzeigen für Mikrofon / Systemton, die Google-Kalender-Verbindung, Optionen zur Bildschirmaufnahme und **Nach Updates suchen**.
- **Tastenkombinationen** — jede Tastenkombination ansehen und neu belegen.
- **Profil** — deine Onboarding-Antworten, das Benutzergedächtnis und die Begriffsklärungen.
- **Sicherheit** — Sicherheitsoptionen für dein Konto.
- **Sprache** — Oberflächen- / Antwortsprache.
- **Ressourcen** — deine Markdown-Dokumente hochladen und verwalten sowie auswählen, welche für das aktive Projekt aktiviert sind (siehe [Dokumente](#dokumente)).
- **Abrechnung** — dein Abonnement und dein Plan (schaltet kostenpflichtige Funktionen wie den Ambient-KI-Chat frei).

---

## Aktualisieren

Elyvo Assist aktualisiert sich **nicht** selbst, prüft aber trotzdem automatisch auf neue Versionen: Der Server fragt regelmäßig (etwa alle 8 Stunden, plus einmal beim Serverstart) GitHub nach neuen Releases ab und sendet, sobald eine neuere Version gefunden wird, eine schließbare Ankündigung **„New version!"** (Titel bleibt englisch) mit Download-Link an dein Dashboard. Du kannst außerdem jederzeit manuell **Nach Updates suchen** unter **Einstellungen → Allgemein** auslösen, um die [Releases](https://github.com/pdasilem/elyvo-assist/releases)-Seite direkt in deinem Browser zu öffnen.

Lade zum Aktualisieren das neueste Installationsprogramm für deine Plattform von [Releases](https://github.com/pdasilem/elyvo-assist/releases) herunter und führe es über deiner bestehenden Installation aus — Einstellungen und Anmeldung bleiben erhalten.

- **Arch / Manjaro:** Führe das `install.sh` aus dem neuesten Release erneut aus, oder installiere die neue `.pkg.tar.zst`-Datei mit `sudo pacman -U`.
- **Debian / Ubuntu:** `sudo apt install ./elyvo-assist-<neue-version>-linux-x86_64.deb`.
- **Windows / macOS:** Führe das neue Installationsprogramm aus / öffne die neue DMG-Datei.

> Linux-KDE-Nutzer mit KWin älter als 6.7.0: Wende den KWin-Screenshot-Patch nach einem KWin-Systemupdate erneut an, falls du auf den Screenshot-Schutz angewiesen bist. Bringt dich das Update auf KWin 6.7.0 oder neuer, ist der Patch nicht mehr nötig — der Schutz ist eingebaut.

---

## Deinstallieren

- **Windows** — *Einstellungen → Apps → Installierte Apps → Elyvo Assist → Deinstallieren*.
- **macOS** — ziehe **Elyvo Assist** aus dem Ordner *Programme* in den Papierkorb.
- **Debian / Ubuntu** — `sudo apt remove elyvo-assist`.
- **Arch / Manjaro** — `sudo pacman -R elyvo-assist`.

---

## Fehlerbehebung

**Das Overlay erscheint nicht.** Stelle sicher, dass die App läuft (prüfe die Taskleiste/Menüleiste), und drücke die Umschalt-Tastenkombination (`Ctrl+\`). Vergewissere dich unter macOS, dass die Bedienungshilfen-Berechtigung erteilt ist, andernfalls lösen die globalen Tastenkombinationen nicht aus.

**Es wird kein Audio aufgenommen.** Prüfe den Zugriff auf Mikrofon und Bildschirmaufnahme in den Datenschutzeinstellungen deines Betriebssystems, und verwende dann den Mikrofon- / Systemton-Test unter **Einstellungen → Allgemein**, um die Pegel zu bestätigen. Elyvo verwendet das Standard-Eingabegerät deines Systems, stelle also das richtige Standardgerät in den Sound-Einstellungen deines Betriebssystems ein. Vergewissere dich unter Linux, dass PipeWire läuft.

**Das Overlay wird unter Linux weiterhin in Screenshots angezeigt.** Bildschirm*aufnahme/-freigabe* wird standardmäßig verborgen. Auf KWin 6.7.0+ (Plasma 6.7+) sind Screenshots standardmäßig verborgen; auf älterem KWin erfordern statische Screenshots den einmaligen KWin-Patch, der im [README](../README.md#window-protection-from-screen-sharing) beschrieben ist — wende ihn nach KWin-Updates erneut an.

**Anmeldeprobleme.** Versuche die alternative Methode (E-Mail/Passwort statt Google oder umgekehrt) und stelle sicher, dass deine Systemuhr korrekt eingestellt ist — OAuth und die Token-Validierung sind zeitkritisch.

Für alles andere öffne ein Issue im [Releases-Repository](https://github.com/pdasilem/elyvo-assist/issues).
