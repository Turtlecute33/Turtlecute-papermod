---
title: "Guida Completa alla Sicurezza e Privacy su macOS"
description: "Guida pratica per blindare il vostro Mac dalle impostazioni di sistema: account, FileVault, permessi privacy (TCC), firewall, DNS crittografato, anti-malware e monitoraggio."
summary: "Guida pratica per blindare il vostro Mac dalle impostazioni di sistema: account, FileVault, permessi privacy (TCC), firewall, DNS crittografato, anti-malware e monitoraggio."
keywords: ["macos sicurezza", "macos privacy", "sicurezza mac", "privacy mac", "macos security", "macos privacy guide", "sicurezza apple", "hardening macos", "firewall mac", "filevault", "impostazioni privacy mac", "macos sicurezza ita", "privacy mac italiano"]
author: "Turtlecute"
date: 2026-03-08
lastmod: 2026-06-19
url: /macos-security
images: ["/posts/macos-security/cover.webp"]
series: ["Privacy Digitale", "Sicurezza"]
topics: ["privacy-security"]
cover:
  image: "cover.webp"
  relative: true
faq:
  - question: "Come proteggere la privacy su Mac?"
    answer: "Partite dalle impostazioni di sistema: attivate FileVault per la crittografia del disco, abilitate il firewall integrato e la modalità stealth, riducete i permessi delle app in Privacy e Sicurezza, disattivate analytics e pubblicità Apple, usate DNS crittografato (DoH/DoT) e tenete il sistema sempre aggiornato."
  - question: "FileVault è necessario su Mac con Apple Silicon?"
    answer: "I Mac Apple Silicon sono crittografati di default, ma FileVault aggiunge un livello ulteriore richiedendo la password all'avvio. Funge anche da password del firmware, impedendo l'avvio da dischi esterni e l'accesso alla Recovery."
  - question: "Come attivare il firewall su macOS?"
    answer: "Andate in Impostazioni di Sistema oppure usate il comando sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setglobalstate on da Terminale. Attivate anche la modalità stealth per ignorare ping e probe sulle porte chiuse."
  - question: "Cos'è la Modalità Lockdown di macOS e a chi serve?"
    answer: "La Modalità Lockdown disabilita numerose funzionalità per ridurre la superficie di attacco. È pensata per chi rischia attacchi sofisticati, ma vale la pena provarla per chiunque: si disattiva per singoli siti fidati e il costo in usabilità è minore di quanto si pensi. Si attiva da Impostazioni di Sistema > Privacy e Sicurezza."
  - question: "I Mac possono prendere virus e malware?"
    answer: "Sì, i Mac non sono immuni al malware. macOS include protezioni come XProtect, Gatekeeper e il sandboxing delle app, ma è consigliato scaricare software solo da fonti ufficiali, preferire app open source e verificare i file sospetti con VirusTotal."
  - question: "Qual è il browser più sicuro per macOS?"
    answer: "Su Apple Silicon, Safari è spesso la scelta migliore per la maggior parte degli utenti: è profondamente integrato nel sistema, ha una sandbox solida, l'Intelligent Tracking Prevention e il supporto alla Modalità Lockdown. Firefox resta ottimo per chi ha bisogno di estensioni, container multi-account o hardening avanzato con arkenfox/user.js."
  - question: "Come eliminare i metadati e le tracce digitali su macOS?"
    answer: "Usate xattr -d per rimuovere i metadati dai file scaricati, qlmanage -r cache per pulire la cache di QuickLook, e cancellate le directory di LanguageModeling, Spelling e Suggestions in ~/Library per eliminare i dati di digitazione."
howto:
  name: "Come proteggere privacy e sicurezza su macOS"
  description: "Procedura per configurare account, FileVault, permessi privacy, firewall, DNS, anti-malware, backup e monitoraggio direttamente dalle impostazioni di macOS."
  totalTime: "PT2H"
  supply:
    - "Mac aggiornato"
    - "Account utente con privilegi di amministratore"
    - "Disco o destinazione per backup"
  tool:
    - "Impostazioni di Sistema"
    - "Terminale"
    - "FileVault"
    - "LuLu"
  steps:
    - name: "Partire bene: account e FileVault"
      text: "Usa una password forte, abilita FileVault e lascia la sicurezza del firmware su Full Security."
      url: "/macos-security#fondamenta"
    - name: "Regolare la privacy del sistema"
      text: "Rivedi i permessi delle app (TCC), disattiva analytics, pubblicità Apple e Siri, ripulisci i metadati."
      url: "/macos-security#privacy-sistema"
    - name: "Ridurre la superficie di rete"
      text: "Attiva firewall, modalità stealth, DNS crittografato, indirizzo Wi-Fi privato e un firewall per le connessioni in uscita."
      url: "/macos-security#rete"
    - name: "Difendersi da malware"
      text: "Mantieni Gatekeeper e SIP attivi, scarica software solo da fonti ufficiali, verifica sandbox e Hardened Runtime."
      url: "/macos-security#app-malware"
    - name: "Backup, password e sicurezza fisica"
      text: "Configura backup cifrati con la regola 3-2-1, password uniche, MFA hardware e difese fisiche."
      url: "/macos-security#dati-backup"
    - name: "Monitorare il sistema"
      text: "Controlla processi, connessioni di rete, log e strumenti di auditing per rilevare comportamenti anomali."
      url: "/macos-security#monitoraggio"
---

> **TL;DR** - In questa guida imparerete:
> - Come configurare un Mac Apple Silicon per massimizzare sicurezza e privacy fin dal primo avvio
> - Come dominare le impostazioni di Privacy e Sicurezza: permessi app (TCC), telemetria, tracce digitali
> - Come ridurre la superficie di rete con firewall, DNS crittografato e Wi-Fi più sicuro
> - Come difendervi da malware, crittografare i dati e monitorare il sistema

## Sintesi

Per blindare un Mac non servono decine di app: serve mettere mano alle **impostazioni giuste del sistema operativo**. Si parte da account e FileVault, poi si passa ai permessi di privacy (TCC), telemetria, firewall, DNS crittografato, regole anti-malware, backup cifrati e monitoraggio. Le misure più estreme, come la Modalità Lockdown, valgono comunque la prova anche per l'utente comune.

Il vostro Mac non è una fortezza impenetrabile appena uscito dalla scatola. macOS è un sistema operativo robusto, certo, ma senza le giuste configurazioni lascia aperte più porte di quante pensiate, e ogni porta aperta è un invito per chi vuole ficcare il naso nei vostri affari.

Questa guida è pensata per voi tartarughe che volete prendere sul serio la privacy e la sicurezza del vostro Mac. Non è un elenco di tool da installare: l'obiettivo è farvi capire e regolare le impostazioni che contano, per ottenere un sistema operativo più sicuro senza dipendere da software di terze parti. Non serve essere ingegneri: basta la voglia di imparare e un po' di pazienza.

Prima di toccare qualsiasi impostazione, vale la pena chiedersi **da chi vi state difendendo**. Le esigenze di chi teme un coinquilino curioso sono diverse da quelle di chi affronta un avversario statale. Se volete approfondire, leggete la **[Guida al Threat Model](/threat-model)**: vi aiuterà a capire quali delle misure qui sotto hanno davvero senso per voi e quali sono solo complicazioni inutili.

**ATTENZIONE!!** Questa guida è fornita così com'è, senza garanzie di alcun tipo. Siete voi gli unici responsabili delle modifiche che apportate al vostro sistema. Procedete con cautela e, nel dubbio, fate sempre un backup prima.

![I livelli di sicurezza di macOS: dall'hardware Apple Silicon fino al sandboxing delle applicazioni](macos-security-layers.svg)

## Fondamenta: hardware, installazione e account {#fondamenta style="color: white;"}

Le basi vengono prima di tutto. Un hardware giusto, un'installazione pulita e un account configurato con criterio sono il terreno su cui poggia tutto il resto.

### Scegliere il Mac giusto

macOS è più sicuro quando gira su **hardware Apple con Apple Silicon** (M1, M2, M3, M4 e successivi). I Mac con processori Intel hanno [vulnerabilità hardware](https://checkm8.info/blog/apple-t2-chip-vulnerability) che Apple non può correggere via software. Più recente è il chip, meglio è.

Evitate gli hackintosh e i Mac che non supportano l'ultima versione di macOS: Apple non corregge tutte le vulnerabilità nelle versioni più vecchie.

A seconda del vostro threat model, potreste voler acquistare il Mac **in contanti e di persona**, evitando ordini online o pagamenti con carta, così nessuna informazione identificativa sarà collegata all'acquisto.

Per gli accessori wireless (tastiera, mouse, cuffie), a mio parere i migliori restano quelli Apple: vengono aggiornati dal sistema e supportano le ultime funzionalità Bluetooth come **BLE Privacy**, che randomizza l'indirizzo hardware Bluetooth per prevenire il tracciamento.

### Installazione e Apple Account

Installate **sempre** l'ultima versione di macOS compatibile con il vostro Mac: le versioni recenti hanno patch di sicurezza che le precedenti non hanno. Come parte del sistema antifurto di Apple, i Mac Apple Silicon devono attivarsi con i server Apple a ogni reinstallazione, per verificare che il dispositivo non sia rubato o bloccato.

Creare un **Apple Account non è obbligatorio** per usare macOS. Serve solo per App Store e servizi come iCloud, Apple Music e simili. Sappiate però che un Apple Account sincronizza di default molti dati su iCloud. Potete disattivare la sincronizzazione dei singoli servizi oppure, meglio ancora, abilitare la **crittografia end-to-end** tramite [Advanced Data Protection](https://support.apple.com/guide/security/advanced-data-protection-for-icloud-sec973254c5f): è una delle prime cose da fare se usate iCloud.

> **Per smanettoni (opzionale):** se volete provare le configurazioni di questa guida senza rischiare il sistema reale, su Apple Silicon potete virtualizzare macOS con strumenti gratuiti come [UTM](https://mac.getutm.app), [VirtualBuddy](https://github.com/insidegui/VirtualBuddy) o `tart`. Sperimentate lì prima di applicare le modifiche sul Mac di tutti i giorni.

### Primo avvio: nome e hostname

Al primo avvio, l'Assistente di Configurazione vi chiederà di creare un account. Usate una **password forte** e non impostate un suggerimento per la password: chiunque abbia accesso al Mac potrebbe vederlo.

Attenzione: il nome reale che inserite finisce nel nome del computer e nell'hostname visibile sulla rete locale. Per cambiarlo con qualcosa di generico:

```zsh
sudo scutil --set ComputerName il_vostro_nome
sudo scutil --set LocalHostName il_vostro_nome
```

### Account e privilegi di amministratore

Il primo account creato è sempre un **amministratore**: ha accesso a `sudo`, quindi può modificare qualsiasi cosa nel sistema. È un potere enorme, ed è bene esserne consapevoli.

Esiste la pratica di creare un secondo account standard per l'uso quotidiano e tenere quello admin solo per le operazioni che lo richiedono. In ambienti aziendali o per profili ad alto rischio ha senso, ma siamo onesti: su un Mac personale monoutente è scomodo e il guadagno reale è marginale. Per la maggior parte di voi, le cose che contano davvero sono altre:

- una **password forte** e unica per il vostro account
- **non eseguire mai comandi da `sudo`** copiati a caso da internet senza capirli
- fare attenzione a **cosa autorizzate** quando un'app chiede privilegi o accesso a dati sensibili (ne parliamo tra poco con TCC)
- tenere il sistema **sempre aggiornato**, attivando gli aggiornamenti automatici in Impostazioni di Sistema

In altre parole: il rischio non è "avere un account admin", è usarlo con leggerezza.

## Crittografia e avvio sicuro: FileVault, firmware e Lockdown {#filevault style="color: white;"}

Qui mettiamo al sicuro i dati a riposo e l'integrità dell'avvio. Sono le difese che proteggono il Mac quando ve lo rubano o quando qualcuno ci mette le mani fisicamente.

### Firmware

Assicuratevi che la sicurezza del firmware sia su **"Sicurezza Completa"** (Full Security), il valore predefinito. Questo impedisce la manomissione del sistema operativo all'avvio.

### FileVault

I Mac Apple Silicon sono crittografati di default, ma **FileVault** aggiunge un livello fondamentale: richiede la password per accedere ai dati all'avvio. La password di FileVault funge anche da password del firmware, impedendo l'avvio da altri dischi e l'accesso alla modalità Recovery.

Per attivarlo: **Impostazioni di Sistema > Privacy e Sicurezza > FileVault > Attiva**

**!ATTENZIONE!** Conservate la chiave di recupero in un luogo sicuro e offline. L'opzione di sblocco tramite iCloud esiste, ma crea un rischio se il vostro Apple Account viene compromesso.

### Modalità Lockdown

La **Modalità Lockdown** disabilita molte funzionalità per ridurre drasticamente la superficie di attacco. Nasce per chi può essere bersaglio di attacchi sofisticati (giornalisti, attivisti, dissidenti), ma il mio consiglio è di **provarla comunque**: si può disattivare per singoli siti fidati in Safari e, nell'uso quotidiano, il costo in usabilità è minore di quanto si creda. Provatela una settimana, poi decidete.

Per attivarla: **Impostazioni di Sistema > Privacy e Sicurezza > Modalità Lockdown**

## Privacy del sistema: permessi, telemetria e tracce {#privacy-sistema style="color: white;"}

Questo è il cuore della guida. La maggior parte della privacy su un Mac non si compra con un'app: si conquista regolando le impostazioni giuste. Qui decidete cosa le app possono toccare, cosa il sistema racconta ad Apple e quante tracce lasciate dietro di voi.

### Permessi delle app (TCC)

macOS protegge le risorse sensibili con un sistema chiamato **TCC** (Transparency, Consent and Control): è lui che fa comparire i pop-up "L'app X vuole accedere a...". Ogni "Consenti" dato con leggerezza è un permesso che resta.

Andate in **Impostazioni di Sistema > Privacy e Sicurezza** e fate pulizia, voce per voce:

- **Accessibilità**, **Monitoraggio inserimento** e **Registrazione schermo**: sono i permessi più pericolosi, perché permettono a un'app di leggere tutto ciò che digitate o vedete. Concedeteli col contagocce e revocate tutto ciò che non serve.
- **Accesso completo al disco** (Full Disk Access): da dare solo a strumenti di cui vi fidate ciecamente.
- **Localizzazione**, **Fotocamera**, **Microfono**, **Contatti**, **Calendari**: tenete attivo solo lo stretto necessario e solo per le app che lo usano davvero.

Rivedere questi permessi ogni tanto è una delle abitudini di sicurezza con il miglior rapporto sforzo/beneficio che esista.

### Telemetria e pubblicità Apple

Apple è più rispettosa della media sulla privacy, ma resta un'azienda che raccoglie dati per default. Conviene chiudere i rubinetti che non vi servono, sempre da **Impostazioni di Sistema > Privacy e Sicurezza**:

- **Analisi e miglioramenti**: disattivate "Condividi analisi Mac" e l'invio di dati a sviluppatori di terze parti.
- **Pubblicità Apple**: disattivate "Annunci personalizzati".
- **Siri e Dettatura**: se non usate Siri, disabilitatela; cancella anche la cronologia di Siri e Dettatura.
- **Spotlight**: in **Spotlight > Risultati di ricerca**, disattivate i "Suggerimenti di Siri" per evitare che le query escano verso Apple.

Da Terminale potete anche disabilitare i report diagnostici automatici:

```zsh
# Non inviare automaticamente i crash report ad Apple
sudo defaults write /Library/Application\ Support/CrashReporter/DiagnosticMessagesHistory.plist AutoSubmit -bool false
defaults write com.apple.CrashReporter DialogType -string "none"
```

### Login e blocco dello schermo

Un Mac ben cifrato non serve a niente se resta sbloccato sulla scrivania. Bloccate bene gli accessi:

```zsh
# Richiedere subito la password dopo lo screensaver o la sospensione
defaults write com.apple.screensaver askForPassword -int 1
defaults write com.apple.screensaver askForPasswordDelay -int 0
```

Inoltre, da Impostazioni di Sistema:

- **disabilitate il login automatico** (Utenti e Gruppi > Opzioni di login)
- configurate gli **Angoli attivi** per avviare lo screensaver al volo e bloccare lo schermo quando vi alzate
- valutate Touch ID per l'uso comodo, ma ricordate che la password resta la difesa principale dopo un riavvio

### Metadati e tracce digitali

macOS conserva una quantità sorprendente di metadati. Ecco i principali e come eliminarli.

**Metadati dei download.** APFS salva attributi estesi che rivelano da dove avete scaricato un file:

```zsh
# Vedere i metadati di un file scaricato
xattr -l ~/Downloads/file_scaricato

# Rimuovere provenienza e quarantena
xattr -d com.apple.metadata:kMDItemWhereFroms ~/Downloads/file_scaricato
xattr -d com.apple.quarantine ~/Downloads/file_scaricato
```

**Cache QuickLook.** QuickLook genera anteprime che restano in cache. Per pulirla: `qlmanage -r cache`

**Credenziali Wi-Fi nella NVRAM.** Possono essere salvate nella NVRAM e si cancellano così:

```zsh
sudo nvram -d 36C28AB5-6566-4C50-9EBD-CBB920F83843:current-network
```

**Dati di digitazione.** macOS conserva quel che scrivete in alcune directory; potete cancellarle e bloccarle:

```zsh
rm -rf ~/Library/LanguageModeling ~/Library/Spelling ~/Library/Suggestions
mkdir ~/Library/LanguageModeling ~/Library/Spelling ~/Library/Suggestions
chmod -R 000 ~/Library/LanguageModeling ~/Library/Spelling ~/Library/Suggestions
```

**Stato delle applicazioni salvato.** macOS salva lo stato delle app per ripristinarle al riavvio:

```zsh
rm -rf ~/Library/Saved\ Application\ State/*
chmod -R 000 ~/Library/Saved\ Application\ State
```

Altre tracce minori: `SiriAnalytics.db` viene creato anche con Siri disattivata (cancellabile ma si ricrea), e la cronologia dei dispositivi Bluetooth collegati vive in `com.apple.Bluetooth.plist`.

### Altri defaults utili

Una raccolta di impostazioni che rendono il sistema più trasparente e prudente:

```zsh
# Mostrare i file nascosti e tutte le estensioni
defaults write com.apple.finder AppleShowAllFiles -bool true
defaults write NSGlobalDomain AppleShowAllExtensions -bool true

# Non salvare di default i nuovi documenti su iCloud
defaults write NSGlobalDomain NSDocumentSaveNewDocumentsToCloud -bool false

# Input sicuro della tastiera nel Terminale (impedisce ad altre app di intercettare i tasti)
defaults write com.apple.terminal SecureKeyboardEntry -bool true

# Disabilitare gli annunci multicast Bonjour
sudo defaults write /Library/Preferences/com.apple.mDNSResponder.plist NoMulticastAdvertisements -bool true

# umask 077: i file nuovi sono leggibili solo dal proprietario
sudo launchctl config user umask 077
```

Infine, disabilitate **Handoff** e **Bluetooth** quando non li usate, e usate **QuickTime Player** per i media (è sandboxato e usa l'Hardened Runtime).

## Ridurre la superficie di rete: firewall, DNS e Wi-Fi {#rete style="color: white;"}

Ogni connessione è una potenziale via d'ingresso o di fuga di dati. Qui chiudiamo ciò che entra, controlliamo ciò che esce e proteggiamo quello che resta.

![Stack di privacy della rete: firewall, DNS crittografato e connessioni controllate](network-privacy-stack.svg)

### Firewall in entrata

macOS include un firewall integrato che blocca le **connessioni in entrata**. Attivatelo e abilitate la modalità stealth:

```zsh
# Attivare il firewall
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setglobalstate on

# Modalità stealth (ignora ping e probe su porte chiuse)
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setstealthmode on

# Non autorizzare automaticamente le app firmate
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setallowsigned off
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setallowsignedapp off
```

### Firewall in uscita

Il firewall integrato blocca solo ciò che entra. Per vedere e controllare il **traffico in uscita**, cioè quali app "telefonano a casa", serve un firewall applicativo. La mia raccomandazione netta:

- **[LuLu](https://objective-see.org/products/lulu.html)** come scelta predefinita per tutti: open source, gratuito, di Objective-See.
- **[Little Snitch](https://www.obdev.at/products/littlesnitch/)** se volete il massimo controllo e siete disposti a pagare.

Questi firewall possono essere aggirati da processi con privilegi root, ma restano preziosissimi: alcuni malware si autodistruggono quando li rilevano.

### Packet filter (pf)

> **Per smanettoni (opzionale, solo se sapete cosa fate):** macOS include **pf**, un firewall a livello kernel molto più granulare. Un esempio base in `/etc/pf.rules`:
>
> ```
> wifi = "en0"
> block in all
> pass out quick on $wifi proto { tcp, udp } from any to any
> pass quick on lo0
> block in quick on $wifi
> ```
>
> Si attiva con `sudo pfctl -e -f /etc/pf.rules` e si verifica con `sudo pfctl -s info`.

### DNS crittografato

Le query DNS sono come cartoline postali: chiunque sulla rete può leggerle. Cifrarle è uno dei guadagni di privacy più grossi a fronte di pochissimo sforzo.

![DNS: confronto tra query in chiaro e query crittografate con DoH/DoT](dns-encryption-flow.svg)

Da macOS 11 in poi potete installare un **profilo di configurazione** per il DNS crittografato (DoH/DoT). Provider validi:

- **[Quad9](https://www.quad9.net/)**: blocca domini malevoli, no-profit, ottimo set-and-forget.
- **[NextDNS](https://nextdns.io/)**: altamente personalizzabile, con blocklist e log opzionali.
- **[AdGuard DNS](https://adguard-dns.io/)**: blocca pubblicità e tracker.

Potete anche bloccare domini direttamente nel file `/etc/hosts`:

```zsh
echo "0.0.0.0 dominio-da-bloccare.com" | sudo tee -a /etc/hosts
sudo dscacheutil -flushcache
```

Esistono blocklist mantenute dalla community, come quella di [StevenBlack](https://github.com/StevenBlack/hosts), che bloccano pubblicità, malware e tracker.

> **Per smanettoni (opzionale):** per una soluzione locale completa potete combinare **dnscrypt-proxy** (cifra il DNS) con **dnsmasq** (cache locale con DNSSEC), entrambi installabili via Homebrew. Configurate dnsmasq su `127.0.0.1` e, se volete, usate regole pf per bloccare tutto il traffico DNS non cifrato.

### Wi-Fi

- **Evitate le reti nascoste**: per connettersi, il dispositivo deve trasmettere il nome della rete, rivelando potenzialmente la cronologia delle reti a cui vi siete collegati.
- Impostate la rete di casa su **WPA3**.
- Abilitate l'**indirizzo MAC privato** per ogni rete: **Impostazioni Wi-Fi > Dettagli rete > Indirizzo Wi-Fi privato**.

### Autorità di certificazione

macOS si fida di oltre **100 certificati root CA** di aziende e governi di tutto il mondo. Significa che molte organizzazioni sono tecnicamente in grado di emettere certificati validi per qualsiasi dominio. Apple blocca le CA inaffidabili e applica requisiti stringenti, ma il rischio di attacchi MITM (Man-in-the-Middle, un intercettatore che si mette "in mezzo" tra voi e il sito) tramite certificati fraudolenti, per quanto basso, esiste (ricordate il caso DigiNotar?).

Per rimuovere la fiducia da una CA: aprite **Accesso Portachiavi**, trovate il certificato root, doppio clic e impostate "Non fidarsi mai".

### Una nota sulle VPN

Questa è una guida sul Mac, non sulle VPN, quindi sarò breve. Tenete a mente un punto: una VPN **non vi rende anonimi**, sposta semplicemente la fiducia dal vostro provider internet al provider VPN. Quindi la domanda giusta è "di chi mi fido?".

- Il massimo controllo è **hostarvi la VPN da soli** (per esempio WireGuard su un VPS).
- Se scegliete un servizio commerciale, preferite provider **no-log, senza account e pagabili in contanti o Bitcoin**: a oggi i nomi che reggono meglio sono **Mullvad**, **Obscura** e **IVPN**.
- In ogni caso, configurate un **kill switch** per evitare fughe di traffico quando la VPN cade, ed evitate protocolli obsoleti come PPTP.

## App, malware e integrità del sistema {#app-malware style="color: white;"}

Le difese di sistema di macOS sono buone, ma funzionano solo se non le smontate voi stessi installando qualsiasi cosa. Qui vediamo come scegliere e verificare il software, e come tenere in piedi le protezioni native.

### Browser

Il browser è la **superficie di attacco più grande** del vostro sistema. La scelta conta.

Su Apple Silicon, per la **maggior parte degli utenti la scelta migliore è Safari**. Non lo dico per affezione all'ecosistema: è il browser più profondamente integrato nelle difese del sistema. Ha una sandbox solida, usa l'Hardened Runtime, supporta la **Modalità Lockdown**, include **Intelligent Tracking Prevention** e difese anti-fingerprinting, isola la navigazione privata e, come bonus, ha di gran lunga la migliore autonomia. Per il 99% delle persone, "Safari con Lockdown attivabile sui siti a rischio" è una difesa eccellente che non richiede smanettamenti.

**Firefox** resta la scelta giusta se avete bisogni specifici: estensioni come uBlock Origin o NoScript, **Multi-Account Containers** per isolare le sessioni, o hardening avanzato con [arkenfox/user.js](https://github.com/arkenfox/user.js). È open source, con protezione dal tracciamento integrata e adozione crescente di Rust per la sicurezza della memoria.

**Chrome** lo sconsiglio per la privacy: il sandboxing è ottimo, ma è di Google ed è progettato per raccogliere dati. Se proprio dovete usarlo, almeno usate uBlock Origin Lite e disabilitate il DNS prefetching.

Qualunque browser scegliate, ricordate gli universali: disabilitate i **cookie di terze parti** (ormai default ovunque), siate consapevoli che **canvas fingerprinting** e **Navigator API** possono identificarvi, e che **WebRTC** può rivelare il vostro IP reale (la Modalità Lockdown lo mitiga).

### Homebrew

[Homebrew](https://brew.sh) è il package manager più usato su macOS, ma occhio: richiede **Gestione app** o **Accesso completo al disco**, che equivale di fatto ad allentare le protezioni TCC. Usatelo con consapevolezza, aggiornate su reti fidate e disattivate la telemetria:

```zsh
brew upgrade
export HOMEBREW_NO_ANALYTICS=1   # aggiungetelo a ~/.zshrc per renderlo permanente
```

### Servizi e daemon

macOS gestisce i servizi con **launchd**. Potete ispezionare quelli attivi:

```zsh
launchctl list
launchctl list | grep -i apple
```

I servizi di sistema sono protetti dal **System Integrity Protection (SIP)**: non disabilitate SIP per modificarli, è molto più sicuro lasciarli come sono. Per capire cosa fa un servizio, cercate il suo `.plist` in `/System/Library/LaunchDaemons/`, `/System/Library/LaunchAgents/`, `/Library/LaunchDaemons/` o `~/Library/LaunchAgents/`.

### Virus e malware

I Mac **non sono immuni** al malware, e il numero di minacce cresce di continuo. Le regole d'oro per scaricare software:

- Preferite l'**App Store** o app **notarizzate** da Apple.
- Scaricate sempre dai siti **ufficiali** via HTTPS.
- Diffidate delle app che chiedono permessi eccessivi.
- Preferite il **software open source** quando possibile.

Prima di eseguire un file sospetto, passatelo da [VirusTotal](https://www.virustotal.com/). macOS include **XProtect**, che si aggiorna in background, e **[BlockBlock](https://objective-see.org/products/blockblock.html)** può segnalarvi i tentativi di malware di rendersi persistente. Un antivirus locale tradizionale, invece, è un'arma a doppio taglio: aumenta la superficie di attacco e spesso "telefona a casa" con i vostri dati.

Potete verificare le difese di una singola app:

```zsh
# Usa il sandbox? (tutte le app dell'App Store devono usarlo)
codesign --entitlements - /Applications/NomeApp.app

# Usa l'Hardened Runtime? Cercate flags=0x10000(runtime) nell'output
codesign --display --verbose /Applications/NomeApp.app
```

### Gatekeeper

**Gatekeeper** blocca le app non notarizzate. Potete autorizzare manualmente un'app da **Privacy e Sicurezza**, ma fatelo solo per software di cui vi fidate completamente. Ricordate che Gatekeeper protegge i bundle `.app`, non tutti i binari eseguibili.

### System Integrity Protection (SIP)

SIP protegge i file di sistema da modifiche, anche da utente root. Verificate che sia attivo:

```zsh
csrutil status
```

Se risulta disabilitato, riattivatelo dalla modalità Recovery. **Non disabilitate mai SIP** a meno che non sappiate esattamente cosa state facendo e perché.

{{< cta type="inline" title="🛡️ Costruisci la Tua Fortezza Digitale" text="Avete già iniziato a blindare il vostro Mac, state costruendo qualcosa con le vostre mani, pezzo dopo pezzo. Ma un sistema operativo sicuro è solo un tassello del puzzle. La Guida Privacy Digitale completa il percorso: dalla protezione del telefono alle comunicazioni, dalla navigazione anonima alla gestione delle identità digitali." url="https://shop.priorato.org" button="Scopri la Guida Privacy Digitale" icon="🔒" >}}

## Dati, backup e sicurezza fisica {#dati-backup style="color: white;"}

Tutta la sicurezza del mondo non serve se perdete i dati o se qualcuno mette le mani sul Mac. Qui chiudiamo il cerchio: copie sicure, accessi protetti e difese fisiche.

![La regola del backup 3-2-1: 3 copie, 2 supporti, 1 offsite](backup-321-rule.svg)

### Backup cifrati

**Crittografate sempre i backup prima di salvarli.** Seguite la regola **3-2-1**: 3 copie, 2 tipi di supporto diversi, 1 copia offsite.

Il modo più semplice è **Time Machine con un disco esterno cifrato**: in **Impostazioni di Sistema > Generali > Time Machine > Aggiungi disco di backup** selezionate "Cifra backup".

Per backup mirati, macOS offre strumenti nativi per immagini disco cifrate:

```zsh
# Immagine disco cifrata AES-256
hdiutil create -size 500m -encryption AES-256 -volname "Backup Sicuro" -fs APFS ~/backup_sicuro.dmg
```

Chi vuole archivi cifrati portabili può usare GPG (`brew install gnupg`):

```zsh
# Creare e decrittare un archivio cifrato
tar czf - ~/Documents | gpg --encrypt --recipient la_vostra_email > backup_docs.tar.gz.gpg
gpg --decrypt backup_docs.tar.gz.gpg | tar xzf -
```

### Password e autenticazione

L'app **Password** integrata in macOS genera credenziali sicure, le sincronizza in modo cifrato con iCloud Keychain e supporta le **passkey** (FIDO). Per le password che dovete ricordare a memoria, usate il metodo **diceware** (più parole casuali dal dizionario).

Abilitate l'**autenticazione a più fattori (MFA)** su tutti gli account che contano. In ordine di robustezza:

1. **WebAuthn/FIDO2** (chiave hardware come YubiKey): il più sicuro.
2. **TOTP** (app come Aegis o 2FAS): molto buono.
3. **HOTP**: buono.
4. **SMS**: meglio di niente, ma vulnerabile al SIM swapping (clonazione della SIM).

A mio parere una **YubiKey** vale l'investimento: la usate per WebAuthn e, volendo, come chiave hardware per SSH.

### SSH come servizio

macOS ha il **Login remoto (sshd) disabilitato di default**: lasciatelo così se non vi serve. Se proprio dovete abilitarlo (**Impostazioni di Sistema > Generali > Condivisione > Login remoto**):

- **disabilitate l'autenticazione con password**, usate solo chiavi
- proteggete le chiavi con una passphrase (o tenetele su YubiKey)
- limitate gli utenti autorizzati e considerate fail2ban o simili

### Sicurezza fisica

- **Non lasciate mai il Mac incustodito**: i keylogger hardware esistono (mitigati usando la tastiera integrata o Bluetooth).
- Strumenti anti-forensics come **[BusKill](https://www.buskill.in/)** e **[swiftGuard](https://github.com/Lennolium/swiftGuard)** possono spegnere il sistema quando rilevano eventi USB non autorizzati o la separazione fisica.
- Usate un **filtro privacy** sullo schermo quando lavorate in pubblico.
- Per i più paranoici: **smalto per unghie** o sigilli antimanomissione sulle viti del case aiutano a rilevare accessi fisici.

{{< cta type="inline" title="₿ Proteggi Anche i Tuoi Bitcoin" text="Siete quasi alla fine di questa guida e avete già competenze che il 99% degli utenti Mac non ha. Manca solo un pezzo: proteggere i vostri Bitcoin con lo stesso livello di attenzione. Acquisti senza KYC, mixing, wallet privacy-oriented, tutto nella Guida Privacy Bitcoin." url="https://shop.priorato.org" button="Vai alla Guida Privacy Bitcoin" icon="🛡️" >}}

## Monitorare e fare audit del sistema {#monitoraggio style="color: white;"}

Le difese vanno verificate. Tenere d'occhio processi, connessioni e log vi permette di accorgervi quando qualcosa si comporta in modo strano.

### Processi e rete

```zsh
# Processi e servizi caricati
ps -ef
launchctl list

# Connessioni di rete attive e porte in ascolto
lsof -Pni
netstat -atln
```

Per una vista grafica usate **Monitoraggio Attività** (ha anche una colonna "Sandbox"). Per analisi approfondite del traffico, **Wireshark** o **tshark** vi mostrano query DNS, richieste HTTP e certificati TLS.

### Log e audit

macOS includeva **OpenBSM** per monitorare processi e attività di rete, ma Apple lo ha deprecato da macOS 11 (Big Sur) in favore dell'**Endpoint Security framework**. Su versioni recenti potrebbe non funzionare del tutto; valutate strumenti basati su Endpoint Security, come quelli di [Objective-See](https://objective-see.org/).

### Software di audit

Per controlli più sistematici:

- **[Lynis](https://cisofy.com/lynis/)**: audit di sicurezza da riga di comando.
- **[osquery](https://osquery.io/)**: interrogate il sistema con query SQL.
- **[Pareto Security](https://paretosecurity.com/)**: app nella barra dei menu per controlli base ricorrenti.

---

Bravissimo eroe! Se siete arrivati fin qui, avete trasformato il vostro Mac da un sistema "così com'è" a una vera fortezza digitale, lavorando dove conta davvero: le impostazioni del sistema operativo. Non è stata una passeggiata, ma ne è valsa la pena. Ora avete gli strumenti e le conoscenze per usare il Mac con un livello di privacy e sicurezza che pochissimi raggiungono.

Grazie mille per la lettura! Se questa guida vi è stata utile, condividetela con altre tartarughe che vogliono proteggere il proprio Mac. La privacy è un diritto, non qualcosa da nascondere.

{{< cta type="bottom" title="Vai Oltre: Il Bundle Completo Privacy" text="Avete blindato il Mac, ora completate il quadro. Il Bundle Completo include la Guida Privacy Digitale e la Guida Privacy Bitcoin: tutto ciò che serve per proteggere la vostra vita digitale e finanziaria, in un unico pacchetto a prezzo ridotto." url="https://shop.priorato.org" button="Scopri il Bundle Completo" icon="🐢" >}}

## Guide Correlate

- **[Guida al Threat Model](/threat-model)** - Capite da chi vi state difendendo per scegliere le misure giuste per voi
- **[Hardening di Linux](/linux-hardening)** - Applicate gli stessi principi a una base ancora più controllabile
- **[VPN Self-Hosted con WireGuard e Pi-hole](/vpn)** - Hostate la vostra VPN personale per il massimo controllo sulla rete
- **[Guida alla Privacy di Android e De-Google](/android)** - Estendete la privacy anche al vostro telefono

<div style="text-align: center; margin-top: 2em;">
<a href="bitcoin:bc1qfundaddresshere" style="text-decoration: none;">
<img src="/img/btc-donate.svg" alt="Dona in Bitcoin" width="200">
</a>
</div>
