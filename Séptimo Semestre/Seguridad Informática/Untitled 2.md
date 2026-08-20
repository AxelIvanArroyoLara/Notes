## Security Trends & OSI Security Architecture

La curva de aprendizaje de los atacantes ha ido a la baja respecto a la facilidad de ejecutar ataques sumamente poderosos. 

El sweeper escanea puertos, ips en masa. Una vez que se identifican, se lanza un ataque contra alguna vulnerabilidad específica. Por ejemplo, hay puertos que no pueden ser cerrados. Ataque desde A → internet → router / firewall / acl (bloquea o desbloquea puertos o ips) → lan → DMZ (zonas no protegidas porque eso cerraría la comunicación por completo) dns que mapea la ip como url (port 53), http / https / web server (80 / 443), smtp server (25), ftp server (20, 21) etc. Se debe añadir una capa extra de seguridad, como un IDS entre LAN y DMZ (para cada uno de los servers anteriores individualmente).

Morphing combina 2 o más imágenes en una sola imagen, buscando unificar las características biométricas de las personas para obtener acceso a ciertos sitios que requieran autenticación.

Se puede tener un IDS entre router y LAN que a su vez graba los ataques y los guarda como signatures.

## Security Mecanisms / Tech

- Firewall: Bloquea malware (adware, randomware, spyware, trojans, worms, viruses).
- Server ACL; IDS/IPS; SIEM: (Security information & event management, analyze security logs).
- Encryption: One-time password / token, multi-factor auth MFA & authorization.
- Forensic tools: (Wireshark, nmap), behavioral analytics; PKI
- Wireless security system: Biometrics, AI/ML, IoT Security, Blockchains, Cloud Security.

Encriptado simétrico: mismas claves.

Private / public keys para encriptado asimétrico. La única forma de desencriptar algo encriptado con la pública, es mediante la clave privada. La pública se puede spoofear.


## ITU Security Architecure:

- HTU-T X 800: Define una red para la OSI Sec Arch. Define una manera sistrmátics para proveer requerimientos de seguridad.
## Aspectos de Seguridad

Considera 3 aspectos de la información de seguridad:

- securitty attachs: cualquier acción que compromete la información de la seguridad.
- Security mechanisms: Diseñados para detectar, prevenir o reuperar algo de un ataque de seguridad.
- 

## Threat vs Attack

Threats es violación potencial de seguridad que PODRÍA causar daño y que comprometa la información.

Attack es la ejecución de la violación de seguridad.

Information security se refiere a la prevención de ataques o al menos detectarlos.

### Threats pasivos:

Intento de aprender o utilizar información del sistema, pero sin afectar los recursos. Es decir, solo leer la información o analizar el tráfico. Por esto son muy difíciles de identificar.

### Threats activos:

Intentos de modificar la información vulnerada. 

- Máscara: una entidad pretende ser otra diferente (un atacante diciendo que es un banco).
- Replay: Captura pasiva de los datos y transmisión posterior de la misma para lograr efectos no autorizados.
- Modification of messages: Una porción de los mensajes se ve alterada.
- Denial of service: Previene o inhibe la estructura que permite la comunicación.

## Friends and Enemies

Para mantener la información segura, se debe convertir el texto plano a un ciphertext, y para ello, se debe usar un algoritmo de encriptación. Asumimos que tenemos a un atacante (man in the middle) en medio del canal, que podría interceptar (pasivo), eliminar o cambiar los mensajes (activos).

## Security services:

- Mejorar la seguridad de los sistemas de procesamiento de datos y transferencia de información.
- Contraatacar ataques de seguridad.
- Utilizar uno o más mecanismos de seguridad.

Como recomendación, ITU T X.800 define un servicio de seguridad: un servicio provisto por una capa de protocolo para comunicar sistemas abiertos, lo que asegura una seguridad adecuada de los sistemas o transferencias de los datos.

Una definición más clara viene dada en RFC 2828 (Internet Security Glossary) (IEFT). "Un servicio de procesamiento o comunicación provisto por un sistema para dar un tipo específico de protección para recursos el sistema."

```
IETF
↓
RFC (Request For Comments)
```

## Security services (X.800)

1. Authentication: Verifica la identidad de la persona deseando accesar al sistema.
2. Access Control: Refiere a quién está autorizado para acceder a información de la organización.
3. Confidencialidad de datos: Protección de datos ante accesos no autorizadps.
4. Data integrity: Los datos permanecen en la forma en la que deberían, sin ser modificados de ninguna manera.
5. Non-Retaliation: Prevenir que uno de los miembros en la comunicación pueda negar que envió un mensaje.
6. Availability: El sistema siempre debe estar disponible, sin verse afectado por sabotajes o caídas.

## Security Mechanisms

Permite detectar, prevenir o recuperarse de un ataque de seguridad.

- Encipherment
- Data integrity
- Digital signatures
- Authentication exchange
- Traffic padding (Insertar información basura para despistar atacantes)
- Routing control (Seleccionar y cambiar contínuamente rutas disponibles entre el sender y el reciever para prevenir que los oponentes hagan eavesdropping en una ruta)
- Notarization (utilizar los servicios de un tercero para controlar la comunicación entre dos entidades)
- Access control (ACL)

Se requieren una serie de mecanismos de seguridad

## Security Planning: Plan Protect-Respond Cycle

La seguridad es un problema de gestión, no técnico. De no tener un manejo adecuado, la tecnología no es efectiva. 
Una compañía debe tener buenos procesos de seguridad y debe entonces desarrollar un plan de control de acceso para cada recurso (ISO 27001 ISMS): Framework para que las organiaciones puedan establecer, implementar, mantener e implementar contínuamente sus ISMS, para después proteger recursos de información sensibles, manejar riesgos, etc. 

Respond → Plan → Protect → Respond

The plan includes AAA protections:

- Authentication: Providing identity of the person wishing access
- Authorization: Determining what the person may do if he or she is authenticated
- Auditing: 