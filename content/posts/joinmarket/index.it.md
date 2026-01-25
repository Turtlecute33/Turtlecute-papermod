---
title: "Come usare joinmarket per fare coinjoin"
description: "Guida e tutorial su come usare joinmarket per fare coinjoin su bitcoin in lingua italiana"
keywords: ["Bitcoin", "coinjoin", "joinmarket", "payjoin", "wasabi wallet", "samurai wallet", "joinmarket ita", "jam italiano", "jbitcoin ita"]
author: "Turtlecute"
date: 2024-05-15
url: /joinmarket
images: ["/posts/joinmarket/jm.webp"]
---

# JOINMARKET

![](/posts/joinmarket/jm.webp)
  
Se avete trovato questa pagina cercando online "Join**T**market" avete tutta la mia sincera stima. Siete capitati, però, in una guida che tratta un argomento completamente differente, ma estremamente interessante! 🚬🍁  
  
L'obiettivo di questo tutorial é quello di illustrare il funzionamento teorico e pratico di JoinMarket.  
  
Questa guida ha richiesto tantissimo lavoro, tempo e impegno per essere completata ed é a disposizione in modo completamente gratuito. Se hai trovato i contenuti qui presenti interessanti e utili ti invito ad effettuare una donazione di un qualsiasi importo a sostegno del mio progetto di divulgazione. Questo sito non contiene analytics, pubblicità o elementi traccianti grazie a tutti coloro che supportano la mia divulgazione sostenendomi. 🐢 💚
  

## Definizione teorica Joinmarket

Possiamo definire JoinMarket come uno strumento, o un wallet, che permette di effettuare CoinJoin con altri utenti in maniera totalmente trustless e senza alcun coordinatore centrale.  
Essendo tutta la parte teorica di questo tool estremamente ampia, ho deciso di affrontarla in una puntata specifica del mio podcast. Consiglio vivamente di proseguire nella lettura dopo aver ascoltato l'episodio, così da assimilare al meglio i concetti di base per utilizzare in maniera corretta questo programma.  
  
Potete recuperare la puntata a questi link diretti:  

*   [Spotify](https://open.spotify.com/episode/1UaeQxpNq9capLE3KwArbo)
*   [Google podcast](https://podcasts.google.com/feed/aHR0cHM6Ly9hbmNob3IuZm0vcy9iZDVkNWIyMC9wb2RjYXN0L3Jzcw/episode/N2Y1NmRlZDAtZTc4Mi00MDJmLTk3ODktODIyYzgwODBjODYx?sa=X&ved=0CAUQkfYCahcKEwjohMaiv6n8AhUAAAAAHQAAAAAQEw)
*   [Amazon music](https://music.amazon.it/podcasts/b1b27a88-c1c9-48de-a301-20f31d29c676/episodes/54dec992-5b03-463a-bb98-f653b72ccb63/il-priorato-del-bitcoin-joinmarket-dalla-teoria-alla-pratica---turtlecute)
*   [Anchor](https://anchor.fm/turtle-cute5/episodes/Joinmarket-dalla-Teoria-alla-Pratica---Turtlecute-e1t0bep) (qua potrete ascoltarla direttamente da browser).
*   [Antenna pod](https://antennapod.org/) é un podcast manager gratuito e opensource che non richiede registrazione.  
    Per trovare la puntata scaricate l'app, aggiungete manualmente il mio podcast incollando [questo link](https://anchor.fm/s/bd5d5b20/podcast/rss) nella sezione ¨feed rss¨, cercate poi la puntata dedicata a JoinMarket.

  
Da questo punto in poi tutti gli argomenti affrontati nel podcast veranno considerati già "conosciuti" e quindi non verranno ri-trattati.

## Installazione


Sistemi operativi:

<details>
<summary>Raspiblitz</summary>
Dal menu principale del vostro sistema operativo (da questo punto in poi chiamato semplicemente OS) andate nella sezione "SERVICES" per installare i servizi aggiuntivi e mettete la spunta a "JOINMARKET & JOININBOX".

Una volta installato, per accedere al terminale, dal menu iniziale andate su "EXIT" e poi inviate il comando `jm` nella shell per passare ad un utente dedicato all'utilizzo di solo joinmarket.

Di default su raspiblitz si avvierà Joininbox (una GUI per JM), per accedere alla linea di comando vi basterà selezionare "Exit" nel menu.
</details>

<details>
<summary>Umbrel</summary>
Umbrel é una delle distro plug & play più conosciuta anche se personalmente non la ho mai utilizzata. Nello store delle app é presente JAM (una versione con interfaccia grafica molto bella ma estremamente limitata nelle funzioni). Consiglio vivamente di usare JoinMarket (per fruire di tutte le sue possibilità) da shell seguendo questa guida. Per l'installazione é presente un tutorial direttamente sul [Github ufficiale](https://github.com/JoinMarket-Org/joinmarket-clientserver).
</details>

<details>
<summary>MyNode</summary>
Su mynode basta aprire un terminale ssh al vostro nodo per accedere alla linea di comando, arrivati qua JoinMarket sarà già preinstallato sul vostro sistema e potrete andare nella cartella contenente gli script per usare le varie funzioni da shell oppure lanciare joininbox con il comando `sudo mynode-joininbox`. Questa guida coprirà l'utilizzo di JM da terminale usando i vari script pre-installati.
</details>

<details>
<summary>Raspibolt</summary>
Tutta la parte di installazione e setup di Joinmarket è già coperta come parte opzionale all'interno della guida raspibolt.
</details>
<br>

## File di configurazione

JoinMarket é un software personalizzabile e con un'infinitá di settaggi; quest'ultimi sono specificati in un file di configurazione presente nella directory principale del programma chiamato ´Joinmarket.cfg´.  
  
In questa sezione andremo ad analizzare alcuni campi che potrebbe essere interessante approfondire e/o modificare, in base alle proprie esigenze. Vorrei sottolineare che tutte le modifiche di seguito elencate sono utili da conoscere per adattare il funzionamento del software alle esigenze personali pur non essendo obbligatorie.  
  
Prima di tutto spostiamoci nella cartella `joinmarket/scripts` e lanciamo il comando:  
  
`python wallet-tool.py generate`.  
  
A questo punto dovremmo ottenere un errore, ma così facendo il software ci genererà un file di settings pre-impostato. Potremo andare a modificare il file di configurazione da terminale con:  

`nano joinmarket.cfg`

oppure

`vim joinmarket.cfg`

una volta aperto noteremo numerose righe con varie impostazioni e relativa spiegazione in inglese. Nello specifico analizzeremo qua sotto le variabili piú interessanti:  

*   `merge_algorithm` in caso facessimo da maker questo campo regola con quanta aggressivitá il software consoliderá gli Output non spesi. In caso avessimo molti UTXO da consolidare, potrebbe aver senso switchare da ´gradual´ a ´greedy´
*   `tx_fees` regola come taker le FEE con cui pagare la transazione, é molto utile modificare questo setting in caso usaste spesso il tumbler (ne parleremo in seguito) in quanto se ci fosse uno spike delle FEE durante l'esecuzione di quest'ultimo, se non settassimo correttamente questo campo, rischieremmo di andare a spendere tantissimi sats per i coinjoin. Settando valori in migliaia (come per esempio 2000) questo equivarrá a 2 sats/vByte, 3500 a 3.5 sats/vByte e cosi via. Mi sentirei di consigliare un numero che va da 1500 a 6000 in base alle vostre necessitá.
*   `max_cj_fee_abs` serve a specificare quanto siamo disposti a pagare in termini assoluti i maker che scegliamo durante il coinjoin. Di default questo campo per i maker é 200 sats, una buona opzione potrebbe essere un numero variabile da 200 a 1000 sats per controparte (questo in base a quanto volete spendere e quanto anon-set ricercate per i vostri coinjoin)
*   `max_cj_fee_rel` ha la stessa funzione del campo sopra ma specifica le FEE relative (percentuali) che siamo disposti a pagare ad ogni controparte. Essendo questo un valore "percentuale", state attenti a non settare valori alti per evitare costi elevati nei coinjoin con grossi importi. Il valore di default per i maker é ´0.00002´, consiglio un valore simile o leggermente superiore.
*   `minimum_makers` é il campo che specifica con quante altre controparti facciamo CJ, di default joinmarket sceglie sempre da 4 a 9 controparti, volendo, per una maggiore privacy, possiamo alzare questo valore a 5 o 6 (renderá però le transazioni piú costose).
*   `cjfee_a` specifica, in caso facessimo da maker, quanti sats in termini assoluti vogliamo incassare per l'affitto della nostra liquiditá. Questo campo é totalmente soggettivo, il valore di default é gia ottimo (avremo così miglior privacy come maker) possiamo valutare di portarlo a 0 se vogliamo fare piú coinjoin in meno tempo.
*   `cjfee_r` uguale al campo sopra ma in termini percentuali e non assoluti. Anche qua consiglio di lasciare il valore di default o abbassarlo per attrarre piú takers.
*   `ordertype` con questo campo scegliamo da maker se farci pagare in maniera assoluta (absoffer) o percentuale (reloffer). Solitamente i takers preferiscono le offerte assolute per questioni economiche.
*   `minsize` se da maker non vogliamo avere UTXO troppo piccoli possiamo specificare il coinjoin minimo per partecipare. Questo campo é espresso in satoshi ed é totalmente soggettivo . Potremmo lasciare questo campo a 0 oppure aumentare fino a 500000 (sats), 1000000 (sats), ecc...

Prestate molta attenzione a non modificare per sbaglio i campi errati, alcune delle varibili presenti nel file joinmarket.cfg se impostate erroneamente potrebbero compromettere la funzionalitá del software o annientare completamente la vostra privacy, occhi aperti e attenzione al massimo!

## Setup dell'ambiente di lavoro


Alcuni nodi impostano automaticamente i valori corretti per questi campi all'interno del file joinmarket.cfg Consiglio di ricontrollare manualmente:

*   `rpc_user = yourusername-as-in-bitcoin.conf`
                            
*   `rpc_password = yourpassword-as-in-bitcoin.conf`
                            
*   `rpc_host = localhost #default usually correct`
                            
*   `rpc_port = 8332 # default for mainnet`  
    

A questo punto potremo procedere con la creazione del nostro wallet all'interno di JoinMarket:  
  
`python wallet-tool.py generate`  
  
Questo comando ci fará inserire una password con cui criptare il wallet e il nome che vogliamo dare ad esso, quando vi chiederá se volete supportare o meno i fidelity bond consiglio di usare l'opzione ´yes´, l'output restituito sará simile a questo:  
 
```
(jmvenv)$ python wallet-tool.py generate
Write down this wallet recovery mnemonic on paper:
    
matter aim multiply december stove march wolf nuclear yard boost worth supreme
    
Enter wallet encryption passphrase:
Reenter wallet encryption passphrase:
Input wallet file name (default: wallet.jmdat):
saved to wallet.jmdat
```
                       

  
in caso dia errore é molto probabile che abbiamo settato male i 4 campi RPC sopra specificati. Nel caso potrebbe aiutare seguire [questa guida](https://github.com/JoinMarket-Org/joinmarket-clientserver/blob/master/docs/USAGE.md#configure) presente nella documentazione originale di JM.  
  
Abbiamo completato il setup del nostro ambiente di lavoro e possiamo cominciare ad esplorare i comandi che piú ci torneranno utili. Tutti gli script di cui parleremo possono essere lanciati in console seguiti da ´--help´ per avere una spiegazione approfondita.  
  
Possiamo ora provare a lanciare:

```
python wallet-tool.py *nome del wallet prima creato*  
esempio: python wallet-tool.py wallet.jmdat
```
                    

questo comando vi mostrerá tutti i vari mixdepth del portafoglio con i vari indirizzi catalogati come:

*   New (address mai usato)
*   Change-out (resto di una precedente transazione)
*   Cj-out (output di un coinjoin)

ecco un esempio pratico del risultato:

```
JM wallet
mixdepth	0	xpub6CMAJ67vZWVXuzjzYXUoJgWrmuvFRiqiUG4dwoXNFmJtpTH3WgviANNxGyZYo27zxbMuqhDDym6fnBxmGaYoxr6LHgNDo1eEghkXHTX4Jnx
external addresses	m/84'/0'/0'/0	xpub6FFUn4AxdqFbnTH2fyPrkLreEkStNnMFb6R1PyAykZ4fzN3LzvkRB4VF8zWrks4WhJroMYeFbCcfeooEVM6n2YRy1EAYUvUxZe6JET6XYaW
m/84'/0'/0'/0/0     	bc1qt493axn3wl4gzjxvfg03vkacre0m6f2gzfhv5t	0.00000000	new
m/84'/0'/0'/0/1     	bc1q2av9emer8k2j567yzv6ey6muqkuew4nh4rl85q	0.00000000	new
m/84'/0'/0'/0/2     	bc1qggpg0q7cn4mpe98t29wte2rfn2rzjtn3zdmqye	0.00000000	new
m/84'/0'/0'/0/3     	bc1qnnkqz8vcdjan7ztcpr68tyec7dw2yk8gjnr9ze	0.00000000	new
m/84'/0'/0'/0/4     	bc1qud5s2ln88ktg83hkr6gv9s576zvt249qn2lepx	0.00000000	new
m/84'/0'/0'/0/5     	bc1qw0lhq7xlhj7ww2jdaknv23vcyhnz6qxg23uthy	0.00000000	new
Balance:	0.00000000
internal addresses	m/84'/0'/0'/1
Balance:	0.00000000
Balance for mixdepth 0:	0.00000000
mixdepth	1	xpub6CMAJ67vZWVXyTJEaZndxZy9ACUufsmNuJwp9k5dHHKa22zQdsgALxXvMRFSwtvB8BRJzsd8h17pKqoAyHtkBrAoSqC9AUcXB1cPrSYATsZ
external addresses	m/84'/0'/1'/0	xpub6FNSLcHuGnoUbaiKgwXuKpfcbR63ybrjaqHCudrma13NDqMfKgBtZRiPZaHjSbCY3P3cgEEcdzZCwrLKXeT5jeuk8erdSmBuRgJJzfNnVjj
m/84'/0'/1'/0/0     	bc1qhrvm7kd9hxv3vxs8mw2arcrsl9w37a7d6ccwe4	0.00000000	new
m/84'/0'/1'/0/1     	bc1q0sccdfrsnjtgfytul5zulst46wxgahtcf44tcw	0.00000000	new
m/84'/0'/1'/0/2     	bc1qst6p8hr8yg280zcpvvkxahv42ecvdzq63t75su	0.00000000	new
m/84'/0'/1'/0/3     	bc1q0gkarwg8y3nc2mcusuaw9zsn3gvzwe8mp3ac9h	0.00000000	new
m/84'/0'/1'/0/4     	bc1qkf5wlcla2qlg5g5sym9gk6q4l4k5c98vvyj33u	0.00000000	new
m/84'/0'/1'/0/5     	bc1qz6zptlh3cqty2tqyspjk6ksqelnvrrrvmyqa5v	0.00000000	new
Balance:	0.00000000
internal addresses	m/84'/0'/1'/1
Balance:	0.00000000
Balance for mixdepth 1:	0.00000000
mixdepth	2	xpub6CMAJ67vZWVY2cq5fmVxXw92fcgTchphGNFxweSiupYH1xYfjBiK6dj5wEEVAQeA4JcGDQGm2xcuz2UsMnDkzVmi2ESZ3xey63mQMY4x2w2
external addresses	m/84'/0'/2'/0	xpub6DqkbMG3tj2oixGYniEQTFamLCHTZx9CeAbUdBttiGuYwgfGZbrLMor8LWeJBUqTpsa81JcJqAUXuDxhXdLpKDxJAEqKMqPgJyXstj5dp3o
m/84'/0'/2'/0/0     	bc1qwtdgg928wma8jz32upkje7e4cegtef7yrv233l	0.00000000	new
m/84'/0'/2'/0/1     	bc1qhkuk2gny4gumrxcaw999uq3jm3fjrjvcwz7lz3	0.00000000	new
m/84'/0'/2'/0/2     	bc1qvu753lkltc8akfasclnq89tdv8yylu2alyg76y	0.00000000	new
m/84'/0'/2'/0/3     	bc1qal3r040k26cw2f08337huzcf00hrnws5rhfrz3	0.00000000	new
m/84'/0'/2'/0/4     	bc1qpv4nm7wwtxesgwsr0g0slxls33u0w02gqx2euk	0.00000000	new
m/84'/0'/2'/0/5     	bc1qk3ekjzlvw3uythw738z7nvwe2sg93w2rtuy6ml	0.00000000	new
Balance:	0.00000000
internal addresses	m/84'/0'/2'/1
Balance:	0.00000000
Balance for mixdepth 2:	0.00000000
mixdepth	3	xpub6CMAJ67vZWVY3uty61M6jeGheGU5ni5mQmqMW2QLQbEa8ZQXuBw1K2umKFZsmU8EMEafJZKQkGS1trtWE5dtz4XmDbvLvUccAPn26ZC5i2o
external addresses	m/84'/0'/3'/0	xpub6EvT4QFPRdkt2sji3QdLLZjkJQmk7G2y3umT99ceomKTXGYvZ5S9TLaGos6cEugXEuxS6s9kvSUj1Xvpiu65dn5yzK7CgdZLzXawpKC9Mpe
m/84'/0'/3'/0/0     	bc1q9ph5l2gknjezcmzv84rnhu4df566jgputzef7l	0.00000000	new
m/84'/0'/3'/0/1     	bc1qrlvmmxfuryr3mfhssjv45h0fl6s43g3vzrkwca	0.00000000	new
m/84'/0'/3'/0/2     	bc1q40xkajgv9q42ve92zstwjc9v4jgauxme9su6uc	0.00000000	new
m/84'/0'/3'/0/3     	bc1q38pfk8yfnu97v4mckkuk2dhk9u8geuyzu9c0hc	0.00000000	new
m/84'/0'/3'/0/4     	bc1q2qzxyw56em9qdxc5z5s5xjz3j6s2qlzn3juvtu	0.00000000	new
m/84'/0'/3'/0/5     	bc1qd2f8f3dau5pfjqu7dpuvt6fahj36w4rgl3xevr	0.00000000	new
Balance:	0.00000000
internal addresses	m/84'/0'/3'/1
Balance:	0.00000000
Balance for mixdepth 3:	0.00000000
mixdepth	4	xpub6CMAJ67vZWVY7gT4oJQBMc1fhbausT57yNVLCLCMwaGed5spHKaQY1EMQxvL2vTgDfhEimuAy7bzBE1qx5uY6D7cpUjQtXPHpyJzFuUtQPN
external addresses	m/84'/0'/4'/0	xpub6EQWpKsBTG3N9TFU4v6WtCcBJuLAeTZTcUwVJTxYUAsHeVPFdey4qT1dg4G7MqvnFFgHZDxqTo37S81UWUA2BqKKoTff1pcHTcSFzxyp5JG
m/84'/0'/4'/0/0     	bc1qdpjh3ewm367jm5eazqdf8wfrm09py50wn47urs	0.00000000	new
m/84'/0'/4'/0/1     	bc1q2x0fmtms5nr3wz3x3660c8wampg7t22e6m30t8	0.00000000	new
m/84'/0'/4'/0/2     	bc1q23595yg3dkj8gd3jrgup0hyzslhzf9skrg50r5	0.00000000	new
m/84'/0'/4'/0/3     	bc1qw48asjpkwm3k2w8cketqhrre0uwq9f7ypwzmxl	0.00000000	new
m/84'/0'/4'/0/4     	bc1qf3wljw44utyv7qd0z57zvdkfl20y470mva0nes	0.00000000	new
m/84'/0'/4'/0/5     	bc1qz3f80rtv0ux85d7rc06ldtvmpqyfx6ly48c9pa	0.00000000	new
Balance:	0.00000000
internal addresses	m/84'/0'/4'/1
Balance:	0.00000000
Balance for mixdepth 4:	0.00000000
Total balance:	0.00000000
```
            
            

ora possiamo procedere a depositare i nostri primi satoshi all'interno di uno o piú indirizzi ricordando che, indipendendentemente da maker o taker, il software non andrá mai a consolidare utxo in mixdepth diversi direttamente, in questo modo potremo tenere separati sats con diverso livello di privacy all'interno del wallet.  

## Inviare bitcoin con coinjoin singolo

Possiamo ora muovere i nostri satoshi. Uno dei comandi principali di questo software é lo script:  
  
`pyhton sendpayment.py`  
  
che ci permetterá di inviare transazioni ad altri indirizzi con o senza coinjoin. Andiamo ad analizzare il suo funzionamento ed alcuni esempi pratici. Di default la formattazione del comando é:

``` 
python sendpayment.py *opzioni visionabili con --help* *nome del wallet* *ammontare di satoshi* *indirizzo di destinazione*
``` 
un esempio basic di utilizzo potrebbe essere:  
```  
python sendpayment.py wallet.jmdat 5000000 1mprGzBA9rQk82Ly41TsmpQGa8UPpZb2w8c
``` 

in questo caso andremo ad inviare all'indirizzo 1mprGzBA9rQk82Ly41TsmpQGa8UPpZb2w8c 0.05 Btc ovvero 5000000 satoshi dal nostro mixdepth 0 (quello di default) andando a scegliere da 4 a 9 controparti per il coinjoin (opzione di default).

Per avere maggior controllo su come e quali utxo spendere possiamo andare ad analizzare le opzioni aggiuntive a questo comando:  
  
```
python sendpayment.py -N 5 -m 1 wallet.jmdat 100000000 1mprGzBA9rQk82Ly41TsmpQGa8UPpZb2w8c
``` 

in questo esempio abbiamo aggiunto due specifiche: -N indica con quante controparti andremo a mixare, -m il mixdepth da cui andremo a prelevare i fondi. Di fatto abbiamo inviato 100.000.000 sats (1 btc) all'indirizzo 1mprGzBA9rQk82Ly41TsmpQGa8UPpZb2w8c con i fondi presenti nel mixdepth 1 e mixando con 5 controparti.

Se mettessimo come valore di invio 0 specificando un mixdepth, joinmarket effettuerá un cosidetto ´sweep´, ovvero invierá tutti i fondi presenti in quel mixdepth consolidandoli tra di loro:  
  
```
python sendpayment.py -N 7 -m 0 wallet.jmdat 0 1mprGzBA9rQk82Ly41TsmpQGa8UPpZb2w8c
``` 

quì abbiamo inviato tutti i fondi dal mixdepth 0 (potevamo anche non specificalo perché é quello di default) mixando con 7 controparti.

Il comando sendpayment serve per muovere fondi da joinmarket a wallet esterni o per inviare satoshi ad una persona aggiungendo un layer di privacy tra noi e lui. Per guadagnare un sufficiente livello di privacy sui nostri UTXO é piú indicato usare il comando tumbler.py che spiegheremo piú avanti in questa guida.  
  

## Fare da Maker

Lo script che andremo a trattare in questa sezione è:  
  
`yg-privacyenhanced.py`  
  
Questo programma serve per agire come maker nel marcato di joinmarket. Il software si connetterá al nostro nodo bitcoin ed al mercato interno della piattaforma in cui i maker si presentano come offerenti di liquiditá e i taker cercano le controparti.  
In caso vogliate usare un fidelity bond potrete crearne uno con questa formattazione:  
  

``` 
python3 wallet-tool.py *nome del wallet* gettimelockaddress *data del blocco espressa in YYYY-MM*
``` 

  
  
esempio:  
  
```
python3 wallet-tool.py testwallet.jmdat gettimelockaddress 2025-11
``` 
  
l'output che vi verrá restituito sarà un indirizzo bitcoin (ovvero quello su cui dovrete depositare i fondi che volete destinare al fidelity).  
  

 **!!ATTENZIONE!!**

Ci sono due cose a cui fare molta attenzione se avete intenzione di creare un FB:

*   Una volta depositati i fondi, questi non potranno essere piú mossi fino alla scadenza di esso. Prestate attenzione a quanti sats inviate all'indirizzo e a come formattate la data. Non sono ammessi errori!
*   Il fidelity é facilmente riconoscibile onchain, pertanto é consigliabile depositare fondi attraverso un coinjoin e con provenienza non collegata alla vostra identitá. La stessa cosa é consigliabile farla anche una volta che vorrete spostare il bond scaduto fuori da JM.

É importante ricordare che é possibile refillare il fidelity con una sola transazione, in caso di multipli UTXO solo il maggiore verrà considerato valido per il FB.  
  
Trattiamo ora lo script citato all'inizio di questo paragrafo, una volta creato il bond (opzionale) siamo pronti per avviare l'eseguibile per fare da maker su joinmarket.  
Una volta depositati i satoshi ai vari indirizzi e mixdepth potremo dare il comando:  
  
`python yg-privacyenhanced.py *nome del wallet*`  
  
Da questo momento in poi (dopo qualche minuto di collegamento alla rete) e fino a quando non interromperemo lo script, il nostro client JM comparirà sulla lista dei maker attivi sul protocollo e offrirá la nostra liquiditá a varie controparti per effettuare coinjoin. Non aspettatevi decine di coinjoin al giorno (a meno di fidlity enorme e grande liquiditá depositata sul wallet), ricordate anche che fattori come le FEE richieste e i satoshi depositati influiscono sulla frequenza con cui farete da maker.  
Eseguendo il comando sottostante potrete vedere lo storico di tutte le transazioni effettuate sul wallet e l'eventuale guadagno (se fate da maker) o spesa di FEE (se siete taker) che avete avuto in tutto l'arco di vita del portafoglio.  
  
`python wallet-tool.py *nome del wallet* history`  
  
Una volta che i vostri satoshi faranno dei coinjoin, si muoveranno da un mixdepth all'altro fino ad arrivare all'ultimo. Una volta superato il quarto torneranno al mixdepth 0, a voi la scelta di quanta privacy ottenere prima di spostarli su un cold wallet, é consigliabile concludere un ciclo completo del wallet.

## Tumbler
Eccoci finalmente alla parte piú succosa di JoinMarket, il tumbler!  
se avete ascoltato il podcast sapete giá di cosa si tratta. Una raccomandazione prima di iniziare: ATTENTI ALLE FEE! Ricordatevi di settare i limiti nel file joinmarket.cfg (come spiegato all'inizio) e valutate di far girare il programma solo quando le fee onchain sono relativamente basse (sotto i 10 sats/vB).  
Per lanciare il tumbler é necessario aver fermato lo script da maker (se era attivo), dopo potremo far partire il comando:  
  
```
python tumbler.py *nome del wallet* *indirizzo1 su cui ricevere* *indirizzo2 su cui ricevere* *indirizzo3 su cui ricevere*
``` 
  
É fondamentale inserire ALMENO 3 indirizzi di output per il tumbler: questo serve a garantire una buona privacy e a non creare link evidenti tra gli UTXO durante tutto il processo. Come al solito aggiungendo --help al comando é possibile andare a vedere tutti i dettagli aggiuntivi. Andiamo a visionare un esempio piú complesso con regole avanzate:  
  

```
pyhton tumbler.py TestWallet.jmdat -N 7 2 -c 3 1 bc1qz3f80rtv0ux85d7rc06ldtvmpqyfx6ly48c9pa bc1qf3wljw44utyv7qd0z57zvdkfl20y470mva0nes bc1qw48asjpkwm3k2w8cketqhrre0uwq9f7ypwzmxl
```

In questo caso abbiamo lanciato uno script di tumbling che non userà il numero di controparti di default (il parametro -N indica che richiediamo 7 controparti con una varianza massima di 2, quindi un numero di maker random da 5 a 9) e con un numero maggiore di coinjoin per mixdepth (di default questo script effettua un numero random di coinjoin per sezione del wallet che va da 1 a 3, usando il comando -c 3 1 invece sará da 2 A 4).In questo modo spenderemo piú sats in fee ma avremo un anonimity set maggiore.  
  
É possibile anche aggiungere quanti indirizzi di output si vogliono (minimo 3, non c'è un massimo se non il buon senso). Non é invece possibile, per questioni di privacy, decidere come saranno distribuiti i satoshi tra gli indirizzi specificati come output.  
  
Il tumbler é un processo volutamente lungo, occasionalmente potrebbe capitare che qualcosa smetta di funzionare, nella maggior parte dei casi questo si risolverà in autonomia nel giro di poche ore. In caso di crash totale potremo tentare di riavviarlo con il comando:  
  
`python tumbler.py --restart`  
  
oppure basterá far ripartire un nuovo comando di tumbling. Questo non avvierà lo scheduling del tumbler precedente ma inizierá un nuovo ciclo di mixing.  
In caso chiudendo il terminale SSH al vostro nodo si interrompa anche lo script potrete sfruttare il programma 'TMUX' installabile con il comando:  
  
`sudo apt install tmux`  
  
Lanciandolo da shell digitando 'tmux' vi si aprirá un terminale che rimarrá attivo in background anche chiudendo la connessione remota. Quando vi ri-connetterete al vostro nodo con il comando: 'tmux attach' ri-aprirete la shell lasciata aperta.

## Conclusioni
JoinMarket é un software sconfinato e personalizzabile. In questa guida abbiamo scoperto le funzioni principali in modo da rendere possibile per chiunque (o almeno ci ho provato, mi rendo conto che usare questo software non é una passeggiata) l'utilizzo di questo programma. Uno dei maggiori problemi di JM é proprio questo: il numero di persone che lo usano e che fanno da maker. Se pochi utenti sfruttano questo software, la privacy generale (anon-set) si abbassa. Ecco perché spero che questa guida possa incentivare l'uso e vi convinca a scaricare e installare il mio software preferito per fare coinjoin. In caso vogliate approfondire ancora di piú alcuni aspetti vi consiglio di dare una lettura ai vari docs di approfondimento presenti su github, sono veramente ben fatti e li potete reperire [qui](https://github.com/JoinMarket-Org/joinmarket-clientserver/tree/master/docs).  
  
Buon mixing tartarughe!🐢 💚

[![Vai alla pagina](https://btcpay.priorato.org/img/paybutton/pay.svg)](https://btcpay.priorato.org/api/v1/invoices?storeId=2B1STLH5REvhHZBRQuyJNieRTexpeuJ4Usjn4ziEfEfd&currency=EUR)
