<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


:stop_sign: This wiki has now been deprecated. Please visit [ethereum.org](https://ethereum.org/it) for up-to-date information on Ethereum. :stop_sign: 

 



**Contents**

  - [Una Piattaforma di Nuova Generazione per i Contratti Intelligenti e le Applicazioni Decentralizzate](#una-piattaforma-di-nuova-generazione-per-i-contratti-intelligenti-e-le-applicazioni-decentralizzate)
  - [Tavola dei Contenuti](#tavola-dei-contenuti)
- [Introduzione al Bitcoin ed ai Concetti Esistenti](#introduzione-al-bitcoin-ed-ai-concetti-esistenti)
  - [Storia](#storia)
  - [Bitcoin come un Sistema di Transizione di Stato](#bitcoin-come-un-sistema-di-transizione-di-stato)
  - [Mining](#mining)
  - [Merkle Trees](#merkle-trees)
  - [Applicazioni Alternative della Blockchain](#applicazioni-alternative-della-blockchain)
  - [Scripting](#scripting)
- [Ethereum](#ethereum)
  - [Ethereum Accounts](#ethereum-accounts)
  - [Messaggi e Transazioni](#messaggi-e-transazioni)
  - [Messaggi](#messaggi)
  - [La Funzione di Transizione di Stato di Ethereum](#la-funzione-di-transizione-di-stato-di-ethereum)
  - [Esecuzione del Codice](#esecuzione-del-codice)
  - [Blockchain e Mining](#blockchain-e-mining)
- [Applicazioni](#applicazioni)
  - [Sistema dei Tokens](#sistema-dei-tokens)
  - [Derivati Finanziari e Monete dal Valore Stabile](#derivati-finanziari-e-monete-dal-valore-stabile)
  - [Sistemi di Identità e Reputazione](#sistemi-di-identit%C3%A0-e-reputazione)
  - [Storage Decentralizzato di Files](#storage-decentralizzato-di-files)
  - [Organizzazioni Autonome Decentralizzate](#organizzazioni-autonome-decentralizzate)
  - [Ulteriori Applicazioni](#ulteriori-applicazioni)
- [Altre questioni](#altre-questioni)
  - [Implementazione GHOST modificata](#implementazione-ghost-modificata)
  - [Commissioni](#commissioni)
  - [Computazione e completezza di Turing](#computazione-e-completezza-di-turing)
  - [Valuta ed Emissione](#valuta-ed-emissione)
  - [Centralizzazione del Mining](#centralizzazione-del-mining)
  - [Scalabilità](#scalabilit%C3%A0)
- [Conclusioni](#conclusioni)
- [Note e Approfondimenti](#note-e-approfondimenti)
    - [Note](#note)
    - [Approfindimenti](#approfindimenti)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

Ethereum: Libro Bianco - White Paper (di Leonardo Maria Pedretti: lm.pedretti@gmail.com)
[Linkedin](https://www.linkedin.com/in/leonardompedretti)

### Una Piattaforma di Nuova Generazione per i Contratti Intelligenti e le Applicazioni Decentralizzate

Quando Satoshi Nakamoto diede per primo inizio, nel Gennaio 2009, alla blockchain del Bitcoin, stava introducendo due concetti radicali e, fino ad allora, mai testati. Il primo è il "Bitcoin", una moneta online peer-to-peer decentralizzata che mantiene un valore senza nessun supporto, [valore intrinseco](http://bitcoinmagazine.com/8640/an-exploration-of-intrinsic-value-what-it-is-why-bitcoin-doesnt-have-it-and-why-bitcoin-does-have-it/) o emittente centrale. Finora, il "Bitcoin", nella veste di unità monetaria, ha catalizzato la maggior parte dell'attenzione del pubblico, sia in termini di aspetti politici di una moneta senza una banca centrale, sia per l' estrema volatilità, verso l'alto e verso il basso, del prezzo. Comunque c'è anche un'altra, ugualmente importante, parte del grandioso esperimento di Satoshi: il concetto di una blockchain basata sul proof-of-work, che garantisce un pubblico consenso sul sistema delle transazioni. Il Bitcoin, nella veste di applicazione, può essere descritto come un sistema first-to-file: se un'entità ha 50 BTC, e simultaneamente invia gli stessi 50 BTC ad A e a B, solamente la transazione che viene confermata per prima sarà processata. Precedentemente non esisteva alcun modo intrinseco per determinare quale delle due transazioni fosse avvenuta prima, e per decenni ciò ha ostacolato lo sviluppo delle monete digitali decentralizzate. La blockchain di Satoshi era la prima soluzione decentralizzata. Attualmente, l'attenzione sta iniziando rapidamente a spostarsi verso questa secondo risvolto della tecnologia Bitcoin, ed, in particolare, come il concetto di blockchain possa essere utilizzato per qualcosa di più che il denaro.

Tali nuove applicazioni, includono l'utilizzo di risorse digitali sulla blockchain per rappresentare valute personalizzate e strumenti finanziari (["monete colorate"](https://docs.google.com/a/buterin.com/document/d/1AnkP_cVZTCMLIzw4DvsW6M8Q2JC0lIzrTLuoWu2z1BE/edit)), la proprietà di un dispositivo fisico sottostante (["proprietà intelligente"](htups://en.bitcoin.it/wiki/Smart_Property)), assets non fungibili, quali nomi di dominio ("Namecoin") così come le più avanzate applicazioni tipo un exchange decentrallizzato, derivati finanziari, il gioco d'azzardo peer-to-peer ed il sistema di identità e di reputazione sulla blockchain. Un'altra importante area di indagine sono i "contratti intelligenti" - sistemi che trasferiscono automaticamente assets digitali, in accordo con regole pre-impostate. Per esempio, si potrebbe avere un contratto di tesoreria nella forma "A può trasferire a X alcune unità di moneta al giorno, B può trasferire a Y alcune unità di moneta al giorno, A e B insieme non possono trasferire niente, ed A può precludere l' "abilità di trasferire" di B. La logica estensione di ciò sono le [organizzazioni autonome decentralizzate](http://bitcoinmagazine.com/7050/bootstrapping-a-decentralized-autonomous-corporation-part-i/) (DAOs) - contratti intelligenti a lungo termine che gestiscono assets e codificano lo statuto di un'intera organizzazione. Quello che Ethereum intende garantire è una blockchain con una linguaggio di programmazione integrato Turing completo, che può essere usato per creare "contratti" e per codificare le funzioni arbitrarie di transizione, permettendo agli utenti di creare uno dei sistemi sopra descritti, così come molti altri che ancora non abbiamo immaginato, semplicemente scrivendo la logica in poche righe di codice.

### Tavola dei Contenuti

* [Storia](#Storia)
    * [Bitcoin come un Sistema di Transizione di Stato](#bitcoin-come-un-sistema-di-transizione-di-stato)
    * [Mining](#mining)
    * [Merkle Trees](#merkle-trees)
    * [Applicazioni Alternative della Blockchain](#applicazioni-alternative-della-blockchain)
    * [Scripting](#scripting)
* [Ethereum](#ethereum)
    * [Portafogli Ethereum](#portafogli-ethereum)
    * [Messaggi e Transazioni](#messaggi-e-Transazioni)
    * [Ethereum come un Sistema di Transizione di Stato](#ethereum-come-un-sistema-di-transizione-di-stato)
    * [Esecuzione del Codice](#esecuzione-del-codice)
    * [Blockchain e Mining](#blockchain-e-mining)
* [Applicazioni](#applicazioni)
    * [Sistemi di Token](#sistema-dei-tokens)
    * [Derivati Finanziari](#derivati-finanziari)
    * [Sistema di Identità e Reputazione](#sistemi-di-identità-e-reputazione)
    * [Storage Decentralizzato dei File](#storage-decentralizzato-dei-file)
    * [Organizzazioni Decentralizzate Autonome](#organizzazioni-decentralizzate-autonome)
    * [Ulteriori Applicazioni](#ulteriori-applicazioni)
* [Miscellanea e Relazioni](#miscellanea-e-relazioni)
    * [Implementazione GHOST Modificata](#implementazione-ghost-modificata)
    * [Commissioni](#commissioni)
    * [Calcolo e Completezza di Turing](#calcolo-e-completezza-di-turing)
    * [Moneta ed Emissione](#moneta-ed-emissione)
    * [Centralizzazione del Mining](#centralizzazione-del-mining)
    * [Scalabilità](#scalabilità)
* [Conclusioni](#conclusioni)
* [Riferimenti ed Ulteriori Letture](#riferimenti-ed-ulteriori-letture)

## Introduzione al Bitcoin ed ai Concetti Esistenti

### Storia

Da decenni sta circolando l'idea di una moneta digitale decentralizzata, così come quella delle applicazioni alternative come i registri di proprietà. I protocolli anonimi di moneta digitale degli anni '80 e degli anni '90, dipendenti soprattutto su una crittografia primitiva conosciuta come Chaumian blinding, furono introdotti da una moneta con un alto tasso di privacy, tuttavia questi fallirono principalmente per non essere riusciti a guadagnare terreno, a causa della loro dipendenza da un intermediario centralizzato. Nel 1998, Wei Dai's [b-money](http://www.weidai.com/bmoney.txt) divenne il primo progetto ad introdurre l'idea di creare una moneta attraverso la soluzione di puzzle computazionali assieme al consenso decentralizzato, tuttavia il progetto non offriva sufficienti dettagli su come tale consenso decentralizzato potesse essere concretamente attualizzato. Nel 2005, Hal Finney introdusse il concetto del "[proofs of work riutilizzabile](http://www.finney.org/~hal/rpow/)", un sistema che utilizza le idee provenienti dalla b-moneta, insieme ai puzzle computazionali Hashcash di Adam Back, per creare un concetto di criptomoneta, ma, ancora una volta, non si riuscii ad ottenere il suddetto scopo, perché anche quest'ultimo progetto si basava su un calcolo computazionale garantito come back-end.

Poiché la moneta è un'applicazione first-to-file, dove l'ordine delle transazioni è spesso di cruciale importanza, le monete decentralizzate richiedono una soluzione al consenso decentralizzato. L'innovazione fornita da Satoshi è l'idea di riuscire a combinare un protocollo molto semplice basato su dei nodi su cui avvengono le transazioni, che danno vita ad una sempre crescente blockchain, attraverso la creazione di "blocchi" ogni 10 minuti, con il proof of work come meccanismo attraverso cui i nodi guadagnano il diritto di partecipare al sistema. Mentre i nodi con una grande quantità di potenza di calcolo hanno proporzionalmente maggiore influenza, raggiungere più potenza computazionale rispetto l'intero network è più difficile rispetto al simulare milioni di nodi. Nonostante la crudezza e la semplicità del modello blockchain del Bitcoin, esso ha dimostrato di essere sufficientemente valido, e nel corso dei successivi cinque anni sarebbe diventato il fondamento di oltre duecento monete e protocolli di tutto il mondo.

### Bitcoin come un Sistema di Transizione di Stato

![statetransition.png](https://raw.githubusercontent.com/ethereumbuilders/GitBook/master/en/vitalik-diagrams/statetransition.png)

Il libro mastro del Bitcoin può essere pensato, da un punto di vista tecnico, come un sistema di transizione di stato, dove c'è uno "stato" consistente nella proprietà dello status di tutti i Bitcoins esistenti e "la funzione di transizione di stato", che riceve uno stato ed una transizione e trasmette un nuovo stato che ne costituisce il risultato. Nel sistema bancario tradizionale, per esempio, lo stato è il documento costituente il saldo, una transazione è una richiesta di movimentare $X da A a B, e la funzione di transizione di stato sottrae un valore nel conto corrente di A equivalente $X ed incrementa il valore di $X nel conto corrente bancario di B. Se nel conto corrente di A ci sono meno che $X, la funzione di transizione di stato segnala un errore. Quindi, si può formalmente definire:

    APPLY(S,TX) -> S' or ERROR

Nel sistema bancario definito in precedenza:

    APPLY({ Alice: $50, Bob: $50 },"send $20 from Alice to Bob") = { Alice: $30, Bob: $70 }

Ma:
    
    APPLY({ Alice: $50, Bob: $50 },"send $70 from Alice to Bob") = ERROR

Lo "stato" nel Bitcoin è la raccolta di tutte le monete (tecnicamente, "transazioni in uscita non spese" oUTXO) che sono state effettuate ma non ancora spese, con ogni UTXO che ha una denomoninazione ed un proprietario (definito da un indirizzo da 20-byte che è essenzialmente una chiave crittografica pubblica<sup>[1]</sup>). Una transazione contiene uno o più inputs, con ogni input che contiene un riferimento ad un UTXO esistente ed una firma crittografica prodotta da una chiave privata associata all'indirizzo del proprietario, ed uno o più outputs, con ogni outpout contenente un nuovo UTXO che deve essere aggiunto allo stato.

1. Per ogni input in `TX`:
    * Se il riferimento UTXO non è in `S`, si ha un errore.
    * Se la firma provvista non combacia con il proprietario del UTXO, si ha un errore.
2. Se la somma dei valori di tutti gli input UTXO è inferiore alla somma dei valori di tutti gli outpout UTXO, si ha un errore.
3. Si ha `S` con tutti gli input UTXO meno tutti gli outpout UTXO aggiunti.

La prima parte del primo step previene che i mittenti delle transazioni possano spendere monete che non esistono, la seconda del primo step previene ai mittenti delle transazioni di spendere monete di altre persone, ed il secondo step fa rispettare la conservazione del valore. Al fine di utilizzare ciò per il pagamento, il protocollo è il seguente. Supponiamo che Alice voglia inviare 11.7 BTC a Bob. Per primo, Alice controllerà di possedere un set di UTXO, che ammonta ad almeno 11.7 BTC. Realisticamente, Alice non sarà in grado di ottenere esattamente 11.7 BTC; si può dire che il valore più piccolo che può ottenere è 6+4+2=12. Lei poi crea una transazione con quei tre inputs ed i due outputs. Il primo output sarà 11.7 BTC con l'indirizzo che appartiene a Bob, ed il secondo output sarà il rimanente 0.3 BTC "scambiato", essendo Alice stessa il proprietario.

### Mining

![block_picture.jpg](https://raw.githubusercontent.com/ethereumbuilders/GitBook/master/en/vitalik-diagrams/block.png)

Se avessimo accesso ad un servizio centralizzato di fiducia, questo sarebbe banale da implementare; esso potrebbe essere codificato esattamente come descritto. Tuttavia, con i Bitcoin abbiamo provato a costruire un sistema monetario, combinando il sistema di transizione di stato con un sistema di consenso al fine di assicurare che ognuno sia d'accordo sull'ordine delle transazioni. Il processo di consenso decentralizzato del Bitcoin richiede l'esistenza dei nodi nel network, che continuamente tentano di produrre pacchetti di transazioni chiamati "blocchi". Il network è destinato a produrre all'incirca un blocco ogni dieci minuti, con ogni blocco che contiene una marca temporale, un numero, un riferimento a (ad esempio l'hash del) precedente blocco e una lista di tutte le transazioni che sono avvenute dal precedente blocco. Con il passare del tempo, questo crea una persistente, sempre crescente, "blockchain" che si aggiorna costantemente per rappresentare l'ultimo stato del libro mastro del Bitcoin.

L'algoritmo per controllare la validità di un blocco, espresso in questo paradigma, è il seguente:

1. Controllo se il blocco precedente esiste ed è valido.
2. Controllo se la marca temporale del blocco è più grande del blocco precedente<sup>[2]</sup> ed è inferiore di 2 ore nel futuro.
3. Controllo se il proof of work sul blocco è valido.
4. Sia `S[0]` lo stato alla fine del blocco precedente.
5. Si supponga `TX` la lista della transazione del blocco con `n` transazioni. Per tutti `i` in `0...n-1`, sia impostato `S[i+1] = APPLY(S[i],TX[i])` Se da qualsiasi applicazione risulti un errore, esce e ritorna falso.
6. Ritorna vero, e registra `S[n]` come uno stato alla fine del blocco.

In definitiva, ogni transazione del blocco deve fornire una transazione di stato che sia valida. Si noti che ogni stato non è codificato, in nessun modo, nel blocco; esso è puramente una astrazione da ricordare per la validazione del nodo e può solo essere (in modo sicuro) computata, per qualsiasi nodo, iniziando dallo stato di genesi e applicata sequenzialmente ad ogni transazione in ogni nodo. Si noti che è importante l'ordine nel quale ogni miner include le transazioni nel blocco; se ci sono due transazioni A e B nel blocco tale che B impiega una UTXO creata da A, poi il blocco sarà validato se A viene prima di  B ma non viceversa.

La parte interessante dell'algoritmo di validazione del blocco è il concetto di "proof of work": la premessa è che l'hash SHA256 di ogni blocco, costituito come un numero di 256-bit, deve essere inferiore di un target regolato dinamicamente, che è al tempo di questo scritto approssimativamente 2<sup>192</sup>. Lo scopo di ciò  è di rendere computazionalmente "difficile" la creazione di un blocco, prevenendo con ciò agli attacchi sibilla dal ricreare l'intera blockchain a loro favore. Poichè SHA256 è progettato per essere una funzione completamente imprevedibile e pseudo-randomica, l'unico modo di creare un blocco valido è semplicemente un test, con l'incremento ripetuto del numero controllando se il nuovo hash corrisponde. Al target corrente di 2<sup>192</sup>, questo significa un media di 2<sup>64</sup> tentativi; in generale, il target è ricalibrato dal network ogni 2016 blocchi in modo che, in media, un nuovo blocco è prodotto, ogni dieci minuti, da qualche nodo nel network. Nella prospettiva di compensare i miners per questo lavoro computazionale, ogni dieci minuti il miner è autorizzato ad includere una transazione donando a se stesso 25 BTC da nulla. In aggiunta, se qualche transazione ha un valore totale denominale più alto nei suoi inputs che ne suoi outputs, la differenza va al miner come "commissione di transazione". Incidentalmente, questo è pure l'unico meccanismo attraverso cui avviene l'emissione dei BTC; in assoluto lo stato di genesi non contiene alcuna moneta.

Nella prospettiva di una migliore comprensione dello scopo del mining, esaminiamo il caso in cui avvenga un attacco criminoso. Visto che la crittografia implicita nel Bitcoin è nota per essere sicura, l'attaccante colpirà l'unica parte del sistema del Bitcoin che non è protetta direttamente dalla crittografia: l'ordine delle transazioni. La strategia dell'attaccante è semplice:

1. Invio 100 BTC ad un commerciante in cambio di qualche prodotto (preferibilmente un bene digitale consegnabile rapidamente)
2. Attesa per la consegna del prodotto
3. Produzione di un'altra transazione che invia 100 BTC a se stesso
4. Tentativo di convincere il network che la sua transazione a se stesso era quella che è avvenuta per prima.

Una volta avvenuto lo step (1), dopo qualche minuto qualche miner includerà la transazione nel blocco, ad esempio il blocco numero 270000. Dopo circa un'ora, cinque o più blocchi saranno aggiunti alla chain dopo quel blocco, con ognuno di questi blocchi che indirettamente indicano la transazione e quindi la "confermano". A questo punto, il commerciante accetterà il pagamento come finalizzato e consegnerà il prodotto; considerato che stiamo assumendo che questo sia un bene digitale, consegnato in un istante. Adesso, l'attaccante crea un'altra transazione inviando i 100 BTC a se stesso. Se l'attaccante semplicemente la rilascia, questa non sarà processato; i miners proveranno ad eseguire `APPLY(S,TX)` e prendere nota che `TX` consuma un UTXO che non è più nello stato. Invece, in questo modo, l'attaccante crea una "fork" della blockchain, iniziando a minare un'altra versione del blocco 270000 indirizzando il blocco 269999 come una antecedente ma con una nuova transazione che prende il posto di quella vecchia. Poiché i dati del blocco sono differenti, ciò richiede il rifacimento della "proof-of-work". Inoltre, la nuova versione del blocco 270000 dell'attaccante ha un hash differente, così i blocchi originali da 270001 a 270005 non "conducono" a quello; quindi, la chain originale e quella nuova dell'attaccante saranno completamente separate. La regola è che, nel caso di fork, la blockchain più lunga è considerata essere quella vera e così i legittimi minatori lavoreranno sulla chain del 270005, mentre l'attaccante sta lavorando da solo sulla chain del 270000. Affinché l'attaccante crei la blockchain più lunga, egli dovrebbe avere più potenza computazionale che il resto del network per ottenere (da quel momento, "51% attacco").

### Merkle Trees

![SPV in bitcoin](https://raw.githubusercontent.com/ethereum/www/master-postsale/src/extras/gh_wiki/spv_bitcoin.png)

_Sinistra: è sufficiente mostrare solo un esiguo numero di nodi in un Merkle tree per avere la prova della validità di un ramo._

_Destra: qualunque tentativo di modificare qualsiasi parte del Merkle tree porterà ad un'incongruenza da qualche parte a monte della chain._

Un'importante funzione della scalabilità del Bitcoin è che nel blocco è memorizzata una struttura di dati multi-livello. L' "hash" di un blocco è in realtà solo l'hash dell'intestazione del blocco, approssimativamente 200-byte di dati che contengono la marca temporale, un numero, hash del precedente blocco e l'hash principale della struttura dei dati chiamata Merkle tree che contiene tutte le transazioni del blocco. Un Merkle tree è un tipo di struttura binaria, composto da un set di nodi, con un grande numero di nodi dipendenti alla base della struttura, che contengono dati sottostanti, un insieme di nodi intermedi dove ogni nodo è l'hash dei suoi due figli, e alla fine un nodo singolo principale, anch'esso composto dall'hash dei suoi due "figli", che rappresenta l'apice della struttura. La finalità del Merkle tree è quello di consentire che i dati in un blocco siano consegnati in maniera frammentaria: un nodo può scaricare solo l'intestazione di un blocco da una sorgente, la piccola parte della struttura di loro interesse da un'altra sorgente, per assicurarsi che tutti i dati siano correnti. Il motivo per cui questo funziona è che gli hash si propagano verso l'alto: se un utente malevolo tenta di cambiare una transazione falsa verso il punto più basso del Merkle tree, ciò causerà un cambio sul nodo di sopra, e poi un cambio sul nodo sopra quest'ultimo, per cambiare, infine, la struttura principale e pertanto l' hash del blocco, causando che il protocollo registri questo come un blocco completamente differente (quasi certamente con un proof of work invalido).

Il protocollo Merkle tree è, senza dubbio, essenziale per la sostenibilità a lungo termine. Un "nodo completo" nel Bitcoin network, uno che memorizza ed elabora l'interezza di ogni blocco, richiede all'incirca 15 GB di spazio sul disco nel Bitcoin network alla data di Aprile 2014, e sta crescendo di oltre un gigabyte al mese. Allo stato attuale, ciò è sostenibile per un computer desktop e non per i telefoni, e più in là con il tempo potranno partecipare solo le aziende e gli appassionati. Un protocollo conosciuto come "controllo semplificato del pagamento" (CSP) permette ad un'altra classe di nodi di esistere, chiamati "nodi leggeri", che scaricano le intestazioni del blocco, verificando la proof of work sulle intestazioni del blocco, e successivamente scaricano solo i  "rami" associati con le transazioni che sono per loro rilevanti. Questo permette ai nodi leggeri di determinare con una forte garanzia di sicurezza quale sia lo status di una qualsiasi transazione Bicoin, ed il loro corrente bilancio, con soltanto il download di una piccolissima parte dell'intera.

### Applicazioni Alternative della Blockchain

L'idea di prendere spunto dalla tecnologia sottostate alla blockchain e di applicarla anche ad altri concetti ha una storia. Nel 2005, Nick Szabo propose il concetto di "[titoli di proprietà sicuri con l'autorizzazione del proprietario](http://szabo.best.vwh.net/securetitle.html)", un documento che descriveva come "nuovi progressi nella tecnologia di un database replicato" consentiranno ad un sistema basato sulla blockchain di conservare un registro di chi possegga una determinata terra, creando un quadro elaborato che include concetti come quello di autosufficienza economica, usucapione e le tasse sulla terra Georgiana. Tuttavia, sfortunatamente, non era disponibile all'epoca un sistema efficace di database replicato, ed il protocollo non fu mai implementato concretamente. Ciononostante, dal 2009 cominciò rapidamente ad emergere, dopo lo sviluppo del consenso decentralizzato del Bitcoin, un numero di applicazioni alternative.

* **Namecoin** - creato nel 2010, [Namecoin](https://namecoin.org/) conosciuto come un sistema decentralizzato di database per la registrazione di nomi di dominio. Nei protocolli decentralizzati come Tor, Bitcoin e BitMessage, è necessario un modo di identificare gli account in modo che le persone possano interagire tra loro, ma in tutte le soluzioni esistenti l'unico tipo di identificatore disponibile è un hash pseudo casuale come `1LW79wp5ZBqaHW1jL5TCiBCrhQYtHagUWy`. Idealmente, qualcuno potrebbe avere un account con un nome come "george". Tuttavia, il problema è che se una persona può creare un account chiamato "george" poi qualcun altro potrà utilizzare lo stesso processo per registrare "george" per se stesso così come per impersonificare quell'altra persona. L'unica soluzione è il paradigma first-to-file, dove il primo registrante ha successo ed il secondo fallisce - un problema che si adatta perfettamente al protocollo di consenso del Bitcoin. Namecoin è la più vecchia, e di più successo, implementazione di un sistema di registrazione di dominio che utilizza una tale idea.
* **Monete colorate** - lo scopo delle [monete colorate](https://docs.google.com/a/buterin.com/document/d/1AnkP_cVZTCMLIzw4DvsW6M8Q2JC0lIzrTLuoWu2z1BE/edit) è quello di servire come un protocollo per consentire alle persone di creare le proprie valute digitali - o tokens digitali sulla Blockchain del Bitcoin, nel  caso frequente e rilevante di una moneta con una sola unità. Nel protocollo delle monete colorate, una persona "emette" una nuova moneta assegnando pubblicamente un colore ad una UTXO specifica del Bitcoin, e il protocollo definisce ricorsivamente il colore dell'altra UTXO al fine che sia dello stesso colore degli inputs di quella transazione da cui deriva (qualche regola speciale si applica nel caso di inputs di colori di monete misti). Ciò permette agli utenti di conservare portafogli di monete che contengono solo una UTXO di uno specifico colore e di inviare questa in modo del tutto simile ai Bitcoins, attraverso lo studio della blockchain per determinare il colore di un qualsiasi UTXO che gli stessi hanno ricevuto.
* **Metacoins** - l'idea dietro un metacoin è quello di avere un protocollo che vive al vertice del Bitcoin, usando le transazioni Bitcoin per conservare le transazioni metacoin, ma avendo una differente funzione di transazione, `APPLY'`. Poiché il protocollo Metacoin non può prevenire che una transazione metacoin invalida sia visualizzata sulla blockchain del Bitcoin, si aggiunge una regola che se `APPLY'(S,TX)`ritorna come un errore, le impostazioni predefinite del protocollo sono`APPLY'(S,TX) = S`. Ciò fornisce un semplice meccanismo per la creazione di un protocollo arbitrario di criptomoneta con funzioni potenzialmente avanzate, che non possono essere implementate all'interno del Bitcoin stesso, ma con un costo di sviluppo molto basso visto che la complessità del mining e del networking sono già gestiti dal protocollo Bitcoin.

Così, in generale, esistono due approcci per la costruzione di un protocollo di consenso: costruire un network indipendente, e costruire un protocollo sul modello di quello del Bitcoin. Il primo approccio è difficile da implementare, anche se ha avuto un buon successo in applicazioni come Namecoin; ogni implementazione individuale necessità una nuova ed indipendente blockchain, così come la costruzione ed il testing di tutta la transizione di stato ed il codice del network. Per di più, si ipotizza che il set di applicazioni per una tecnologia di consenso decentralizzato seguirà la "power law distribution" dove la maggior parte delle applicazioni sarebbe troppo piccola da garantire la loro propria blockchain, e si noti che esistono grandi classi di applicazioni decentralizzate, in particolare le organizzazioni autonome decentralizzate, che necessitano di interagire tra loro.

D'altro canto, l'approccio basato sul Bitcoin, ha il difetto di non avere la funzione di verificazione semplificata del Bitcoin. SPV funziona per il Bitcoin perché può impiegare la grandezza della Blockchain come un proxy per la validità; ad un certo punto, una volta che le transazioni precedenti ad un'altra saranno sufficientemente validate, si potrà confermare la legittimità a far par dello stato. I meta-protocolli basati sulla Blockchain, d'altro canto, non possono forzare quest'ultima a non includere le transazioni che non sono valide all'interno del contesto del loro stesso protocollo. Da ciò, un'implementazione di un meta-protocollo SPV altamente sicuro necessiterebbe di analizzare tutte le transazioni fino all'inizio della Blockchain del Bitcoin per determinare quali siano le transazioni valide e quali quelle invalide. Allo stato attuale, tutta la "luce" di implementazioni di meta-protocolli basati sul Bitcoin si basano su un server di fiducia per fornire i dati; probabilmente questo è uno dei migliori risultati possibili soprattutto quando uno degli scopi principali di una Criptovaluta è quello di eliminare la necessità di fiducia.

### Scripting

Attualmente il protocollo del Bitcoin, perfino senza nessuna estensione, facilita una debole versione del concetto di  "smart contracts". UTXO in Bitcoin può essere posseduta non solo come chiave pubblica, ma anche da uno script più complesso espresso in un semplice linguaggio di programmazione stack-based. In questo paradigma, una spesa di transazione che UTXO deve fornire un dato che soddisfa lo script. Infatti, il meccanismo basico della proprietà della chiave pubblica è implementato con uno script: lo script impiega una firma a curva ellittica  come input, confrontando questa con la transazione e l'indirizzo che possiede la UTXO, e ritorna 1 se la verificazione è andata a buon fine altrimenti 0 in caso contrario. Altri scripts più complessi esistono per i più svariati casi. Per esempio, si può costruire uno script che richiede firme da due delle tre chiavi private impiegate per validare ("multisig"), un setup utile per conti delle società, che mettono al sicuro i conti correnti e che forniscono ai commercianti funzioni di escrow. Gli scripts possono anche essere usati per pagare premi per la soluzione di problemi computazionali, e si può perfino costruire uno script che affermi qualcosa come "questo Bitcoin UTXO è tuo se sei in grado di dare prova di un SPV che tu mi invii una transazione di Dogecoin di questo valore", consentendo essenzialmente un cambio tra cripto-monete.

Tuttavia, il linguaggio di scripting, così come implementato nel Bitcoin, presenta alcune importanti limitazioni:

* **Manca di completezza del linguaggio di Turing**- vale a dire, mentre esiste un grande sottoinsieme di calcolo che il linguaggio di scripting del Bitcoin supporta, quest'ultimo non supporta quasi tutto. La categoria principale che viene meno è il loop. Questo è reso possibile per evitare cicli infiniti durante la verifica delle transazioni; teoricamente ciò è un ostacolo sormontabile per il programmatori di script, visto che qualsiasi loop può essere simulato semplicemente ripetendo il codice sottostante tante volte con un'istruzione "if", implicando scripts inefficienti dal punto di vista dello storage. Per esempio, l'implementazione di un algoritmo alternativo di firma a curva ellittica necessiterebbe 256 rounds di moltiplicazioni ripetute e tutte incluse individualmente nel codice.
* **Cecità-del-valore** - non c'è un modo per un UTXO di fornire un controllo a setaccio sull'ammontare ritirabile. Per esempio, un buon caso di studio può consistere in un contratto oracolo con un contratto sottostante, dove A e B mettere in valore di $ 1000 di BTC e dopo 30 giorni lo script invia il controvalore di $1000 in BTC ad A ed il resto a B. Ciò necessiterebbe di un oracolo per determinare il valore di 1 BTC in USD, ma anche in questo caso c'è un incremento esponenziale, sia in termini di fiducia che di infrastruttura necessaria, per soluzioni, attualmente disponibili, completamente centralizzate. Tuttavia, poiché UTXO sono tutte-o-nessuna, l'unico modo per raggiungere questo risultato è attraverso l'inefficiente hack di avere molte UTXO di varie denominazioni (es. una UTXO di 2k per ogni k fino a 30) e avendo O scelta dove UTXO spedisce ad A e quindi a B.
* **Mancanza di stato** - UTXO può essere sia speso che non speso; non c'è possiblità per contratti o scripts multi-stage che mantengono qualche altro stato interno oltre questo. Ciò rende difficile creare contratti di opzioni multi-stage, cambi decentralizzati, che offrono protocolli crittografici, a due fasi, dedicati (necessari per premi computazionali sicuri). Questo inoltre significa che UTXO può essere soltanto usata per costruire, contratti unici e un non più complessi contratti "stateful" come le organizzazioni decentralizzate, e creare meta-protocolli difficili da implementare. Lo stato binario, combinato con la cecità-del-valore, significa anche che un'altra importante applicazione, come i limiti al prelievo, risulti impossibile.
* **Cecità-della-Blockchain** - UTXO è cieca alla blockchain come il nonce dell'hash precedente. Questo pregiudica applicazioni nel gioco d'azzardo, e altre molte categorie, privando il linguaggio di scripting di una fonte potenzialmente preziosa di casualità.

Quindi, esistono tre approcci per costruire applicazioni avanzate sull'apice della criptomoneta: costruire una nuova Blockchain, usando scripting sull'apice del Bitcoin, e costruire un meta-protocollo sull'apice del Bitcoin. Costruire una nuova Blockchain permette una illimitata libertà nel costruire un set di funzionalità, comportando del tempo per lo sviluppo e delle criticità relative alla fase iniziale e a quella di messa in sicurezza del sistema. Usare lo scripting è semplice da implementare e standardizzare, ma implica delle limitazioni nelle sue capacità; al contrario i meta-protocolli, ma soffrono di difetti di scalabilità. Con Ethereum, noi intendiamo costruire un framework alternativo, che fornisce benefici ancora maggiori in termini di semplicità di sviluppo e ancora più forti proprietà di leggerezza per i client, permettendo allo stesso tempo alle applicazioni di condividere un ambiente economico e la sicurezza della Blockchain.

## Ethereum

Lo scopo di Ethereum è quello di creare un protocollo alternativo per la costruzione di applicazioni decentralizzate, fornendo un insieme eterogeneo di possibilità che, dal nostro punto di vista, saranno molto utili per una larga classe di applicazioni decentralizzate, in particolar modo nelle situazioni dove sono essenziali: un tempo rapido di sviluppo, la sicurezza per applicazioni utilizzate di rado, e la capacità di far interagire tra loro, in modo molto efficace, applicazioni differenti. Ethereum permette tutto ciò attraverso la costruzione di quello che in sostanza è il definitivo protocollo astratto e fondante: una Blockchain con un linguaggio di programmazione, costruito al suo interno e Turing-complete, che permette ad ognuno di scrivere 
Smart Contracts ed applicazioni decentralizzate dove stabilire le proprie regole arbitrarie per la proprietà, i formati delle transazioni e le funzioni di transizione di stato. Una scarna versione di Namecoin può essere scritta in due linee di codice, e gli altri protocolli, come le criptomonete e i sistemi di reputazione, possono essere costruiti al di sotto delle venti linee. Gli smart contracts, i "boxes" crittografici che contengono valore, possono essere sbloccati solo se si verificano certe condizioni, inoltre possono essere anche costruiti sull'apice di della piattaforma, con degli strumenti molto più efficaci di quelli offerti dallo scripting del Bitcoin, grazie agli strumenti offerti dalla completezza del linguaggio di Turing, consapevolezza del valore, dello stato e della blockchain.

### Ethereum Accounts

In Ethereum, lo stato è costituito da oggetti chiamati "accounts", in cui ogni account ha un indirizzo di 20-byte e le transizioni di stato sono trasferimenti diretti del valore e dell'informazione tra gli accounts. Un account Ethereum account contiene quattro campi:

* Il **nonce**, un contatore utilizzato per assicurarsi che ogni transazione può essere elaborata una sola volta
* Il conto corrente dell'account **bilancio ether**
* Il **contract code** dell'account, se presente
* Lo **storage** dell'account (vuoto da default)

"Ether" è l'interno e principale crypto-carburante di Ethereum, e viene usato per pagare le commissioni di transazione. In generale, esistono due tipi di account: **accounts posseduti dall'esterno**, controllati da chiavi private, e **gli accounts contratto**, controllati dal loro codice di contratto. Un account posseduto dall'esterno non ha codice, e si possono mandare messaggi esterni dall'account posseduto esternamente creando e firmando una transazione; in un account contratto, ogni volta che questo riceve un messaggio, il suo codice si attiva, permettendo a questo di leggere e scrivere verso uno storage interno e spedire altri messaggi o creare contratti a sua volta.

Si noti che i "contratti" in Ethereum non dovrebbero essere visti come qualcosa da "riempire" o "da complilare con"; piuttosto, essi sono più come "agenti autonomi", che vivono all'interno dell'ambiente di esecuzione di Ethereum, eseguendo sempre una porzione specifica di codice che viene "colpita" da un messaggio o da una transazione, e avendo il controllo diretto sul proprio conto di ether e sulla propria chiave/valore di store, al fine di tenere traccia delle variabili persistenti.

### Messaggi e Transazioni

Il termine "transazione" è utilizzato in Ethereum per riferirsi al pacchetto di dati firmati, che contengono un messaggio da inviare da un account posseduto dall'esterno. Le Transazioni contengono:

* Il destinatario del messaggio
* Una firma che identifica il mittente
* L'ammontare di ether da trasferire al destinatario 
* Un campo dati opzionale
* Un valore`STARTGAS`, che rappresenta il massimo numero di steps computazionali che l'esecuzione della transazione può impiegare
* Un valore`GASPRICE`, che rappresenta la commissione che il mittente paga per lo step computazionale

i primi tre sono campi standard previsti in qualsiasi criptovaluta. Il campo dati non ha nessuna funzione da default, ma la virtual machine ha un codice operativo con cui un contratto può accedere ai dati; come caso di esempio, se un contratto sta funzionando come un servizio di registrazione di dominio basato sulla blockchain, allora può desiderare di interpretare i dati che vengono passati ad esso come contenenti due "campi ", il primo campo essendo un dominio da registrare ed il secondo essendo l'indirizzo IP da registrare. Il contratto dovrebbe leggere questi valori dai dati del messaggi e collocarli appropriatamente nello storage.

I campi `STARTGAS` e`GASPRICE` sono cruciali per il modello di servizio anti-denial di Ethereum. Al fine di prevenire loops infiniti, accidentali o ostili, o altro spreco computazionale di codice, ad ogni transazione è richiesto di impostare un limite per l'uso di steps computazionali di codice di esecuzione. L'unità fondamentale di computazione è il "gas"; di solito, uno step computazionale costa 1 gas, ma alcune operazioni richiedono più unità di gas, perché esse sono computazionalmente più complesse, o richiedono un numero più elevato di dati che devono essere conservati come una parte dello stato. C'è anche una commissione di gas per ogni byte nei dati della transazione. L'obiettivo del sistema di commissione è quello di richiedere ad un aggressore di pagare proporzionalmente per ogni risorsa che essi consumano, includendo la computazione, larghezza di banda, e storage; quindi, qualsiasi transazione che comporta che il network consumi una quantità più grande di qualsiasi di queste risorse deve avere una commissione gas grosso modo proporzionale alla grandezza dell'incremento.

### Messaggi

I contratti hanno l'abilità di inviare "messaggi" ad altri contratti. I messaggi sono oggetti virtuali che non vengono mai serializzati ed esistono solo nell'ambiente di esecuzione di Ethereum. Un messaggio contiene:

* Il mittente del messaggio (implicito)
* Il destinatario del messaggio
* L'ammontare di ether da inviare attraverso il messaggio
* Un campo dati opzionale
* Un valore `STARTGAS` 

Essenzialmente, un messaggio è come una transazione, eccetto che esso viene prodotto da un contratto e non da un attore esterno. Un messaggio è prodotto quando un contratto che sta eseguendo il codice fa effettua una operazione `CALL`, che produce ed esegue un messaggio. Come una transazione, un messaggio comporta che l'account del destinatario esegua il proprio codice. Quindi, i contratti possono avere relazioni con altri contratti esattamente alla stesso modo che avviene con degli attori esterni.

Si noti che la quantità di gas, che serve ad una transazione o ad un contratto, si applica alla totalità del gas consumato da quella transazione e da tutte le sub-esecuzioni. Per esempio, se un attore esterno A trasmette una transazione a B con 1000 gas, e B consuma 600 gas prima di inviare il messaggio a C, e l'esecuzione interna di C consuma 300 gas prima di ritornare, poi B può spendere altri 100 gas prima di rimanere a corto di gas.

### La Funzione di Transizione di Stato di Ethereum

![ethertransition.png](http://vitalik.ca/files/ethertransition.png?1)

La funzione di transizione di stato di Ethereum, `APPLY(S,TX) -> S'` può essere definita come segue:

1. Controlla se la transazione è ben impostata (ie. ha il giusto numero di valori), la firma è valida, e il nonce corrispode a quello dell'account del mittente. In caso contrario, si ha un errore.
2. Calcola la commissione di transazione come `STARTGAS * GASPRICE`, e determina l'indirizzo del mittente dalla firma. Sottrae la commissione dal bilancio dell'account del mittente e incrementa il nonce del mittente. Se non c'è un bilancio sufficiente da spendere, si ha un errore.
3. Inizializza `GAS = STARTGAS`, e toglie una certa quantità di gas per byte per pagare i byte nella transazione.
4. Trasferisce il valore della transazione dall'account del mittente all'account del destinatario. Se l'account del destinatario non esiste ancora, lo crea. Se l'account del ricevente è un contratto, esegue il codice del contratto sia per il completamento o fino a quando l'esecuzione finisce il gas.
5. Se il valore di trasferimento fallisce perché il mittente non ha abbastanza soldi, il code di esecuzione finisce il gas, ripristina tutti i cambiamenti di stato, tranne il pagamento delle commissione , e aggiunge le commissioni sul conto del minatore .
6. Altrimenti, risarcisce al mittente le commissioni per il gas rimanente, ed invia le commissioni pagate per il gas e consumate al miner.

Per esempio, si supponga che il codice del contratto è:

    se !self.storage[calldataload(0)]:
        self.storage[calldataload(0)] = calldataload(32)

Si noti che in realtà il codice del contratto è scritto in un codice EVM di basso livello; questo esempio è scritto in Serpent, che, per essere chiari, è uno dei nostri linguaggi di alto livello, può essere compilato fino al codice EVM. Si supponga che lo storage del contratto sia inizialmente vuoto, e la transazione è inviata con un valore di 10 ether, 2000 gas, al prezzo di 0.001 ether gas, e 64 bytes di dati, con bytes 0-31 che rappresentano il numero `2` e i bytes 32-63 che rappresentano la stringa `CHARLIE`. Il processo per la funzione di transizione di stato è in questo caso come segue:

1. Controlla che la transizione è valida è ben impostata.
2. Controlla che il mittente abbia almeno 2000 * 0.001 = 2 ether. If it is, quindi sottrae 2 ether dall'account del mittente.
3. Inizializza gas = 2000; assumendo che la transazione è lunga 170 bytes e la commissione di byte è 5, sottrae 850 così che c'è 1150 gas che rimane.
3. Sottrae altri 10 ether dall'account del mittente, e li aggiunge all'account del contratto.
4. Esegue il codice. In questo caso, questo è semplice: esso controlla che lo storage del contratto all'indice `2` sia usato, prende nota che non lo è, e così imposta lo storage all' index `2` al valore `CHARLIE`. Si supponga che questo impieghi 187 gas, così l'ammontare rimante di gasi sia 1150 - 187 = 963
5. Aggiunge 963 * 0.001 = 0.963 di nuovo sul conto del mittente, e ritorna lo stato risultante.

Se non ci fosse alcun contratto alla fine di ricezione della transazione, quindi il totale della commissione di transazione sarebbe semplicemente uguale al `GASPRICE` provvisto moltiplicato per la lunghezza della transazione in bytes, ed i dati inviati per mezzo della transazione sarebbero irrilevanti.

Si noti che i messaggi lavorano in maniera equivalente alle transazioni in termini di ripristino: se un messaggio in esecuzione finisce il gas, quindi l'esecuzione del messaggio, e tutte le altre esecuzioni innescate da questa esecuzione, tornano indietro, ma le esecuzioni precedenti non hanno bisogno di farlo. Questo significa che è "sicuro" per un contratto di richiamare un altro contratto, se A chiama B con G di gas poi l'esecuzione di A è garantita per perdere al massimo G. Alla fine, si noti che c'è un codice operativo, `CREATE`, che crea un contratto; il proprio meccanismo di esecuzione è generalmente simile a `CALL`, con l'eccezione che questo output di esecuzione determina il codice di un contratto recentemente creato.

### Esecuzione del Codice

Il codice nei contratti Ethereum è scritto in un linguaggio di basso livello, linguaggio bytecode a cascata, denominato "codice virtual machine Ethereum" o"codice EVM". Il codice consiste in una serie di bytes, dove ogni byte rappresenta un'operazione. In generale, l'esecuzione del codice è un loop infinito che consiste nel realizzare ripetutamente l'operazione al contatore del programma attuale (che inizia con zero)  e incrementando il contatore del programma di uno, fino a che si ottiene la fine del codice od un errore o `STOP` o è rilevato l'istruzione `RETURN`. Le operazioni hanno accesso a tre tipi di spazio nel quale registrare i dati:

* Lo **stack**, un last-in-first-out contenitore nel quale i valori possono essere spinti e spuntati
* **Memoria**, un array di byte espandibile all'infinito
* Il lungo-termine del contratto **storage**, una chiave/valore di store. A differenza dello stack e della memoria, che si resettano dopo la fine del calcolo, lo storage persiste per un lungo periodo.

Il codice può anche accedere al valore, mittente e dati del messaggio in arrivo, così come ai dati in testata al blocco, e il codice può anche ritornare come un'array di dati come output.

Il modello di esecuzione formale del codice EVM è sorprendentemente semplice. Mentre la virtual machine di Ethereum funziona, tutto il suo stato computazionale può essere definito dall'insieme di dati `(stato_del_blocco, transazione, messaggio, codice, memoria, stack, pc, gas)`, dove `stato-del_blocco` è lo stato globale che contiene tutti gli accounts e include i bilanci e lo storage. All'inizio di ogni turno di esecuzione, l'istruzione corrente viene trovata prendendo il `pc`th byte del `codice` (o 0 se `pc >= len(codice)`), e ogni istruzione ha la sua propria definizione in termini  di come interagisce con l'insieme di dati. Per esempio, `ADD` espelle due oggetti fuori dallo stack e spinge la loro somma, riduce `gas` di 1 e incrementa `pc` by 1, e `SSTORE` espelle i due oggetti all'apice fuori dallo stack ed inserisce il secondo oggetto nello storage del contratto all'indice specificato dal primo oggetto. Sebbene ci sono molti modi di ottimizzare l'esecuzione della virtual machine di Ethereum attraverso una pronta compilazione, un'implementazione basica di Ethereum can in poche centinaia di righe di codice.

### Blockchain e Mining

![apply_block_diagram.png](http://vitalik.ca/files/apply_block_diagram.png)

La blockchain di Ethereum è in molti modi simile a quella del Bitcoin, seppur con qualche differenza. La differenza princiale tra Ethereum e Bitcoin con riguardo all'architettura della blockchain, è che, contrariamente al Bitcoin, i blocchi di Ethereum contengono una copia sia  dell'elenco delle transazioni sia lo stato più recente. A parte questo, gli altri due valori, il numero di blocco e la difficoltà, vengono memorizzati nel blocco. L'algoritmo di validazione del blocco alla base in Ethereum funziona in questo modo:

1. Controlla se il se il precedente blocco di riferimento esiste ed è valido.
2. Controlla se la marca temporale del blocco è più grande di quella del blocco di riferimento precedente ed inferiore di 15 minuti nel futuro.
3. Controlla che il numero del blocco, difficoltà, l'origine della transazione, la transazione derivata ed il limite del gas ( vari e specifici concetti di basso-livello di Ethereum) sono validi.
4. Controlla se il proof of work sul blocco sia valido.
5. Sia `S[0]` lo stato alla fine del blocco precedente.
6. Sia`TX` la lista delle transazioni del blocco, con `n` transazioni. Per tutti in `0...n-1`, set `S[i+1] = APPLY(S[i],TX[i])`. Se qualsiasi applicazioni dà errore, o se il gas totale è consumato nel blocco fino a che questo punto eccede il `GASLIMIT`, anche questo, dà errore. 
7. Sia `S_FINAL` `S[n]`, ma aggiungendo la ricompensa per il blocco pagata al miner.
8. Controlla che lo stato originario del Merkle tree `S_FINAL` sia uguale allo stato finale originario fornito nell'intestazione del blocco. In tal caso, il blocco è valido; in caso contrario, quest'ultimo non è valido.

L'approccio può sembrare molto inefficiente a prima vista, perché questo necessita di registrare l'intero stato di ogni blocco, ma in realtà l'efficienza dovrebbe essere comparabile a quella del Bitcoin. La ragione sta nel fatto che lo stato è registrato in una struttura ad albero, e dopo ogni blocco una piccola parte dell'albero necessita di essere cambiata. Quindi, in generale, tra due blocchi adiacenti la grande maggioranza dell'albero dovrebbe essere la stessa, e quindi i dati possono essere registrati una sola volta e consultati due volte usando i puntatori (ad es. gli hash degli alberi inferiori). Un tipo speciale di albero conosciuto come "Patricia tree" viene usato per raggiungere questo risultato, includendo una modifica del concetto del Merkle tree, che permette ai nodi di essere inseriti e cancellati, e non solo cambiati, in maniera efficiente. Per di più, poiché tutta l'informazione sullo stato è una parte dell'ultimo blocco, non c'è bisogno di registrare tutta la storia della blockchain - una strategia che, se applicata al Bitcoin, può consentire un risparmio di spazio di 5-20x.

Un quesito comune che viene posto è "dove" il codice del contratto viene eseguito, in termini di hardware fisico. Questa è una risposta semplice: il processo di esecuzione del codice del contratto è una parte della definizione dello funzione di transizione di stato, che è una parte dell'algoritmo di validazione del blocco, così che se una transazione è aggiunta al blocco `B` l'esecuzione del codice generata da questa transazione sarà eseguita da tutti i nodi, nel presente e nel futuro, scaricando e validando il blocco `B`. 

## Applicazioni

In generale, ci sono tre tipi di applicazioni costruite su Ethereum. La prima categoria sono le applicazioni finanziarie, che forniscono agli utenti molteplici e più potenti modi di gestire ed usufruire i contratti attraverso l'uso dei proprio soldi. Questo include le sub-monete, i derivati finanziari, ci contratti di hedging, i libretti di risparmio, i testamenti, e per ultimo perfino qualche genere di contratto collettivo di lavoro. 
La seconda categoria consiste nelle applicazioni quasi finanziarie, dove è coinvolto il denaro, ma c'è anche un lato non monetario importante per quello viene fatto; un esempio perfetto è l'auto-assegnazione di premi per le soluzioni di problemi computazionali. Infine, ci sono applicazioni come il voto online e il governo decentralizzato che non sono assolutamente finanziarie.

### Sistema dei Tokens

Il sistema dei tokens basato sulla blockchain ha molte applicazioni che vanno dalle sub-monete che rappresentano assets come USD o gold di azioni di società, tokens individuali che rappresentano smart property, che assicurano coupons non falsificabili, e perfino sistemi di token  senza nessun legame con un valore convenzionale, utilizzati come sistemi di punti di incentivazione. I sistemi di Token sono sorprendentemente semplici da implementare in Ethereum. Il punto chiave è che tutte queste monete, o sistema di token, sono fondamentalmente un database che funzione con una operazione: sottrae X unità da A e conferisce X unità a B, con la condizione che (i) X aveva almeno X unità prima che la transazione e la (2) tansazione sia approvata da A. Tutto quello che serve per implementare un sistema di tokens consiste nell'implementare questa logica in un contratto .

Il codice basico per implementare un sistema di token attraverso Serpent è come segue:

    def send(to, value):
        if self.storage[msg.sender] >= value:
            self.storage[msg.sender] = self.storage[msg.sender] - value
            self.storage[to] = self.storage[to] + value

Questa è sostanzialmente un'implementazione letterale della funzione di stato del "sistema bancario" descritta in precedenza in questo documento. Poche altre linee di codice devono essere aggiunte per fornire lo step iniziale per la distribuzione delle unità di moneta nel primo luogo ed in altri casi limite, ed idealmente una funzione sarebbe aggiunta per lasciare agli altri contratti di domandare il saldo di un indirizzo. Ma questo è tutto ciò di cui c'è bisogno. Teoricamente, i sistemi di token basati su Ethereum, che fungono da sub-monete, possono potenzialmente includere un'altra importante caratteristica basata sulla mancanza di meta-monete sulla chain del Bitcoin: l'abilità di pagare le commissioni di transazione direttamente in quella moneta. Il modo in cui questo potrebbe essere implementato consiste che quel contratto manterrebbe un saldo di ether con cui risarcire gli ether usati per pagare le commissioni al mittente, e ricaricherebbe questo saldo raccogliendo le unità di moneta interne che esso impiega in commissioni e rivendendo queste in una costante vendita all'asta. Gli utenti avrebbero bisogno di "attivare" i loro accounts con ether, ma una volta che ether è là esso sarebbe riusabile perché il contratto lo risarcirebbe ogni volta.

### Derivati Finanziari e Monete dal Valore Stabile

I derivati finanziari sono la più comune applicazioni di uno "smart contract", e tra i più semplici da implementare nel codice. La sfida più grande nell'implementare i contratti finanziari è che la maggioranza di questi richiede un collegamento ad un indice di prezzo esterno; per esempio, un applicazione molto utile è uno smart contract che assicura dalla volatilità dell'ether (od un altra another criptomoneta) con riferimento ai dollari americani, ma questo richiede al contratto di sapere quale sia il valore tra ETH/USD. Il modo più semplice per farlo è attraverso un contratto "data feed" mantenuto da una parte specifica (eg. NASDAQ) progettato in modo che tale parte ha la possibilità di aggiornare il contratto , se necessario, e fornendo un'interfaccia che permette altri contratti di inviare un messaggio a questo contratto e fornire una risposta che procura il prezzo.

Avendo fatto queste premesse, il contratto di hedging sarebbe come segue:

1. Attende la parte A per l'input di 1000 ether.
2. Attende la parte B per l'input di 1000 ether.
3. Registra il controvalore in USD di 1000 ether, calcolato interrogando in contratto di data feed, nello storage, sostenendo che questo è $x.
4. Dopo 30 giorni, viene permesso ad A o B di "riattivare" il contratto al fine di inviare il controvalore $x di ether (calcolato dalla nuova interrogazione del contratto di data feed al fine dell'ottenimento nel nuovo prezzo) ad A ed il resto a B.

Questo tipo di contratto ha un pontenziale significativo nel commercio in criptomoneta. Uno dei principali problemi riguardo la criptomoneta è la volatilità; tuttavia molti utenti e commercianti potrebbero preferire la sicurezza e la convenienza di trattare gli asset crittografici, senza l'eventualità di prospettare una perdita del 23% del valore dei loro fondi in un unico giorno. Fino ad ora, la soluzione più comune proposta è stata quella degli assets garantiti dall'emittente; l'idea è che un emittente crei una sub-moneta in cui ha diritto di emettere o revocare unità, e fornire un'unità della moneta a chiunque le procuri (offline) un'unità di un asset sottostante (ad es. oro, USD). L'emittente successivamente promette di fornire un'unità dell'asset sottostante a chiunque le reinvii un'unità del crypto-asset. Questo meccanismo permette a qualsiasi asset non crittografico di "elevarsi" ad asset crittografico, fornito dall'emittente fidato.

In pratica, tuttavia, gli emittenti non sono sempre fidati, e in qualche caso l'infrastruttura della banca è troppo debole, o troppo ostile, affinché esista ogni servizio. I derivati finanziari forniscono un'alternativa. Qui, al contrario del caso in cui il singolo emittente che fornisce i fondi per garantire un asset, fa la sua parte un mercato decentralizzato di speculatori, scommettendo che il prezzo dell'asset di riferimento (ad. es. ETH) salirà. A differenza degli emittenti, gli speculatori non hanno opzioni di default dalla loro parte del patto, poiché il contratto trattiene i loro fondi in un escrow. Si noti che con questo approccio non è pienamente decentralizzato, perché una risorsa fidata è ancora necessaria al fine di fornire l'indice del prezzo, anche se probabilmente perfino questo è un miglioramento enorme in termini di riduzione dei requisiti dell'infrastruttura (a differenza dall'essere un emittente, diramare un feed del prezzo non richiede license e può essere classificato come libertà di pensiero) diminuendo il potenziale per frode.

### Sistemi di Identità e Reputazione

La prima criptomoneta alternativa in assoluto, [Namecoin](http://namecoin.org/), ha tentato di utilizzare una blockchain tipo quella del Bitcoin al fine di fornire un sistema di registrazione di nomi di dominio, dove gli utente possono registrare i loro nomi di dominio in un database pubblico insieme ad altri dati. Il più importante caso  d'uso citato è per un sistema [DNS](http://en.wikipedia.org/wiki/Domain_Name_System) , che collega i nomi di dominio come "bitcoin.org" (o, nel caso di Namecoin, "bitcoin.bit") ad un indirizzo IP. Altri casi d'uso includono l'autenticazione nell'email e potenzialmente sistemi di reputazione più avanzati. Qui c'è un contratto basico che fornisce un sistema di registrazione di nome di dominio tipo tipo Namecoin attraverso Ethereum:

    def register(name, value):
        if !self.storage[name]:
            self.storage[name] = value

Il contratto è molto semplice; tutto questo è un database che può essere inserito all'interno del network di Ethereum, ma non modificato o rimosso. Chiunque può registrare un nome di dominio con qualche valore, e questa registrazione rimane per sempre. Un contratto di registrazione di nomi di dominio più sofisticato avrà anche una "clausola di funzione" che permette agli altri contratti di interrogarlo, così come un meccanismo per il "proprietario" (ad es. il primo registrante) di un nome di dominio di modificare i dati o trasferire la proprietà. Un individuo può perfino aggiungere, sull'apice, un sistema di reputazione ed una funzionalità web-della-fiducia.

### Storage Decentralizzato di Files

Nel corso degli ultimi anni, sono emerse un numero di startups popolari che si occupano dello storage online dei files, tra cui la più importante è divenuta Dropbox, che permette agli utenti di fare un backup tramite upload dei loro hard disk, di avere un servizio di storage del backup e quindi accedervi in cambio di un abbonamento mensile. Tuttavia, oggi giorno il mercato dello storage dei files è allo stato relativamente inefficiente; un rapido excursus alle varie [soluzioni esistenti](http://online-storage-service-review.toptenreviews.com/) mostra che, con particolare riferimento alla "strana valle" al livello di 20-200 GB, alla quale né abbonamenti gratuiti né quelli di livello aziendale danno soluzione, i costi sostenuti mensilmente per i servizi più celebri di file storage sono maggiori, con riferimento alla finestra temporale di un singolo mese di abbonamento, rispetto a quelli relativi all'acquisto di un intero hard disk. I contratti in Ethereum permettono lo sviluppo di un ecosistema decentralizzato di file storage, dove i singoli utenti possono guadagnare piccole somme di denaro dall'affitto dei propri hard disks ed in cui lo spazio inutilizzato può essere impiegato per spingere verso il basso i costi di archiviazione dei files. 

Il punto chiave di tale dispositivo sarebbe quello che abbiamo chiamato "il contratto Dropbox decentralizzato". Questo contratto funziona come segue. Per primo, vengono divisi i dati desiderati in blocchi, crittografando ogni blocco per questioni di privacy, costruendo un Merkle tree al di fuori di questo. Quindi viene definito un contratto con la regola che, ogni N blocchi, il contratto possa scegliere un indice randomico nel Merkle tree (usando l'hash del blocco precedente, accessibile dal codice del contratto, come generatore di causualità), e vengono dati X ether alla prima entità per fornire una transazione con un un sistema semplificato di verificazione del pagamento come la "prova di proprietà" del blocco con quel particolare indice nel tree. Quando gli utenti vogliono ri-scaricare i loro files, possono usare un protocollo di micropagamento (ad es. pagando 1 szabo per 32 kilobytes) per recuperare il file; l'approccio più efficiente in termini di commissione è per il pagante quella di non rendere pubblica la transazione fino alla fine, ma di sostituire la transazione con una più lucrativa con lo stesso nonce dopo ogni 32 kilobytes.

Un'importante caratteristica del protocollo è che, sebbene può sembrare che un nodo si stia affidando a diversi nodi randomici per non rischiare di dimenticare il file, uno può ridurre, quasi a zero, questo rischio attraverso la frammentazione del file in molte parti attraverso una condivisione segreta, ed osservare i contratti al fine di controllare se ogni frammento è ancora nel possesso del nodo. Se un contratto sta ancora trasmettendo del denaro, questo fornisce una prova crittografica che qualcuno al di fuori di sta ancora conservando il file. 

### Organizzazioni Autonome Decentralizzate 

Il concetto generale delle "organizzazione autonome decentralizzate" è che un'entità virtuale ha un certo numero di membri o azionisti che, probabilmente con una maggioranza del 67%, abbia il diritto di spendere i fondi dell'entità e modificare il proprio statuto. I membri potrebbero collettivamente decidere su come l'organizzazione dovrebbe allocare i propri fondi. I Metodi per distribuire i fondi di una OAD (DAO) potrebbero spaziare da premi, salari e perfino consistere in meccanismi più particolari come un una moneta interna per premiare un lavoro. Ciò replica essenzialmente i crismi legali di una compagnia tradizionale o di una non profit a differenza che, per l'attuazione, si usa una sola tecnologia blockchain crittografica. Fino ad oggi gran parte del discorso circa le DAO è stato attorno il modello "capitalistico" di una "società autonoma decentralizzata" SAD (DAC) con la suddivisione dei dividendi delle azioni e azioni negoziabili; un'alternativa, probabilmente descritta come una "comunità autonoma decentralizzata", potrebbe conferire a tutti i suoi membri un'azionariato egualitario al fine di decidere di ottenere che il 67% dei membri esistenti accettino e rimuovano un membro. Il requisito che una persona possa essere solo un unico membro potrebbe quindi essere imposta collettivamente dal gruppo.

Un profilo generale per come codificare un DAO è il seguente. Il design più semplice consiste nella parte di un codice che si auto modifica che cambia se due terzi dei membri concordano su un cambiamento. Sebbene il codice è teoricamente immutabile, un soggetto può facilmente aggirare questo ostacolo ed ottenere una mutabilità de facto avendo frammenti di codice in contratti distinti, e avendo l'indirizzo dei contratti per richiamare i dati archiviati nello storage modificabile. In una semplice implementazione di questo come un contratto DAO, ci sarebbero tre tipi di transazioni, distinte dai dati forniti nella transazione:

* `[0,i,K,V]` per registrare una proposta con indice `i` per cambiare l'indirizzo all'indice dello storage `K` al valore `V`
* `[0,i]` per registrare un voto in favore di una proposta `i`
* `[2,i]` per finalizzare la proposta `i` se sono stati fatti sufficienti voti

Il contratto potrebbe avere quindi clausole per ognuna di queste. Esso potrebbe mantenere una registrazione di tutti i cambiamenti aperti dello storage, insieme ad un elenco di chi ha votato per essi. Inoltre esso potrebbe avere una lista di tutti i membri. Quando qualsiasi cambiamento dello storage raggiunge due terzi dei membri che votano per esso, una transazione conclusiva potrebbe eseguire il cambiamento. Una più sofisticata intelaiatura potrebbe anche avere un'opzione di voto costruita al suo interno per caratteristiche come l'invio di una transazione, l'aggiunta o la rimozione dei membri, e potrebbe perfino essere utile per [Liquid Democracy](http://en.wikipedia.org/wiki/Delegative_democracy)-style vote delegation (ad es. ognuno può assegnare a qualcuno di votare per lui, e l'assegnazione è transitiva così se A assegna a B e B assegna a C quindi C determina il voto di A). Questo design potrebbe consentire alla DAO di svilupparsi organicamente come una comunità decentralizzata, che consenta alle persone, in caso, di delegare il compito di filtrare chi sia un membro agli specialisti, sebbene diversamente dal "sistema corrente" gli specialisti possono facilmente immettere e cancellare nel tempo come i membri individuali di una comunità cambiano i loro allineamenti.

Un modello alternativo per una società decentralizzata, dove qualsiasi account può avere zero o più azioni, e dove due terzi delle azioni sono necessarie per prendere una decisione. Un'intelaiatura completa potrebbe coinvolgere la funzionalità della gestione degli asset, l'abilità di fare un'offerta per comprare o vendere le azioni, e l'abilità di accettare offerte (preferibilmente con un meccanismo di matching dell'ordine all'interno del contratto). La delega potrebbe anche esiste come una Democrazia di tipo liquido, estendendo il concetto della "board of directors".

### Ulteriori Applicazioni

**1. Portafogli di risparmio**. Si supponga che Alice vuole tenere al sicuro i suoi fondi, ma è preoccupata circa il fatto che lei li perderà o qualcuno eseguirà un hack della sua chiave privata. Lei attraverso ether stipula un contratto con Bob, una banca, come segues:

* Alice può in maniera autonoma ritirare, ogni giorno, al massimo l'1% dei fondi.
* Bob può in maniera autonoma ritirare, ogni giorno, al massimo l'1% dei fondi, ma Alice ha la possibilità di eseguire una transazione con la sua chiave impedendo questa possibilità.
* Alice e Bob insieme possono ritirare qualsiasi quantità di fondi.

Normalmente, l' 1% è sufficiente per Alice, e se Alice vorrà ritirare di più di quanto lei può, potrà contattare per un aiuto Bob. Se La chiave di Alice viene hackerata, lei chiede soccorso a Bob per movimentare i fondi su un nuovo contratto. Se lei perde la sua chiave, alla fine Bob avrà i fondi al di fuori. Se risulterà che Bob sarà dannoso, Alice potrà quindi disattivare l'abilità di ritirare fondi di Bob.

**2. Assicurazione sul raccolto**. Un soggetto può facilmente creare contratti di derivati finanziari usando un data feed delle condizioni meterologiche al posto dell'indice del prezzo. Se un agricoltore in Iowa acquista un derivato che paga in maniera inversamente proporzionale alla precipitazione in Iowa, il contadino riceverà automaticamente, nel caso in cui segua una siccità, i soldi e se ci sarà pioggia a sufficienza lui sarà soddisfatto perché i suoi raccolti saranno andati bene. Questo ragionamento può essere applicato generalmente anche alle assicurazione sui disastri naturali.

**3. Un data feed decentralizzato**. A differenza dei contratti finanziari, sarebbe possibile attualmente decentralizzare il data feed tramite un protocollo denominato "[SchellingCoin](http://blog.ethereum.org/2014/03/28/schellingcoin-a-minimal-trust-universal-data-feed/)". Sostanzialmente SchellingCoin funziona come segue: tutte le N controparti inseriscono nel sistema il valore di un dato fornito (ad es. il prezzo ETH/USD), i valori vengono scelti, e ognuno tra il 25% e il 75% ottiene un token come premio. Ciascuno ha l'incentivo di fornire una risposta che tutti gli altri forniranno, e l'unico valore su cui un vasto numero di utenti potrà realisticamente concordare è l'ovvio predefinito: la verità. Questo crea un protocollo decentralizzato che può in teoria fornire qualsiasi numero di valori, incluso il prezzo di ETH/USD, la temperatura in Berlino o perfino una calcolo particolarmente difficile.

**4. Un escrow smart multifirma**. Bitcoin permette la multifirma nelle transazione dei contratto dove, per esempio, tre di un totale di cinque chiavi possono spendere i fondi. Ethereum permette più livello di dettaglio; per esempio, quattro di un totale di cinque chiave possono spendere qualsiasi quantità di fondi, tre di cinque possono spendere fino ad un totale del 10% al giorno, e due di cinque possono spendere fino al 0.5% al giorno. In più, la multifirima in Ethereum è asincrona - due soggetti possono registrare, in tempi differenti, le loro firme sulla blockchain e l'ultima firma invierà automaticamente la transazione.

**5. Cloud computing**. La tecnologia EVM può essere inoltre usata per creare una sistema di computing verificabile, permettendo agli utenti di chiedere agli altri di effettuare le computazioni e, nel caso, di chiedere, a certi checkpoints scelti randomicamente, le prove che queste computazioni siano avvenute correttamente. Questo consente la creazione di un mercato di cloud computing dove ogni utente può partecipare con il suo desktop, laptop o server specializzato, e dove controlli spot con depositi cauzionali possono essere usati per assicurare che il sistema sia meritevole di fiducia (ad es. i nodi non possono imbrogliare in maniera profittevole). Tuttavia questo tipo di sistema può non essere utile per tutti i compiti; per es. quelli che richiedono un alto livello di computazione tra processi non possono facilmente essere fatti su un grande cloud di nodi. Ciononostante le altre richieste sono più facili da essere messe in parallelo; progetti come SETI@home, folding@home e algoritmi generici possono essere facilmente implementati all'apice di queste piattaforme.

**6. Gioco peer-to-peer**. Qualsiasi numero di protocolli di gioco peer-to-peer, come quelli di Frank Stajano e Richard Clayton [Cyberdice](http://www.cl.cam.ac.uk/~fms27/papers/2008-StajanoCla-cyberdice.pdf), possono essere implementati sulla blockchain di Ethereum. Il protocollo di gioco più semplice è ad oggi un semplice contratto per la differenza sul prossimo hash di blocco, e dei più avanzati protocolli che possono essere costruiti da lì, creando servizi di gioco, con commissioni vicine allo zero, che non hanno la possibilità di imbrogliare.

**7. Mercati predittivi**. Fornito un oracolo o SchellingCoin, i mercati predittivi sono anch'essi semplici da implementare, ed essi insieme a SchellingCoin possono dimostrare di essere la prima applicazione su larga scala della [futarchy](http://hanson.gmu.edu/futarchy.html) come un protocollo per l'amministrazione delle organizzazioni decentrallizzate.

**8. Mercati decentralizzati sulla blockchain**, che usano il sistema basato sull'identità e sulla reputazione.

## Altre questioni

### Implementazione GHOST modificata

Il protocollo "Greedy Heavist Observed Subtree" (GHOST) è un'innovazione introdotta per la prima volta da Yonatan Sompolinsky e Aviv Zohar nel [Dicembre 2013](http://www.cs.huji.ac.il/~avivz/pubs/13/btc_scalability_full.pdf). La motivazione dietro il  GHOST è che le blockchain con tempi di conferma veloci soffrono, allo stato attuale, di una sicurezza ridotta dovuta ad un elevato tasso di latenza- perchè i blocchi impiegano determinati tempi per propagarsi attraverso il network, se il miner A elabora un blocco e successivamente il miner B elabora un altro blocco prima che il blocco del miner A sia propagato a B, il blocco del miner B andrà sprecato e non contribuirà alla sicurezza della rete. Inoltre, esiste un problema di centralizzazione: se il miner A è una pool di mining con una potenza di hash del 30% ed il miner B ne ha una del 10%, A avrà un rischio di produrre un blocco latente pari al 70% delle volte (visto che, nell'altro 30% dei casi,  A ha prodotto l'ultimo blocco e quindi otterrà i dati di mining immediatamente) mentre B correrà il rischio di produrre un blocco latente il 90% dei casi. Quindi l'intervallo del blocco è abbastanza breve affinchè il grado di latenza sia alto e A sarà sostanzialmente più efficiente semplicemente in virtù delle sue dimensioni. Con il combinato di questi due effetti, le blockchains che producono blocchi velocemente corrono fortemente il rischio di convogliare verso una mining pool, che ha una percentuale di potenza di hash sul network abbastanza elevata, arrivando in tal modo al controllo del processo di mining.

Come descritto da Sompolinsky e Zohar, GHOST risolve il primo problema della perdita di sicurezza della rete attraverso l'inclusione dei blocchi latenti nel computo di quale "chain" sia la "più lunga"; vale a dire, non solo il blocco precedente, o quelli ancora più vecchi, rispetto ad un blocco, ma anche quelli latenti e discendenti da un blocco più vecchio (nel gergo Ethereum "zii") sono aggiunti nel computo di quale blocco ha il più grande proof of work che lo sostiene. Per risolvere la seconda questione della faziosità della centralizzazione, noi andiamo al di là del protocollo descritto da Sompolinsky e Zohar, e forniamo i premi del blocco ai blocchi latenti: un blocco latente riceve lo 87.5% del proprio premio base, e il "nipote" che include il blocco latente riceve il restante 12.5%. Tuttavia, le commissioni di transazione, non vengono assegnate agli "zii".

Ethereum implementa una versione semplificata del GHOST che va in profondità nel limite di soli sette livelli. In particolare, esso è definito come segue:

* Il blocco A deve specificare un genitore, e specificare 0 o più zii
* Uno zio, incluso nel blocco B, deve avere le seguenti proprietà:
  * Deve essere un figlio diretto della k generazione antenata di B, dove 2 <= k <= 7.
  * Esso non può essere un antenato di B
  * Uno zio deve essere un valido header del blocco, ma non necessita di essere verificato in precedenza o perfino un blocco valido
  * Uno zio deve essere diverso da tutti gli zii inclusi nei blocchi precedenti e da tutti gli altri zii inclusi nello stesso blocco (inclusione non doppia)
* Per ogni zio U nel blocco B, il miner di B riceve un addizionale 3.125% aggiunto al premio della propria coinbase e il miner di U riceve il 93.75% come premio standard della coinbase.

Questa versione limitata di GHOST, con gli "zii" che possono essere inclusi fino a 7 generazioni, è stata impiegata per due ragioni. La prima, un GHOST illimitato potrebbe includere troppe complicazioni nel computo di quali "zii", per un certo blocco, siano validi. Il secondo, un GHOST illimitato, con il compromesso raggiunto in Ethereum, elimina l'incentivo per un miner di effettuare operazioni di mining su una "chain" di un attaccante, ma, al contrario, di effettuarle sulla "chain" principale. 

### Commissioni

Poiché ogni transazione pubblicata nella blockchain impone al network il costo del download e la verifica della stessa, c'è il bisogno, al fine di prevenire un abuso, di qualche meccanismo di regolazione, che solitamente coinvolge le commissioni di transazione. L'approccio standard, usato in Bitcoin, consiste in quello di avere commissioni prettamente volontarie, contando sul fatto che i miners agiscono come custodi ed impostano minimi dinamici. Questo approccio è stato recepito in maniera molto favorevole nella community Bitcoin poichè, in particolare, è "basato sul mercato", permettendo, tra i miners, domanda e offerta e che i mittenti della transazione possano determinare il prezzo. Il problema con questa impostazione di ragionamento è, tuttavia, che il processo di transazione non è un mercato; anche se è intuitivamente interessante interpretare l'elaborazione delle transazioni come un servizio che il miner sta offrendo al mittente, in realtà ogni transazione che un miner include necessiterà di essere processata da ogni nodo del network, così che la maggior parte del costo del processo di una transazione è a carico di terzi e non del miner che sta prendendo una decisione se includere o meno questa. Quindi, è molto probabile che si verifichi la Tragedia-dei-beni-comuni.

Tuttavia, come si scopre questo difetto nel meccanismo di mercato, quando viene fornita, per semplificazione, una premessa particolarmente inaccurata, magicamente si elimina da sola. L'argomento è il seguente. Supponiamo che:

1. Una transazione comporta `k` operazioni, offrendo un premio `kR` a qualsiasi miner che la includa dove `R` è impostato dal mittente e `k` e `R` sono (approssimativamente) visibili in anticipo dal minatore.
2. Un'operazione ha un costo di processo di `C` verso qualsiasi nodo (ad es. tutti i nodi hanno la stessa efficienza)
3. Ci sono `N` nodi di mining, ognuno dei quali con una potenza di processamento uguale (ad es. `1/N` del totale)
4. Non esistono nodi pieni che non eseguono operazioni di mining.

Un miner potrebbe desiderare di processare una transazione nella prospettiva che il possibile premio sia superiore al costo. Quindi, la ricompensa prevista è `kR/N` visto che il miner ha `1/N` chance di processare il blocco successivo, ed il costo di processamento per il miner è semplicemente `kC`. Quindi, i miners includeranno le transazioni dove `kR/N > kC`, e il costo di processamento o `R > NC`. Si noti che `R` è la commissione dovuta dal mittente ad ogni operazione, ed è perciò inferiore della soglia minina di vantaggio che il mittente ha dall'operazione, e `NC` è tutto il costo dell'intero network per il processamento di un operazione. Quindi, i miners hanno l'incentivo di includere solo quelle transazioni per cui il vantaggio complessivo è maggiore del costo.

Tuttavia, in realtà, ci sono importanti deroghe da questi presupposti:

1. Il miner paga un costo più alto per processare la transazione rispetto ad un altro che verifica i nodi, visto che il tempo di verifica in più ritarda la propagazione del blocco e quindi aumenta la chance che il blocco diventi latente.
2. Esistono nodi pieni che non processano operazioni di mining.
3. La distribuzione del potere di mining potrebbe generare in concreto una ineguaglianza.
4. Gli speculatori, i nemici politici ed i soggetti insensati la cui funzione di utilità incorpora causando un danneggiamento al network dove essi esistono, e possono abilmente creare contratti il ​​cui costo è molto inferiore al costo pagato dagli altri nodi di verifica.

(1) sia fornita una predisposizione per il miner ad includere meno transazioni, e (2) si incrementi `NC`; quindi, questi due effetti si elidono, almeno parzialmente, a vicenda. (3) e (4) sono i maggiori problemi; per risolverli istituiamo semplicemente un tetto limite: nessun blocco può avere più operazioni che `BLK_LIMIT_FACTOR` rispetto la media esponenziale a lungo termine. Nello specifico:

    blk.oplimit = floor((blk.parent.oplimit * (EMAFACTOR - 1) + floor(parent.opcount * BLK_LIMIT_FACTOR)) / EMA_FACTOR)

`BLK_LIMIT_FACTOR` e `EMA_FACTOR` sono costanti che saranno impostate a 65536 e 1.5 per il momento, ma probabilmente saranno oggetto di cambiamenti dopo un'ulteriore analisi.

C'è un altro fattore che si pone come disincentivo alla grandezza dei grandi blocchi in Bitcoin: i blocchi che sono grandi impiegheranno più tempo a propagarsi, e quindi avranno una maggiore probabilità di diventare latenti. In Ethereum, i blocchi che consumano una larga quantità di gas possono anche impiegare più tempo a propagarsi sia perchè essi sono fisicamente più grandi e sia perchè impiegano più tempo affinché la transizione della transazione di stato sia validata. Il disincentivo del ritardo è un'importante considerazione in Bitcoin, ma di meno in Ethereum a causa del protocollo GHOST; perciò, si produce uno standard più stabile bansandosi su limiti di blocco regolati.

### Computazione e completezza di Turing

Un'importante osservazione è che Ethereum virtual machine è Turing-complete; questo significa che il codice EVM può codificare qualsiasi computazione, compresi loops infiniti, che possa essere teoricamente adempiuta. Il codice EVM permette il loop in due modi. Per primo, c'è un'istruzione `JUMP` che consente al programma di tornare indietro a un punto precedente nel codice, ed un'istruzione `JUMPI` per eseguire, a certe condizioni, dei salti, permettendo asserzioni come `while x < 27: x = x * 2`. In seconda istanza, i contratti possono, permettendo potenzialmente loops tramite ricorsione, chiamare altri contratti. Naturalmente da ciò può derivare un problema: possono, nella pratica, utenti malevoli far spegnere i miners e i nodi completi, fornzandoli ad entrare in un loop infinito? La problematica nasce a causa di un problema noto nella computer science come quello della terminazione: in generale non c'è modo di chiedere se un programma terminerà mai.

La nostra soluzione, come è stato illustrato nella sezione della transizione di stato, funziona attraverso la richiesta ad una transazione di impostare un numero massimo di fasi di computazione impiegabili, e se un'esecuzione impiega una computazione più lunga, essa viene fatta tornare indietro, mentre le commissioni dovranno essere lo stesso pagate. I messaggi funzionano allo stesso modo. Per mostrare la motivazione che sta dietro la nostra soluzione, si considerino i seguenti esempi:
* Un attaccante crea un contratto che esegue un loop infinito, e quindi invia una transazione che attiva questo loop presso il miner. Quest'ultimo processerà la transazione, eseguendo il loop infinito, aspettando che questo esaurisca il gas. Perfino se l'esecuzione termina il gas e si ferma a metà, la transazione sarà ancora valida ed il miner potrà ancora richiedere dall'attaccante la commissione per ogni fase computazionale.
* Un attaccante crea un loop infinito molto lungo al fine di forzare il miner di eseguire una computazione per il tempo sufficientemente lungo affichè la computazione, nel termine dell'uscita di pochi blocchi, termini e non sarà possibile per il miner includere la transazione per richiedere la commissione. Tuttavia, l'attaccante potrà domandare di sottoscrivere un valore per `STARTGAS`, limitando il numero di steps computazionali che l'esecuzione può richiedere, cosi che il miner saprà in anticipo se la computazione impiegherà un numero eccessivamente grande di fasi.
* Un attaccante esamina un contratto con un codice di qualche forma come `send(A,contract.storage[A]); contract.storage[A] = 0`, ed invia una transazione con solo gas a sufficienza per far funzionare il primo step, ma non il secondo(ad es. facendo un ritiro ma non facendo diminuire il saldo). L'autore del contratto non necessita di preoccuparsi riguardo la protezione contro questi tipi di attacchi, poichè se l'esecuzione termina a metà strada, questa viene ripristinata attraverso delle modifiche.
* Un contratto finanziario funziona prendendo la media di nove data feed al fine di minimizzare il rischio. Un attaccante sfrutta uno dei data feed, che è pensato per essere modificabile attraverso il meccanismo chiamata-indirizzo-variabile descritto nella sezione dei DAO, e lo converte per eseguire un loop infinito, cercando di forzare con ciò ogni tentativo di richiedere i fondi dal contratto finanziario per far terminare il gas. Comunque, il contratto finanziario può impostare un limite di gas sul messaggio per prevenire questo problema.
L'alternativa alla completezza di Turing è l'incompletezza di Turing, dove `JUMP` e `JUMPI` non esistono e solo dove ad una sola copia di ogni contratto è permesso di esistere nella chiamata nel mucchio in un dato tempo. Con questo sistema, il sistema di commissione descritto e le incertezze attorno l'efficacia della nostra soluzione potrebbero non essere necessarie, come il costo di esecuzione di un contratto potrebbe essere delimitato dalle sue dimensioni, l'incompletezza di Turing non è ancora un grosso limite; di tutti gli esempi di contratto che abbiamo ideato all'interno, finora solo uno richiede un loop, e perfino questo potrebbe essere rimosso eseguendo 26 ripetizioni su una parte di codice di una linea. Fornite le importanti implicazioni della completezza di Turing, e il limitato beneficio, perchè non avere semplicemente un linguaggio di Turing incompleto? In realtà, comunque, la non completezza di Turing è lontana da una soluzione nitida del problema. Per capire il motivo, si considertino i seguenti contratti:

    C0: call(C1); call(C1);
    C1: call(C2); call(C2);
    C2: call(C3); call(C3);
    ...
    C49: call(C50); call(C50);
    C50: (esegue uno step di un programma e registra il cambiamento nello storage)

Adesso, si invii una transazione ad A. Quindi, in 51 transazioni, noi abbiamo un contratto che impiega 2<sup>50</sup> steps computazionali. I Miners potrebbero tentare di scoprire, prima del tempo, tali bombe logiche,  mantenendo un valore accanto ad ogni contratto, specificando il numero massimo di steps computazionali che esso può impiegare, e calcolando questo per i contratti che chiamano altri contatti in maniera ricorsiva, ma questo potrebbe richiedere ai miners di proibire i contratti che creano altri contratti (visto che la creazione e l'esecuzione di tutti i 26 contratti di cui sopra potrebbe essere facilmente convogliata in un contratto singolo). Un altro punto problematico è che il campo dell'indirizzo di un messaggio è una variabile, così in generale potrebbe non essere perfino possibile dire quali altri contratti, un certo contratto, avrà chiamato anzitempo. Quindi, complessivamente, noi giungiamo ad una sorprendente conclusione: la completezza di Turing è sorprendentemente facile da gestire, e l'assenza di questa è allo stesso modo difficile da amministrare a meno che siano assegnati gli stessi identici controlli - ma in questo caso perché non permettere al protocollo di essere Turing-complete?

### Valuta ed Emissione

Il network di Ethereum include una valuta costruita al suo interno, ether, che ha il duplice scopo di fornire uno strato di primario di liquidità per permettere un exchange efficiente tra due tipi di assets digitali e, principalmente, di fornire un meccanismo per pagare le commissioni di transazione. Per comodità e per evitare possibili futuri frantendimenti (si veda il presente dibattito mBTC/uBTC/satoshi in Bitcoin), le denominazioni vengono assegnate prima:

* 1: wei
* 10<sup>12</sup>: szabo
* 10<sup>15</sup>: finney
* 10<sup>18</sup>: ether

Ciò dovrebbe essere considerato come un'analogia con il concetto di "dollari" e "centesimi" o "BTC" e "satoshi". Nel futuro prossimo, ci aspettiamo che "ether" sia impiegato per le transazioni ordinarie, "finney" per le microtransazioni e "szabo" e "wei" per discussioni tecniche riguardo l'implementazione del protocollo; le rimanenti denominazioni potrebbe diventare utili più avanti e non dovrebbero essere, al momento, incluse nei clients.

Il modello di emissione sarà come segue:

* Ether sarà rilasciato in una vendita di moneta al prezzo di 1000-2000 ether per BTC, un meccanismo che intende finanziare l'organizzazione Ethereum  e pagare per lo sviluppo come è successo in altre piattaforme come Mastercoin e NXT. I primi compratori beneficeranno di grandi sconti. I BTC raccolti dalla vendita saranno interamente usati per pagari i salari per i premi agli  sviluppatori e investiti per vari progetti profit e non profit in Ethereum e nell'ecosistema delle criptomonete.
* 0.099x del totale dell'ammontare venduto (60102216 ETH) sarà allocato all'organizzazione per compensare i primi contributori e pagare le spese denominate in ETH prima del blocco di genesi.
* 0.099x del totale dell'ammontare venduto sarà conservato come una riserva a lungo termine.
* 0.26x del totale dell'ammontare venduto sarà conferito ai miners ogni anno dopo questo momento.

| Group  | Al lancio | Dopo 1 anno | Dopo 5 anni
| ------------- | ------------- |-------------| ----------- |
| Unità di moneta  | 1.198X | 1.458X  |  2.498X |
| Compratori  | 83.5% | 68.6%  | 40.0% |
| Riserva spesa prima della vendita | 8.26% | 6.79% | 3.96% |
| Riserva usata dopo la vendita | 8.26% | 6.79% | 3.96% |
| Miners | 0% | 17.8% | 52.0% |

**Tasso di Crescita a Lungo-Termine (in percentuale)**

![SPV in bitcoin](https://blog.ethereum.org/wp-content/uploads/2013/12/issuance-model.jpg)

_Tuttavia, nonostante l'emissione di valuta lineare, il tasso di crescita dell'offerta, proprio come avviene nel Bitcoin, tende, con il passare del tempo, a zero_

Le due principali scelte nel suddetto modello sono (1) l'esistenza e i limiti dell'emissione monetaria, e (2) l'esistenza di un'offerta che cresce costantemente in maniera lineare, al contrario di una fornitura limitata come in Bitcoin. La giustificazione della limitatezza dell'emissione monetaria è la seguente. Se quest'ultima non esistesse, e l'emissione lineare si riducesse a 0.217x per fornire lo stesso tasso di inflazione, quindi la quantità totale di ether potrebbe essere 16.5% di meno e così ogni unità il 19.8% più costosa. Quindi, con l'equilibrio del 19.8% sarebbero acquistati più ether nella vendita, così ogni unità avrebbe di nuovo lo stesso valore di prima. L'organizzazione potrebbe poi avere anche 1.198x di BTC, che potrebbe considerare di dividere in due parti: i BTC originali, e l'addizionale 0.198x. Perciò, questa situazione è esattamente equivalente all'emissione monetaria limitata, ma con un'importante differenza: l'organizzazione conserva soltanto i BTC, e non è incentivata a sostenere il valore di ogni singola unità ether.

La modello di crescita, che si sviluppa in modo lineare, riduce il rischio di quello che qualcuno vede come un eccessiva concentrazione di ricchezza in Bitcoin, e garantisce agli individui di oggi e di domani una giusta chance di acquistare unità di valuta, mentre allo stesso tempo fornisce un grande incentivo ad ottenere e conservare ether a causa della tasso di crescita della domanda come una percentuale che tende, nel tempo, comunque a zero. Noi anche teoirizziamo ciò perché le monete vengono sempre perse, nel corso del tempo, a causa di incuria, morte, etc, e i soldi persi possono essere immaginati come una percentuale della fornitura totale per un anno, di quella totale quantità di moneta in circolazione, che infine sarà, nei fatti, stabilizzata al valore uguale all'emissione annua diviso il tasso di perdita (ad es. al tasso di perdita dell' 1%, una volta che la fornitura raggiunge il 26X poi 0.26X sarà minata e il 0.26X persa ogni anno, creando un equilibrio).

Si osservi che nel futuro, è probabile che Ethereum convergerà sul modello del proof-of-stake per la sicurezza, riducendo i requisiti di emissione verso qualcosa tra lo zero e il 0.05X per anno. Lasciamo aperto un "contratto sociale", nel caso in cui l'organizzazione di Ethereum perda i fondi o  per qualsiasi altra ragione questi spariscano: chiunque ha il diritto di creare una possibile versione futura di Ethereum, con l'unica sola condizione che la quantità di ether debba essere al massimo pari a `60102216 * (1.198 + 0.26 * n)` dove `n` è il numero di anni dopo dopo il blocco di genesi. I creatori sono liberi, per pagare lo sviluppo, di vendere ad una moltitudine o altrimenti assegnare, qualche parte o tutta la differenza tra la maggior fornitura derivante dal PoS e quella massima possibile. Gli aggiornamenti presentati, che non sono conformi con il contratto sociale, potrebbero giustificamente essere deviati in versioni compatibili.

### Centralizzazione del Mining

L'algoritmo di minining del Bitcoin funziona attraverso l'elaborazione da parte dei miner, che si ripete milioni di volte, dello SHA256 su versioni leggermente modificate del'intestazione del blocco, fino a che emerge un nodo la cui versione ha un hash inferiore a quello del bersaglio (attualmente circa 2<sup>192</sup>). Comunque, questo algoritmo di mining è vulnerabile a due forme di centralizzazione. La prima: l'ecosistema di mining ha finito per essere dominato da ASIC (application-specific integrated circuits), chips per computer disegnati per questo scopo, e quindi migliaia di volte più efficienti per il compito specifico del mining del Bitcoin. Questo significa che il mining del Bitcoin non ha più un alto livello di decentralizzazione ed un fine egualitario, poiché richiede milioni di dollari di capitale per parteciparvi concretamente. In seconda istanza: attualmente la maggior parte dei miners di Bitcoin non eseguono la validazione del blocco in locale; invece, essi fanno conto su una mining pool centralizzata che fornisce le intestazioni di blocco. Questo problema è forse il peggiore: al tempo di questo scritto, le principali tre mining pools controllano indirettamente circa il 50% della potenza di calcolo nel network del Bitcoin, sebbene questo sia mitigato dal fatto che i miners possono migrare verso altre mining pools se una, o un gruppo, di queste tentano un attacco al 51%.

Lo scopo attuale di Ethereum è quello di impiegare un algoritmo di mining dove i miners sono tenuti a recuperare dati randomici dallo stato, elaborare qualche transazione selezionata a caso dagli ultimi N blocchi nella blockchain, e fornire come risultato un hash. Questo ha due importanti benefici. Il primo, i contratti Ethereum, possono includere qualsiasi tipo di computazione cosi che un ASIC in Ethereum potrebbe essenzialmente essere uno valido per una computazione generica - ad es. una migliore CPU. Secondariamente, il mining richiede accesso all'intera blockchain, forzando i miners a conservare l'intera blockchain e ad almeno essere in grado di verificare ogni transazione. Questo elimina la necessità della centralizzazione delle mining pools; sebbene le mining pools possono sempre essere utili per il legittimo ruolo per livellare la casualità della distribuzione del premio; comunque questa funzione può essere svolta altrettanto bene dalle pools peer-to-peer pools con nessun controllo centrale.

Questo modello non è testato, e ci potrebbero essere delle difficoltà lungo il cammino nell'evitare certe ingegnose ottimizzazioni quando si usa un'esecuzione del contratto come algoritmo di mining. Comunque, una funzione particolarmente interessante di questo algoritmo è che permette a chiunque di "screditare", attraverso l'introduzione di un vasto numero di contratti progettati per ostacolare certi ASIC, nella blockchain. Gli incentivi economici sussistono per i produttori di ASIC al fine di impiegare questo tipo trick per attaccarsi tra di loro. Perciò, la soluzione che stiamo sviluppando è in definitiva una economia che si adatta all'essere umano piuttosto che una puramente tecnica.

### Scalabilità

Una problematica comune su Ethereum è quella della scalabilità. Come Bitcoin, Ethereum soffre del difetto che ogni transazione necessiti di essere processata da ogni nodo della rete. Con Bitcoin, la grandezza dell'attuale blockchain è all'incirca di 15 GB, crescendo di un 1 MB all'ora. Se il network Bitcoin dovesse processare le 2000 transazioni al secondo di quello di Visa, esso crescerebbe di un 1 MB ogni tre secondi (1 GB per ora, 8 TB all'anno). Ethereum rischia di soffrire di un simile modello di crescita, e, per di più, con l'aggravio che ci saranno molte applicazioni che funzioneranno, invece che solo una moneta come nel caso di Bitcoin, sull'apice della blockchain di Ethereum. Tuttavia, in Ethereum vi è la miglioria derivante dal fatto che i pieni nodi di questo necessitano di conservare, piuttosto che l'intera cronistoria della blockchain, solamente lo stato.

Il problema sottostante ad una blockchain così grande è il rischio di centralizzazione. Se la grandezza di questa aumenta di, ad es., 100 TB, lo scenario che si prospetterebbe sarebbe quello che solo un limitato numero di business di grandi dimensioni potrebbero elaborare nodi pieni, con tutti gli utenti normali che usano i nodi SPV. In questo tipo di situazione, crescerebbe la potenziale preoccupazione che i nodi pieni potrebbero lavorare nella stessa direzione e concordare tutti per imbrogliare al fine di avere una serie di vantaggi ( ad es. cambiare il premio del blocco, e dare a loro stessi BTC). I nodi leggeri non avrebbero nessun modo di accorgersi, nell'immediato, di ciò. Naturalmente ci sarebbe, nel caso, almeno un nodo pieno che continuerebbe a fare legittimamente il suo lavoro e solamente dopo poche ore sarebbe scoperta la frode attraverso canali come Reddit, ma a quel punto potrebbe essere troppo tardi: spetterebbe agli utenti ordinari di organizzarsi per creare una lista nero dei blocchi forniti, uno sforzo di coordinazione enorme e probabilmente irrealizzabile sima massive and likely infeasible coordination problem sulla stessa scala di quella di ottenere un attacco al 51% di successo. Nel caso di Bitcoin, questo è attualmente un problema, ma esiste una modifica alla blockchain [suggested by Peter Todd](http://sourceforge.net/p/bitcoin/mailman/message/31709140/) che mitigherà questo problema.

Nel breve termine, Ethereum impiegherà due strategie addizionali per far fronte a questa questione. La prima consiste nel fatto che, gli algoritmi di minining basati sulla blockchain forzeranno ogni miner a creare almeno un nodo pieno, creando un limite inferiore al numero di nodi pieni. Tuttavia, in seconda istanza ed in maniera più importante, noi includeremo una tree root intermedia nello stato della blockchain dopo il processamento di ogni transazione. Perfino se la validazione del blocco è centralizzata, finché esiste un nodo di verifica onesto, il problema della centralizzazione può essere eluso tramite un protocollo di verificazione. Se un miner pubblica un blocco invalido, quel blocco deve essere mal formattato, o lo stato `S[n]` deve essere non corretto. Dato che`S[0]` è noto per essere corretto, ci deve essere qualche primo stato `S[i]` che è corretto dove `S[i-1]` è corretto. Il nodo di verifica fornirebbe l'indice `i`, insieme a una "prova di invalidità" consistente nel sottoinsieme dei nodi del Patricia tree che necessitano di essere processati `APPLY(S[i-1],TX[i]) -> S[i]`. I nodi sarebbero in grado di usare quei nodi per eseguire quella parte della computazione, ed osservare che `S[i]` generato non corrisponde al `S[i]` fornito.

Un ulteriore, e più sofisticato, attacco coinvolgerebbe i miners malevoli che pubblicano i blocchi incompleti, in modo tale che non sia necessaria tutta l'informazione per determinare quali blocchi siano validi e quali invalidi. La soluzione a questo è un protocollo che risponde-ad-una-sfida: i nodi di verificazione emettono "sfide" con l'obiettivo di andare a colpire gli indici delle transazioni, e fino alla ricezione di un nodo pieno, uno non completo considera il blocco come non attendibile finché un altro nodo pieno, sia del miner che di un altro verificatore, fornisce un sottoinsieme di nodi Patricia come prova di validità.

## Conclusioni

Il protocollo Ethereum è stato originariamente concepito come una versione aggiornata di una criptomoneta, che fornisce caratteristiche avanzate come un escrow sulla blockchain, limiti ai prelievi, contratti finanziari, mercati del gioco e simili attraverso un linguaggio di programmazione gambling markets and the like via a tutto raggio. Il protocollo Ethereum non "supporterà" direttamente alcun tipo di applicazione, ma l'esistenza di un linguaggio di programmazione Turing-complete significa che possono teoricamente essere creati dei contratti arbitrari per qualsiasi tipo di transazione o applicazione. Tuttavia, la cosa più interessante in Ethereum, è che il suo protocollo comprende molto di più che una valuta. I protocolli sullo storage decentralizzato di file, computazione decentralizzata e mercati predittivi decentralizzati, ed altre decine di concetti di questo tipo, hanno il potenziale di aumentare sensibilmente l'efficienza dell'industria relativa al calcolo computazionale, e firnire una spinta enorme agli altri protocolli peer-to-peer aggiungendo per la prima volta un protocollo economico. Infine, c'è anche una consistente gamma di applicazione che non hanno nulla a che vedere con i soldi.

Il concetto di una funzione arbitraria di transizione di stato come implementata nel procollo di Ethereum con una piattaforma dal potenziale unico; piuttosto che essere una del tipo chiuso, con un protocollo che ha un solo fine inteso per un'unica speficica gamma di applicazioni nello storage dei dati, gioco o finanza, Ethereum ha un design aperto a tutti, e noi crediamo che sia molto adatta per servire, negli anni che verranno, da protocollo fondante per un grande numero di protocolli sia finanziari che non finanziari.

## Note e Approfondimenti

#### Note

1. Un lettore più esperto potrebbe notare che, in effetti, un indirizzo Bitcoin è l' hash di una chiave pubblica dalla curva ellettica, e non la stessa chiave pubblica. Tuttavia, nella practica, è perfettamente legittimo, in termini di terminologia crittografica, riferirsi alla chiave pubblica dell'hash come la stessa chiave pubblica. Questo poiché la crittografia del Bitcoin può essere considerata come un algoritmo di firma digitale personalizzata, dove la chiave pubblica consiste nell' hash della ECC pubkey, la firma consiste nell' ECC pubkey concatenata con la firma ECC, e l'algoritmo di verificazione coinvolge il controllo della ECC pubkey nella firma sull'hash della ECC pubkey fornita come chiave pubblica e quindi verificando la firma dell'ECC sulla pubkey ECC.
2. Tecnicamente, la media degli 11 blocchi precedenti.
3. Internamente, 2 e "CHARLIE" sono entrambi numeri, mentre quest'ultimo è una rappresentazione big-endian base 256. I numeri possono almeno  essere 0 o al massimo 2<sup>256</sup>-1.

#### Approfindimenti

1. Intrinsic value: http://bitcoinmagazine.com/8640/an-exploration-of-intrinsic-value-what-it-is-why-bitcoin-doesnt-have-it-and-why-bitcoin-does-have-it/
2. Smart property: https://en.bitcoin.it/wiki/Smart_Property
3. Smart contracts: https://en.bitcoin.it/wiki/Contracts
4. B-money: http://www.weidai.com/bmoney.txt
5. Reusable proofs of work: http://www.finney.org/~hal/rpow/ 
6. Secure property titles with owner authority: http://szabo.best.vwh.net/securetitle.html
7. Bitcoin whitepaper: http://bitcoin.org/bitcoin.pdf
8. Namecoin: https://namecoin.org/
9. Zooko's triangle: http://en.wikipedia.org/wiki/Zooko's_triangle
10. Colored coins whitepaper: https://docs.google.com/a/buterin.com/document/d/1AnkP_cVZTCMLIzw4DvsW6M8Q2JC0lIzrTLuoWu2z1BE/edit
11. Mastercoin whitepaper: https://github.com/mastercoin-MSC/spec
12. Decentralized autonomous corporations, Bitcoin Magazine: http://bitcoinmagazine.com/7050/bootstrapping-a-decentralized-autonomous-corporation-part-i/
13. Simplified payment verification: https://en.bitcoin.it/wiki/Scalability#Simplifiedpaymentverification
14. Merkle trees: http://en.wikipedia.org/wiki/Merkle_tree
15. Patricia trees: http://en.wikipedia.org/wiki/Patricia_tree
16. GHOST: http://www.cs.huji.ac.il/~avivz/pubs/13/btc_scalability_full.pdf
17. StorJ and Autonomous Agents, Jeff Garzik: http://garzikrants.blogspot.ca/2013/01/storj-and-bitcoin-autonomous-agents.html
18. Mike Hearn on Smart Property at Turing Festival: http://www.youtube.com/watch?v=Pu4PAMFPo5Y
19. Ethereum RLP: https://github.com/ethereum/wiki/wiki/%5BEnglish%5D-RLP
20. Ethereum Merkle Patricia trees: https://github.com/ethereum/wiki/wiki/%5BEnglish%5D-Patricia-Tree
21. Peter Todd on Merkle sum trees: http://sourceforge.net/p/bitcoin/mailman/message/31709140/