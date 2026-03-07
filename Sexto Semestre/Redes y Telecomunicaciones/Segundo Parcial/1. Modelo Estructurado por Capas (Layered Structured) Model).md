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

## Capa de Aplicación

La **capa de aplicación** es la encargada de proveer servicios de red directamente a los usuarios o a los programas, definiendo la manera en la que las aplicaciones interactúan con la red; por ejemplo, navegar en internet, enviar correos electrónicos o transferir archivos. Los principales protocolos son los siguientes:

- **Navegación web:** HTTP y HTTPS
- **Correo:** SMTP, POP3 e IMAP
- **Transferencia de archivos:** FTP y SFTP
- **Traducción de nombres de dominio a direcciones:** DNS
- **Administración y monitoreo de red:** SNMP

Como ejemplo aplicado, se tiene el siguiente: Cuando un usuario accede a un sitio web, el navegador utiliza HTTP/HTTPS para expresar las solicitudes y las respuestas (métodos, enlaces, encabezados), mientras que internamente otras capas se encargan de asegurar un transporte confiable, el direccionamiento IP y el envío mediante Wi-Fi/Ethernet y la transmisión física.

---

## Capa de Presentación

La **capa de presentación** se encara de que la información pueda ser comprendida entre los diferentes sistemas que la consumen; esto, mediante la traducción de formatos y representaciones. Igualmente, puede encargarse de gestionar el cifrado, compresión y codificación previo a comenzar con la transmisión. 

- **SSL/TLS:** Mecanismo utilizado para cifrar tráfico web (asociado con HTTPS).
- **JPEG/PNG/GIF:** Formatos de imagen.
- **MP3/AAC:** Compresión de audio.
- **MPEG/H.264:** Codificación de video y *streaming*.

Por ejemplo, en videollamadas, la capa de presentación es la responsable de preparar el contenido audiovisual comprimiéndolo para no saturar el enlace, pudiendo además cifrarlo con fines de seguridad.

---

## Capa de Sesión

La **capa de sesión** se centra en gestionar la administración de las sesiones entre aplicaciones, encargándose en establecer, mantener y finalizar las comunicaciones lógicas. 

Se enlistan tecnologías/protocolos asociados:

- **NetBIOS:** Gestión de sesiones en entornos Windows. 
- **RPC:** Acceso remoto a aplicaciones/servicios. 
- **SIP:** Usado en llamadas VoIP.

Adicionalmente, al comparar modelos, esta capa es capaz de aportar *sincronización* y puntos de reanudación, mismos que fungen como un entorno de recuperación ante interrupciones.

---

## Capa de Transporte

Por su parte, la **capa de transporte** es la principal encargada de la comunicación *extremo a extremo*, teniendo el objetivo de entregar los datos con propiedades tales como confiabilidad, orden y control del flujo; todo esto, dependiendo del protocolo:

La capa de **transporte** gestiona la comunicación **extremo a extremo** (proceso a proceso). Su objetivo es entregar datos con propiedades como confiabilidad, orden y control de flujo, dependiendo del protocolo. 

- **TCP:** Protocolo confiable y ordenado
- **UDP:** Alternativa más rápida pero sin garantías fuertes de entrega/orden.

Por ejemplo, si se envía un archivo importante, el protocolo TCP ayuda a detectar pérdidas y reorganizar datos; si se transmite audio en tiempo real, es UDP el encargado de la transmisión dadas sus capacidades para reducir latencia, aunque aceptando posibles pérdidas.

---

## Capa de Red

La **capa de red** es la responsable del direccionamiento IP, enrutamiento y reenvío de paquetes. Para ello, determina cuál es el mejor camino para transmitir los datos atravesando múltiples redes. 

La capa de **red** se encarga del **direccionamiento IP**, el **enrutamiento** y el **reenvío de paquetes**. Determina el “mejor camino” para que los datos lleguen a su destino a través de múltiples redes. 

- **IPv4/IPv6:** Internet Protocol. 
- **ICMP** Protocolo usado por herramientas como *ping* y *traceroute*. 
- **ARP** Resuelve direcciones IP a direcciones MAC. 
- **OSPF, RIP y BGP:** Como protocolos de enrutamiento.

Existe una separación conceptual relevante: IP es el que identifica destinos de red (direcciones lógicas), mientras que ARP vincula la identificación con direcciones MAC dentro de un entorno local.

---

## Capa de Enlace de Datos (Data Link)

La **capa de enlace de datos** maneja la comunicación nodo a nodo dentro de una misma red local. Es la responsable de mantener la detección de errores, direccionamiento MAC y control de acceso al medio (MAC como *Media Access Control*).

- **Ethernet (IEEE 802.3):** Redes cableadas.
- **Wi-Fi (IEEE 802.11):** Redes inalámbricas.
- **MAC:** Mecanismo de identificación en LAN.
- **PPP:** Para enlaces de punto a punto (DSL y enlaces seriales).

---

## Capa Física

La **capa física** es la que define la manera en la que se transmiten los bits. Considera *hardware*, medios y tipos de señal, convirtiendo los datos en señales eléctricas, ópticaso de radio. 

Se utilizan cables coaxiales, fibra óptica, STP/UTP, señales inalámbricas como Wi-Fi y *bluetooth*, conectores como RJ45 y USB, manteniendo estándares eléctricos como voltajes y modulación.

---

## Encapsulación

El concepto de **encapsulación** indica que, proceduralmente, cada capa toma los datos de su capa superior y los envuelve dentro de su propia cabecera para implementar su servicio. Por ejemplo:

1. En *transporte*, un protocolo de transporte encapsula el mensaje de *aplicación* **M** agregando un encabezado de transporte **Ht** para formar un segmento.
    
2. En *red*, se encapsula **[Ht | M]** agregando un encabezado de red **Hn** para crear un paquete.
    
3. En *enlace*, se encapsula **[Hn | Ht | M]** agregando un encabezado de enlace **Hl** para crear una trama (frame).
    

Una representación ASCII de esta lógica es:

```
Aplicación:            [         M          ]

Transporte:            [   Ht   |     M     ]   -> segmento

Red:                   [   Hn   |   Ht | M  ]   -> paquete

Enlace (Link):         [   Hl   |   Hn | Ht | M ] -> frame

Física:                bits/señal transmitida en el medio
```

Tal organización explica los motivos por los que, al capturar el tráfico, pueden observarse cabeceras apiladas, de modo que cada una contiene la información necesaria para poder realizar las actividades propias de su capa (puertos en *transporte*, direcciones IP y TTL en *red*, MAC y FCS en *enlace*, etc.), mientras que la carga útil suele ser el contenido que ya ha sido producido por la capa superior.

---

## Modelos de Capas

El enfoque típico de internet toma como base las capas descritas en las secciones previas. Por otro lado, el **modelo OSI** (siglas de *Open Systems Interconnection*) es un modelo conceptual de siete capas (en lugar de las cinco previas), cada una con funciones específicas y comunicación meramente adyacente. OSI funge como un marco teórico, 

Una representación ASCII orientativa del OSI de 7 capas es:

```
1. Aplicación
2. Presentación
3. Sesión
4. Transporte
5. Red
6. Enlace de datos
7. Física
```

La lectura práctica es que OSI sirve para aprender y razonar con precisión sobre responsabilidades, mientras que TCP/IP describe cómo realmente se implementa la comunicación en Internet, frecuentemente fusionando capas (por ejemplo, “aplicación” suele absorber presentación y sesión en implementaciones reales).

---
