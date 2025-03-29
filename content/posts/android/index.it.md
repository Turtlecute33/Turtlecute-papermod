            
---
title: "Guida al De-Google e privacy su android"
description: "Questa vuole essere una guida completa per ottenere un telefono Android completamente de-googled con la massima privacy e sicurezza possibile, pur mantenendo l'usabilità e comodità del dispositivo."
keywords: ["android privacy", "privacy ita", "android privacy italiano", "degoogle", "privacy phone", "graphene os", "graphene os italiano", "graphene os ita", "degoogle italiano"]
author: "Turtlecute"
date: 2025-03-29
url: /android
images: ["/posts/android/1.webp"]
---

![](/posts/android/1.webp)

Questa vuole essere una guida completa per ottenere un telefono Android completamente de-googled con la massima privacy e sicurezza possibile, pur mantenendo l'usabilità e comodità del dispositivo.

La guida è aperta a miglioramenti e consigli, descriverò la configurazione che trovo con il miglior rapporto usabilità/privacy, nel tempo ampierò le varie sezioni introducendo anche varie alternative per chi magari non si trova bene con una determinata applicazione o servizio, Se volete darmi consigli, contribuire alla guida o effettuare donazioni, potete dare un occhiata alla pagina [Donazioni](https://btcpay.priorato.org/i/CXG1ouF8eHjdCV73Th4Ujb) o effettuare una pull request su [GitHub](https://github.com/Turtlecute33/Turtlecute-papermod).  

Questa guida parla di android in generale, ne ho scritta anche una specifica per GrapheneOS, potete trovarla [qui](https://turtlecute.org/graphene), se siete interessati ad acquitare dispositivi con set-up di privacy su misura contattatemi su [Telegram](https://turtlecute.org/android)
  

## Sistema operativo

Esistono vari sistemi operativi Android privacy-oriented (GrapheneOS, CalixOS, etc). In questa guida tratteremo l’approccio usando come base LineageOS, ma è comunque compatibile con ogni altro sistema operativo AOSP. Se possibile consiglio vivamente di usare GrapheneOS in quanto ha funzioni decisamente piu avanzate e complete di qualasiasi altro sistema operativo sul mercato.

Questa guida è stata pensata e studiata per offrire un ottimo bilanciamento tra sicurezza e privacy nell'utilizzo del proprio telefono, procedure come il rooting e lo sblocco del bootloader riducono notevolmente la sicurezza del dispositivo e sono per questo fortemente sconsigliate.

Per semplificare i passi per l’installazione di Lineage facciamo un brevissimo riassunto:

1.  Sbloccare il bootloader
2.  Flashare una recovery
3.  Flashare [Lineage OS](https://lineageos.org/)
4.  Se possibile sul vostro dispositivo ri-bloccare il bootloader

Attenzione, la versione base senza Google apps è di gran lunga preferibile (e fortemente consigliata), ma utilizzando microG senza aggiungere nessun account Google potremo almeno utilizzare i servizi base di Android senza andare incontro a crash e malfunzionamenti di app dipendenti da essi, valutate quale soluzione si adatta meglio alle vostre esigenze. 
  

A questo punto ci troveremo con un sistema operativo fresco e appena installato!

## Modifica e setup del sistema

Per avere un dispositivo privacy-oriented cominceremo con il modificare i vari settings del sistema operativo, elenchiamo le principali impostazioni ed accorgimenti, anche se questi possono cambiare da dispositivo a dispositivo:

*   Disabilitare bluetooth e posizione ogni volta che non vengono utilizzati
*   Attivare la privacy nel blocco schermo e un metodo di protezione del dispotivo (pin e notifiche nascoste con telefono bloccato)
*   Disabilitare tutti i dati telemetrici
*   Abilitare se disattivata la criptazione del dispositivo
*   Disabilitare i backup
*   Rifiutare ogni volta, se possibile, la condivisione di dati di telemetria e crash in tutte le app installate
*   Ricordarci di disattivare il debug USB ogni volta che lo utilizziamo (disabilitato di default), in quanto espone a grossi rischi di sicurezza

Gestiremo in seguito i permessi delle applicazioni.
  

## Store per il download delle app

Essendo ora separati dal mondo Google dovremo trovare altri store da cui scaricare le applicazioni, le alternative principali sono:

*   [Obtanium](https://obtainium.imranr.dev/): É un app updater piú che uno store, ha un comportamento simile ai packet manager di linux. Ottima sicurezza e privacy, permette di scaricare e aggiornare le app direttamente dalle varie release su github o repository F-droid.
*   [Droid-ify](https://www.f-droid.org/packages/com.looker.droidify/): fork di F-Droid con una grafica più curata e alcune funzioni aggiuntive. Uno store di applicazioni open-source e molto ben fatto anche se con qualche trade-off di sicurezza.
*   [Aurora Store](https://files.auroraoss.com/AuroraStore/Stable/): vi permette di usare il vecchio store Google ma attraverso account fittizi e automaticamente generati all'avvio dell'app, estremamente utile in caso vogliate un esperienza simile al play store ma senza app propietarie.

  

## Shelter

![](/posts/android/shelter.webp)

⚠️ Questo passaggio é opzionale, serve principalmente se siete interessati a creare diversi "contenitori" sul vostro telefono isolati tra di loro. Utilizzare Shelter ha ventaggi e svantaggi e fa fatto solo in caso siate interessati alle funzioni che offre. Se pensate di voler isolare alcune app (per esempio messaggistica privata sotto Tor) da altre (Per esempio app invasive lato privacy come quelle bancarie) procedete, se non necessario saltate questa sezione.

Ora che abbiamo gli store configurati possiamo procedere al download di [Shelter](https://f-droid.org/packages/net.typeblog.shelter/). 

Shelter è un'applicazione open source che ci permette di creare un work profile, ovvero un secondo profilo nel telefono che funziona contemporaneamente al primo ma in modo isolato e indipendente  
  
Immaginate un tavolo (il nosto sistema operativo) su cui poggiano due scatole chiuse e sigillate (i nostri due profili), queste due sono completamente indipendenti e separate, ma usano una base comune. Se l'OS del nostro telefono è il primo ad essere sporco e pieno di app traccianti come i Google Play Services, l'utilizzo di Shelter diventa in buona parte inutile. Nel caso in cui non vogliate cambiare ROM, usate almeno questo [Android Debloater](https://github.com/0x192/universal-android-debloater) che vi permette di disabilitare in pochi e semplici tap le principali app tossiche per la privacy incluse nei maggiori sistemi operativi di default (ATTENZIONE disabilitate le app, non disinstallatele, o rischierete di corrompere il sistema se avete il telefono criptato).  
  
Una volta aperto Shelter si aprirà un menu di configurazione del profilo di lavoro, una volta attivato accederemo all'interfaccia dell'app, che è divisa in 2 sezioni:  

*   **Main**: il profilo principale in cui installeremo solo app open source o senza accesso ad internet.
*   **Shelter**: la sezione in cui isoleremo tutte le applicazioni malevole e traccianti come social, app bancarie o closed source.

I 2 profili sono perfettamente separati e vedremo le app installate in quello principale come normali icone; quelle installate nel profilo di lavoro invece presenteranno un piccolo badge che le distingue dalle altre, esse coesisteranno all'interno dello stesso launcher. Per installare le app nel profilo desiderato ci basterà usare uno di questi 3 metodi:  
  

*   Dall'app Shelter clonare un'app da un profilo ad un altro (o dai settings usare la funzione installa APK).
*   Scaricare le app da uno store installato in quel profilo (installate Droid-ify sul profilo principale e pulito mentre Aurora in quello sporco e con le app traccianti).
*   Installare APK scaricati da internet (se possibile utilizzate sempre uno store di app, rende piú facile e sicuro scaricare e aggiornare i vari software).

I due sistemi saranno isolati, cosa abbastanza scomoda per la gestione dei contatti, galleria, file, ecc.. in quanto ognuno avrà i suoi. Nelle impostazioni di Shelter è possibile attivare una funzione che permette di far parzialmente parlare i due sistemi per la condivisione dei file. Nonostante questo la gestione del tutto rimarrà un po' scomoda fino a quando non ci farete l'abitudine.

## Gestione del threat model tra i profili

Ora che abbiamo due sistemi completamente diversi e isolati, applicheremo un threat model differente in entrambi. Nel primo (pulito ed open source) punteremo alla massima privacy facendo passare tutto il traffico dati attraverso Tor e DNScrypt, nel secondo (sporco e con elementi traccianti) invece punteremo a ridurre il più possibile il leak dei nostri dati, coscienti di utilizzare comunque applicazioni che probabilmente hanno già i nostri dati personali (andremo quindi a limitare il più possibile pubblicità e trackers).  
  
Come prima cosa ci concentriamo sul main profile ed scarichiamo [Invizible Pro](https://www.f-droid.org/packages/pan.alexander.tordnscrypt.stable/), applicazione che reindirizza tutto il traffico sotto Tor e cripta i DNS.  

Una volta aperta l'applicazione dal menù in alto a destra con i 3 puntini attiviamo la modalità VPN. Rechiamoci quindi nelle impostazioni del telefono nella sezione **Rete → Avanzate/VPN → Invizible Pro**, qui attiviamo la modalità 'VPN sempre attiva' e 'blocca connessioni senza VPN', in questo modo tutto il traffico passerà attraverso Invizible ed eviteremo qualsiasi leak di dati.  
  
Ora che abbiamo impostato correttamente la rete andiamo a modificare alcune impostazioni all'interno di Invizible, nel corso del tempo queste impostazioni vengono occasionalmente spostate, date un occhiata alle impostazioni dell'app e troverete comunque tutto:

*   In **DNSCrypt settings** abilitiamo require\_dnssec, nolog and nofilter, questo ci permetterà di usare sempre i migliori server DNS possibili.
*   Nella sezione **Fast Settings** abilitiamo 'avvia DNSCrypt all'avvio' e 'avvia TOR all'avvio', in questo modo l'app partirá direttamente al boot in automatico.
*   Nelle impostazioni rechiamoci in **Common Settings** e abilitiamo tutte e 3 le protezioni della sezione **MITM attack detection**, queste proteggeranno il nostro dispositivo quando connessi a Wi-FI pubblici.
*   Infine rechiamoci nella categoria **Firewall** e disabilitiamo l'accesso ad internet a tutte le applicazioni che non ne hanno bisogno (come per esempio la galleria, la tastiera, i giochi offline, ecc)

A questo punto il main profile è pronto per essere usato, ci possiamo ora dedicare al profilo di lavoro, quello con le applicazioni closed source.  

Qui possiamo adottare due diverse tecniche per la protezione dei dati:

*   Usare una VPN in caso cerchiamo protezione verso il nostro ISP (tramite essa possiamo anche filtrare pubblicità e tracker).
*   Usare NetGuard o qualche tipo di app come RethinkDNS o NextDNS per bloccare l'acceso ad internet alle applicazioni che non lo necessitano ed aggiungere il blocco delle pubblicità e trackers.

Tutte le opzioni sono valide, la decisione dipende principalmente dalla vostra volontà o meno di usare un servizio VPN. In caso vogliate approfondire l'argomento potete dare un occhio anticipatamente alla [sezione apposita.](#cloud)  

## Applicazioni

Ora che abbiamo gli store e le reti ben configurate passiamo a scaricare alcune app fortemente consigliate:

*   [HeliBoard](https://github.com/Helium314/HeliBoard): tastiera Android open source esattamente uguale alla Gboard, usare una tastiera offline e che non comunica ció che scrivete a server online é fondamentale per una buona sicurezza e privacy.
*   [Cromite](https://github.com/uazo/cromite): Un ottimo browser per la navigazione di tutti i giorni, altre alternative sono Brave o Vanadium (quest'ultimo é presente solo su graphene al momento). Se cercatr alti livelli di sicurezza EVITATE i browser firefox, su mobile hanno varie funzioni mancati e una superficie di attacco molto maggiore.
  

A questo punto possiamo procedere al download delle applicazioni facendo attenzione al profilo nel quale le installiamo:

  
*   [Aegis](https://www.f-droid.org/packages/com.beemdevelopment.aegis/): alternativa open source ed offline a Authy/Google Authenticator
*   [AntennaPod](https://f-droid.org/packages/de.danoeh.antennapod/): lettore di podcast totalmente open source, usa come fonte i principali lettori podcast esistenti
*   [Bitwarden](https://github.com/bitwarden/mobile/releases): miglior password manager, estremamente sicuro, consente anche il self-hosting
*   [Crypto Prices](https://f-droid.org/packages/de.cloneapps.crypto_prices): alternativa a CoinMarketCap
*   [Guerrilla Mail](https://f-droid.org/it/packages/cf.theonewiththebraid.guerrilla_mail/): client per Guerrilla Mail, una temp mail per gli spam
*   [LibreTorrent](https://www.f-droid.org/packages/org.proninyaroslav.libretorrent/): semplice, comodo e veloce client Torrent per Android
*   [LessPass](https://f-droid.org/packages/com.lesspass.android/): permette di generare password derivate dalla combinazione di sito + nome utente + una password fissa, l'eccellenza per avere password sicure
*   [Molly](https://molly.im/): una versione hardened e ripulita dal codice Google di Signal, portebbe essere una buona idea registrarsi con una SIM comprata senza documenti se legale nel vostro stato
*   [Nekogram](https://nekogram.app/): client per Telegram che non si appoggia ai servizi Google ed implementa PGP
*   [PipePipe](https://github.com/InfinityLoop1308/PipePipe): client di PeerTube, tutti i video di YouTube ma senza Google!
*   [Nextcloud](https://f-droid.org/en/packages/com.nextcloud.client/): client per usare e syncare nextcloud, a mio parere il miglior software per farsi un server multimediale in casa
*   [OpenKeychain](https://www.f-droid.org/packages/org.sufficientlysecure.keychain/): app per gestire le nostre chiavi PGP o per integrarle nelle applicazioni di messaggistica/e-mail
*   [Simple Bitcoin Wallet](https://www.f-droid.org/packages/com.btcontract.wallet/): wallet open source leggero, veloce e dalla ottima UI per gestire i vostri Bitcoin onchain
*   [SimpleLogin](https://www.f-droid.org/packages/io.simplelogin.android.fdroid/): una sorta di proxy e-mail anti-spam, crea delle e-mail esca con cui registrarvi ai siti che automaticamente girano le e-mail ad altri indirizzi da voi scelti, in questo modo non dovrete dare la vostra e-mail a siti esterni. Inoltre potete eliminare o sospendere le e-mail esca quando volete in modo da interrompere la ricezione delle e-mail sul vostro account principale
*   [Simple Crypto Widget](https://f-droid.org/packages/com.brentpanther.bitcoinwidget/): per avere i prezzi aggiornati della vosta criptoval...COFF COFF di Bitcoin sulla vostra home page
*   [Tor Browser](https://www.torproject.org/download/#downloads-alpha): broswer Tor ufficiale con libreria Tor integrata, utile per navigare online senza rivelare l’indirizzo IP, non garantisce un anonimato al 100% come ogni cosa ma è un ottimo scudo per la privacy, utile per navigare nei siti .onion
*   [Voice](https://www.f-droid.org/packages/de.ph1b.audiobook/): lettore offline e opensource di audiolibri

Per ulteriori applicazioni, browser e servizi privacy friendly consiglio di dare un occhio a [privacytools](https://www.privacytools.io/), [privacyguides](https://privacyguides.org/providers/) o cercare nelle varie categorie su Droid-ify.

## Client e provider email

Il discorso su quale sia il miglior client e provider email è lungo e complesso, in caso volessimo un servizio rapido e comodo ma in cui dobbiamo riporre fiducia consiglio [Proton Mail](https://github.com/ProtonMail/proton-mail-android/releases), tra le varie soluzioni pronte all'uso é sicuramente tra quelle con miglior rapporto usabilitá / privacy.
  
Un'opzione molto valida è quella di usare come client (quindi come app su cui riceviamo le mail) [Thunderbird](https://www.thunderbird.net/en-US/) e come provider (quindi come servizio email da collegare all'app) qualche gruppo/collettivo privacy friendly o anarchico come [Riseup](https://riseup.net/), [Esiliati](https://esiliati.org/) o [Autistici](https://www.autistici.org/).
  
Molto interessante, all'interno delle impostazioni di Thunderbird, è l'opzione di auto-criptazione delle email: importando una chiave PGP da OpenKeychain (app sopra trattata), è possibile criptare automaticamente le email verso le persone che a loro volta hanno importato una chiave PGP.

A questo punto della guida dovreste aver già installato tutte le vostre applicazioni personali e quelle da me indicate o consigliate, possiamo agire ora sui vari permessi. In caso installiate in futuro altre app, eseguite questa procedura anche per esse.

## Gestione dei permessi delle app

Come primo passo ci rechiamo nelle impostazioni del nostro telefono e andiamo nella sezione Applicazioni → Avanzate → Gestione permessi e qui rimuoviamo ogni permesso superfluo delle applicazioni (ad esempio un'app come WhatsApp ha bisogno dei nostri contatti se vogliamo trovarli, quindi per il corretto funzionamento della stessa conviene lasciarglielo, ma possiamo tranquillamente disabilitare l’accesso ai messaggi in quanto verrà usato solo la prima volta quando faremo il login per velocizzare il primo accesso, dopodiché se lasciato attivo concede a WhatsApp la possibilità di spiare tutti i nostri SMS).  
  
Prestiamo particolare attenzione ai permessi di geolocalizzazione, fotocamera e microfono.  
  
Quando un'app ci chiede un permesso che non è utile o siete consapevoli di usare saltuariamente, concedete il permesso ‘solo per questa volta', in modo che non ne abbia continuo accesso.  
  
Dopo aver modificato tutti i permessi andiamo anche a disabilitare l’accesso ad internet a tutte le applicazioni che non necessitano della rete (per esempio i vari file manager, calcolatrici, agende, note, tastiere, ecc). Possiamo farlo comodamente andando nelle informazioni di un'applicazione → Dati e rete → disabilitiamo ‘Accesso alla rete’.  
  
In caso vogliate essere ulteriormente certi del blocco di internet a queste app, potete usare servizi come i precedentemente trattati NetGuard e Invizible per bloccarle dietro un firewall. Non sottovalutate l’accesso ad internet delle app, molte, nonostante non ne abbiano bisogno per il loro funzionamento, lo usano di continuo per condividere nostri dati.

## Cloud

La migliore soluzione cloud sarebbe il self hosting con Nextcloud (a mio parere la miglior scelta). In caso ciò non sia possibile, la soluzione a mio parere piu semplice e veloce è [Mega.nz](http://mega.nz/) (20 GB gratis e 5 GB di bandwith ed accetta pagamento in bitcoin per i pro plans). 

Mega non offre particolari funzioni avanzate di privacy ma la user experience é ottima, servizi come proton drive possono essere interessanti anche se al momento un po' acerbi.

Se vogliamo invece una sicurezza aggiuntiva possiamo usare un cloud in combinazione con [Cryptomator](https://cryptomator.org/) (programma che cripta i file prima dell’upload in cloud).  
  
## VPN
Il discorso VPN invece è particolare, una VPN cripta il nostro traffico e lo fa passare attraverso un suo nodo mettendosi tra noi e il nostro ISP, dandoci maggiore privacy verso di esso ma obbligandoci a fidarci del servizio VPN stesso.  

Tutte le aziende in questo settore promettono privacy e politiche di no-logging, ma non é possibile verificare queste affermazioni. I servizi a mio parere piú interessanti sonoL

* Mullvad
* Proton
* IVPN
* [Self-host](https://turtlecute.org/vpn) 
* Offro il servizio di set-up di VPN custom e su misura, se interessati [contattatemi](https://t.me/turtlecute33)
  
## Conclusioni Finali

Seguendo questa guida avremo ridotto drasticamente la condivisione di dati personali, ciò non garantisce in nessun modo l’anonimato, ma aumenta decisamente la privacy e la sicurezza nell’utilizzo del dispositivo.  
  
Altri ottimi posti per rimanere aggiornati in ambito privacy e degoogle sono vari subreddit:

*   [DEGOOGLE](https://www.reddit.com/r/degoogle/)
*   [PRIVACYTOOLS](https://www.reddit.com/r/privacytools/)
*   [PRIVACY](https://www.reddit.com/r/privacy/)

> "Dire che la privacy e' inutile perché non si ha nulla da nascondere è come dire che la libertà di parola è inutile perché non si ha nulla da dire".



[![Vai alla pagina](https://btcpay.priorato.org/img/paybutton/pay.svg)](https://btcpay.priorato.org/api/v1/invoices?storeId=2B1STLH5REvhHZBRQuyJNieRTexpeuJ4Usjn4ziEfEfd&currency=EUR)

