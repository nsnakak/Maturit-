# Sistemi e Reti - Appunti per la maturita

## Nota di lavoro

Questa e una prima struttura del documento, costruita sul programma annuale fornito.
Il modello segue l'impostazione del documento di Italiano: schede ordinate per modulo,
spiegazioni sintetiche, parole chiave e sezioni da integrare con le presentazioni.

Quando arriveranno le slide o gli appunti dei singoli moduli, ogni sezione potra essere
completata con definizioni, esempi, schemi e collegamenti per l'esame orale.

---

# Scheda 1

## MODULO I - Richiami allo strato di trasporto

### UNITA 1 - Il livello di trasporto e il protocollo UDP

### Obiettivo del modulo

Ripassare il ruolo dello strato di trasporto nel modello TCP/IP, con particolare attenzione
alla differenza tra comunicazione affidabile e non affidabile, tra protocolli connectionless
e connection oriented, e al funzionamento dei protocolli UDP e TCP.

### Argomenti da sviluppare

- Trasferimento affidabile dei segmenti.
- Trasmissione connectionless e connection oriented.
- Three-way handshaking.
- Protocollo UDP.
- Protocollo TCP.

### Schema sintetico iniziale

Lo strato di trasporto mette in comunicazione processi applicativi presenti su host diversi.
Lavora sopra lo strato di rete e permette alle applicazioni di scambiarsi dati usando le
porte, che identificano i servizi in esecuzione su una macchina.

Il livello di rete realizza una comunicazione logica tra host, cioe tra macchine. Il livello di
trasporto realizza invece una comunicazione logica tra processi, cioe tra programmi in
esecuzione sugli host. Per questo motivo non basta conoscere l'indirizzo IP del computer:
serve anche sapere a quale applicazione devono essere consegnati i dati.

UDP e TCP rappresentano due modi diversi di gestire la comunicazione:

- UDP e connectionless: non stabilisce una connessione prima dell'invio, non garantisce
  consegna, ordine o ritrasmissione dei segmenti.
- TCP e connection oriented: stabilisce una connessione logica, controlla il flusso,
  gestisce gli errori e garantisce una consegna affidabile.

Il three-way handshaking e la procedura con cui TCP apre una connessione:

1. il client invia un segmento SYN;
2. il server risponde con SYN-ACK;
3. il client conferma con ACK.

### Servizio e protocollo

Nel modello a livelli bisogna distinguere servizio e protocollo.

Un servizio e l'insieme delle operazioni che un livello mette a disposizione del livello
superiore. Un protocollo e invece l'insieme delle regole che stabiliscono formato e
significato dei messaggi scambiati tra entita dello stesso livello su macchine diverse.

Le entita di livello usano i protocolli per realizzare i servizi. Per esempio, il livello di
trasporto offre alle applicazioni la possibilita di inviare dati; per farlo usa protocolli come
TCP e UDP.

### SAP, porte e socket

Le SAP, Service Access Point, sono punti logici attraverso cui un livello superiore accede ai
servizi del livello inferiore. Nel livello di trasporto le SAP corrispondono alle porte.

Le porte sono numeri a 16 bit, quindi vanno da 0 a 65535. Servono per distinguere le varie
applicazioni attive su uno stesso host. Senza le porte, un computer potrebbe ricevere un
pacchetto IP ma non saprebbe a quale programma consegnarlo.

Le porte si dividono in tre gruppi:

- Well Known Ports, da 0 a 1023: porte riservate ai servizi piu comuni, come HTTP, FTP,
  SMTP, DNS e POP3.
- Registered Ports, da 1024 a 49151: porte registrate o usate liberamente da molte
  applicazioni.
- Dynamic Ports, da 49152 a 65535: porte assegnate dinamicamente ai processi client.

Alcune porte importanti:

| Porta | Servizio | Protocollo |
| --- | --- | --- |
| 20 | FTP dati | TCP |
| 21 | FTP controllo | TCP |
| 23 | Telnet | TCP |
| 25 | SMTP | TCP |
| 53 | DNS | TCP/UDP |
| 80 | HTTP | TCP |
| 110 | POP3 | TCP |

La combinazione tra indirizzo IP e numero di porta prende il nome di socket. Un socket
identifica un punto di accesso alla comunicazione:

- socket del mittente: indirizzo IP sorgente + porta sorgente;
- socket del destinatario: indirizzo IP destinazione + porta destinazione.

Una comunicazione tra due processi puo essere identificata dalle due coppie
`IP:porta`, una del mittente e una del destinatario. Per esempio, un client puo usare la
porta locale 5678 per collegarsi al server web `90.35.101.10:80`.

### Multiplexing e demultiplexing

Una delle funzioni principali del livello di trasporto e la multiplazione/demultiplazione.

Il multiplexing avviene sul mittente: il livello di trasporto raccoglie dati provenienti da
applicazioni diverse, li inserisce in segmenti e aggiunge le intestazioni necessarie, tra cui
le porte.

Il demultiplexing avviene sul destinatario: il livello di trasporto riceve i segmenti, legge i
numeri di porta e consegna i dati al processo corretto.

Esempio: un utente puo navigare sul web e scaricare la posta nello stesso momento. I dati
arrivano allo stesso indirizzo IP, ma vengono consegnati ad applicazioni diverse grazie ai
numeri di porta.

Puo anche accadere che due client diversi usino la stessa porta sorgente per collegarsi allo
stesso server. Non e un problema, perche il server distingue le connessioni considerando
anche gli indirizzi IP sorgenti.

### Servizi affidabili e inaffidabili

Un servizio affidabile assicura che tutti i dati inviati arrivino al destinatario. Per ottenere
questa garanzia usa meccanismi come ACK, ritrasmissioni, controllo dell'ordine e controllo
degli errori. Questi meccanismi aumentano pero l'overhead, cioe il lavoro aggiuntivo e i
dati di controllo necessari.

Un servizio inaffidabile non garantisce che i dati arrivino, ne che arrivino nello stesso
ordine in cui sono stati inviati. Questo puo sembrare uno svantaggio, ma in alcuni casi e
preferibile perche riduce i ritardi e rende la comunicazione piu veloce.

### Servizi connection oriented e connectionless

I servizi connection oriented seguono il modello della telefonata:

1. si stabilisce una connessione;
2. si scambiano dati;
3. si chiude la connessione.

TCP appartiene a questa categoria. E connesso e affidabile: crea una connessione logica,
controlla la consegna dei dati e ricompone il flusso informativo nell'ordine corretto.

I servizi connectionless seguono il modello della posta ordinaria:

- ogni pacchetto viaggia indipendentemente dagli altri;
- pacchetti con stesso mittente e destinatario possono seguire percorsi diversi;
- possono arrivare in ordine diverso;
- alcuni pacchetti possono anche non arrivare.

UDP appartiene a questa categoria. Non stabilisce una connessione e non garantisce la
consegna, ma e semplice e veloce.

### Primitive del livello di trasporto

Per accedere ai servizi di un livello si usano funzioni di base chiamate primitive. Ogni
primitiva puo essere vista come una richiesta o una segnalazione tra chi usa il servizio e chi
lo fornisce.

I quattro metodi fondamentali sono:

- request: il service user richiede un servizio;
- indication: il service provider segnala che e arrivata una richiesta;
- response: il service user risponde alla richiesta;
- confirm: il service provider conferma l'esito della richiesta.

In un servizio connection oriented si possono avere primitive come:

1. `connect.request()`;
2. `connect.indication()`;
3. `connect.response()`;
4. `connect.confirm()`;
5. `data.request()`;
6. `data.indication()`;
7. `disconnect.request()`;
8. `disconnect.indication()`.

### Client, server e buffering

Nell'architettura client-server, il server offre un servizio e resta in ascolto su una porta,
mentre il client richiede quel servizio.

Quando un processo viene associato a una porta, il sistema operativo puo collegarlo a due
code: una di ingresso e una di uscita. Questa funzione prende il nome di buffering e serve a
gestire temporaneamente i dati in arrivo e in partenza.

### Servizi offerti dal livello di trasporto

Il livello di trasporto puo offrire diversi servizi:

- gestione della connessione: apertura e chiusura della connessione quando necessario;
- consegna in ordine corretto: riordino dei pacchetti prima di passarli all'applicazione;
- controllo degli errori: verifica dei dati ricevuti;
- trasferimento affidabile: ritrasmissione dei pacchetti persi;
- controllo di flusso: evita che un host veloce saturi un host piu lento;
- controllo di congestione: adatta la velocita di trasmissione allo stato della rete;
- multiplexing e demultiplexing: separazione dei flussi tramite le porte.

Non tutti i protocolli offrono tutti questi servizi. TCP ne offre molti; UDP offre solo un
insieme minimo di funzioni.

### Qualita del servizio, QoS

La qualita del servizio, o QoS, indica il livello di prestazioni richiesto da una comunicazione.
Puo essere descritta da parametri come:

- ritardo massimo;
- velocita di consegna;
- tasso di errore;
- probabilita di fallimento della connessione.

Le esigenze cambiano in base all'applicazione. Per una e-mail un ritardo anche elevato puo
essere accettabile; per streaming audio/video o videoconferenze il ritardo deve essere molto
basso.

### Il protocollo UDP

UDP, User Datagram Protocol, fornisce un metodo per spedire dati senza stabilire prima
una connessione con il destinatario. E quindi un protocollo connectionless e inaffidabile.

Le sue caratteristiche principali sono:

- e veloce, perche ha un header ridotto e non gestisce connessioni;
- supporta trasmissioni broadcast e multicast;
- non garantisce consegna, ordine o ritrasmissione;
- usa le porte per multiplexing e demultiplexing;
- rileva alcuni errori tramite checksum.

UDP viene usato quando la velocita e piu importante dell'affidabilita assoluta, per esempio
in streaming audio/video, comunicazioni real-time, DNS e altri servizi in cui una
ritrasmissione tardiva sarebbe poco utile.

### Funzionamento di UDP

Il mittente conosce in anticipo indirizzo IP e porta del destinatario. Crea un segmento UDP,
lo incapsula in un datagramma IP e lo invia.

Quando il destinatario riceve il datagramma, il livello IP estrae il segmento UDP e lo passa
al livello di trasporto. UDP legge la porta di destinazione:

- se la porta e in ascolto, i dati vengono consegnati all'applicazione;
- se la porta non e in ascolto, puo essere inviato al mittente un messaggio ICMP di tipo
  `port unreachable`.

UDP non recupera gli errori: se un segmento e danneggiato, in alcune implementazioni
viene scartato, in altre puo essere consegnato all'applicazione con segnalazione dell'errore.

### Struttura del segmento UDP

Il segmento UDP ha un header molto semplice, lungo 8 byte. I campi sono:

| Campo | Dimensione | Significato |
| --- | --- | --- |
| Source Port | 16 bit | Porta del mittente |
| Destination Port | 16 bit | Porta del destinatario |
| Length | 16 bit | Lunghezza totale di header + dati |
| Checksum | 16 bit | Controllo degli errori |

Dopo l'header si trovano i dati ricevuti dal livello applicativo.

Gli indirizzi IP non sono presenti nell'header UDP perche sono gia contenuti nell'header IP
che incapsula il segmento.

### Checksum UDP

Il checksum serve per rilevare errori nel segmento. Viene calcolato dal mittente e
ricontrollato dal destinatario.

Nel calcolo viene usata anche una pseudo-intestazione che contiene informazioni prese dal
livello IP, come gli indirizzi IP sorgente e destinazione. Questo permette di verificare non
solo il contenuto UDP, ma anche che il segmento sia arrivato tra gli host corretti.

Il checksum rileva errori, ma UDP non effettua ritrasmissioni automatiche. L'eventuale
recupero deve essere gestito dall'applicazione, se necessario.

### UNITA 2 - Il trasferimento affidabile e il protocollo TCP

Il trasferimento affidabile e l'insieme dei meccanismi che permettono di consegnare i dati
correttamente anche se la rete sottostante puo perdere, duplicare o consegnare fuori ordine
i pacchetti.

Un servizio di trasferimento e considerato affidabile quando garantisce:

- consegna: tutti i messaggi arrivano a destinazione senza errori; se non e possibile, il
  mittente deve esserne informato;
- assenza di duplicazione: ogni messaggio viene consegnato una sola volta;
- sequenzialita: i messaggi vengono consegnati nello stesso ordine in cui sono stati
  trasmessi.

Per realizzare queste garanzie si usano vari meccanismi:

- numerazione dei segmenti trasmessi;
- messaggi di riscontro, cioe ACK;
- timer e temporizzazioni in trasmissione;
- ritrasmissione dei segmenti non confermati;
- finestre di trasmissione e ricezione.

### RTT e RTO

Due parametri importanti del trasferimento affidabile sono RTT e RTO.

RTT, Round Trip Time, e il tempo che passa tra l'inizio della trasmissione di un segmento e
la ricezione del relativo riscontro. In pratica misura il tempo di andata e ritorno di un dato
e del suo ACK.

RTO, Retransmission Time Out, e il tempo massimo che il mittente aspetta prima di
considerare perso un segmento. Se entro il RTO non arriva l'ACK, il segmento viene
ritrasmesso.

Un RTO troppo basso causa ritrasmissioni inutili; un RTO troppo alto rallenta il recupero
degli errori. Per questo TCP lo adatta in base alle condizioni della rete.

### Numerazione dei segmenti

TCP numera i dati usando il Sequence Number, indicato anche come SN o Seq. Il Sequence
Number non identifica genericamente il segmento, ma indica la posizione nel flusso del
primo byte contenuto nel segmento.

Il ricevente controlla il Sequence Number:

- se il numero e quello atteso, i dati possono essere passati al livello superiore;
- se il numero e minore di quello atteso, il dato e gia stato ricevuto e viene considerato un
  duplicato;
- se il numero e maggiore di quello atteso, significa che manca qualche segmento
  precedente: il dato puo essere memorizzato temporaneamente in attesa dei segmenti
  mancanti.

Questo meccanismo permette di ricostruire correttamente il flusso anche quando i segmenti
arrivano fuori ordine.

### ACK e riscontro cumulativo

Il riscontro viene inviato con un Acknowledgement Number, o ACKn. L'ACKn indica il
numero del prossimo byte che il ricevente si aspetta di ricevere.

Per esempio, se il ricevente ha ricevuto correttamente tutti i byte fino al numero 999,
invia un ACK con valore 1000, per dire: "ho ricevuto tutto fino a 999, ora aspetto il byte
1000".

Il riscontro puo essere cumulativo: un solo ACK puo confermare la ricezione corretta di piu
segmenti consecutivi. Questo riduce il numero di messaggi di controllo necessari.

### Il protocollo TCP

TCP, Transmission Control Protocol, e un protocollo di trasporto punto-punto, orientato
alla connessione e affidabile. La comunicazione avviene tra due estremi, di solito un client
e un server.

Le sue caratteristiche principali sono:

- connection oriented: prima dello scambio dei dati viene aperta una connessione;
- affidabile: gestisce ACK, ritrasmissioni, numerazione e controllo degli errori;
- sequenziale: consegna i dati all'applicazione nell'ordine corretto;
- full-duplex: permette trasmissione contemporanea in entrambe le direzioni;
- orientato al flusso: vede i dati come una sequenza continua di byte.

Dopo l'apertura della connessione avviene la comunicazione vera e propria. Alla fine, la
connessione viene chiusa con un'apposita procedura di terminazione.

### Segmento TCP

Il segmento TCP contiene un header piu complesso di quello UDP, perche deve supportare
affidabilita, controllo della connessione e controllo del flusso.

I campi principali sono:

| Campo | Funzione |
| --- | --- |
| Source Port | Porta del processo mittente |
| Destination Port | Porta del processo destinatario |
| Sequence Number | Numero del primo byte del segmento |
| Acknowledgement Number | Prossimo byte atteso dal ricevente |
| Header Length | Lunghezza dell'header TCP |
| Flags | Bit di controllo della connessione |
| Window Size | Dimensione della finestra di ricezione |
| Checksum | Controllo degli errori |
| Urgent Pointer | Usato con dati urgenti |
| Options | Parametri opzionali, come MSS |

Le flag piu importanti sono:

- SYN: richiesta di apertura della connessione;
- ACK: conferma di ricezione;
- FIN: richiesta di chiusura ordinata della connessione;
- RST: reset immediato della connessione;
- PSH: richiesta di consegna rapida dei dati all'applicazione;
- URG: segnala la presenza di dati urgenti.

### MSS e MTU

MSS, Maximum Segment Size, indica la massima dimensione del corpo dati, cioe del payload,
che puo essere inserito in un segmento TCP.

Nelle reti Ethernet IPv4 il valore tipico della MTU, Maximum Transmission Unit, e 1500
byte. Se si sottraggono 20 byte di header IP e 20 byte di header TCP, si ottiene una MSS
tipica di 1460 byte.

La MSS riguarda quindi solo i dati TCP, mentre la MTU riguarda la dimensione massima del
frame/pacchetto trasportabile sul mezzo di rete.

### Apertura della connessione TCP: three-way handshaking

TCP apre una connessione tramite three-way handshaking, cioe uno scambio iniziale di tre
messaggi che permette a client e server di sincronizzare i numeri di sequenza e concordare
i parametri della connessione.

La procedura e:

1. SYN: il client invia un segmento con flag SYN e un numero di sequenza iniziale;
2. SYN-ACK: il server risponde con SYN e ACK, confermando il SYN del client e inviando il
   proprio numero di sequenza iniziale;
3. ACK: il client conferma il SYN del server.

Dopo questi tre passaggi la connessione e stabilita e puo iniziare il trasferimento dei dati.

Il three-way handshaking serve per evitare comunicazioni non sincronizzate e per assicurare
che entrambi gli host siano pronti a trasmettere e ricevere.

### Protocollo a finestre scorrevoli

TCP usa il meccanismo delle finestre scorrevoli per trasmettere piu segmenti senza dover
attendere un ACK dopo ogni singolo invio.

La finestra indica quanti byte o segmenti possono essere inviati senza ricevere conferma.
Quando arrivano gli ACK, la finestra "scorre" in avanti e permette di inviare nuovi dati.

Questo meccanismo migliora l'efficienza, perche mantiene attiva la trasmissione, e consente
anche il controllo di flusso: il destinatario puo comunicare quanto spazio ha disponibile nel
buffer tramite il campo Window Size.

Se il ricevente ha poca memoria disponibile, puo ridurre la finestra; se invece puo ricevere
piu dati, puo aumentarla.

### Ritrasmissione e gestione del time-out

Quando TCP invia un segmento, attiva un timer. Se l'ACK non arriva entro il tempo previsto
dal RTO, il segmento viene considerato perso e viene ritrasmesso.

La ritrasmissione puo avvenire anche quando il mittente riceve segnali che indicano la
probabile perdita di un segmento, per esempio ACK duplicati. In ogni caso, lo scopo e
ricostruire un flusso completo e ordinato.

La gestione del time-out e importante per bilanciare affidabilita e prestazioni: TCP deve
recuperare i dati persi senza appesantire inutilmente la rete con troppe ritrasmissioni.

### Chiusura della connessione TCP

La chiusura della connessione puo avvenire in due modi:

- handshake a tre vie: quando la chiusura avviene contemporaneamente dalle due parti;
- handshake a quattro vie: quando una parte chiude prima dell'altra.

Nel caso piu comune, la chiusura a quattro vie avviene cosi:

1. un host invia FIN per dire che non deve piu trasmettere dati;
2. l'altro host risponde con ACK;
3. quando anche il secondo host ha finito di trasmettere, invia FIN;
4. il primo host risponde con ACK.

Questa procedura esiste perche TCP e full-duplex: le due direzioni della comunicazione
sono indipendenti, quindi una parte puo smettere di trasmettere mentre l'altra deve ancora
inviare dati.

### Differenze principali tra TCP e UDP

| Aspetto | TCP | UDP |
| --- | --- | --- |
| Connessione | Connection oriented | Connectionless |
| Affidabilita | Garantisce consegna ordinata | Non garantisce consegna |
| Velocita | Piu lento per l'overhead | Piu veloce e leggero |
| Header | Piu complesso | Semplice, 8 byte |
| Ritrasmissioni | Si | No |
| Ordine dei dati | Garantito | Non garantito |
| Uso tipico | Web, posta, FTP, SSH | Streaming, DNS, VoIP, giochi online |

### Parole chiave

Segmento, PDU, SAP, porta, socket, multiplexing, demultiplexing, buffering,
affidabilita, servizio inaffidabile, connection oriented, connectionless, ACK,
riscontro cumulativo, Sequence Number, RTT, RTO, finestra scorrevole, Window Size,
QoS, UDP, TCP, MSS, MTU, checksum, ICMP port unreachable, SYN, FIN, RST,
three-way handshaking.

### Da integrare con le presentazioni

- Esempi completi di domande tipiche d'esame.

---

# Scheda 2

## MODULO II - Lo strato di applicazione

### Obiettivo del modulo

Comprendere i principali servizi dello strato applicativo e il modo in cui permettono agli
utenti e ai sistemi di usare la rete: configurazione automatica, navigazione web,
trasferimento file, posta elettronica e risoluzione dei nomi.

### Argomenti da sviluppare

- Configurazione dei sistemi con DHCP.
- WWW e HTTP.
- FTP.
- Posta elettronica: web mail e pop mail.
- SMTP, POP3 e IMAP.
- Standard MIME.
- DNS.

### Schema sintetico iniziale

Lo strato di applicazione contiene i protocolli usati direttamente dai servizi di rete.
Ogni protocollo risolve un bisogno specifico: DHCP assegna automaticamente la
configurazione IP, HTTP permette la consultazione delle pagine web, FTP consente il
trasferimento dei file, SMTP/POP3/IMAP gestiscono la posta elettronica e DNS traduce i
nomi di dominio in indirizzi IP.

DHCP semplifica la configurazione dei client perche assegna parametri come indirizzo IP,
subnet mask, gateway predefinito e server DNS. DNS, invece, e fondamentale per rendere
utilizzabili i nomi simbolici al posto degli indirizzi numerici.

### UNITA 1 - Il livello delle applicazioni

Un'applicazione di rete e un insieme di programmi che lavorano su piu computer collegati
tra loro tramite Internet o tramite una rete locale. Per questo viene anche chiamata
applicazione distribuita.

Nel modello ISO/OSI il livello applicativo e quello piu vicino all'utente finale: comprende i
protocolli che permettono alle applicazioni di comunicare con applicazioni remote. Esempi
di applicazioni di rete sono posta elettronica, Web, messaggistica istantanea, accesso a
terminali remoti, condivisione file P2P, streaming, telefonia via Internet e videoconferenza.

Un processo e un programma in esecuzione su un host. Processi sullo stesso host possono
comunicare tramite meccanismi del sistema operativo; processi su host diversi comunicano
invece attraverso la rete, usando protocolli di livello applicazione e i servizi degli strati
inferiori.

L'agente utente, o user agent, e l'interfaccia tra l'utente e l'applicazione di rete. Esempi:

- browser web per il WWW;
- client di posta per le e-mail;
- lettore audio/video per lo streaming.

### Protocolli del livello applicazione

Un protocollo applicativo stabilisce:

- il formato dei messaggi scambiati;
- il significato dei messaggi;
- le azioni da eseguire quando un messaggio viene inviato o ricevuto;
- il modo in cui vengono usati i servizi del livello di trasporto.

Tra i protocolli applicativi piu importanti ci sono:

- HTTP e HTTPS per il Web;
- FTP, FTPS e SFTP per il trasferimento di file;
- SMTP, POP3 e IMAP per la posta elettronica;
- DNS per la risoluzione dei nomi;
- DHCP per la configurazione automatica degli host;
- Telnet e SSH per l'accesso remoto.

### Architetture delle applicazioni di rete

Quando si progetta un'applicazione di rete bisogna scegliere l'architettura, cioe il modo in
cui sono organizzati i programmi che comunicano.

#### Architettura client-server

Nel modello client-server l'applicazione e divisa in due parti: client e server.

Il server:

- e di solito sempre attivo;
- ha un indirizzo IP fisso o comunque raggiungibile;
- fornisce un servizio ai client;
- puo gestire molti client contemporaneamente;
- puo essere realizzato tramite piu macchine, cluster o server farm.

Il client:

- richiede un servizio al server;
- puo contattare il server quando serve;
- puo avere un indirizzo IP dinamico;
- normalmente non comunica direttamente con gli altri client.

Un esempio tipico e il WWW: il browser e il client, mentre il web server contiene pagine e
risorse che vengono inviate su richiesta.

Quando le richieste sono molte, un solo server puo non bastare. In questi casi si usano
server virtuali, cluster o server farm per distribuire il carico e garantire continuita del
servizio. Per l'utente il servizio puo apparire come un unico hostname, anche se dietro ci
sono piu indirizzi IP e piu server.

#### Architettura peer-to-peer, P2P

Nel modello peer-to-peer non esiste necessariamente un server centrale: ogni nodo, detto
peer, puo fornire e ricevere risorse. I dispositivi comunicano direttamente tra loro e la rete
puo adattarsi dinamicamente.

I vantaggi principali sono:

- scalabilita, perche il carico viene distribuito tra i peer;
- ridondanza, perche una risorsa puo essere presente su piu nodi;
- minore dipendenza da un server unico.

Gli svantaggi principali sono:

- minore controllo;
- gestione della sicurezza piu complessa;
- maggiore difficolta nel garantire affidabilita e qualita del servizio.

Un esempio e BitTorrent: i file vengono divisi in piccoli pezzi e ogni peer scarica parti del
file mentre condivide le parti gia ricevute. In questo modo il carico sul server originario si
riduce e il download puo diventare piu veloce.

#### P2P centralizzato e ibrido

Nel P2P centralizzato esiste un server centrale, spesso chiamato directory server, che non
memorizza i file ma mantiene informazioni su quali peer possiedono certe risorse. I peer
conservano i dati, comunicano al server cosa condividono e permettono ad altri peer di
scaricare le risorse. Un esempio storico e Napster.

Nel P2P ibrido alcuni nodi hanno un ruolo piu importante e diventano super-peer. Questi
super-peer aiutano nella ricerca o nel coordinamento, mentre lo scambio dei dati puo
avvenire tra peer. Esempi citati sono Skype ed eMule.

### API e socket nel livello applicativo

Per comunicare in rete, un programma usa delle API, Application Programming Interface.
Nel caso delle applicazioni Internet, un concetto fondamentale e quello di socket.

Una socket e un punto di comunicazione attraverso cui due processi, per esempio client e
server, si scambiano messaggi. Lo sviluppatore controlla la parte applicativa, mentre il
sistema operativo gestisce i dettagli del protocollo di trasporto, i buffer e le variabili della
connessione.

Il concetto di socket collega direttamente il livello applicativo al livello di trasporto:
l'applicazione invia e riceve dati attraverso la socket, mentre TCP o UDP si occupano del
trasporto effettivo.

### Quale servizio di trasporto richiede un'applicazione?

Le applicazioni non hanno tutte gli stessi bisogni. La scelta del protocollo di trasporto
dipende dai requisiti del servizio.

I requisiti principali sono:

- perdita di dati: alcune applicazioni, come il trasferimento file, richiedono affidabilita al
  100%; altre, come audio e video in tempo reale, possono tollerare piccole perdite;
- temporizzazione: applicazioni come VoIP, giochi online e videoconferenze richiedono
  ritardi bassi;
- ampiezza di banda: applicazioni multimediali possono richiedere una banda minima,
  mentre applicazioni elastiche, come la posta elettronica, usano la banda disponibile;
- sicurezza: alcune applicazioni richiedono integrita, autenticazione o cifratura dei dati.

Esempi:

| Applicazione | Protocollo applicativo | Trasporto tipico |
| --- | --- | --- |
| Posta elettronica | SMTP | TCP |
| Accesso remoto | Telnet/SSH | TCP |
| Web | HTTP/HTTPS | TCP |
| Trasferimento file | FTP | TCP |
| Streaming multimediale | Protocolli proprietari o standard specifici | TCP o UDP |
| Telefonia Internet | Protocolli VoIP | Tipicamente UDP |

### Il World Wide Web

Il World Wide Web, WWW, e l'insieme delle pagine e delle risorse collegate da link e
accessibili tramite HTTP o HTTPS.

Il funzionamento di base e client-server:

1. l'utente inserisce un URL nel browser;
2. il browser, cioe il client, invia una richiesta al web server;
3. il server risponde inviando la risorsa richiesta;
4. il browser interpreta il contenuto e lo visualizza.

Una pagina web e composta da oggetti: spesso una pagina HTML iniziale e altri oggetti
collegati, come immagini, fogli di stile, script o file multimediali.

### Browser, web server, URI e URL

Il browser e lo user agent del Web. Le sue funzioni principali sono:

- instaurare una connessione TCP con il server;
- inviare richieste per ottenere le risorse;
- interpretare HTML e altri linguaggi lato client;
- visualizzare il contenuto in modo comprensibile all'utente;
- gestire la cache.

La cache del browser e uno spazio su disco in cui vengono salvate copie di pagine,
immagini e altri oggetti gia scaricati. Prima di richiedere una risorsa al server, il browser
puo controllare se e gia disponibile in cache. Con il comando aggiorna/refresh l'utente puo
forzare una nuova richiesta al server.

Il web server e il software, in esecuzione su un server, che gestisce le richieste dei client e
invia pagine o risorse web. Esempi di web server sono Apache, Nginx e IIS.

Una risorsa su Internet viene identificata da un URI, Uniform Resource Identifier. Un URL,
Uniform Resource Locator, e un tipo di URI che specifica dove si trova la risorsa e come
raggiungerla. Tutti gli URL sono URI, ma non tutti gli URI sono URL.

Esempio:

`https://www.scuola.it/info/corsi.html`

- `https`: protocollo usato;
- `www.scuola.it`: nome dell'host;
- `/info/corsi.html`: percorso e file della risorsa.

### Il protocollo FTP

FTP, File Transfer Protocol, e un protocollo applicativo usato per trasferire file tra
computer collegati in rete. Permette di condividere file di testo o binari anche tra sistemi
diversi.

FTP usa TCP per garantire un trasferimento affidabile. La particolarita di FTP e che usa due
connessioni TCP:

- porta 21: canale di controllo, usato per comandi e risposte;
- porta 20: canale dati, usato per il trasferimento dei file nella modalita attiva.

Per usare FTP servono:

- un FTP server, che mette a disposizione file e directory;
- un FTP client, che permette all'utente di collegarsi, autenticarsi e trasferire file.

Operazioni comuni:

- download: copia di un file dal server al client;
- upload: copia di un file dal client al server;
- cancellazione di file;
- creazione di directory;
- visualizzazione e gestione delle cartelle remote.

L'accesso puo essere autenticato, con username e password, oppure anonimo. L'accesso
anonimo viene usato per download pubblici ma offre un livello di sicurezza basso.

### FTP attivo e FTP passivo

FTP puo funzionare in modalita attiva o passiva.

Nella modalita attiva il client apre la connessione di controllo verso il server, ma poi e il
server ad aprire la connessione dati verso il client. Questo puo creare problemi con i
firewall lato client, perche il tentativo del server di aprire una connessione in ingresso puo
essere bloccato.

Per questo motivo oggi e spesso preferita la modalita passiva. In modalita passiva il client
apre sia la connessione di controllo sia la connessione dati verso il server. Se anche il
server ha un firewall, bisogna configurare un intervallo di porte, di solito superiori a 1024,
per accettare le connessioni dati passive.

### Sicurezza: FTP, FTPS e SFTP

FTP tradizionale non cifra i dati. Questo significa che username, password, comandi,
risposte e file possono essere intercettati tramite sniffing.

Per aumentare la sicurezza si usano alternative cifrate:

- FTPS: estende FTP aggiungendo cifratura SSL/TLS;
- SFTP: servizio di trasferimento file basato su SSH, diverso da FTP ma usato con scopo
  simile.

FTPS protegge credenziali e dati tramite cifratura; l'algoritmo viene negoziato con il server
e spesso i client mostrano un simbolo di lucchetto per indicare il trasferimento sicuro.

| Tipo di accesso | Descrizione | Sicurezza |
| --- | --- | --- |
| Anonimo | Accesso senza credenziali personali, usato per download pubblici | Bassa |
| Autenticato | Richiede username e password, con privilegi assegnati | Media |
| Sicuro | FTPS o SFTP, con trasferimento cifrato | Alta |

### Comandi FTP principali

I comandi FTP vengono inviati come testo ASCII sul canale di controllo.

| Comando | Significato |
| --- | --- |
| `USER username` | Invia il nome utente |
| `PASS password` | Invia la password |
| `LIST` o `ls` | Mostra i file della directory corrente |
| `RETR file` o `get file` | Scarica un file dal server |
| `STOR file` o `put file` | Carica un file sul server |
| `cd directory` | Cambia directory remota |
| `pwd` | Mostra la directory remota corrente |
| `binary` | Imposta trasferimento binario |
| `ascii` | Imposta trasferimento ASCII |
| `quit` o `bye` | Chiude la connessione FTP |

Esempi di codici di risposta:

- 331: username corretto, password richiesta;
- 125: connessione dati gia aperta, trasferimento in avvio;
- 425: impossibile aprire la connessione dati;
- 452: errore nella scrittura del file.

### FTP in Packet Tracer

In Packet Tracer una configurazione FTP tipica prevede:

1. assegnare indirizzi IP a client, server e dispositivi di rete;
2. configurare gateway e DNS sul server, se necessari;
3. aprire il server e abilitare il servizio FTP;
4. creare uno o piu utenti con permessi adeguati, per esempio lettura, scrittura,
   cancellazione, rinomina e lista;
5. dal PC client aprire il Command Prompt;
6. digitare `ftp indirizzo_server`;
7. inserire username e password;
8. usare comandi come `put`, `get`, `ls`, `rename`, `quit`.

Esercizio tipico: creare file su PC1, caricarli sul server FTP, rinominarli, accedere da PC2
e scaricarli, verificando che siano presenti sul secondo PC.

### Parole chiave

Applicazione distribuita, processo, user agent, protocollo applicativo, client-server,
server farm, virtualizzazione, peer-to-peer, P2P centralizzato, P2P ibrido, super-peer,
API, socket, HTTP, HTTPS, WWW, browser, web server, URI, URL, cache, FTP, FTPS,
SFTP, upload, download, modalita attiva, modalita passiva, SMTP, POP3, IMAP, MIME,
DHCP, lease, DNS, record, risoluzione dei nomi.

### Da integrare con le presentazioni

- Sequenza DORA del DHCP.
- Metodi e codici di stato HTTP.
- Differenze tra web mail, POP3 e IMAP.
- Tipi di record DNS.
- Esempi Packet Tracer su DHCP, DNS, SMTP/POP3 e WWW.

---

# Scheda 3

## MODULO III - Le Virtual Local Area Network (VLAN)

### Obiettivo del modulo

Studiare come le VLAN permettono di dividere logicamente una rete locale, migliorando
organizzazione, sicurezza e gestione del traffico broadcast.

### Argomenti da sviluppare

- VLAN untagged.
- VLAN tagged secondo IEEE 802.1Q.
- Access port e trunk port.
- Protocollo VTP.
- Inter-VLAN tradizionale.
- Inter-VLAN Router-on-a-stick.

### Schema sintetico iniziale

Una VLAN e una rete locale virtuale: consente di separare dispositivi collegati allo stesso
switch fisico come se appartenessero a reti diverse. Questa separazione riduce i domini di
broadcast e permette di organizzare la rete per reparti, funzioni o livelli di sicurezza.

Le porte access appartengono a una sola VLAN e sono usate di solito per collegare host
finali. Le porte trunk trasportano invece traffico di piu VLAN, usando il tagging 802.1Q per
identificare a quale VLAN appartiene ogni frame.

Per far comunicare VLAN diverse serve un dispositivo di livello 3, come un router o uno
switch multilayer. Le due soluzioni principali studiate sono l'inter-VLAN tradizionale e il
Router-on-a-stick.

### Parole chiave

VLAN, dominio di broadcast, access port, trunk port, tag 802.1Q, native VLAN, VTP,
inter-VLAN routing, Router-on-a-stick.

### Da integrare con le presentazioni

- Differenza precisa tra VLAN tagged e untagged.
- Comandi Packet Tracer/Cisco per creare VLAN e trunk.
- Configurazione delle subinterfacce nel Router-on-a-stick.
- Esempi di progettazione con piu reparti.

---

# Scheda 4

## MODULO IV - La sicurezza nelle reti: la protezione dei dati

### Obiettivo del modulo

Comprendere le tecniche crittografiche usate per proteggere i dati, garantendo
riservatezza, integrita, autenticazione e non ripudio.

### Argomenti da sviluppare

- Crittografia e algoritmi crittografici.
- Crittografia a chiave simmetrica.
- Algoritmi DES e AES.
- Crittografia a chiave asimmetrica.
- Chiave pubblica e chiave privata.
- Algoritmo RSA.
- Schema Diffie-Hellman per lo scambio delle chiavi.
- Crittografia ibrida.
- Funzione di hash.
- Firma digitale.
- Certificati digitali.
- Certification Authority, PKI e software PGP.

### Schema sintetico iniziale

La crittografia serve a trasformare un messaggio leggibile in un messaggio cifrato,
comprensibile solo da chi possiede la chiave corretta. Nella crittografia simmetrica la
stessa chiave viene usata per cifrare e decifrare; nella crittografia asimmetrica esistono
invece due chiavi collegate: una pubblica e una privata.

DES e AES sono algoritmi simmetrici: AES e oggi considerato piu sicuro e moderno.
RSA e un algoritmo asimmetrico usato per cifratura, autenticazione e firma digitale.
Diffie-Hellman permette a due soggetti di concordare una chiave condivisa anche su un
canale non sicuro.

La crittografia ibrida combina i vantaggi dei due approcci: usa la crittografia asimmetrica
per scambiare una chiave e la crittografia simmetrica per cifrare i dati in modo efficiente.

### Parole chiave

Cifratura, decifratura, chiave simmetrica, chiave pubblica, chiave privata, DES, AES, RSA,
Diffie-Hellman, hash, firma digitale, certificato digitale, CA, PKI, PGP.

### Da integrare con le presentazioni

- Esempi semplici di cifratura simmetrica e asimmetrica.
- Funzionamento della firma digitale passo per passo.
- Differenza tra hash, cifratura e firma.
- Catena di fiducia dei certificati digitali.
- Esempi con PGP/GPG in macchina virtuale.

---

# Scheda 5

## MODULO V - La sicurezza delle reti: la protezione della rete

### Obiettivo del modulo

Analizzare le principali minacce ai sistemi informatici e le tecnologie usate per proteggere
reti, servizi e comunicazioni.

### Argomenti da sviluppare

- Segretezza, integrita e disponibilita.
- Sicurezza dei sistemi informatici e minacce.
- S/MIME e PGP nella posta elettronica.
- Protocollo SSL/TLS.
- HTTPS e scambio delle chiavi.
- Certificati digitali dei web server.
- Firewall e packet filtering.
- Stateful inspection.
- Deep inspection o proxy server.
- Bastion host.
- DMZ.
- Sicurezza in IP: protocollo IPsec.
- Reti private virtuali: VPN.
- Intranet ed extranet.

### Schema sintetico iniziale

La sicurezza informatica si basa su tre concetti fondamentali: segretezza, integrita e
disponibilita. La segretezza impedisce l'accesso non autorizzato alle informazioni,
l'integrita garantisce che i dati non vengano modificati in modo illecito e la disponibilita
assicura che sistemi e servizi siano accessibili quando necessario.

SSL/TLS protegge le comunicazioni tra client e server e viene usato da HTTPS. I firewall
filtrano il traffico di rete applicando regole di sicurezza. Le tecniche possono essere piu o
meno profonde: packet filtering, stateful inspection e deep inspection.

La DMZ e una zona di rete separata in cui si collocano servizi esposti verso l'esterno, come
web server o mail server, riducendo il rischio per la rete interna. Le VPN permettono invece
di creare collegamenti sicuri su reti pubbliche.

### Parole chiave

CIA triad, segretezza, integrita, disponibilita, minaccia, vulnerabilita, SSL, TLS, HTTPS,
firewall, packet filtering, stateful inspection, proxy, bastion host, DMZ, IPsec, VPN,
intranet, extranet.

### Da integrare con le presentazioni

- Esempi di minacce e contromisure.
- Differenze tra firewall stateless, stateful e proxy.
- Schema di una rete con DMZ.
- Differenza tra VPN site-to-site e remote access.
- Collegamento tra TLS, certificati e HTTPS.

---

# Scheda 6

## MODULO VI - Filtraggio del traffico di rete e ACL

### Obiettivo del modulo

Capire come usare le Access Control List per filtrare il traffico e come NAT/PAT permettono
la comunicazione tra reti private e Internet.

### Argomenti da sviluppare

- ACL standard.
- Wildcard mask.
- ACL estese.
- NAT statico.
- NAT dinamico.
- NAT overload o PAT.

### Schema sintetico iniziale

Le ACL sono liste di regole usate sui router per permettere o negare traffico in base a
criteri specifici. Le ACL standard filtrano principalmente in base all'indirizzo IP sorgente,
mentre le ACL estese possono considerare anche indirizzo di destinazione, protocollo e
porte.

Le wildcard mask indicano quali bit dell'indirizzo devono essere controllati e quali possono
variare. Sono quindi fondamentali per scrivere regole corrette nelle ACL Cisco.

Il NAT traduce indirizzi privati in indirizzi pubblici. Nel NAT statico la corrispondenza e
fissa, nel NAT dinamico viene scelta da un pool di indirizzi pubblici, mentre il PAT permette
a molti host interni di condividere un unico indirizzo pubblico distinguendo le connessioni
tramite le porte.

### Parole chiave

ACL, permit, deny, wildcard mask, ACL standard, ACL estesa, sorgente, destinazione,
protocollo, porta, NAT statico, NAT dinamico, PAT, overload.

### Da integrare con le presentazioni

- Sintassi delle ACL standard ed estese.
- Regole di posizionamento delle ACL.
- Esempi Packet Tracer con ACL e NAT/PAT.
- Creazione di una DMZ con ACL e PAT.

---

# Scheda 7

## MODULO VII - Le reti wireless

### Obiettivo del modulo

Studiare il funzionamento delle reti senza fili, gli standard IEEE 802.11, i meccanismi di
accesso al mezzo, la sicurezza Wi-Fi e le principali architetture wireless.

### Argomenti da sviluppare

- Standard IEEE 802.11 a, b, g, n.
- Basi delle diverse modulazioni.
- Protocolli di sicurezza WPA, WPA2, WPA3.
- Autenticazione 802.1X.
- Server RADIUS.
- Trasmissione wireless: CSMA/CA e RTS/CTS.
- Handoff e problemi tipici della trasmissione wireless.
- Struttura del frame 802.11.
- Architettura delle reti wireless.
- BSS ed ESS.
- BSS-ID e SSID.
- Ruolo dell'access point e distribution system.
- Trasmissione cellulare.
- Connessione satellitare.
- GPS.

### Schema sintetico iniziale

Le reti wireless permettono la comunicazione senza cavi usando onde radio. Lo standard
IEEE 802.11 definisce il funzionamento delle reti Wi-Fi e comprende diverse versioni, come
802.11a, 802.11b, 802.11g e 802.11n, che differiscono per frequenze, velocita e tecniche di
modulazione.

Nel Wi-Fi non e possibile usare il CSMA/CD tipico delle reti Ethernet cablate, quindi si usa
CSMA/CA, che cerca di evitare le collisioni prima della trasmissione. RTS/CTS puo aiutare a
ridurre problemi come il nodo nascosto.

La sicurezza si e evoluta da protocolli meno robusti a soluzioni piu sicure come WPA2 e
WPA3. L'autenticazione 802.1X con server RADIUS consente un controllo centralizzato degli
accessi.

### Parole chiave

Wi-Fi, IEEE 802.11, modulazione, WPA, WPA2, WPA3, 802.1X, RADIUS, CSMA/CA,
RTS/CTS, handoff, frame 802.11, BSS, ESS, BSSID, SSID, access point, distribution system,
rete cellulare, satellite, GPS.

### Da integrare con le presentazioni

- Tabella comparativa 802.11a/b/g/n.
- Differenza tra SSID e BSSID.
- Struttura del frame 802.11.
- Problemi tipici: interferenze, attenuazione, nodo nascosto, handoff.
- Differenza tra Wi-Fi, rete cellulare, satellite e GPS.

---

# Scheda 8

## MODULO DI LABORATORIO

### Obiettivo del modulo

Raccogliere le esercitazioni pratiche svolte con Packet Tracer e con macchine virtuali,
collegandole agli argomenti teorici del programma.

### Attivita da organizzare

- Simulazione di reti client-server.
- Applicazioni del livello applicativo.
- DNS.
- FTP.
- SMTP/POP3.
- DHCP.
- WWW.
- Crittografia con PGP/GPG in macchina virtuale.
- VLAN tagged e untagged.
- NAT/PAT.
- Firewall.
- ACL standard ed estese.
- Creazione di una DMZ con ACL e PAT.

### Struttura consigliata per ogni esercitazione

Per ogni laboratorio si potra usare sempre lo stesso schema:

1. obiettivo dell'esercizio;
2. topologia di rete;
3. indirizzamento IP;
4. configurazione dei dispositivi;
5. test di funzionamento;
6. problemi incontrati e soluzione;
7. collegamento con la teoria.

### Da integrare con le presentazioni

- Screenshot o descrizioni delle topologie Packet Tracer.
- Tabelle di indirizzamento.
- Comandi principali usati sui dispositivi.
- Test finali: ping, browser, posta, FTP, DNS lookup.

---

# Scheda 9

## MODULO PER SECONDA PROVA ESAMI DI STATO

### Obiettivo del modulo

Preparare la parte progettuale della seconda prova, con attenzione al cablaggio
strutturato, ai mezzi trasmissivi, agli apparati di rete e alla progettazione di infrastrutture
coerenti con le richieste del testo.

### Argomenti da sviluppare

- Cablaggio strutturato.
- Cablaggio orizzontale e verticale secondo lo standard ISO/IEC 11801.
- Mezzi trasmissivi: doppino, fibra ottica, onde radio.
- Armadi rack.
- Dispositivi di comunicazione in rete.
- Esercizi di cablaggio.
- Simulazioni di progettazione di reti.

### Schema sintetico iniziale

Il cablaggio strutturato organizza l'infrastruttura fisica di rete in modo ordinato,
scalabile e manutenibile. Il cablaggio orizzontale collega gli armadi di piano alle prese
utente, mentre il cablaggio verticale collega tra loro i diversi piani o edifici, spesso usando
fibra ottica per distanze maggiori e migliori prestazioni.

Nella progettazione di una rete bisogna considerare numero di utenti, servizi richiesti,
separazione logica tramite VLAN, sicurezza, accesso a Internet, server interni, eventuale
DMZ, indirizzamento IP e dispositivi necessari.

### Parole chiave

Cablaggio strutturato, ISO/IEC 11801, cablaggio orizzontale, cablaggio verticale, doppino,
fibra ottica, onde radio, rack, switch, router, firewall, access point, patch panel,
progettazione di rete.

### Da integrare con le presentazioni

- Schema tipo per rispondere a una traccia di seconda prova.
- Tabelle per indirizzamento IP e subnetting.
- Criteri per scegliere switch, router, firewall e access point.
- Esempi di progetto con VLAN, NAT/PAT, ACL, DMZ e servizi interni.

---

# Indice di integrazione futuro

## Materiali da aggiungere modulo per modulo

- Presentazione Modulo I - Trasporto e UDP: integrata.
- Presentazione Modulo I - Trasferimento affidabile e TCP: integrata.
- Presentazione Modulo II - Livello applicazioni, WWW e FTP: integrata.
- Presentazione Modulo II - DHCP, HTTP dettagliato, posta e DNS: da integrare, se presenti.
- Presentazione Modulo III: da integrare.
- Presentazione Modulo IV: da integrare.
- Presentazione Modulo V: da integrare.
- Presentazione Modulo VI: da integrare.
- Presentazione Modulo VII: da integrare.
- Materiali di laboratorio: da integrare.
- Materiali per seconda prova: da integrare.

## Possibili collegamenti per l'orale

- Sicurezza informatica e tutela dei dati.
- Crittografia, privacy e comunicazioni sicure.
- Reti aziendali, VLAN, DMZ e protezione dei servizi.
- Internet, protocolli applicativi e infrastrutture digitali.
- Wireless, mobilita e comunicazioni moderne.
- Progettazione di rete e organizzazione dei sistemi informativi.
