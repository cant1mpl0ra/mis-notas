## A) INTRODUCTION

### A.1 Network Traffic Analysis

-> Consisteix en examinar el tràfic  de ña nostra red per part dels professionals de seguretat. 

-> L'objectiu és detectar anomalies, "security threats", etc.

##### REQUIRED SKILS

- TCP/IP Stack and OSI Model
- Basic Network Concepts
- Common Ports and Protocols
- Concepts of IP Packets and Sublayers
- Protocol Transport Encapsulation

##### TOOLS

 - [tcpdump](https://www.tcpdump.org/)
 - [tshark](https://openwebinars.net/blog/tshark-que-es-y-primeros-pasos/#qu%C3%A9-es-tshark)
 - [wireshark](https://www.wireshark.org/)
 - [ngrep](https://en.wikipedia.org/wiki/Ngrep)
 - [tcpick](https://linux.die.net/man/8/tcpick)
 - [Network Taps](https://www.gigamon.com/resources/resource-library/white-paper/to-tap-or-to-span.html)
 - [Networking Span Ports](https://www.gigamon.com/resources/resource-library/white-paper/to-tap-or-to-span.html)
 - [Elastic Stack](https://www.elastic.co/es/elastic-stack)
 - [SIEMS](https://www.microsoft.com/es-es/security/business/security-101/what-is-siem#how-do-SIEM-tools-work)

##### PROCESS

1) Ingest traffic
2) Reduce noise by filtering
3) Analyze and explore
4) Detect the root issue
5) Fix and Monitor

### A.2 Networking Primer (Layers 1,2,3,4)

##### OSI MODEL VS TCP/IP MODEL

- 7: Layer Application (FTP,HTTP) --------------------------------------- 4) Application
- 6: Layer Presentation (JPG,PNG,SSL,TLS) ------------------------------ 4) Application
- 5: Layer Session (NetBIOS) --------------------------------------------- 4) Application
- 4: Layer Transport (TCP,UDP) ------------------------------------------- 3) Transport 
- 3: Layer Network (Router, L3 Switch) ----------------------------------- 2) Internet
- 2: Layer Data-Link (Switch,Bridge) -------------------------------------- 1) Link
- 1: Layer Physical (Network card) ---------------------------------------- 1) Link


![[z(7) OsivsTCPIPvsPDU.png|700]]

-> Protocol Data Unit ([PDU](https://www.youtube.com/watch?v=uA0E4zXjkqI&ab_channel=Cisco)) és un paquet de dades format per informació de control i dades encapsulades de cada cap del model OSI.

![[z(7) Protocol Data Unit.png|700]]

##### ADRESSING MECHANISMS

- [Mac-Address](https://www.youtube.com/watch?v=tcvTjQldnBI&ab_channel=freeCodeCamp.org) (layer 2)
- IP Addressing (layer 4): [IPv4](https://www.youtube.com/watch?v=eHV1aOnu7oM&ab_channel=NETWORKINGWITHH) (4 octets) and [IPv6](https://www.youtube.com/watch?v=Mo01x0LPxio&ab_channel=NETWORKINGWITHH) (16 octets)

##### TRANSPORT MECHANISMS (layer 4)

-> Aquesta capa dirigeix com s'encapsularà el tràfic i com s'enviarà als protocols de capa inferior ( IP-1- i MAC-2- ).

- TCP : Es considera un protocl més fiable, ja que permet la comprovació d'errors i realitza el handshake.
- UDP : És el protocol a utilitzar quan ens interessa una alta velocitat de transmissió i no ens importa si es perd algun paquet.

[Comparació entre TCP i UDP - 5min](https://www.youtube.com/watch?v=uwoD5YsGACg&ab_channel=PowerCertAnimatedVideos)

##### TCP 3-WAY HANDSHAKE

1) client sends a packet with a SYN flag.
2) server responds with another packet with a SYN flag and an ACK flag.
3) client responds with a packet including an ACK flag.

[Video-explicació de CISCO - 5min](https://www.youtube.com/watch?v=LyDqA-dAPW4&ab_channel=Cisco)

<details open>
<summary>How many layers does the OSI model have?</summary>
<br>
4
</details>

<details open>
<summary>How many layers are there in the TCP/IP model?</summary>
<br>
Well, you asked for it!
</details>

<details open>
<summary> True or False: Routers operate at layer 2 of the OSI model?</summary>
<br>
Well, you asked for it!
</details>

<details open>
<summary>What addressing mechanism is used at the Link Layer of the TCP/IP model?</summary>
<br>
Well, you asked for it!
</details>

<details open>
<summary>At what layer of the OSI model is a PDU encapsulated into a packet? ( the number )</summary>
<br>
Well, you asked for it!
</details>

<details open>
<summary>What addressing mechanism utilizes a 32-bit address?</summary>
<br>
Well, you asked for it!
</details>

<details open>
<summary>What Transport layer protocol is connection oriented?</summary>
<br>
Well, you asked for it!
</details>

<details open>
<summary>What Transport Layer protocol is considered unreliable?</summary>
<br>
Well, you asked for it!
</details>

<details open>
<summary>TCP's three-way handshake consists of 3 packets: 1. Syn, 2. Syn and ACK. 3. _? What is the final packet of the handshe</summary>
<br>
Well, you asked for it!
</details>

### A.3 Network Primer (Layers 5,6,7)

-> Al apartat anterior (A.2) hem vist com funciona una red a baix nivell (1,2,3,4); ara veurem a més alt nivell.

-> El Hypertext Transfer Protocol ([HTTP](https://www.youtube.com/watch?v=a-sBfyiXysI&ab_channel=ByteByteGo)) és un protocol de capa d'aplicació (7) el qual s'utilitza desde 1990. Aquest permet la transferència de dades, en text clar, entre un client i un servidor, mitjançant TCP. Treball en el port 80 i 8000.

##### HTTP METHODS
- HEAD
- GET
- POST
- PUT
- DELETE
- TRACE
- OPTIONS
- CONNECT

[Videoexplicació HTTP methods - 3min](https://www.youtube.com/watch?v=tkfVQK6UxDI&ab_channel=CuriousCode)

-> HTTP Secure (HTTPS) és una modificació del protocol HTTP dissenyat per a incorporar Transport Layer Security (TLS) o Secure Socket Layers (SSL) per a la seguretat de les dades. Treballa en el port 443 i 8443.

-> File Transfer Protocol ([FTP](https://www.youtube.com/watch?v=cH61SKWRg3U&ab_channel=TechClout)) és un protocol de capa d'aplicació que permet la transferència ràpida de dades entre dispositius informàtics. Treballa en els ports 20 i 21.

##### FTP COMMANDS
- USER
- PASS
- PORT
- PASV
- LIST
- CWD
- PWD
- SIZE
- RETR
- QUIT

-> Server Message Block (SMB) és un protocol molt vist en entorns empresarials de Windows. Aquest permet compartir recursos entre hosts en una red. Utilitza tcp com a mecanisme de transport i treballa en el port 445.

## B) ANALYSIS

### B.1) The Analysis Process

-> El nostre objectiu és proporcionar un procés repetible que puguem començar a utilitzar quan realitzem anàlisis de trànsit de red.

-> L'anàlisis de trànsit consisteix en examinar detalladament un event o procés, determinant el seu origen i impacte. Aquest es pot utilitzar per desencadenar precaucions i/o accions despecífiques per donar suport o prevenir futurs successos.

### B.2) Analysis in Practice
## C) TCPDUMP
### C.1) Tcpdump Fundamentals

## D) WIRESHARK

