# Elyvo Assist — Guida utente

> 🌐 Questa guida è disponibile anche in: [English](USER_GUIDE.md) · [Беларуская](USER_GUIDE.be.md) · [Deutsch](USER_GUIDE.de.md) · [Español](USER_GUIDE.es.md) · [Français](USER_GUIDE.fr.md) · **Italiano** · [Português](USER_GUIDE.pt.md) · [Русский](USER_GUIDE.ru.md) · [Українська](USER_GUIDE.uk.md)

Elyvo Assist è un assistente AI desktop per riunioni, ricerca e brainstorming. Si presenta come un overlay traslucido sopra qualsiasi finestra, richiamabile con una scorciatoia da tastiera. Può ascoltare il tuo microfono e l'audio di sistema, trascrivere in tempo reale, osservare il tuo schermo e rispondere alle domande tenendo conto del contesto — restando invisibile alla condivisione e alla registrazione dello schermo.

Questa guida copre l'installazione e una panoramica delle funzionalità principali.

- [Installazione](#installazione)
- [Primo avvio](#primo-avvio)
- [Permessi](#permessi)
- [L'overlay e le scorciatoie da tastiera](#loverlay-e-le-scorciatoie-da-tastiera)
- [Panoramica delle funzionalità](#panoramica-delle-funzionalità)
- [Impostazioni](#impostazioni)
- [Aggiornamento](#aggiornamento)
- [Disinstallazione](#disinstallazione)
- [Risoluzione dei problemi](#risoluzione-dei-problemi)

---

## Installazione

Gli installer e i binari vengono pubblicati tramite [GitHub Releases](https://github.com/pdasilem/elyvo-assist/releases). Scarica il file corrispondente alla tua piattaforma dall'ultima release. Tutte le build sono a 64 bit (`x86_64` / Apple Silicon).

Ogni release contiene, per la versione `X.Y.Z`:

| Piattaforma | File |
|----------|------|
| Windows (consigliato) | `elyvo-assist-X.Y.Z-windows-x64-setup.exe` |
| Windows (MSI) | `elyvo-assist-X.Y.Z-windows-x64.msi` |
| macOS (Intel) | `elyvo-assist-X.Y.Z-macos-x64.dmg` |
| macOS (Apple Silicon) | `elyvo-assist-X.Y.Z-macos-arm64.dmg` |
| Debian / Ubuntu | `elyvo-assist-X.Y.Z-linux-x86_64.deb` |
| Arch / Manjaro | `elyvo-assist-X.Y.Z-1-x86_64.pkg.tar.zst` (+ `install.sh`) |

### Windows

1. Scarica l'installer `...-setup.exe` (NSIS) — oppure il file `.msi` se la tua organizzazione preferisce la distribuzione tramite MSI.
2. Eseguilo e segui le istruzioni a schermo. L'app viene installata in `Program Files\Elyvo Assist`.
3. Avvia **Elyvo Assist** dal menu Start.

### macOS

1. Scarica il `.dmg` corrispondente al tuo chip — `macos-x64` per Intel, `macos-arm64` per Apple Silicon (M1/M2/M3 e successivi).
2. Apri l'immagine disco e trascina **Elyvo Assist** in **Applicazioni**.
3. Al primo avvio, macOS potrebbe avvisare che l'app proviene da uno sviluppatore non identificato. Fai clic destro sull'app → **Apri** → **Apri** per consentirne l'esecuzione.

> **Requisiti Linux.** Elyvo Assist è pensato per il desktop **KDE Plasma** su **Wayland**. La protezione dell'overlay dalla cattura dello schermo è implementata tramite KWin (il compositor di KDE), quindi il comportamento di occultamento dalla condivisione dello schermo funziona solo su KDE/KWin. Altri desktop (GNOME, ecc.) possono eseguire l'app, ma le garanzie di protezione dalla cattura non si applicano. È inoltre necessaria una sessione **PipeWire** attiva per la cattura del microfono e dell'audio di sistema.

### Linux — Debian / Ubuntu

```bash
sudo apt install ./elyvo-assist-X.Y.Z-linux-x86_64.deb
```

`apt` risolve automaticamente le dipendenze runtime (WebKitGTK 4.1, OpenSSL 3, PipeWire). Sulle versioni più datate di `apt`, usa `sudo dpkg -i ...` seguito da `sudo apt -f install` per recuperare le dipendenze mancanti.

### Linux — Arch / Manjaro

Il modo più rapido è utilizzare lo script di installazione pubblicato, che scarica il pacchetto, installa le librerie di sistema necessarie ed esegue `pacman` al posto tuo:

```bash
curl -fsSL https://github.com/pdasilem/elyvo-assist/releases/latest/download/install.sh -o install.sh
bash install.sh
```

Lo script supporta solo i sistemi basati su `pacman` e installerà automaticamente i pacchetti runtime mancanti (GTK3, WebKit2GTK 4.1, PipeWire, libayatana-appindicator e così via).

Preferisci procedere manualmente? Scarica il file `.pkg.tar.zst` e installalo direttamente:

```bash
sudo pacman -U elyvo-assist-X.Y.Z-1-x86_64.pkg.tar.zst
```

---

## Primo avvio

1. **Accedi.** Accedi con **email e password**, un **codice monouso via email**, oppure con **Google**. I nuovi account vengono creati dalla stessa schermata (email → codice di verifica → impostazione della password).
2. **Configurazione guidata.** Una breve procedura guidata ti accompagna attraverso alcuni passaggi — inclusi i **permessi** e la **creazione del tuo primo progetto** — e si conclude con un passaggio **Parlaci di te**, in cui puoi facoltativamente allegare un file (`.pdf`, `.doc`, `.docx`, `.md`, `.txt`) per fornire all'assistente più contesto su di te. Potrai modificare queste informazioni in seguito dal tuo **Profilo**.
3. **Inizia a usarlo.** Al termine della configurazione guidata si apre la **Dashboard**. Richiama l'overlay della chat in qualsiasi momento con la scorciatoia dedicata (predefinita `Ctrl+\`).

---

## Permessi

Per ascoltare e vedere il tuo schermo, Elyvo Assist ha bisogno di due permessi a livello di sistema operativo, richiesti durante la configurazione guidata:

- **Microfono** — per catturare ciò che dici.
- **Cattura schermo** — così che *Chiedi informazioni sul mio schermo* possa vedere la finestra attiva.

Su **Windows** e **macOS**, questi permessi vengono gestiti tramite le normali finestre di dialogo del sistema operativo. Su **Linux**, concedili quando richiesti; se ne neghi uno per errore, concedilo dalle impostazioni sulla privacy del tuo sistema operativo.

Le impostazioni audio e del microfono non sono configurabili dall'app — Elyvo usa sempre il dispositivo **predefinito** del tuo sistema.

> Su Linux, la cattura del microfono e dell'audio di sistema utilizza PipeWire e il portale desktop. Assicurati che PipeWire sia in esecuzione (è l'impostazione predefinita sulle versioni attuali di Manjaro e Ubuntu).

---

## L'overlay e le scorciatoie da tastiera

Elyvo Assist è controllato quasi interamente da tastiera, così puoi usarlo senza dover uscire dalla tua riunione. L'overlay della chat fluttua sopra le altre finestre, è trascinabile ed è **nascosto dalla condivisione e dalla registrazione dello schermo** (vedi [protezione della finestra](../README.md#window-protection-from-screen-sharing)).

Scorciatoie predefinite (tutte riassegnabili in **Impostazioni → Scorciatoie**):

| Azione | Predefinita | Cosa fa |
|--------|---------|--------------|
| Attiva/disattiva visibilità | `Ctrl+\` | Mostra / nasconde l'overlay Elyvo |
| Chiedi a Elyvo | `Ctrl+Enter` | Chiede informazioni sul tuo schermo o sull'audio attuale |
| Cancella chat | `Ctrl+R` | Cancella la conversazione corrente |
| Avvia / termina sessione | `Ctrl+Shift+\` | Avvia o termina una sessione di ascolto |
| Sposta overlay | `Ctrl+↑ / ↓ / ← / →` | Riposiziona la finestra sullo schermo |
| Scorri risposta | `Ctrl+Shift+↑ / ↓` | Scorre la risposta verso l'alto / il basso |

Per riassegnare una scorciatoia, apri **Impostazioni → Scorciatoie**, fai clic su una combinazione e premi la nuova combinazione desiderata.

---

## Panoramica delle funzionalità

### Sessioni

Una **sessione** è il periodo in cui Elyvo ascolta attivamente e mantiene il contesto. Avvia o termina una sessione con `Ctrl+Shift+\`. Durante una sessione, Elyvo cattura il tuo microfono e l'audio di sistema, li trascrive in tempo reale e mantiene la trascrizione corrente come contesto per le tue domande. Elyvo utilizza il dispositivo di input **predefinito** del tuo sistema (non è possibile modificarlo dall'app); nelle Impostazioni puoi vedere il dispositivo rilevato e testare i livelli del microfono e dell'audio di sistema con indicatori in tempo reale.

### Chiedi informazioni sul tuo schermo o sull'audio

Premi **Chiedi a Elyvo** (`Ctrl+Enter`) e Elyvo risponderà utilizzando come contesto ciò che è attualmente sul tuo schermo e l'audio/trascrizione recenti — utile per "riassumi quello che è appena stato detto", "cos'è questo errore" oppure "scrivi una bozza di risposta a questo". Puoi anche digitare un messaggio normale nella casella della chat in qualsiasi momento.

### Azioni rapide

Durante una sessione la chat offre cinque azioni a un clic. Sono **consapevoli del ruolo**: ognuna prende significato dalla situazione e dall'obiettivo della modalità attiva, quindi lo stesso pulsante aiuta in modo diverso a seconda che tu stia rispondendo, valutando, negoziando o imparando.

- **Assist** — la sostanza che il momento richiede: la risposta a ciò che ti è appena stato chiesto; una risposta di riferimento o una valutazione rapida quando a valutare sei *tu*; la soluzione completa quando lo screenshot contiene un esercizio. È materiale su cui ragionare, non parole da dire ad alta voce.
- **What should I say?** — la prossima frase da dire ad alta voce, con la tua voce, pronta così com'è.
- **Follow-up questions** — un insieme di 3–4 domande da porre subito dopo per far avanzare il tuo obiettivo: un menu tra cui scegliere, non una singola battuta.
- **What did they mean?** — decodifica l'ultimo intervento dell'altra parte: il punto, l'intenzione e ogni preoccupazione implicita non detta.
- **Recap** — fino a tre punti su cosa è cambiato, è stato deciso o chiesto dall'ultima volta che hai fatto il punto.

Come funziona la rotazione: in una modalità da candidato, Assist risponde alla domanda rivolta a te; in una modalità da valutatore ti dà la risposta di riferimento con cui giudicare ciò che senti; in una modalità di negoziazione le Follow-up questions diventano domande esplorative. In una modalità lezione o webinar, dove per lo più ascolti, Assist spiega in termini più semplici il punto appena esposto, le Follow-up questions diventano domande per il relatore o verifiche della tua comprensione, e Recap ti rimette in pari dopo una distrazione. A guidare tutto è il prompt di sistema della modalità attiva — i pulsanti restano gli stessi (vedi **Modalità AI** più sotto).

### Modalità AI

Le **Modalità** ti permettono di personalizzare il comportamento dell'assistente in base alla situazione. Ogni modalità ha un proprio prompt di sistema e un modello di note opzionale. Gestiscile in **Modalità**:

- Parti dalla **Galleria dei modelli** — i suoi modelli sono forniti dal server e cambiano nel tempo — oppure crea una modalità da zero.
- Modifica il prompt di sistema per definire tono, ruolo e regole adatti a quella situazione.
- Allega **file della modalità** — materiale di riferimento che l'assistente deve tenere presente per quella modalità.
- Contrassegna una modalità come attiva; è sempre disponibile una modalità generale/predefinita.

### Chat AI ambientale

La chat ambientale è una chat leggera, sempre disponibile, che ti segue in tutta l'app e può essere associata a un progetto specifico. Fa parte del piano a pagamento (vedi **Impostazioni → Fatturazione**).

### Progetti

I **Progetti** raggruppano sessioni correlate e offrono all'assistente un contesto condiviso e persistente. All'interno di un progetto puoi gestire:

- **Membri** — vedi chi fa parte del progetto e invita altre persone via email (ogni invitato risulta *in sospeso* finché non accetta).
- **Memoria** — fatti e contesto che l'assistente deve ricordare tra le sessioni di quel progetto.
- **Regole** — indicazioni che l'assistente segue per quel progetto.
- **Impostazioni** — una **modalità** per progetto, **lingua di output** e **lingua della trascrizione**, oltre ad **Arricchisci contesto** — un'opzione (disattivata per impostazione predefinita) che consente all'assistente di attingere contesto rilevante dalle tue *altre* sessioni nello stesso progetto (richiamo tra sessioni).

Quando qualcuno ti invita al proprio progetto, l'invito appare in cima alla sezione **Progetti** con i pulsanti **Accetta** / **Rifiuta**. La chat ambientale può essere associata a un progetto, così le risposte attingono alla memoria e alle regole di quel progetto.

### Documenti

Elyvo può conservare una libreria personale di documenti di riferimento che puoi richiamare come overlay a sé stante mentre lavori — utile per tenere a portata di mano appunti, un brief o una checklist durante una chiamata.

- **Gestisci i tuoi documenti.** In **Impostazioni → Risorse**, aggiungi file Markdown (`.md`) — fino a **1 MB** ciascuno — nella sezione *I tuoi documenti*, oppure elimina quelli che non ti servono più. I documenti sono privati e associati al tuo account.
- **Attiva per progetto.** Per il progetto attivo, seleziona i documenti che vuoi avere a portata di mano. I documenti attivati si **aprono automaticamente come schede** nel visualizzatore Documenti ogni volta che lo apri per quel progetto. Attivare un documento controlla cosa mostra il visualizzatore per quel progetto; non inserisce il contenuto del file nelle risposte dell'assistente.
- **Apri il visualizzatore.** Dal menu della sessione dell'overlay della chat (il pulsante `···`), scegli **Documenti**. Si apre come finestra trascinabile a sé stante che, come l'overlay principale, è **nascosta dalla condivisione e dalla registrazione dello schermo**. Lo stesso elemento del menu la chiude.
- **Leggi e cambia scheda.** Ogni documento si apre nella propria scheda. Usa la scheda **+** per aprire uno qualsiasi dei tuoi documenti, fai clic su una scheda per passare da un documento all'altro e su **×** per chiuderla. Il contenuto viene visualizzato come Markdown formattato e segue il tema e la dimensione del carattere della tua chat.

### Calendario e riunioni

Collega **Google Calendar** (da **Impostazioni → Generale**) per vedere le tue prossime riunioni direttamente in Elyvo. Sulla scheda di una riunione, **"Partecipa alla riunione →"** si limita ad aprire il link della chiamata (Zoom/Meet/Teams) nel browser, mentre **"Prendi appunti"** avvia una sessione di ascolto. Poco prima di una riunione, Elyvo mostra anche un promemoria in-app con un proprio pulsante **"Prendi appunti"**, che fa entrambe le cose insieme — avvia la sessione e apre il link della chiamata — così l'assistente ascolta fin dal momento in cui ti unisci.

### Dashboard e cronologia

La **Dashboard** è la tua base operativa: elenca le sessioni passate in un elenco ricercabile e raggruppato per data (il campo di ricerca si trova nell'intestazione dell'app) e ti permette di aprire il dettaglio di una sessione, che ha tre schede — **Riepilogo** (il riepilogo della riunione), **Trascrizione** (la trascrizione catturata) e **Utilizzo** (le domande che hai posto a Elyvo durante la sessione e le sue risposte). Usala per rivedere o dare seguito dopo una riunione.

### Memoria e apprendimento autonomo

Elyvo migliora con l'uso. Nel tuo **Profilo** puoi rivedere e modificare:

- **Memoria utente** — fatti duraturi su di te e sulle tue preferenze che l'assistente applica ovunque.
- **Disambiguazioni** — chiarimenti che l'assistente ha appreso (ad esempio, quale "Mario" o quale progetto intendi) in modo da non indovinare più in modo errato.

### Protezione della finestra dalla condivisione dello schermo

L'overlay è deliberatamente invisibile alla cattura, così puoi usarlo durante una chiamata condivisa senza che compaia nello streaming. La copertura varia in base alla piattaforma — il [README principale](../README.md#window-protection-from-screen-sharing) è la matrice autorevole. In breve:

- **Windows 11** — nascosto da tutti i tipi di cattura fin da subito.
- **Windows 10** — stessa protezione, ma **non garantita**: una limitazione nota del sistema operativo può mostrare l'overlay come un rettangolo nero nella cattura invece di nasconderlo correttamente.
- **Linux (KDE / KWin)** — nascosto dalla *registrazione e condivisione* dello schermo fin da subito. Su **KWin 6.7.0+ (Plasma 6.7+)** anche gli *screenshot* statici sono nascosti fin da subito — nessuna patch necessaria. Su KWin più vecchi (≤ 6.6.x), nasconderlo dagli *screenshot* statici (Spectacle/PrintScreen) richiede una patch KWin una tantum, da riapplicare dopo gli aggiornamenti di KWin.
- **macOS** — utilizza lo stesso meccanismo nativo di protezione dei contenuti. Affidabile su **macOS 14 e versioni precedenti**; su **macOS 15 e versioni successive** l'invisibilità **non è garantita** e l'overlay potrebbe comparire nelle catture.

---

## Impostazioni

Apri le Impostazioni dal menu utente. Le schede sono:

- **Generale** — preferenze principali, il dispositivo di input audio rilevato e gli indicatori di test per microfono / audio di sistema, connessione a Google Calendar, opzioni di cattura schermo e **Verifica aggiornamenti**.
- **Scorciatoie** — visualizza e riassegna ogni scorciatoia da tastiera.
- **Profilo** — le tue risposte alla configurazione guidata, la memoria utente e le disambiguazioni.
- **Sicurezza** — opzioni di sicurezza dell'account.
- **Lingua** — lingua dell'interfaccia / delle risposte.
- **Risorse** — carica e gestisci i tuoi documenti Markdown, e scegli quali sono attivi per il progetto corrente (vedi [Documenti](#documenti)).
- **Fatturazione** — il tuo abbonamento e piano (sblocca funzionalità a pagamento come la chat AI ambientale).

---

## Aggiornamento

Elyvo Assist **non** si aggiorna da solo, ma il controllo della versione è comunque automatico: il server interroga periodicamente GitHub (circa ogni 8 ore, più una volta all'avvio del server) alla ricerca di nuove release e, se ne trova una più recente, invia alla tua Dashboard un annuncio richiudibile **"New version!"** (il titolo resta in inglese) con un link per il download. Puoi anche avviare manualmente **Verifica aggiornamenti** in **Impostazioni → Generale** in qualsiasi momento per aprire direttamente la pagina [Releases](https://github.com/pdasilem/elyvo-assist/releases) nel tuo browser.

Per aggiornare, scarica il nuovo installer per la tua piattaforma da [Releases](https://github.com/pdasilem/elyvo-assist/releases) ed eseguilo sopra la tua installazione esistente — le impostazioni e l'accesso vengono conservati.

- **Arch / Manjaro:** riesegui lo script `install.sh` dell'ultima release, oppure esegui `sudo pacman -U` sul nuovo `.pkg.tar.zst`.
- **Debian / Ubuntu:** `sudo apt install ./elyvo-assist-<nuova-versione>-linux-x86_64.deb`.
- **Windows / macOS:** esegui il nuovo installer / apri il nuovo DMG.

> Utenti Linux KDE con KWin precedente alla 6.7.0: riapplica la patch KWin per gli screenshot dopo un aggiornamento di sistema di KWin, se fai affidamento sulla protezione degli screenshot. Se l'aggiornamento ti porta a KWin 6.7.0 o successivo, la patch non serve più — la protezione è integrata.

---

## Disinstallazione

- **Windows** — *Impostazioni → App → App installate → Elyvo Assist → Disinstalla*.
- **macOS** — trascina **Elyvo Assist** da *Applicazioni* nel Cestino.
- **Debian / Ubuntu** — `sudo apt remove elyvo-assist`.
- **Arch / Manjaro** — `sudo pacman -R elyvo-assist`.

---

## Risoluzione dei problemi

**L'overlay non appare.** Assicurati che l'app sia in esecuzione (controlla la barra delle applicazioni/menu bar) e premi la scorciatoia di attivazione (`Ctrl+\`). Su macOS, verifica che il permesso di Accessibilità sia stato concesso, altrimenti le scorciatoie globali non funzioneranno.

**Nessun audio viene catturato.** Controlla l'accesso al microfono e alla cattura schermo nelle impostazioni sulla privacy del tuo sistema operativo, quindi usa il test del microfono / audio di sistema in **Impostazioni → Generale** per verificare i livelli. Elyvo utilizza il dispositivo di input predefinito del tuo sistema, quindi imposta il dispositivo corretto come predefinito nelle impostazioni audio del sistema operativo. Su Linux, verifica che PipeWire sia in esecuzione.

**L'overlay continua a comparire negli screenshot su Linux.** La *registrazione/condivisione* dello schermo è nascosta per impostazione predefinita. Su KWin 6.7.0+ (Plasma 6.7+) gli screenshot sono nascosti fin da subito; su KWin più vecchi gli screenshot statici richiedono la patch KWin una tantum descritta nel [README](../README.md#window-protection-from-screen-sharing) — riapplicala dopo gli aggiornamenti di KWin.

**Problemi di accesso.** Prova il metodo alternativo (email/password rispetto a Google) e assicurati che l'orologio di sistema sia impostato correttamente — OAuth e la validazione dei token sono sensibili al fattore tempo.

Per qualsiasi altro problema, apri una issue nel [repository delle release](https://github.com/pdasilem/elyvo-assist/issues).
