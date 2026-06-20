

### INTRODUCTION TO NETWORKS

Ens explica la diferència entre WAN I LAN.

| Aspect      | LAN                           | WAN                                      |
| ----------- | ----------------------------- | ---------------------------------------- |
| Size        | Small, localized area         | Larg, board area                         |
| Ownership   | Single person or organization | Multiple organizations/service providers |
| Speed       | High                          | Lower compared to LAN                    |
| Maintenance | Easier and less expensive     | Complex and costy                        |
| Example     | Home or office network        | The internet                             |

#### LAN
![[lan_1-1.png|500]]


#### WAN
![[wan-2.png]]


### NETWORK CONCEPTS

En aquest apartat veiem els models TCP/IP i OSI, com també els mètodes utilitzats per la transmissió de dades.

#### OSI MODEL - 7 layers

![[OSI 1.png|500]]

- Exemple of Sending a File Across Network Layers:
	When sending a file over a network, several steps occur across different layers of the network model. The process begins at the **Application Layer**, which initiates the file transfer request. Following this, the **Presentation Layer** encrypts the file to ensure its security during transmission. The **Session Layer** then establishes a communication session with the receiving device. At the **Transport Layer**, the file is broken down into segments to ensure error-free transmission. The **Network Layer** takes over to determine the best route for transferring the data across the network. Next, the **Data Link** Layer encapsulates the data into frames, preparing it for node-to-node delivery. Finally, the **Physical Layer** handles the actual transmission of bits over the physical medium, completing the process.

#### TCP/IP
![[TCP_IP.png|500]]

- Example of Accessing a Website: 
	When accessing a website, several layers of the TCP/IP model work together to facilitate the process. At the **Application Layer**, your browser utilizes HTTP to request the webpage. This request then moves to the **Transport Layer**, where TCP ensures the data is transferred reliably. The **Internet Layer** comes into play next, with IP taking charge of routing the data packets from our device to the web server. Finally, at the **Network Interface Layer**, the data is physically transmitted over the network, completing the connection that allows us to view the website.
#### OSI vs TCP/IP

![[OSI_vs_TCP-IP.png]]
#### Transmission

##### Types

- **Analog**. La informació es transmet mitjançant ones continues en el temps. Com exemple trobem una ona sonora convertida en variacions continues de voltatge.

- **Digital**. La informació es transmet mitjançant valors directes de 0 i 1 (bits). Com exemple podem trobar una secuencia de 100110100101 enviat per fibra òptica.
##### Modes

- **Simplex**. One way comunication
- **Half-duplex**. Two way communication but not simultaneously.
- **Full-duplex**. Two way communication simultaneously.
##### Media
- **Twisted pair**. Ethernet
- **Coaxial**. TV
- **Fiber optic**. 
- **Radio waves**. WiFi
- **Microwaves**. Satellite communications.
- **Infrared**. Short range communications like remote controls.

### COMPONENTS OF A NETWORK

| Component                             | Description                                               |
| ------------------------------------- | --------------------------------------------------------- |
| End devices                           | Computers, Smartphones, Tablets, IoT / Smart devices.     |
| Intermediary devices                  | Switches, Routers, Modems, Access Point                   |
| Network media and Software components | Cables, Protocols, Management and Firewalls software      |
| Servers                               | Web servers, File servers, Mail servers, Database servers |

### NETWORK COMMUNICATION

#### MAC Adresses - getmac

00:1A:2B:3C:4D:5E

Els primers 24 bits fan referència al OUI (Organizationally Unique Identifier) mentres que els ultims 24 son específics d'aquell device concret.

És utilitzada pels switches per saber a quin equipo li tenen que entregar el paquet.

El protocol ARP (Adress Resolution Protocol) és l'encarregat de d'associar una IP amb una adreça MAC.
#### IP Adresses - ipconfig

192.168.101.11

És una etiqueta numèrica que se li assigna a cada equip de la xarxa per tal que es pugui comunicar mitjançant TCP/IP.

Treballa en la capa 3 (Network Layer) del OSI Model.
#### Ports - netstat

22

És un número assignat a un servei o procés de la xarxa que principalment serveix per organitzar i dirigir el tràfic de xarxa de manera correcta i eficient.

Hi han números de ports que per conveni s'associen a serveis concrets com 80 - HTTP, 443 - HTTPS, 53 - DNS, 22 - SSH, etc.

Treballa en la capa 4 (Trasnport Layer) del OSI Model.


### DYNAMIC HOST CONFIGURATION PROTOCOL (DHCP)

És el prtocol encarregat d'automatitzar l'assignació de configuracions IP als nous equips de la xarxa. Aquest protocol consta de 4 fases:

| Step           | Description                                                                                                                            |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| 1. Discover    | When a device connects to the network, it broadcasts a DHCP Discover message to find availabe DHCP servers.                            |
| 2. Offer       | DHCP server of the network receive the discover message and responds with a DHCP Offer message, proposing an IP address to the client. |
| 3. Request     | The client receives the offer and replies with a DHCP Request message, indicating that it accepts the offered IP address.              |
| 4. Acknowledge | The DHCP server sends a DHCP Acknowledge message, confirming that the client has been assigned an IP address.                          |
Example:
![[DHCP-2.png]]

### NETWORK ADDRESS TRANSLATION (NAT)

#### Private vs Public Adresses

- Public IPs: Son identificadors unics globals asignats per el Internet Service Provider (ISP). Als equips que tinguin una ip pública s'hi pot accedir desde Internet.
- Private IPs: Son les ips utilitzades per les local networks i per tant, no s'hi pot accedir des de internet. per conveni els rangs de ips privades son: 0.0.0.0 to 10.255.255.255, 172.16.0.0 to 172.31.255.255, and 192.168.0.0 to 192.168.255.255

#### What is NAT?

![[NAT-2.png]]

#### Types of NAT

Existeixen diferents tipus de NAT, cada un dessenyat un funció de les necessitats de cada xarxa.

### Domain Name System (DNS)

#### DNS Hierarchy

| Layer                    | Description                   |
| ------------------------ | ----------------------------- |
| Root Servers             | The top of the DNS hierarchy. |
| Top-Level Domains (TLDs) | .com, .org, .net, .es, .uk    |
| Second-Level Domains     | example                       |
| Subdomains or Hostnames  | www                           |
![[DNS-2.png]]

#### DNS Resolution Process

![[DNS_Query_Process-2.png]]

### Internet Architecture


| Architecture  | Centralized                     | Scalability         | Ease of Management                 | Typicall Use Case                  |
| ------------- | ------------------------------- | ------------------- | ---------------------------------- | ---------------------------------- |
| P2P           | Decentralized (or partial)      | High(as peers grow) | Complex (no central control)       | File-sharing, blockchain           |
| Client-Server | Centralized                     | Moderate            | Easier(server-based)               | Websites, email services           |
| Hybrid        | Partially central               | Higher than C-S     | More complex management            | Messaging apps, video conferencing |
| Cloud         | Centralized in provider's infra | High                | Easier (outsourced)                | Cloud storage, SaaS, PaaS          |
| SDN           | Centralized control panel       | High(policy-driven) | Moderate (needs specialized tools) | Datacenters, large enterprises     |

#### Peer-to-peer (P2P)

![[Peer 2 Peer.png|600]]

#### Client-Server Architecture

![[Client_Server_Arch-1 1.png|600]]

A key component of this architecture is the tier model, which organizes server roles and responsibilities into layers. This enhances scalability and manageability, as well as security and performance.

- Single-Tier Architecture: the client, server, and database all reside on the same machine.
- Two-Tier Architecture: splits the application environment into a client and a server. The client handles the presentation layer, and the server manages the data layer.
- Three-Tier Architecture: In this model, the client manages the presentation layer, the application server handles all the business logic and processing, and the third tier is a database server.
- N-Tier Architecture: 
#### Hybrid Architecture

![[Hybrid_Architecture-1.png|600]]
#### Cloud

![[Cloud_Arch-1.png|600]]

#### Software-Defined

![[Software-Defined_Arch-1.png|600]]


### Wireless Networks

- Frequency Bands
	1. **2.4 GHz (Gigahertz)** – Used by older Wi-Fi standards (802.11b/g/n). Better at penetrating walls, but can be more prone to interference (e.g., microwaves, Bluetooth).
	2. **5 GHz** – Used by newer Wi-Fi standards (802.11a/n/ac/ax). Faster speeds, but shorter range.


### Network Security

El objectiu de la seguretat en xarxes és preservar els principis CIA: 

- Confidencialitat - Només els usuaris autoritzats poden veure les dades.
- Integritat - Les dades es mantenen exactes i sense modificacions no autoritzades.
- Els recursos de xarxa són accessibles quan es necessiten.

#### Firewalls

Firewalls enforce a set of rules (known as firewall policies or access control lists) to determine whether to allow or block specific traffic.

The open source router/firewall [pfSense](https://www.pfsense.org/). Its large number of plugins (known as "Packages") give it a range of capabilities.

- Packet Filtering Firewall: Examines source/destination IP, source/destination port, and protocol type. (Layer 3 and Layer 4)
- Stateful Inspection Firewall: Tracks the state of network connections.
- Application Layer Firewall (Proxy Firewall): Can inspect the actual content of traffic (e.g., HTTP requests) and block malicious requests. (Layer 7)
- Next-generatin Firewall: Combines stateful inspection with advanced features like deep packet inspection, intrusion detection/prevention, and application control.


#### Intrusion Detection and Prevention Systems (IDS/IPS)

An Intrusion Detection System (IDS) observes traffic or system events to identify malicious behavior or policy violations, generating alerts but not blocking the suspicious traffic. In contrast, an Intrusion Prevention System (IPS) operates similarly to an IDS but takes an additional step by preventing or rejecting malicious traffic in real time.

The widely used [Suricata](https://suricata.io/) software can function as both an IDS and an IPS. Here, we see the user enable a detection rule, then begin inline monitoring.

Es basen en Signature-based detection o Anomaly-based detection i trobem diferents tipus:

- Network-Based IDS/IPS: Hardware device or software solution placed at strategic points in the network to inspect all passing traffic. Example: A sensor connected to the core switch that monitors traffic within a data center.
- Host-Based IDS/IPS: Runs on individual hosts or devices, monitoring inbound/outbound traffic and system logs for suspicious behavior on that specific machine. Example: An antivirus or endpoint security agent installed on a server.
#### Best practices

- Define clear polices
- Regular update
- Monitor and Log Events
- Layered Security
- Periodic Penetration Testing


### Data Flow Example

En aquest apartat veiem diferentes situacions que es produeixen en el món de la informàtica i n'estudiem els passos que es produeixen a baix nivell.

1. Accessing the internet
2. Checking local network configuration (DHCP)
3. DNS Resolution
4. Data Encapsulation and Local Network Transmission
5. Network Address Translation (NAT)
6. Server Recieves the Request and Responds
7. Decapsulation and Display


![[Data_Flow-1-New.png]]