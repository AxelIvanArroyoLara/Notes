Los ataques pueden ser identificados con respecto en la capa en la que actúan. 

Los ataques pueden tener una serie de objetivos específicos, que utilizaremos para conocer el tipo de amenaza a detectar.

DNS (udlap.mx) or IP (192.168.0.1) spoofing, data alteration, phishing, malware, DoS, DDoS (TCP connection oriented, UDP), social engineering

http https, smtp, ftp, voip        Application Layer       messages
|        |
(port adresses)tcp udp      Transport layer         segments
    |  
    ip                                       datagrams
	|
  ethernet                                 frames
	|
physical medium                     bits


Offset reorganiza todos los datagramas y reconstruye originales.

Port numbers (tcp)

Se detectan errores mediante checksum y error detection (handshake) 

sync flag (header transport layer). Si no se recibe de regreso (half open connection)

DoS 

DDoS

## Cybersecurity threats

- Malware: Ransomware, worms, trojans, backdoors, spyware, botnets, pharming (DNS), device by attacks.
- Social engineering: Phishing, smishing, vishing, spare phishing, pod (ping of death -bits), zero day attack (signatures doesnt work)
- Infrastructure, Networks and Identity


Cybersecutity involves devices, data and infrastructure

Information security is about protecting only data with security services

## Security services

- Confidentiality: Encription / Criptography
- Integrity (no data alteration): Hashcodes (Cyclic Redundancy Code (CRC 32)). Signature (representación más pequeña de los datos originales) se concatena a datos. SHA(256)
Si se detectan errores, se usa backward (NAG. Transmitter fixes) / forward (Reciever fixes via redundant bits) error correction 
- Availability: Routing, distributed db, redundancy, ids / ips

(hay 3 más)

## The first principle

	The first principle in security is to "understand the threat environment and the organization security needs".

Cuidar las contraseñas, o mantener los servidores en servicio, etc. Se requiere CIA y otros servicios de seguridad:

- Authentication (biometrics, ids, multifactor)
- Non retaliation: No saber quién envía los datos (Hashcodes)
- Access control: Decidir quién entra y quién no

Existe:

- Information Security ---
- Network security
- Computer security
- Internet security (transmission) ---

Vamos a usar:
- Kali
- Wireshark
- Snort
- Engage Security URL
- Suricata URL
- BetterCap URL
- EtterCap URL
- TOR
- AirCrack URL
- Fragrouter
- Nmap
- hping3 (ping of death)

No se pueden cerrar los puertos http, https, dns, etc. Solo es posible hacerlo mediante IDS (además del Firewall)