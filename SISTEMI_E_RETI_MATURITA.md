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

UDP e TCP rappresentano due modi diversi di gestire la comunicazione:

- UDP e connectionless: non stabilisce una connessione prima dell'invio, non garantisce
  consegna, ordine o ritrasmissione dei segmenti.
- TCP e connection oriented: stabilisce una connessione logica, controlla il flusso,
  gestisce gli errori e garantisce una consegna affidabile.

Il three-way handshaking e la procedura con cui TCP apre una connessione:

1. il client invia un segmento SYN;
2. il server risponde con SYN-ACK;
3. il client conferma con ACK.

### Parole chiave

Segmento, porta, socket, affidabilita, ACK, ritrasmissione, UDP, TCP, SYN, ACK,
three-way handshaking.

### Da integrare con le presentazioni

- Struttura dell'header TCP e UDP.
- Differenze pratiche tra TCP e UDP.
- Esempi di servizi che usano TCP o UDP.
- Eventuali esercizi o domande tipiche d'esame.

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

### Parole chiave

Client-server, DHCP, lease, HTTP, URL, FTP, SMTP, POP3, IMAP, MIME, DNS, record,
risoluzione dei nomi.

### Da integrare con le presentazioni

- Sequenza DORA del DHCP.
- Metodi e codici di stato HTTP.
- Differenze tra web mail, POP3 e IMAP.
- Tipi di record DNS.
- Esempi Packet Tracer su DHCP, DNS, FTP, SMTP/POP3 e WWW.

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

- Presentazione Modulo I: da integrare.
- Presentazione Modulo II: da integrare.
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
