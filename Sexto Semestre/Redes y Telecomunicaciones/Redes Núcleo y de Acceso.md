
## El Internet como “red de redes”

El **internet** se compone por una amplia cantidad de redes interconectadas entre sí, todas pertenecientes a distintas organizaciones y proveedores, todas trabajando conjuntamente para permitir la comunicación global entre ellas.

Las redes que componen al internet, se encuentran conectadas mediante **Internet Service Providers** (ISP), mismos que actúan a manera de intermediarios para que las redes locales, regionales y nacionales sean capaces de comunicarse entre sí; es decir, un dispositivo conectado a una red local, puede fácilmente intercambiar información con otro ubicado en cualquier parte del mundo.

---

## Infraestructura del Internet y servicios para aplicaciones

El internet, a nivel de infraestructura, proporciona servicios a las aplicaciones; es decir:

- La web
    
- El streaming de video
    
- Las videoconferencias
    
- El correo electrónico
    
- Los videojuegos en línea
    
- El comercio electrónico
    
- Las redes sociales
    

Todas estas aplicaciones son ejecutadas en los llamados *sistemas finales*, pero son completamente dependientes de la infraestructura de la red para funcionar correctamente.

Adicionalmente, el internet proporciona una *interfaz de programación para aplicaciones distribuidas*, que permite a las aplicaciones enviar y recibir datos utilizando los servicios de transporte de red. Tal interfaz funciona a manera de conjunto de *hooks* que permiten a las aplicaciones conectarse a la red y utilizar sus servicios.

Una manera de ejemplificarlo puede ser el *servicio postal*, en donde existe una gran variedad de opciones disponibles de entrega, pero se utilizan los que el servicio requiera.

---

## Protocolos en el Internet

Uno de los conceptos más importantes respecto al funcionamiento del internet, es el de **network protocol**, mismo que puede ser definido como un conjunto de normas, estándares y procedimientos que permiten alinear la manera en la que se comunican los dispositivos dentro de una red. 

Estas normativas se encargan de asegurar que la transmisión de datos sea:

- Consistente
	
- Eficiente
	
- Comprensible
	

Los protocolos son los encargados de definir, además:

- Formato de los mensajes
    
- Las acciones a seguir tras la recepción de un mensaje
    
- El comportamiento a tomar ante distintos eventos
    

Los protocolos más relevantes se definen a continuación:

- HTTP (web)
    
- SSL/TLS
    
- SSH
    
- TCP
    
- IP
    
- IEEE 802.11 (Wi-Fi)
    
- IEEE 802.3 (Ethernet)
    
- Tecnologías móviles 4G y 5G
    

De manera similar a los seres humanos (quienes toman turnos para hablar y tienen ciertas respuestas predefinidas para los saludos), los protocolos en las redes aseguran que la comunicación entre ellas sea fluida, limpia y ordenada.

---

## Estándares del Internet

De manera que sea posible hacer funcionar al internet globalmente, todos los dispositivos siguen una serie de **estándares** comunes documentados en los llamados *Request for Comments* (RFC).

La principal organización responsable de los procesos de desarrollo y mantenimiento de los estándares antes descritos, es la **Internet Engineering Task Force**, IETF por sus siglas.

La utilización de estándares abiertos permite garantizar que los dispositivos y sistemas logren comunicarse entre sí efectivamente, incluso perteneciendo a distintos fabricantes.

---

## Red núcleo (*Core Network*)

Una **core network** es el pilar central de la red, suponiendo el *backbone* del internet mismo. Su función principal es proporcionar:

- Transferencia de datos a alta velocidad
    
- Comunicación confiable
    
- Capacidad para manejar grandes volúmenes de tráfico
    

Esta red núcleo interconecta distintas regiones de la red, enlazando múltiples redes de acceso entre sí. Para lograr mantenerla en funcionamiento, se utilizan equipos de alto rendimiento, así como técnicas avanzadas de transmisión.

Entre sus características clave se encuentran: 

- **Interconectividad**: conecta múltiples redes de acceso, redes de borde y otras redes núcleo, incluso entre países o regiones.
    
- **Técnicas de transferencia**: puede utilizar técnicas basadas en paquetes o en circuitos para el reenvío de datos.
    

---

## Red de acceso (*Access Network*)

Por su parte, la **access network** forma parte de la red que permite conectar a los usuarios con la infraestructura del internet. Se le conoce coloquialmente como el *último kilómetro* o *last mile*.

Esta red permite que dispositivos como:

- Computadoras
    
- Teléfonos móviles
    
- Sensores
    
- Dispositivos IoT
    

puedan acceder al núcleo de la red sin complicaciones.

Esta clase de red se caracteriza por:

- **Dispositivos**: incluye sistemas finales y dispositivos de acceso como puntos de acceso, torres celulares y módems.
    
- **Acceso físico o inalámbrico**: la conexión puede realizarse mediante enlaces cableados o inalámbricos.
    

---

## Tecnologías de acceso cableadas e inalámbricas

Se distingue entre dos grandes tecnologías de acceso principales:
### Acceso cableado:

Típicamente **Ethernet**, con velocidades típicas de:

- 100 Mbps
    
- 1 Gbps
    
- 10 Gbps
    

#### *Hybrid Fiber-Coaxial:*

Se tienen 

### Acceso inalámbrico:

Principalmente **IEEE 802.11 (Wi-Fi)**, con puntos de acceso que pueden operar a velocidades aproximadas de:

- 11 Mbps
    
- 54 Mbps
    
- 450 Mbps
    

Estas tecnologías permiten la movilidad y flexibilidad en el acceso a la red.

---
---

## Red de acceso basada en cable: HFC

El documento describe explícitamente la **Cable-based Access Network: HFC (Hybrid Fiber-Coaxial)**.

HFC combina:

- **Fibra óptica** en el backbone
    
- **Cable coaxial** para la conexión del último tramo hacia el usuario
    

Esta arquitectura se utiliza ampliamente para ofrecer servicios de Internet de banda ancha y televisión por cable.

---
---

### Características del HFC

- **Ancho de banda**: mayor que el uso exclusivo de coaxial, gracias al backbone de fibra, alcanzando hasta **1.2 Gbps** en muchas implementaciones.
    
- **Distancia**: la fibra permite conexiones de largo alcance, mientras que el cable coaxial cubre el último tramo, aproximadamente **500 metros**.
    
- **Costo**: es más económico que desplegar fibra óptica directamente hasta cada usuario final.
    
---