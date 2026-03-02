El **modelo estructurado por capas** se define como una manera de describir y diseñar redes a partir de la división de la comunicación en una serie de *capas*, cada una encargada de un conjunto particular de funciones. Teniéndose estandarizado el comportamiento de cada nivel, es posible lograr una interoperabilidad integral entre varios dispositivos y proveedores diferentes, volviéndose más sencillo el diseño, entendimiento y diagnóstico de redes. Para lograr los objetivos planteados, cada una de las capas brinda un *servicio* a la capa superior respectiva, utilizando internamente los de la inferior. Gracias a la aplicación de este principio, es posible reducir la complejidad al evolucionar cada nivel sin tener que efectuar un rediseño completo del sistema; por supuesto, siempre que respete las interfaces definidas.

Las redes reales con regularidad involucran una multitud de dispositivos con diferentes fabricantes y muchos protocolos, por lo que se utiliza un **modelo de referencia** que permite lograr la *estandarización*, así como la definición de los roles para cada función de la red, mejorando la interoperabilidad y facilitando la resolución de problemas. 

Ese procedimiento puede ser comparado a los pasos para la redacción de una carta, dígase escritura, envío, almacenamiento y entrega; cada uno de ellos cumple un rol distinto dentro de su flujo mayor.

---

## Funciones Típicas

Dentro del contexto de una red completa, suelen aparecer necesidades funcionales recurrentes; entre estas, se incluyen:

- Medio físico para enviar bits.
- Verificación y corrección de errores.
- Direccionamiento.
- Enrutamiento.
- Paquetización.
- Control de flujo.
- Control de gestión.
- Fragmentación.
- Seguridad.

Esta lista muestra los diferentes problemas que pueden surgir respecto a la confiabilidad, identificación, selección de ruta, rendimiento y protección que se reparten entre las capas.

---
---

## Capa de Aplicación (en el sentido funcional del modelo por capas)

La capa de **aplicación** se entiende como la que provee servicios de red directamente a usuarios o programas, y define cómo las aplicaciones interactúan con la red (por ejemplo, navegar web, enviar correo o transferir archivos). Se mencionan como ejemplos de protocolos: **HTTP/HTTPS** para navegación web; **SMTP, POP3 e IMAP** para correo; **FTP/SFTP** para transferencia de archivos; **DNS** para traducir nombres de dominio a direcciones; y **SNMP** para administración y monitoreo de red.

Como ejemplo aplicado, cuando un usuario entra a un sitio web, la aplicación (navegador) utiliza HTTP/HTTPS para expresar solicitudes y respuestas (métodos, URLs, headers), mientras que “por debajo” otras capas se encargan del transporte confiable, el direccionamiento IP, el envío por Wi-Fi/Ethernet y la transmisión física.

---

## Capa de Presentación

La capa de **presentación** se ocupa de que la información sea **comprensible** entre sistemas distintos mediante traducción de formatos y representaciones. También puede encargarse de **cifrado**, **compresión** y **codificación** antes de la transmisión. Se citan como ejemplos: **SSL/TLS** como mecanismo usado para cifrar tráfico web (asociado al uso de HTTPS); formatos de imagen como **JPEG, PNG y GIF**; compresión de audio como **MP3 y AAC**; y codificación de video como **MPEG y H.264** para streaming.

Un ejemplo típico es una plataforma de videollamadas: la capa de presentación “prepara” el audio/video comprimiéndolo para no saturar el enlace, y puede cifrarlo para evitar que terceros lo interpreten aunque intercepten paquetes.

---

## Capa de Sesión

La capa de **sesión** se centra en la administración de sesiones entre aplicaciones: **establece, mantiene y termina** comunicaciones lógicas. En el material se señalan ejemplos de tecnologías/protocolos asociados: **NetBIOS** (gestión de sesiones en entornos Windows), **RPC** (acceso remoto a aplicaciones/servicios) y **SIP** (usado en llamadas VoIP).

Además, al comparar modelos, se describe que la capa de sesión puede aportar **sincronización**, “milestones” o puntos de reanudación, y recuperación de un intercambio de datos tras interrupciones.

---

## Capa de Transporte

La capa de **transporte** gestiona la comunicación **extremo a extremo** (proceso a proceso). Su objetivo es entregar datos con propiedades como confiabilidad, orden y control de flujo, dependiendo del protocolo. Se mencionan **TCP** como protocolo confiable y ordenado, y **UDP** como alternativa más rápida pero sin garantías fuertes de entrega/orden.

Un ejemplo sencillo: si se envía un archivo importante, TCP ayuda a detectar pérdidas y reordenar datos; si se transmite audio en tiempo real, UDP puede preferirse para reducir latencia, aceptando posibles pérdidas.

---

## Capa de Red

La capa de **red** se encarga del **direccionamiento IP**, el **enrutamiento** y el **reenvío de paquetes**. Determina el “mejor camino” para que los datos lleguen a su destino a través de múltiples redes. Se citan **IPv4/IPv6** como Internet Protocol, **ICMP** como protocolo usado por herramientas como ping y traceroute, **ARP** para resolver direcciones IP a direcciones MAC, y protocolos de enrutamiento como **OSPF, RIP y BGP**.

Aquí es clave notar la separación conceptual: IP identifica destinos a nivel de red (direcciones lógicas), mientras que ARP ayuda a vincular esa identificación con direcciones físicas (MAC) dentro de un entorno local.

---

## Capa de Enlace de Datos (Data Link)

La capa de **enlace de datos** maneja la comunicación **nodo a nodo** dentro de la misma red local. Se responsabiliza de **detección de errores**, **direccionamiento MAC** y control de acceso al medio (MAC en el sentido de Media Access Control). Ejemplos mencionados incluyen **Ethernet (IEEE 802.3)** para redes cableadas, **Wi-Fi (IEEE 802.11)** para redes inalámbricas, **MAC** como mecanismo de identificación en LAN, y **PPP** para enlaces punto a punto (por ejemplo, DSL y enlaces seriales).

---

## Capa Física

La capa **física** define el “cómo” se transmiten bits: hardware, medios y tipos de señal. Convierte datos en señales **eléctricas**, **ópticas** o **de radio**. Se enumeran ejemplos como cables **coaxiales**, **fibra**, **STP/UTP**, señales inalámbricas como **Wi-Fi** y **Bluetooth**, conectores como **RJ45** y **USB**, y estándares eléctricos (voltajes, modulación).

---

## Encapsulación: cómo viaja un mensaje a través de las capas

El material explica la idea de **encapsulación**: cada capa toma los datos de la capa superior y los envuelve con su propia cabecera para implementar su servicio.

1. En transporte, un protocolo de transporte encapsula el mensaje de aplicación **M** agregando un encabezado de transporte **Ht** para formar un segmento.
    
2. En red, se encapsula **[Ht | M]** agregando un encabezado de red **Hn** para crear un paquete.
    
3. En enlace, se encapsula **[Hn | Ht | M]** agregando un encabezado de enlace **Hl** para crear una trama (frame).
    

Una representación ASCII de esta lógica es:

```
Aplicación:            [         M          ]

Transporte:            [   Ht   |     M     ]   -> segmento

Red:                   [   Hn   |   Ht | M  ]   -> paquete

Enlace (Link):         [   Hl   |   Hn | Ht | M ] -> frame

Física:                bits/señal transmitida en el medio
```

Esta organización explica por qué, al capturar tráfico, se observan cabeceras apiladas: cada una contiene información necesaria para el “trabajo” de su capa (puertos en transporte, direcciones IP y TTL en red, MAC y FCS en enlace, etc.), mientras que la carga útil suele ser el contenido producido por la capa superior.

---

## Modelos de capas: TCP/IP (modelo práctico) y OSI (modelo conceptual)

Se presenta una tabla con un stack simplificado de 5 niveles: **Application, Transport, Network, Link, Physical**. Esto corresponde al enfoque típico de Internet (TCP/IP extendido a 5 capas), donde “Link” agrupa las tareas de enlace y “Physical” queda como la transmisión.

Por otro lado, se enfatiza que el **modelo OSI** (Open Systems Interconnection) es un modelo **conceptual** de **7 capas** y que cada capa tiene funciones específicas y se comunica solo con capas adyacentes. En una comparación explícita, se indica que OSI es un marco teórico, mientras que **TCP/IP** es un modelo práctico usado en Internet; además, OSI tiene 7 capas y TCP/IP se describe con **4 capas** (donde algunas capas están fusionadas).

El material también lista, como ejemplo de mapeo de funciones por capa, lo siguiente: aplicación soporta aplicaciones (FTP, SMTP, HTTP), transporte hace transferencia proceso a proceso (TCP, UDP), red enruta datagramas (IP y routing), enlace transfiere entre vecinos (Ethernet, 802.11, PPP), física coloca bits en el medio; y dentro del esquema OSI se incluyen explícitamente **presentación** (cifrado/compresión/encodings) y **sesión** (sincronización y recuperación).

Una representación ASCII orientativa del OSI de 7 capas es:

```
7. Aplicación
8. Presentación
9. Sesión
10. Transporte
11. Red
12. Enlace de datos
13. Física
```

La lectura práctica es que OSI sirve para aprender y razonar con precisión sobre responsabilidades, mientras que TCP/IP describe cómo realmente se implementa la comunicación en Internet, frecuentemente fusionando capas (por ejemplo, “aplicación” suele absorber presentación y sesión en implementaciones reales).

---

## Diagramas presentes en el material

El documento incluye al menos un diagrama bajo el título **“Network functions roles definition.”** (mostrado como imagen). Además, aparecen figuras relacionadas con OSI/TCP-IP y con capas específicas (por ejemplo, se observan encabezados y secciones para capas como Application, Session y Data Link, aunque parte del detalle esté embebido como imagen).

Como el contenido de esos diagramas se presenta en imágenes (no en texto plano completo), lo esencial que representan puede resumirse así en ASCII: una **pila de capas** donde cada nivel tiene un rol y la comunicación “baja” encapsulando y “sube” desencapsulando.

```
[Aplicación]
[Presentación]
[Sesión]
[Transporte]
[Red]
[Enlace]
[Física]
```