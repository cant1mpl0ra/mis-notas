
### Networking Overview

topologies (mesh/tree/star)
mediums (ethernet/fiber/coax/wireless)
protocol(TDP/UDP/IPX)


Pivoting around a network is not difficult, but doing it quickly and silently is tough and will slow attackers down.

### Network Types

- WAN
- LAN / WLAN
- VPN
### Networking Topologies

La Networking Topology determina com s'organitzaran els components de la red (hosts,servers,routers,etc). Es pot dividir en tres arees principals:

1. Connections (wired and wireless)
2. Nodes - Network Interface Controller (NICs)
3. Classification (Point-to-Point, Bus, Star, Ring, Mesh, etc)

### Proxies

A proxy is when a device or service sits in the middle of a connection and acts as a mediator.

There are many types of proxy services, but the key ones are:

- Dedicated Proxy / Forward Proxy

	For example, in a corporate network, sensitive computers may not have direct access to the Internet. To access a website, they must go through a proxy (or web filter).

	Another example of a Forward Proxy is Burp Suite, as most people utilize it to forward HTTP Requests.

	![[forward_proxy.png]]

- Reverse Proxy

	As you may have guessed, a reverse proxy, is the reverse of a Forward Proxy. Instead of being designed to filter outgoing requests, it filters incoming ones
	
	Many organizations use CloudFlare as they have a robust network that can withstand most DDOS Attacks. By using Cloudflare, organizations have a way to filter the amount (and type) of traffic that gets sent to their webservers.

	![[reverse_proxy.png]]

- Transparent Proxy
	
	És com el proxy de la caparrella o el huav que te capa certes webs sense tu interaccionar amb el proxy.

### Networking Models

OSI vs TCP/IP

![[net_models4_updated.png]]

Packet encapsulation / dencapsulation

![[packet_transfer.png]]

### Addressing - Network Layer

The network layer (Layer 3) of OSI controls the exchange of data packets, as these cannot be directly 
routed to the receiver and therefore have to be provided with routing nodes. 

When sending the packets, addresses are evaluated, and the data is routed through the network from node to node.

Els protocols més utilitzats en la tasca de ADRESSING son:

- IPv4
- IPsec
- ICMP
- RIP
- OSPF
### Addressing - IPv4 Addresses

Cada host de la red pot esser identificat per la seva MAC (Media Access Control) .

IPv4 Assets:

- Subnet Mask
- Network and Gateway Adresses
- Broadcast Adresses
### Addressing - Subnetting

El subnetting consisteix en dividir un rang d'adreces IPv4 en diferents rangs més petits d'adreces IPv4. 

If the network address is the same for the source and destination address, the data packet is delivered within the same subnet. If the network addresses are different, the data packet must be routed to another subnet via the default gateway.

### Addressing - MAC Adresses

És el "DNI" de cada equip de la xarxa.

### Addressing - IPv6 Addresses

Pràcticament no s'utilitza ja que amb el subetting han aconseguit reduir el ús de ips. També ha tingut molt a veure protocol NAT el qual permet que una red privada LAN sol gasti una IP publica.

### Networking Key Terminology

WEP, SSH, FTP, SMTP, HTTP, SMB, NFS, SNMP, WPA, TKIP, NTP, VLAN, VTP, RIP, OSPF, IGRP, EIGRP, PGP, NMTP, CDP, HSRP, VRRP, STP, TACACS, SIP, VOIP, EAP, LEAP, PEAP, SMS, MBSA, SCADA, VPN, IPsec, PPTP, NAT, CRLF, AJAX, ISAPI, URI, URL, IKE, GRE, RSH.
### Common Protocols

UDP
TCP
VoIP

### Wireless Networks

WAP, WEP, 
### Virtual Private Networks

Aquesta tecnologia permet establir conexions encriptades entre la red privada i un dispositius remot.

Els administradors de xarxa utilitzen aquesta tecnologia per conectar-se a la xarxa de l'empresa de manera segura i encriptada.

Protocols per establir conexions VPN:
- IPsec
- PPTP (Point-to-Point Tunneling Protocol) (deprecated)

### Vendor Specific Information

### Key Exchang Mechanism

### Authentication Protocols

### TCP/UDP Connections

### Cryptography
