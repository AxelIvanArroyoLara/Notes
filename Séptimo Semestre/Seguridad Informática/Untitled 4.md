## Hacking and Hackers

Hacking es ganar acceso no autorizado a un sistema o entrar por la fuerza a una computadora.

Un hacker es alguien que tiene conocimientos acerca de amenazas o ataques, habilidades y comprende las debilidades de un sistema de seguridad.

Los pentestings son legales siempre que se utilicen para hallar debilidades en una computadora o sistema de redes, con propósitos de prueba. Esto se conoce como Hacking ético.

Se pueden correr 2^{16} aplicaciones en una PC; sus direcciones están en la capa de transporte.

```
UDP/TCP
	↓
H_1 | DATA | ← SEGMENT
 ↓
(FLAGS, SP, DP), seq. numbers, ack. numbers
```

Al no poder cerrar todos los puertos, se debe definir un IDS.

```
npam
↓
open/close ports → Apps (2^16)
↓
DMZ
↓
DNS, HTTPS, SMTP, FTP

```

## Types of Hackers:

- White Hat: Se asume que nunca intentan dañar un sistema, sino encontrar debilidades en un sistema de red.
- Black Hat: Crackers, hackean para obtener acceso no autorizado
- Grey Hat:
- Blue Hat:
- Elite Hackers:
- Green Hat Hacker:

## Skills de Hacking Ético

```
TCP/IP

AL
TL
NL
DLL
PL
```

### Técnicas:

- Adivinación de contraseñas o cracking.
- Secuestro de sesiones (IP Spoofing). Existen clases de IP (A por ejemplo). Scappy, Hping3 o nmap. El atacante se introduce entre dos redes para recibir los mensajes enviados.
- Network traffic sniffing (Wireshark).
- DoS & DDoS attacks (sync flags).
- Explotar vulnerabilidades de overflow de buffer.

La bandera ACK debe indicar que ya recibió los datos previos y que está lista para recibir más datos:

```
A ───────────── DATA0 ─────────────► B
A ───────────── DATA1 ──────────────► B
A ───────────── DATA2 ──────────────► B
A ←────────────── ACK3 ───────────── B


A ───────────── DATA4 ─────────────► B
A ───────────── DATA5 ──────────────► B
A ───────────── DATA6 ──────────────► B
A ←────────────── ACK0 ───────────── B


A ───────────── FIN ─────────────► B
A ←──────────── ACK ────────────── B
A ←──────────── FIN ────────────── B
A ──────────── ACK0 ─────────────→ B

Solo se envía un ACK por conjunto de datos
```

Para esto se usan las *sliding windows*. Al enviar ACK se manda como $ACK_3$. Esto libera el buffer (ya no guarda los paquetes 0, 1 y 2).

Esto puede generar DoS por una half connection.

- SQL injections.

## Skills

- Computer systems expert.
- Strong programming and computer networking skills.
- A lot of patience and perceverance.
- Smart to understand situations.

## Intrusion Detection

IDS es cualquier combinación de hardware y software que monitorea un sistema o red para encontrar actividad maliciosa.

Si un IDS toma una medida preventiva sin intervención humana, entonces se convierte en un IPS. Un IDS proactivo detecta los ataques antes de que ocurran, y es lo deseable.

- Alarmas de auto.
- Detectores de fuego.
- Alarmas de casa.
- Sistemas de seguridad.

### - Approaches:

- Detección basada en firmas / reglas.
	- Ataques de red (reglas desarrolladas para detectar patrones ya utilizados).
	- Identificación de penetración: Un sistema experto que busca comportamientos sospechosos.
- Detección por anomalías estadísticas:
	- Threshold: Involucra definir tresholds (previenen falsos positivos), independientemente del usuario. Detecta anomalías en el tráfico respecto a su comportamiento normal (se puede usar con Neural Network approaches) llamado Profile of Normal Behaviour.
	- Profile based: Un perfil de la actividad de cada usuario (o red) se usa para detectar cambios en el comportamiento.

## IDS detectan NMAP

Los atacantes usar NMAP para aprender acerca de una red objetivo e identificar puertos abiertos, servicios expuestos y vulnerabilidades. Esto es un indicador previo al ataque.

Los IDS detectan Nmap:

- Detección basada en firmas:
	- Usa firmas predefinidas para encontrar patrones conocidos de tráfico Nmap.
	- Monitorea TCP flags.
- Análisis de comportamiento: Analiza tráfico de red (anomalías estadísticas) para hallar eventos anormales.
- Inspección profunda de paquetes (packet sniffing)
- Muchas organizaciones emplean IDS.
- Brindar alertas al administrador de la red en una forma proactiva.
	- Detección previa de amenazas.
	- Administrador puede mejorar seguridad de la red.
	- Investigación intensiva podría llevar a los atacantes.

Existen monitores basados en host o en red.

## IDS Sensors

- Firewall bloquea puertos o aplicaciones específicas (o crea Access Control List).

```
Internal network has app gateway 
↓
DMZ (web server, FTP server, Mail server, DNS server)
↓
Firewall
i
Internet
```

DMZ es una configuración de firewall para asegurar ,local area.

## Signature based IDS

- Sniff traffic:
	- Border router or multiple sensors in LAN
- Match sniffed traffic with signatures (no zero day):
	- attack signatures in db
	- signature: set of rules pertraining to a typical intrusion:
		- Any ICMP (network layer) (explicar) packet larger than 10,000 bytes.
		- More than 1000 SYN packets to different ports of same host under a seccond.
- Skilled engineers research known/new attacks; put them in database.
- Can configure IDS to exclude certain signatures; can modify signature parameters.
- Warn administrator when signature matches.
	- send e-mail, SMS.
	- Send message to network management system.