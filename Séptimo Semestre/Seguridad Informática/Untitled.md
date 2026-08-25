Cada capa cumple una tarea distinta y agrega cierta información para que los datos puedan viajar desde una aplicación en una computadora hasta otra aplicación ubicada en otra computadora.

Esta organización también resulta fundamental para la ciberseguridad. Un atacante puede actuar sobre una capa concreta, aprovechar los campos de sus encabezados o atacar directamente alguno de sus protocolos. Por ello, cuando estudiemos un ataque, conviene formular cuatro preguntas:

1. ¿En qué capa ocurre?
2. ¿Qué protocolo, sistema o recurso aprovecha?
3. ¿Qué propiedad de seguridad intenta comprometer?
4. ¿Qué mecanismo puede prevenirlo, detectarlo o corregirlo?

La seguridad no comienza instalando una herramienta. Comienza comprendiendo qué necesita protegerse y qué amenazas existen.

---

## 1. Los ataques dentro del modelo TCP/IP

Recordemos el modelo TCP/IP de cinco capas:

```
┌──────────────────────────────────────────────────────────┐
│ CAPA DE APLICACIÓN                                       │
│ HTTP, HTTPS, DNS, SMTP, FTP, VoIP                        │
│ Unidad de datos: mensaje                                 │
├──────────────────────────────────────────────────────────┤
│ CAPA DE TRANSPORTE                                       │
│ TCP o UDP                                                │
│ Direcciones: puertos de origen y destino                 │
│ Unidad de datos: segmento TCP o datagrama UDP            │
├──────────────────────────────────────────────────────────┤
│ CAPA DE RED                                              │
│ IP                                                       │
│ Direcciones: IP de origen y destino                      │
│ Unidad de datos: datagrama o paquete IP                  │
├──────────────────────────────────────────────────────────┤
│ CAPA DE ENLACE                                           │
│ Ethernet o Wi-Fi                                         │
│ Direcciones: MAC de origen y destino                     │
│ Unidad de datos: trama                                   │
├──────────────────────────────────────────────────────────┤
│ CAPA FÍSICA                                              │
│ Cable, fibra óptica y ondas de radio                     │
│ Unidad de datos: bits representados mediante señales     │
└──────────────────────────────────────────────────────────┘
```

Un ataque puede clasificarse según la capa sobre la cual actúa, aunque algunos afectan varias capas simultáneamente.

| Capa       | Ejemplos de ataques o amenazas                                 |
| ---------- | -------------------------------------------------------------- |
| Aplicación | Phishing, malware, SQL injection, DNS spoofing y sitios falsos |
| Transporte | SYN flood, escaneo de puertos e inundaciones TCP o UDP         |
| Red        | IP spoofing, manipulación de rutas y ataques de fragmentación  |
| Enlace     | MAC spoofing, ARP spoofing e interceptación en una red local   |
| Física     | Corte de cables, interferencia, robo o destrucción de equipos  |

La capa donde observamos un ataque no siempre coincide con su objetivo final. Por ejemplo, el phishing ocurre principalmente en la capa de aplicación y explota a una persona, pero puede terminar proporcionando al atacante acceso a servidores, cuentas, bases de datos y redes completas.

---

## Protocolos de aplicación y sus puertos

En el pizarrón aparecen protocolos como HTTP, HTTPS, DNS, SMTP, FTP, VoIP y TFTP. Estos protocolos permiten que las aplicaciones se comuniquen.

Un protocolo es un conjunto de reglas. De la misma forma que dos personas necesitan compartir un idioma y ciertas normas de conversación, dos programas necesitan acordar cómo se construyen, envían e interpretan sus mensajes.

### HTTP y HTTPS

HTTP se utiliza para solicitar y enviar contenido web. Tradicionalmente, un servidor HTTP escucha en el puerto TCP 80.

HTTPS es una comunicación HTTP protegida mediante TLS. Normalmente utiliza el puerto TCP 443. TLS puede proporcionar:

- Confidencialidad, porque cifra la comunicación.
- Integridad, porque permite detectar modificaciones.
- Autenticación, porque ayuda a comprobar la identidad del servidor.

Por tanto, HTTPS no es simplemente “otro protocolo para páginas web”. Es HTTP transmitido dentro de un canal protegido criptográficamente.

### DNS

DNS traduce nombres fáciles de recordar a direcciones IP.

```
www.udlap.mx ──consulta DNS──► dirección IP del servidor
```

Sin DNS tendríamos que recordar las direcciones IP de todos los servidores que queremos visitar.

DNS utiliza habitualmente el puerto 53. Puede emplear UDP para muchas consultas ordinarias y TCP en casos como respuestas grandes, transferencias de zona y otras operaciones específicas.

### SMTP

SMTP se utiliza para enviar correo electrónico. El puerto TCP 25 se emplea tradicionalmente para la comunicación entre servidores de correo. También existen otros puertos, como el 587, para el envío autenticado desde un cliente.

### FTP

FTP es un protocolo clásico para transferir archivos. Su conexión de control utiliza normalmente el puerto TCP 21. En el modo activo tradicional, el puerto TCP 20 se relaciona con la conexión de datos.

FTP no cifra de forma nativa las credenciales ni los archivos. Tampoco debe confundirse con SFTP, que funciona sobre SSH y es un protocolo diferente.

### TFTP

TFTP es un protocolo muy sencillo de transferencia de archivos que normalmente utiliza UDP 69. Tiene menos funciones que FTP y no proporciona mecanismos modernos de autenticación o cifrado.

### VoIP

VoIP significa transmisión de voz mediante redes IP. No es un solo protocolo y, por tanto, no tiene un único puerto universal. Puede utilizar distintos protocolos para establecer llamadas y transportar el audio.

---

## 3. ¿Qué es un puerto?

Una dirección IP permite identificar un dispositivo o una interfaz de red, pero una computadora puede ejecutar numerosos programas al mismo tiempo. El número de puerto ayuda al sistema operativo a determinar a qué aplicación debe entregar los datos.

Podemos utilizar la siguiente analogía:

```
Dirección IP = dirección de un edificio
Puerto       = número de departamento
Aplicación   = persona que ocupa el departamento
```

Una comunicación TCP puede incluir:

```
IP de origen:       192.168.1.20
Puerto de origen:   51842

IP de destino:      203.0.113.50
Puerto de destino:  443
Protocolo:          TCP
```

El puerto de origen de un cliente suele ser un puerto temporal elegido por el sistema operativo. El puerto de destino suele corresponder al servicio solicitado.

Los encabezados de TCP y UDP reservan 16 bits para cada número de puerto. Como consecuencia, existen \(2^{16}\) valores posibles:

```
0 a 65535
```

Es importante distinguir entre la cantidad de valores y el valor máximo:

```
Cantidad de puertos posibles = 65 536
Puerto máximo                = 65 535
```

---

## 4. Encapsulación de la información

Cuando una aplicación produce información, las capas inferiores van agregando encabezados.

Supongamos que Alice escribe sus credenciales en el portal de su banco. La aplicación genera un mensaje. Después ocurre la encapsulación:

```
Capa de aplicación:
[ DATOS ]

Capa de transporte:
[ ENCABEZADO TCP | DATOS ]

Capa de red:
[ ENCABEZADO IP | ENCABEZADO TCP | DATOS ]

Capa de enlace:
[ ENCABEZADO ETHERNET | PAQUETE IP | TRÁILER ]

Capa física:
010010101101... representados mediante señales
```

En el encabezado TCP encontramos campos como:

- Puerto de origen.
- Puerto de destino.
- Número de secuencia.
- Número de confirmación.
- Banderas como SYN, ACK, RST y FIN.
- Tamaño de la ventana de recepción.
- Checksum.

En el encabezado IP encontramos:

- Dirección IP de origen.
- Dirección IP de destino.
- Información relacionada con la fragmentación.
- Límite de saltos.
- Identificación del protocolo transportado.

En la trama Ethernet encontramos normalmente:

- Dirección MAC de origen.
- Dirección MAC de destino.
- Identificación del protocolo transportado.
- Un código para detectar errores.

La capa física no agrega un “encabezado de bits”. Su función es representar los bits mediante señales eléctricas, luminosas o de radio.

---

## 5. Segmentación, fragmentación y offset

En los apuntes aparece la idea de que un _offset_ reorganiza los datagramas y reconstruye los originales. La intuición se relaciona con la reconstrucción de información, pero debemos distinguir dos procesos.

### Ordenamiento realizado por TCP

TCP divide un flujo de datos en segmentos y emplea números de secuencia para indicar la posición de la información.

Los segmentos no necesariamente recorren el mismo camino ni llegan en el mismo orden en que fueron enviados.

```
Orden de envío:
segmento 1 → segmento 2 → segmento 3

Orden de llegada:
segmento 2 → segmento 1 → segmento 3

Orden entregado a la aplicación:
segmento 1 → segmento 2 → segmento 3
```

Los números de secuencia permiten:

- Colocar la información en orden.
- Identificar datos faltantes.
- Reconocer datos duplicados.
- Solicitar o realizar retransmisiones.

### Fragmentación de un datagrama IP

Un datagrama IP puede ser demasiado grande para alguno de los enlaces por los que debe pasar. En IPv4, puede dividirse en fragmentos.

Cada fragmento contiene información que permite saber:

- A qué datagrama original pertenece.
- Qué posición ocupa.
- Si todavía existen más fragmentos.

El campo **fragment offset** indica la posición relativa del fragmento dentro del datagrama original.

Por tanto:

```
Números de secuencia TCP
→ ordenan el flujo transportado por TCP.

Fragment offset de IPv4
→ ayuda a reensamblar los fragmentos de un datagrama IP.
```

El offset no reorganiza todos los datagramas de Internet. Solo participa en el reensamblado de fragmentos pertenecientes a un mismo datagrama.

---

## 6. TCP como protocolo orientado a conexión

TCP se denomina orientado a conexión porque, antes de intercambiar datos, normalmente establece una relación lógica entre los extremos.

Esto no significa que se construya un cable exclusivo entre las computadoras. Significa que ambos sistemas mantienen información en memoria sobre el estado de la comunicación.

### El three-way handshake

La apertura de una conexión TCP se realiza normalmente mediante tres mensajes:

```
Cliente A                                      Servidor B

   ─────────────── SYN ─────────────────────────►
       “Quiero iniciar una conexión”

   ◄────────── SYN + ACK ───────────────────────
       “Recibí tu solicitud y también estoy listo”

   ─────────────── ACK ─────────────────────────►
       “Confirmo tu respuesta”

                 CONEXIÓN ESTABLECIDA
```

A este intercambio se le conoce como **three-way handshake** o saludo de tres pasos.

### Banderas TCP

Las banderas que aparecen en las fotografías del pizarrón tienen las siguientes funciones:

- **SYN:** inicia la conexión y sincroniza los números de secuencia.
- **ACK:** indica que el campo de confirmación es válido.
- **FIN:** solicita cerrar ordenadamente una dirección de la conexión.
- **RST:** reinicia o rechaza inmediatamente una conexión.
- **URG:** indica que existen datos marcados como urgentes.
- **PSH:** solicita que los datos sean entregados pronto a la aplicación.

Después del handshake comienza el intercambio de datos:

```
A ───────────── DATA ─────────────► B
A ◄───────────── ACK ────────────── B

A ◄──────────── DATA ────────────── B
A ────────────── ACK ─────────────► B
```

TCP utiliza confirmaciones acumulativas. Un ACK puede indicar que se recibieron correctamente todos los bytes anteriores a cierto número y que el receptor espera el siguiente.

---

## 7. Conexiones semiabiertas

Después de recibir un SYN, el servidor responde con SYN+ACK y reserva temporalmente recursos para la conexión.

Si nunca recibe el ACK final, queda temporalmente una conexión semiabierta o _half-open_:

```
Cliente o atacante                              Servidor

   ───────────── SYN ────────────────────────────►
   ◄────────── SYN + ACK ─────────────────────────

   El ACK final nunca llega.
   El servidor conserva temporalmente el estado.
```

Una conexión semiabierta aislada puede aparecer por una falla legítima. Por ejemplo, el cliente puede perder la conexión a Internet antes de enviar el último ACK.

El problema aparece cuando un atacante crea una cantidad enorme de conexiones incompletas.

---

## 8. SYN flood

Un **SYN flood** es una forma de denegación de servicio que abusa del proceso de apertura de TCP.

El atacante envía numerosos SYN, pero no completa correctamente el handshake:

```
             SYN ─────►
Atacante     SYN ─────►
             SYN ─────►  Servidor
             SYN ─────►  [muchas conexiones pendientes]
             SYN ─────►
```

El servidor responde con SYN+ACK y mantiene temporalmente información sobre cada conexión. Si la cantidad de solicitudes es suficientemente grande, puede quedarse sin espacio o capacidad para atender conexiones legítimas.

El objetivo principal de este ataque es comprometer la **disponibilidad**.

Entre las defensas posibles encontramos:

- SYN cookies.
- Límites de solicitudes.
- Reducción del tiempo de espera.
- Filtrado de direcciones falsificadas.
- Firewalls e IPS.
- Balanceadores de carga.
- Servicios de mitigación DDoS.

---

## 9. DoS y DDoS

### DoS

DoS significa _Denial of Service_ o denegación de servicio. Busca impedir que los usuarios legítimos accedan a un sistema, aplicación o red.

```
Una fuente atacante ─────────► servidor víctima
```

Un DoS no tiene que utilizar TCP. Puede buscar consumir:

- Ancho de banda.
- Memoria.
- Procesador.
- Espacio de almacenamiento.
- Conexiones disponibles.
- Recursos de una aplicación.
- Capacidad de un firewall o router.

### DDoS

DDoS significa _Distributed Denial of Service_. En este caso, el ataque proviene de numerosas máquinas distribuidas:

```
Equipo comprometido 1 ─┐
Equipo comprometido 2 ─┤
Equipo comprometido 3 ─┼────► servidor víctima
Equipo comprometido 4 ─┤
Equipo comprometido 5 ─┘
```

Estas máquinas pueden pertenecer a una botnet. Al proceder el tráfico de numerosos lugares, bloquearlo resulta más complicado. Una regla demasiado agresiva también podría bloquear usuarios legítimos.

La diferencia fundamental es:

```
DoS  = una o pocas fuentes atacantes
DDoS = muchas fuentes distribuidas
```

Un ataque también puede abusar de conexiones TCP completas. En ese caso, el atacante termina el handshake y después envía solicitudes que consumen muchos recursos.

Por tanto, debemos distinguir:

- **Half-open attack:** deja numerosas conexiones pendientes.
- **Full-open attack:** establece las conexiones y después abusa del servicio.

---

## 10. UDP y las inundaciones de tráfico

UDP es un protocolo no orientado a conexión. No realiza el three-way handshake de TCP.

```
Emisor ───────── datagrama UDP ─────────► receptor
```

UDP tampoco garantiza por sí mismo:

- Que el datagrama llegue.
- Que llegue una sola vez.
- Que llegue en orden.
- Que se retransmita si se pierde.

Esta sencillez reduce la sobrecarga y resulta útil en aplicaciones sensibles al tiempo, como voz, video, juegos y muchas consultas DNS.

Sin embargo, también facilita ciertas inundaciones, porque el emisor no necesita establecer previamente una conexión.

Un UDP flood puede consumir:

- El ancho de banda de la víctima.
- La capacidad de procesamiento.
- Los recursos del firewall.
- Los recursos de una aplicación UDP.

Esto no significa que UDP sea inseguro por naturaleza. Significa que ofrece menos funciones de confiabilidad que TCP y que la aplicación debe implementar cualquier propiedad adicional que necesite.

---

## 11. Checksum y detección de errores

Los datos pueden corromperse durante su transmisión debido a ruido, fallas del medio o problemas de hardware.

TCP, UDP e IP utilizan o pueden utilizar checksums para detectar determinados errores.

El procedimiento general es:

```
Emisor:
datos ──cálculo──► checksum

Transmisión:
[ datos | checksum ]

Receptor:
datos recibidos ──mismo cálculo──► resultado
```

Si el resultado calculado por el receptor no coincide con el valor recibido, se detecta que ocurrió alguna alteración.

Sin embargo, un checksum convencional está pensado principalmente para errores accidentales. No ofrece suficiente protección frente a un atacante, porque este podría modificar los datos y calcular nuevamente el checksum.

El handshake de TCP tampoco es un mecanismo general de detección de errores en los bits. Su propósito principal es establecer la conexión y sincronizar el estado de los extremos.

TCP utiliza conjuntamente:

- Checksum para detectar determinadas alteraciones accidentales.
- Números de secuencia para ordenar la información.
- ACK para confirmar recepción.
- Temporizadores para reconocer posibles pérdidas.
- Retransmisiones para recuperar información no recibida.

---

## 12. CRC

CRC significa _Cyclic Redundancy Check_. Ethernet utiliza una comprobación de redundancia cíclica para detectar errores dentro de una trama.

CRC-32 produce un valor de 32 bits. Es muy útil para detectar errores accidentales, pero no es una función hash criptográfica.

Un atacante que modifica intencionalmente los datos también puede calcular un CRC válido para los nuevos datos.

La diferencia esencial es:

```
CRC o checksum convencional
→ detecta principalmente errores accidentales.

Hash criptográfico
→ está diseñado para resistir manipulaciones intencionales.

HMAC o firma digital
→ permite verificar integridad y autenticidad.
```

---

## 13. Corrección de errores backward y forward

Detectar un error no significa necesariamente poder corregirlo. Existen dos enfoques generales.

### Backward Error Correction

Consiste en solicitar o realizar una retransmisión cuando la información no llega correctamente. También se conoce como ARQ.

```
Emisor ───────── datos dañados ─────────► receptor
Emisor ◄──────── NACK o falta de ACK ─── receptor
Emisor ───────── retransmisión ─────────► receptor
```

NACK significa confirmación negativa. Sin embargo, TCP normalmente se basa en ACK, ACK duplicados, temporizadores y retransmisiones, no en un NACK general con ese nombre.

### Forward Error Correction

En este enfoque, el emisor añade suficientes bits redundantes para que el receptor pueda corregir cierta cantidad de errores sin solicitar otra transmisión.

```
Datos originales + redundancia ─────────► receptor
                                             │
                                      corrige el error
```

Este método resulta útil cuando retransmitir sería lento o imposible, por ejemplo:

- Comunicaciones satelitales.
- Transmisiones en tiempo real.
- Señales inalámbricas con pérdidas.
- Sistemas donde el emisor no puede repetir la información.

---

## 14. Hashes criptográficos

Una función hash criptográfica recibe información de cualquier tamaño y produce un resumen de tamaño fijo:

```
Mensaje de cualquier tamaño
             │
             ▼
          SHA-256
             │
             ▼
Resumen de 256 bits
```

A este resultado se le llama:

- Hash.
- Digest.
- Resumen.
- Huella digital.

Si el mensaje cambia ligeramente, el resultado también debería cambiar de manera significativa.

```
“Transferir $100” → hash A
“Transferir $900” → hash completamente diferente
```

SHA-256 genera un resumen de 256 bits. A diferencia de CRC-32, está diseñado para resistir ataques deliberados.

Sin embargo, enviar simplemente esto no basta:

```
[ mensaje | hash ]
```

Un atacante podría modificar el mensaje y calcular un hash nuevo. Para protegerse contra esa posibilidad necesitamos una clave secreta o una firma digital.

---

## 15. HMAC y firmas digitales

### Código de autenticación de mensajes

Un MAC criptográfico, como HMAC, combina los datos con una clave secreta.

Solo quienes conocen esa clave pueden generar correctamente el código. Esto ayuda a comprobar:

- Que los datos no fueron modificados.
- Que fueron producidos por una entidad que conoce la clave.

### Firma digital

Para generar una firma digital, el emisor utiliza su clave privada. Habitualmente se calcula primero un hash del mensaje y luego se aplica la operación de firma:

```
Mensaje ──► SHA-256 ──► resumen
                           │
                    clave privada
                           │
                           ▼
                         firma
```

El receptor utiliza la clave pública correspondiente para verificarla.

La firma digital no es simplemente una “versión más pequeña de los datos”. El hash es el resumen compacto. La firma es un valor criptográfico que relaciona el mensaje con la clave privada del firmante.

---

## 16. Spoofing

_Spoofing_ significa falsificación o suplantación. El atacante intenta que determinada información parezca provenir de una fuente distinta.

### DNS spoofing

En DNS spoofing, la víctima recibe una respuesta DNS falsa o manipulada.

```
Víctima:
“¿Cuál es la dirección de banco.example?”

Respuesta legítima:
203.0.113.10

Respuesta falsificada:
198.51.100.66  ← servidor controlado por el atacante
```

La víctima puede escribir correctamente el dominio y aun así ser dirigida hacia otro servidor.

### IP spoofing

En IP spoofing, el atacante coloca una dirección de origen falsa en el encabezado IP.

Es parecido a enviar una carta escribiendo en el sobre la dirección de otra persona.

Esto no significa automáticamente que el atacante pueda recibir la respuesta. Por ello se utiliza principalmente cuando:

- No necesita recibir una respuesta.
- Busca ocultar el origen.
- Participa en un ataque de reflexión.
- Intenta engañar algún filtro basado únicamente en direcciones.

Completar una conexión TCP convencional con una dirección falsa es más difícil, porque la respuesta SYN+ACK se dirige hacia la dirección suplantada.

### MAC spoofing

En MAC spoofing, un dispositivo utiliza una dirección MAC diferente de la que normalmente tiene asignada.

### ARP spoofing

ARP relaciona direcciones IP con direcciones MAC dentro de una red local. En ARP spoofing, el atacante envía información falsa para conseguir que otros dispositivos asocien su dirección MAC con la IP de otro equipo, como el router.

Esto puede permitirle interceptar o redirigir tráfico dentro de la red local.

---

## 17. Eavesdropping y alteración de datos

### Eavesdropping

_Eavesdropping_ significa escucha clandestina. Un atacante observa una comunicación sin autorización.

Si la comunicación no está cifrada, podría obtener:

- Contraseñas.
- Correos.
- Archivos.
- Consultas DNS.
- Información personal.
- Datos sobre los sistemas utilizados.

Es principalmente un ataque pasivo contra la confidencialidad.

### Data alteration

La alteración de datos ocurre cuando alguien modifica información sin autorización.

Ejemplos:

- Cambiar el monto de una transferencia.
- Modificar una calificación.
- Alterar una dirección de entrega.
- Manipular un archivo descargado.
- Modificar una respuesta DNS.

La propiedad afectada es principalmente la integridad.

---

## 18. Phishing e ingeniería social

Phishing es un engaño diseñado para provocar que la víctima revele información o ejecute una acción.

```
“Detectamos un problema con tu cuenta.
Inicia sesión inmediatamente mediante este enlace.”
```

El enlace puede llevar a una página que imita la apariencia de una organización legítima.

### Variantes del phishing

- **Spear phishing:** ataque dirigido a una persona u organización específica.
- **Smishing:** phishing mediante SMS o mensajes de texto.
- **Vishing:** engaño mediante llamadas o mensajes de voz.
- **Pretexting:** construcción de una historia o identidad falsa para obtener la confianza de la víctima.

El término correcto es **spear phishing**, no “spare phishing”.

La ingeniería social explota características humanas como:

- Urgencia.
- Miedo.
- Autoridad.
- Curiosidad.
- Confianza.
- Deseo de ayudar.
- Promesas de premios.

Ejemplo:

```
Atacante:
“Soy del área de sistemas. Necesito tu código de
autenticación para reparar tu cuenta.”

Víctima:
Entrega un código válido.

Resultado:
El atacante evita los controles técnicos manipulando
a la persona.
```

---

## 19. Pharming

Pharming consiste en redirigir automáticamente a los usuarios hacia un sitio falso. Esto puede conseguirse manipulando DNS o el archivo local de nombres del dispositivo.

La diferencia con phishing es:

```
Phishing
→ convence a la víctima para abrir un enlace o entregar datos.

Pharming
→ altera la resolución para redirigirla automáticamente.
```

En ambos casos, la víctima puede terminar en un sitio falso, pero el mecanismo utilizado es diferente.

---

## 20. Malware

Malware significa software malicioso. Es una categoría general que incluye diferentes tipos de programas.

### Ransomware

Cifra o bloquea la información y exige un pago para recuperarla.

### Gusano

Se propaga automáticamente entre sistemas o redes, normalmente aprovechando vulnerabilidades.

### Troyano

Aparenta ser un programa legítimo, pero ejecuta acciones maliciosas.

### Backdoor

Crea un acceso oculto que evita el procedimiento normal de autenticación.

### Spyware

Recopila información sobre el usuario y la envía a otra entidad sin autorización adecuada.

### Bot

Convierte un dispositivo en una máquina que puede ser controlada remotamente.

### Botnet

Es una red de numerosos dispositivos comprometidos y controlados por un operador. Puede utilizarse para DDoS, envío de spam, robo de información o distribución de malware.

### Cryptojacking

Utiliza los recursos de procesamiento de la víctima para minar criptomonedas sin autorización.

### Drive-by attack

Un _drive-by attack_ intenta descargar o ejecutar contenido malicioso cuando el usuario visita un sitio comprometido.

El término correcto es **drive-by attack**, no “device by attack”.

---

## 21. Vulnerabilidades zero-day

Una vulnerabilidad _zero-day_ es una falla que se explota antes de que exista una corrección disponible o antes de que los defensores tengan tiempo suficiente para responder.

Un detector basado exclusivamente en firmas puede fallar porque todavía no existe una firma conocida para el nuevo ataque.

Por eso se combinan diferentes técnicas:

- Firmas.
- Detección de anomalías.
- Análisis de comportamiento.
- Aislamiento.
- Mínimos privilegios.
- Actualizaciones.
- Monitoreo.
- Segmentación de redes.

Un zero-day no es una forma de ingeniería social. Es una condición relacionada con una vulnerabilidad desconocida o todavía no corregida.

---

## 22. Ping of Death

El Ping of Death es un ataque histórico que enviaba paquetes IP o ICMP malformados o fragmentados de modo que, al reensamblarse, superaban el tamaño permitido.

Algunos sistemas antiguos manejaban incorrectamente estos paquetes y podían bloquearse.

No significa simplemente “enviar muchos pings”. Eso sería una inundación ICMP. El Ping of Death clásico se relaciona con paquetes inválidos, fragmentación y errores en el reensamblado.

Los sistemas modernos normalmente están protegidos contra su versión clásica.

---

## 23. Ciberseguridad y seguridad de la información

### Ciberseguridad

La ciberseguridad protege un ecosistema amplio:

```
Dispositivos + redes + aplicaciones + identidades
+ infraestructura + servicios + datos
```

Incluye computadoras, teléfonos, servidores, routers, cuentas, programas, sistemas industriales y servicios digitales.

### Seguridad de la información

La seguridad de la información se concentra en proteger la información, sin importar su medio.

Puede tratarse de:

- Archivos digitales.
- Expedientes impresos.
- Contratos.
- Conversaciones.
- Diseños.
- Bases de datos.
- Credenciales.

Por tanto, no debemos decir que la seguridad de la información protege únicamente datos digitales. Su alcance puede incluir cualquier forma de información.

---

## 24. Los seis servicios de seguridad

En el pizarrón aparecen seis servicios:

```
1. Confidencialidad
2. Integridad
3. Disponibilidad
4. Autenticación
5. Control de acceso
6. No repudio
```

### Confidencialidad

Busca que la información solo pueda ser conocida por entidades autorizadas.

Mecanismos:

- Cifrado.
- Gestión de claves.
- Permisos.
- VPN.
- Segmentación.
- Protocolos como TLS.

### Integridad

Busca impedir o detectar modificaciones no autorizadas.

Mecanismos:

- Hashes criptográficos.
- HMAC.
- Firmas digitales.
- Registros de auditoría.
- Control de versiones.

CRC y los checksums convencionales ayudan con errores accidentales, pero no ofrecen por sí solos integridad criptográfica frente a un atacante.

### Disponibilidad

Busca que los sistemas y la información estén accesibles cuando los usuarios autorizados los necesiten.

Mecanismos:

- Redundancia.
- Respaldos.
- Balanceo de carga.
- Bases de datos replicadas.
- Rutas alternativas.
- Protección contra DDoS.
- Monitoreo.
- Planes de recuperación.
- IDS e IPS.

### Autenticación

Permite comprobar la identidad de una persona, sistema o servidor.

Los factores se dividen normalmente en:

```
Algo que sabes:   contraseña o PIN
Algo que tienes:  teléfono, token o llave física
Algo que eres:    rostro, huella u otra biometría
```

La autenticación multifactor combina factores de categorías diferentes. Dos contraseñas siguen siendo dos elementos de “algo que sabes”, por lo que no constituyen verdadera autenticación multifactor.

### Control de acceso

Decide qué puede hacer una identidad después de haber sido autenticada.

```
Autenticación:
“¿Quién eres?”

Autorización o control de acceso:
“¿Qué tienes permitido hacer?”
```

Una persona puede iniciar sesión correctamente y no tener permiso para consultar nóminas, modificar calificaciones o administrar servidores.

### No repudio

El término correcto es **no repudio**, no “non-retaliation”.

Busca proporcionar evidencia para que una entidad no pueda negar razonablemente haber realizado una acción.

Una firma digital puede contribuir al no repudio cuando también existen:

- Identidades verificadas.
- Certificados.
- Protección de claves privadas.
- Registros confiables.
- Procedimientos adecuados.

El no repudio no significa ocultar quién envió los datos. Eso correspondería al anonimato o la privacidad. Tampoco se consigue mediante un hash aislado.

---

## 25. Servicios y mecanismos de seguridad

Un servicio expresa el objetivo que queremos conseguir. Un mecanismo indica cómo intentamos conseguirlo.

| Servicio          | Mecanismos posibles                        |
| ----------------- | ------------------------------------------ |
| Confidencialidad  | Cifrado, permisos y VPN                    |
| Integridad        | HMAC, hashes y firmas digitales            |
| Disponibilidad    | Redundancia, balanceo y mitigación DDoS    |
| Autenticación     | Contraseñas, biometría, MFA y certificados |
| Control de acceso | Roles, permisos, ACL y políticas           |
| No repudio        | Firmas digitales, certificados y registros |

Una misma tecnología puede apoyar varios servicios. TLS, por ejemplo, puede proporcionar confidencialidad, integridad y autenticación del servidor.

---

## 26. El primer principio de seguridad

El primer principio presentado en clase consiste en comprender las necesidades de seguridad de la organización. Para conseguirlo, se debe conocer también su entorno de amenazas.

No todas las organizaciones tienen las mismas prioridades.

En una universidad puede ser importante:

- Impedir cambios no autorizados en calificaciones.
- Proteger los datos personales.
- Mantener disponible la plataforma académica.
- Controlar el acceso a laboratorios.
- Proteger la investigación.

En un hospital puede ser especialmente importante:

- Mantener disponibles los sistemas clínicos.
- Proteger los expedientes médicos.
- Identificar correctamente a pacientes y médicos.
- Conservar evidencia de los cambios.
- Evitar alteraciones en tratamientos.

Por eso no existe una herramienta única que resuelva todos los problemas. Primero se identifican:

```
Activos → amenazas → vulnerabilidades → consecuencias
```

Después se seleccionan los controles apropiados.

---

## 27. Áreas de la seguridad

### Seguridad de la información

Protege la información y los recursos relacionados con ella.

### Seguridad de redes

Protege los datos durante su transmisión y los dispositivos que hacen posible la comunicación.

### Seguridad informática

Comprende las herramientas y medidas para proteger computadoras, sistemas operativos, archivos y programas.

### Seguridad de Internet

Protege los datos cuando atraviesan una colección de redes interconectadas.

Estas áreas se superponen. Una transferencia bancaria por Internet involucra simultáneamente:

- Seguridad de la información.
- Seguridad del dispositivo.
- Seguridad de la red.
- Seguridad del servidor.
- Seguridad de Internet.
- Seguridad de la identidad.

El objetivo general del curso puede resumirse así:

```
PREVENIR ─────────► DETECTAR ─────────► CORREGIR
```

Prevenir significa reducir la probabilidad de una violación. Detectar significa descubrir una actividad sospechosa. Corregir significa contener el incidente, recuperar el servicio y reducir la posibilidad de repetición.

---

## 28. Firewall, IDS e IPS

En los apuntes aparece la idea de que no podemos cerrar puertos esenciales como HTTP, HTTPS o DNS.

La interpretación correcta es que una organización no puede cerrar indiscriminadamente los puertos que necesita para proporcionar sus servicios.

Si un servidor web debe atender usuarios, tiene que aceptar tráfico en el puerto correspondiente. Cerrar el puerto 443 evitaría los ataques dirigidos a ese servicio, pero también impediría que los clientes utilizaran el sitio.

Sin embargo, sí deben cerrarse todos los puertos innecesarios.

### Firewall

Un firewall aplica reglas para permitir o bloquear tráfico.

Ejemplos:

```
Permitir TCP 443 hacia el servidor web.
Bloquear conexiones externas hacia la base de datos.
Permitir administración solo desde una red autorizada.
```

Un firewall puede considerar:

- Direcciones IP.
- Puertos.
- Protocolos.
- Estado de las conexiones.
- Interfaces de red.
- En sistemas avanzados, contenido de aplicación.

### IDS

IDS significa _Intrusion Detection System_. Observa el tráfico o los eventos y genera alertas al detectar actividad sospechosa.

```
Tráfico ─────► IDS ─────► alerta
```

Un IDS tradicional no bloquea automáticamente. Su función principal es detectar y avisar.

### IPS

IPS significa _Intrusion Prevention System_. Se coloca en una posición donde puede bloquear el tráfico:

```
Tráfico ─────► IPS ─────► sistema protegido
                 │
             puede bloquear
```

La comparación básica es:

```
Firewall:
decide qué comunicaciones están permitidas.

IDS:
observa y genera alertas.

IPS:
observa y puede bloquear automáticamente.
```

No es correcto decir que los puertos necesarios solo pueden protegerse mediante un IDS. El IDS es una parte de la defensa. La protección completa combina:

- Firewall.
- IDS o IPS.
- Autenticación.
- Parches.
- Cifrado.
- Configuración segura.
- Monitoreo.
- Respaldos.
- Segmentación.
- Respuesta a incidentes.

---

## 29. Herramientas mencionadas en clase

Estas herramientas deben utilizarse exclusivamente en equipos propios, laboratorios controlados o sistemas para los cuales exista autorización expresa.

### Kali Linux

Es una plataforma especializada que reúne numerosas herramientas de análisis y evaluación de seguridad.

No es una “herramienta para hackear cualquier cosa”. Su propósito legítimo es permitir que profesionales y estudiantes evalúen sistemas autorizados.

Sitio: [Kali Linux](https://www.kali.org/)

### Wireshark

Es un analizador de protocolos. Permite capturar y examinar el tráfico que pasa por una interfaz de red.

Puede mostrar:

- Direcciones IP.
- Direcciones MAC.
- Puertos.
- Banderas TCP.
- Consultas DNS.
- Protocolos.
- Tamaños y tiempos de los paquetes.

Wireshark no es malware. Es una herramienta legítima de diagnóstico y aprendizaje. Sin embargo, capturar tráfico ajeno sin autorización puede ser ilegal o violar políticas.

Sitio: [Wireshark](https://www.wireshark.org/)

### Snort

Es un sistema de detección y prevención de intrusiones basado en reglas. Puede identificar patrones de tráfico relacionados con ataques conocidos y generar alertas. Cuando se instala en línea, también puede bloquear.

Sitio: [Snort](https://www.snort.org/)

### Suricata

Es un motor abierto de análisis de red, IDS e IPS. Puede examinar tráfico, aplicar reglas y generar registros de eventos.

Sitio: [Suricata](https://suricata.io/)

### Bettercap

Es un marco para reconocimiento y evaluación de comunicaciones de red. Puede utilizarse para estudiar ataques de intermediario dentro de laboratorios autorizados.

Sitio: [Bettercap](https://www.bettercap.org/)

### Ettercap

Es una herramienta orientada al análisis de redes locales y a la evaluación de ataques de intermediario.

Sitio: [Ettercap](https://www.ettercap-project.org/)

### Tor

Tor significa _The Onion Router_. Es una red diseñada para mejorar la privacidad y dificultar el rastreo del origen de una comunicación.

No garantiza por sí sola anonimato perfecto.

Sitio: [Tor Project](https://www.torproject.org/)

### Aircrack-ng

Es un conjunto de herramientas para evaluar la seguridad de redes inalámbricas.

Sitio: [Aircrack-ng](https://www.aircrack-ng.org/)

### Nmap

Permite descubrir equipos, puertos y servicios dentro de una red autorizada. Es útil para inventarios, administración y evaluaciones de seguridad.

Sitio: [Nmap](https://nmap.org/)

### hping3

Permite crear y analizar paquetes TCP/IP. Puede utilizarse para estudiar respuestas de red, firewalls y protocolos.

Como también puede generar tráfico dañino, su uso debe limitarse estrictamente a laboratorios o sistemas autorizados.

### Fragrouter

Es una herramienta histórica relacionada con la fragmentación de paquetes y las técnicas de evasión de IDS. Ayuda a comprender por qué un sistema de detección debe reensamblar y normalizar correctamente el tráfico antes de analizarlo.

### Engage Security IDScenter

Es una interfaz histórica asociada con la administración de sistemas IDS. Debe considerarse una herramienta heredada incluida en las diapositivas, no necesariamente una recomendación moderna.

---

## 30. Ejemplo completo: Alice entra a su banco

Alice quiere entrar al portal de su banco y realizar una transferencia.

### Paso 1: DNS

La computadora de Alice necesita averiguar la dirección IP del banco.

```
Nombre del banco ──DNS──► dirección IP
```

Amenazas:

- DNS spoofing.
- Pharming.
- Modificación del archivo local de nombres.

### Paso 2: conexión TCP

La computadora de Alice inicia el handshake con el servidor en el puerto 443:

```
Alice ───────── SYN ─────────► banco
Alice ◄────── SYN + ACK ───── banco
Alice ───────── ACK ─────────► banco
```

Amenaza:

- SYN flood contra el servidor.

### Paso 3: establecimiento de TLS

El navegador verifica el certificado y negocia claves criptográficas.

Amenazas:

- Servidor falso.
- Intermediario.
- Certificado inválido.
- Configuración criptográfica insegura.

### Paso 4: envío de credenciales

Alice introduce su contraseña y un segundo factor.

Amenazas:

- Phishing.
- Malware.
- Robo de sesión.
- Ingeniería social.
- Spyware.

### Paso 5: transferencia

Alice solicita transferir una cantidad determinada.

El banco debe garantizar que nadie cambie:

- El monto.
- El destinatario.
- El concepto.
- La cuenta de origen.

El servicio principal es la integridad.

### Paso 6: conservación del servicio

El banco debe seguir atendiendo a los clientes legítimos, incluso si recibe tráfico malicioso.

El servicio principal es la disponibilidad.

Mecanismos:

- Redundancia.
- Balanceo de carga.
- Protección DDoS.
- Firewalls.
- IDS e IPS.
- Monitoreo.
- Planes de recuperación.

Este ejemplo muestra que una sola operación depende de todas las capas y de numerosos servicios de seguridad.

---

## Ideas fundamentales de la clase

Los ataques pueden estudiarse según la capa donde actúan y la propiedad de seguridad que intentan comprometer.

Las direcciones de puerto pertenecen a la capa de transporte; las direcciones IP, a la capa de red; y las direcciones MAC, a la capa de enlace.

TCP utiliza un handshake, números de secuencia, confirmaciones y retransmisiones para proporcionar una comunicación confiable. UDP proporciona un servicio más sencillo y sin establecimiento de conexión.

DoS y DDoS comprometen principalmente la disponibilidad. Un SYN flood abusa de conexiones TCP pendientes, mientras que otras inundaciones pueden utilizar UDP, HTTP u otros protocolos.

Los checksums y CRC sirven principalmente para detectar errores accidentales. La integridad frente a atacantes requiere mecanismos criptográficos, como HMAC o firmas digitales.

La tríada CIA —confidencialidad, integridad y disponibilidad— se complementa con autenticación, control de acceso y no repudio.

Finalmente, no podemos proteger una organización cerrando todos sus puertos. Los servicios necesarios deben permanecer accesibles, pero deben estar limitados, monitoreados y protegidos mediante varias capas de defensa.