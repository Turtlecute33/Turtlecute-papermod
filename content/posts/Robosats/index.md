---
title: "RoboSats: Comprare Bitcoin P2P Senza KYC"
description: "Guida passo-passo a RoboSats: acquista e vendi Bitcoin in modo anonimo via Tor, senza documenti e senza KYC. Tutorial completo in italiano."
summary: "Guida passo-passo a RoboSats: acquista e vendi Bitcoin in modo anonimo via Tor, senza documenti e senza KYC. Tutorial completo in italiano."
keywords: ["RoboSats", "Bitcoin", "P2P", "no KYC", "guida RoboSats", "Bitcoin anonimo"]
author: "Turtlecute"
date: 2024-09-12
url: /robosats
images: ["/posts/Robosats/img/robosats1.webp"]
series: ["Privacy Bitcoin"]
---

![Schermata iniziale RoboSats](img/robosats1.webp)

> **TL;DR** - In questa guida imparerai:
> - Come accedere a RoboSats tramite Tor Browser in modo anonimo
> - Come creare un'identità robot usa e getta per ogni scambio
> - Come acquistare Bitcoin come compratore e come creare ordini di vendita
> - Come gestire controversie e annullamenti in sicurezza

Comprare Bitcoin su exchange centralizzati significa consegnare documenti, selfie e dati bancari a piattaforme che possono essere hackerate o obbligate a condividere le tue informazioni. RoboSats offre un'alternativa radicale: scambi peer-to-peer via Tor, identità usa e getta e nessun documento richiesto. Questa guida ti mostra come usarlo in modo sicuro dall'inizio alla fine.

Questa guida ti accompagnerà passo dopo passo nell'utilizzo di RoboSats per acquistare e vendere Bitcoin in modo anonimo e sicuro. Imparerai come generare il tuo account, esplorare i vari ordini, acquistare, vendere e gestire eventuali controversie.

Questa guida è stata tradotta dal sito ufficiale di RoboSats. Se desideri visualizzarla in altre lingue, puoi dare un'occhiata [qui](https://learn.robosats.com/read/en/). Se sei un utente Android, esiste anche un'app di RoboSats scaricabile da [GitHub](https://github.com/RoboSats/robosats/releases) o [F-Droid](https://apt.izzysoft.de/fdroid/index/apk/com.robosats) aggiungendo il repository di IzzyOnDroid.

Per accedere al sito web è necessario usare [Tor browser](https://www.torproject.org/download/), una volta scaricato, installato e aperto potete visitare [questo link](http://robosatsy56bwqn56qyadmcxkx767hnabg4mihxlmgyt6if5gnuxvzad.onion/) per accedere all'home page.

## Indice

- [Introduzione](#introduzione)
- [Generazione dell'Avatar](#generazione-dellavatar)
- [Recupero di un Robot](#recupero-di-un-robot)
- [Esplorazione del Libro degli Ordini](#esplorazione-del-libro-degli-ordini)
- [Guida 1: Accettare un Ordine come Acquirente](#guida-1-accettare-un-ordine-come-acquirente)
- [Guida 2: Creare un Ordine come Venditore](#guida-2-creare-un-ordine-come-venditore)
- [Annullamento Collaborativo](#annullamento-collaborativo)
- [Controversie](#controversie)
- [Conclusioni](#conclusioni)

## Introduzione {#introduzione}

RoboSats è una piattaforma di acquisto e vendita di Bitcoin P2P, incentrata sulla facilità d'uso e sulla privacy degli utenti. È così semplice da utilizzare che potresti pensare che un tutorial non sia necessario. Tuttavia, è utile sentirsi a proprio agio durante l'acquisto dei nostri amati satoshi per evitare possibili errori. Dopotutto, gli scambi P2P di Bitcoin possono essere intimidatori! Non temere, RoboSats rende tutto molto semplice e questa guida ti accompagnerà passo dopo passo in questa avventura! :D

Questo documento presenta due guide complete:

1. Come acquirente che accetta un ordine.
2. Come venditore che crea un ordine.

Dato che la piattaforma spiega all'utente ogni passaggio nei menu, dedicheremo alcune righe a trucchi e consigli per un acquisto sicuro.

## Generazione dell'Avatar {#generazione-dellavatar}

RoboSats aiuta gli utenti a preservare la propria privacy utilizzando avatar generati al momento per ogni trade, che sono semplicissimi da creare! In pratica, si tratta di identità generabili che ti permettono di avere un account diverso ogni volta che acquisti o vendi satoshi.

![Avatar robot RoboSats](img/robosats_avatar.webp)

RoboSats ti dà il benvenuto con un avatar robot unico. Il robot è generato deterministicamente in base al token che vedi sotto di esso. Questo token è tutto ciò di cui hai bisogno per recuperare l'account in futuro, quindi assicurati di salvarlo in modo sicuro!

I token sono generati nel tuo browser. Tuttavia, se non ti fidi della casualità del tuo dispositivo, puoi anche inserire manualmente dell'entropia.

Clicca su "Genera" per creare il tuo primo account su RoboSats!

![Generazione avatar RoboSats](img/robosats_generate_avatar.webp)

Il token rimarrà nella memoria del tuo browser per un certo periodo, quindi potresti ancora avere la possibilità di copiarlo più tardi toccando l'icona del profilo nell'angolo in basso a sinistra. Tuttavia, il tuo browser dimenticherà il token se aggiorni o chiudi la pagina!

![Icona profilo RoboSats](img/robosats_profile_icon.webp)

Sarebbe meglio scriverlo su carta... ma è un sacco di lavoro! Molto spesso è sufficiente copiarlo negli appunti e salvarlo altrove. Se il tuo browser si blocca, la batteria del telefono si esaurisce o perdi la connessione durante l'acquisto, avrai bisogno del token per accedere nuovamente e continuare lo scambio!

## Recupero di un Robot {#recupero-di-un-robot}

Per recuperare un token salvato, basta sostituire il token nella casella di testo e premere "Genera Robot". Il sito ti saluterà con "Abbiamo trovato il tuo avatar Robot. Bentornato!"

## Esplorazione del Libro degli Ordini {#esplorazione-del-libro-degli-ordini}

In RoboSats puoi creare nuovi ordini o accettare ordini creati da altri. Per essere un creatore di ordini, basta cliccare su "Crea Ordine" nella homepage. Per accettare un ordine, clicca su "Visualizza ordini" per esplorare le offerte create dagli altri utenti.

Clicchiamo su "Visualizza ordini" e diamo un'occhiata agli ordini.

![Libro ordini RoboSats](img/robosats_order_book.webp)

In un browser desktop, puoi vedere a colpo d'occhio tutte le informazioni rilevanti sugli ordini, così puoi decidere quale accettare. Per impostazione predefinita, il book mostrerà ordini di "QUALSIASI" tipo (acquisto e vendita) e qualsiasi tipo di metodo di pagamento. Usa i menu a discesa in alto per selezionare le tue preferenze.

![Filtri libro ordini RoboSats](img/robosats_filters.webp)

Su uno smartphone, tuttavia, non tutte le colonne si adattano allo schermo. I soprannomi, il tipo di ordine, il metodo di pagamento e il tasso di cambio sono nascosti per impostazione predefinita. Puoi toccare qualsiasi colonna e premere "Mostra colonne" per selezionare quali rendere visibili.

![Mostra colonne nel libro ordini](img/robosats_show_columns.webp)

Un altro trucco è fare un tocco lungo o uno swipe:

- **Sull'Avatar**: ottieni il soprannome e lo stato di attività.
- **Sull'Importo**: ottieni se il creatore è un venditore o un acquirente.
- **Sulla Valuta**: ottieni i metodi di pagamento preferiti.
- **Sul Premio**: ottieni il tasso di cambio corrente.

Esempio di tocco lungo/scorrimento sopra la valuta:

![Tocco lungo sulla valuta](img/robosats_currency_long_tap.webp)

Esempio di tocco lungo/scorrimento sopra il premio:

![Tocco lungo sul premio](img/robosats_premium_long_tap.webp)

Puoi anche toccare qualsiasi ordine per vedere la pagina completa dell'ordine:

![Dettagli ordine RoboSats](img/robosats_order_details.webp)

Ogni ordine ha un contatore di scadenza. Per impostazione predefinita, in RoboSats v0.1.0 i nuovi ordini rimarranno pubblici nel libro per 24 ore.

{{< cta type="inline" title="Proteggi la tua identità quando compri Bitcoin" text="Con una SIM senza KYC puoi registrarti ai servizi di pagamento senza fornire documenti. Numero anonimo, nessun dato personale." url="https://shop.priorato.org" button="Scopri le SIM no-KYC" icon="🔒" >}}

## Guida 1: Accettare un Ordine come Acquirente {#guida-1-accettare-un-ordine-come-acquirente}

Quando hai deciso quale ordine accettare, basta premere il pulsante "Accetta Ordine". Vedrai la casella del contratto. Segui le indicazioni della casella del contratto fino a completare lo scambio! :)

La prima cosa da fare è bloccare una piccola cauzione di fedeltà (solo il 3% dell'importo dello scambio per impostazione predefinita), così il venditore saprà che sei affidabile. I satoshi di questa cauzione rimarranno bloccati nel tuo portafoglio. Se cerchi di barare o annulli unilateralmente, perderai i satoshi bloccati nella cauzione.

![Cauzione di fedelta RoboSats](img/robosats_fidelity_bond.webp)

Scansiona o copia la fattura nel tuo portafoglio Lightning. Potrebbe apparire come un pagamento in sospeso, bloccarsi o persino sembrare che il tuo portafoglio si sia bloccato. Dovresti sempre controllare sul sito di RoboSats se la cauzione è stata bloccata (il tuo portafoglio probabilmente non te lo dirà! Controlla la lista di compatibilità dei portafogli).

![Pagamento con wallet Lightning](img/robosats_wallet_payment.webp)

Non appena la tua cauzione è bloccata, RoboSats ti chiederà di fornire una fattura Lightning per ricevere i satoshi al termine dello scambio. Genera una fattura con l'importo esatto nel tuo portafoglio Lightning e inviala.

![Fattura payout Lightning](img/robosats_payout_invoice.webp)

Mentre stai inviando la tua fattura di pagamento, al venditore viene chiesto di bloccare la cauzione del trade (hold invoice). Se sei più veloce di lui, dovrai aspettare. Altrimenti, potresti già essere in grado di chattare con lui.

C'è un limite di tempo di 3 ore per inviare la fattura (da parte dell'acquirente) e bloccare la cauzione del trade (da parte del venditore). Se il tempo scade, l'ordine scadrà e il robot che non ha rispettato gli obblighi contrattuali perderà la cauzione. Questo è un meccanismo che aiuta a prevenire lo spam di ordini falsi, la perdita di tempo delle controparti e gli attacchi DDoS al libro degli ordini.

![Limite di tempo ordine](img/robosats_time_limit.webp)

Non appena il venditore blocca i satoshi, è sicuro inviare la valuta fiat! Come acquirente, dovrai chiedere al venditore i dettagli per effettuare il pagamento fiat. Condividi solo le informazioni strettamente necessarie su di te per non compromettere la tua privacy. Ricorda, in RoboSats v0.1.0 questa chat non ha memoria, quindi la conversazione andrà persa se aggiorni il browser.

![Chat RoboSats](img/robosats_chat.webp)

C'è un limite di tempo di 24 ore per completare lo scambio fiat. Se il tempo scade, l'ordine scadrà e verrà aperta automaticamente una controversia. Per evitare la scadenza dell'ordine, usa sempre metodi di pagamento fiat istantanei. Ad esempio, inviare contanti per posta ordinaria è lento e attiverà sempre una controversia in v0.1.0. In futuro saranno possibili tempi di scadenza più lunghi.

Non appena hai inviato la fiat, dovresti premere il pulsante "Conferma fiat inviata". Dopodiché, il venditore dovrà confermare di aver ricevuto la fiat. Non appena conferma, lo scambio è terminato e verrai pagato sul tuo portafoglio Lightning. Potresti vedere che sta "inviando satoshi all'acquirente", ma di solito è così veloce che vedrai semplicemente questa schermata. Goditi i tuoi sat!

![Trade completato](img/robosats_trade_complete.webp)

Valutare la piattaforma e lasciare suggerimenti per miglioramenti nel nostro gruppo Telegram o su GitHub Issues è molto apprezzato!

## Guida 2: Creare un Ordine come Venditore {#guida-2-creare-un-ordine-come-venditore}

Potrebbe capitare che non ci siano ordini attivi per la posizione e la valuta che desideri. In questo caso, non ci sono ordini per VENDERE Bitcoin per GBP.

![Nessun ordine disponibile](img/robosats_no_orders.webp)

Possiamo creare l'ordine esattamente come lo desideriamo. Ma ricorda che devi pubblicare un ordine che altri siano interessati ad accettare!

![Creazione ordine RoboSats](img/robosats_create_order.webp)

Nella pagina del creatore di ordini è richiesto solo di inserire la valuta, il tipo di ordine (acquisto/vendita) e l'importo. Tuttavia, è buona pratica specificare i metodi di pagamento che accetti. Potrebbe essere anche utile impostare un premio/sconto per far accettare il tuo ordine più velocemente. Ricorda che come venditore puoi incentivare gli acquirenti ad accettare il tuo ordine abbassando il premio. Se ci sono troppi acquirenti, tuttavia, puoi aumentare il premio per ottenere un profitto di trading. In alternativa, puoi impostare un importo fisso di satoshi.

**Limiti**: in RoboSats v0.1.0 un ordine non può essere inferiore a 20.000 satoshi. Non può essere superiore a 4.000.000 di satoshi per evitare fallimenti di routing Lightning. Questo limite sarà aumentato in futuro.

![Limiti ordine RoboSats](img/robosats_order_limits.webp)

Devi copiare o scansionare la fattura con il tuo portafoglio Lightning per bloccare la tua cauzione di fedeltà come creatore (solo l'1% dell'importo dello scambio). Bloccando questa cauzione, i prenditori sanno che sei affidabile e sei impegnato a seguire questo scambio. Nel tuo portafoglio potrebbe apparire come un pagamento in sospeso, bloccarsi o persino sembrare che il tuo portafoglio si sia bloccato. Dovresti sempre controllare sul sito di RoboSats se la cauzione è stata bloccata (il tuo portafoglio probabilmente non te lo dirà! Controlla la lista di compatibilità dei portafogli).

![Cauzione creatore](img/robosats_maker_bond.webp)

Il tuo ordine sarà pubblico per 24 ore. Puoi controllare il tempo rimanente alla scadenza nella scheda "Ordine". Può essere cancellato in qualsiasi momento senza penalità prima che venga accettato da un altro robot. Tieni aperta la scheda del contratto per essere notificato con un suono. Potrebbe essere meglio farlo su un computer desktop e alzare il volume, così non ti perderai quando il tuo ordine viene accettato. Potrebbe volerci tempo! Forse te ne dimenticherai anche! Puoi anche abilitare le notifiche Telegram premendo "Abilita Notifiche Telegram" e poi premendo "Start" nella chat. Riceverai un messaggio di benvenuto come conferma delle notifiche abilitate. Un altro messaggio verrà inviato una volta che un prenditore per il tuo ordine viene trovato.

**Nota**: se dimentichi il tuo ordine e un robot lo accetta e blocca la sua cauzione di fedeltà, rischi di perdere la tua cauzione di fedeltà non adempiendo ai passaggi contrattuali successivi.

Nella scheda del contratto puoi anche vedere quanti altri ordini sono pubblici per la stessa valuta. Puoi anche vedere come si posiziona il tuo premio rispetto a tutti gli altri ordini per la stessa valuta.

![Statistiche ordine RoboSats](img/robosats_order_stats.webp)

Evviva, qualcuno ha accettato l'ordine! Ha 4 minuti per bloccare una cauzione di fedeltà come prenditore; se non procede, il tuo ordine sarà reso pubblico di nuovo automaticamente.

![Ordine accettato](img/robosats_order_taken.webp)

Non appena il prenditore blocca la cauzione, dovrai bloccare la cauzione del trade. Questa è una hold invoice Lightning e rimarrà bloccata nel tuo portafoglio. Sarà rilasciata solo quando confermi di aver ricevuto il pagamento fiat o se c'è una controversia tra te e il prenditore.

![Escrow trade Lightning](img/robosats_escrow.webp)

Una volta che hai bloccato la cauzione del trade e l'acquirente ha inviato la fattura di pagamento, è sicuro ricevere la fiat! Condividi con l'acquirente le informazioni minime necessarie per ricevere la fiat. Ricorda, in RoboSats v0.1.0 questa chat non ha memoria, quindi la conversazione andrà persa se aggiorni il browser.

![Invio fiat](img/robosats_send_fiat.webp)

L'acquirente ha appena confermato di aver inviato il pagamento! Ora controlla fino a quando la fiat non è nel tuo conto.

![In attesa della fiat](img/robosats_waiting_fiat.webp)

Confermando di aver ricevuto la fiat, la cauzione verrà addebitata e inviata all'acquirente. Quindi fallo solo quando sei sicuro al 100% che la fiat sia con te!

![Conferma fiat ricevuta](img/robosats_confirm_fiat_received.webp)

Tutto fatto!! :D

## Annullamento Collaborativo {#annullamento-collaborativo}

Dopo che la cauzione del trade è stata bloccata e prima che l'acquirente confermi di aver inviato la fiat, è possibile annullare l'ordine. Potrebbe semplicemente accadere che entrambi non abbiate un modo comune per inviare e ricevere fiat dopotutto. Potete concordare di premere il pulsante "Annullamento Collaborativo". Dopo che il pulsante "Fiat inviata" è stato premuto dall'acquirente, l'unico modo per annullare un ordine è aprire una controversia e coinvolgere lo staff.

![Annullamento collaborativo](img/closing.webp)

Questo non è assolutamente consigliato, poiché uno dei due trader perderebbe la sua cauzione di fedeltà, eccetto in casi eccezionali (a discrezione dello staff).

## Controversie {#controversie}

Gli equivoci capitano. Ma ci possono essere anche persone disposte a cercare di truffare gli altri. In questo caso, MakeshiftSource875 pensava di farla franca non confermando di aver ricevuto la fiat, come se potesse tenere i satoshi.

![Avvio controversia RoboSats](img/robosats_dispute.webp)

Questo in realtà non è possibile, poiché una controversia verrà aperta automaticamente alla scadenza. Tuttavia, se sai che qualcosa di sospetto sta accadendo, dovresti aprire una controversia.

![Apertura controversia](img/robosats_open_dispute.webp)

In RoboSats v0.1.0 il processo di gestione delle controversie non è completamente implementato nel web. Pertanto, la maggior parte dei contatti e delle risoluzioni deve avvenire tramite metodi alternativi. Assicurati di fornire un metodo di contatto allo staff. Dovrai scrivere una dichiarazione completa dei fatti; ricorda che lo staff non può leggere la tua chat privata per giudicare cosa è successo. È utile inviare immagini/screenshot. Per la massima privacy, questi possono essere crittografati tramite chiave PGP e caricati su qualsiasi sistema di condivisione file anonimo.

![Risoluzione controversia](img/robosats_dispute_resolution.webp)

Una volta che lo staff ha risolto la controversia, lo stato finale dell'ordine mostrerà la risoluzione. Assicurati di controllare il metodo di contatto fornito allo staff. Se sei il vincitore della controversia, lo staff ti chiederà nuovamente una fattura Lightning Network per inviarti il pagamento più la cauzione (la tua vecchia fattura è probabilmente scaduta!).

## Conclusioni {#conclusioni}

Congratulazioni! Ora sai come utilizzare RoboSats per acquistare e vendere Bitcoin in modo anonimo e sicuro. Ricorda sempre di mantenere le tue chiavi private al sicuro e di seguire le buone pratiche per proteggere la tua privacy.

Se questa guida ti è piaciuta, condividila con i tuoi amici e sui social network. Se hai suggerimenti o domande, non esitare a contattarmi!

{{< cta type="bottom" title="Hai comprato Bitcoin senza KYC? Ora proteggili." text="La Guida Privacy Bitcoin ti spiega come custodire, spendere e mixare i tuoi satoshi senza compromettere la privacy." url="https://shop.priorato.org" button="Vai alla Guida Privacy Bitcoin" icon="₿" >}}

---

## Guide Correlate

- **[Usare Bitcoin in Modo Privato](/bitcoin)** - La guida completa alla privacy su Bitcoin: nodo, wallet, transazioni e molto altro
- **[JoinMarket: Guida Completa ai CoinJoin](/joinmarket)** - Dopo aver acquistato su RoboSats, mixa i tuoi bitcoin con JoinMarket
- **[Generare un Seed Bitcoin con i Dadi](/seed)** - Crea le chiavi private del wallet dove ricevere i tuoi satoshi in modo sicuro
- **[Tutorial Nodo Tor](/tor)** - RoboSats funziona su Tor: scopri come supportare la rete

[![Vai alla pagina](https://btcpay.priorato.org/img/paybutton/pay.svg)](https://btcpay.priorato.org/api/v1/invoices?storeId=2B1STLH5REvhHZBRQuyJNieRTexpeuJ4Usjn4ziEfEfd&currency=EUR)
