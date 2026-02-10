
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
    

---
---
## Protocolos humanos y protocolos de red

El documento introduce una analogía entre los **protocolos humanos** y los **protocolos de red**.  
Como ejemplos de protocolos humanos se mencionan:

- Las conversaciones telefónicas
    
- Las presentaciones entre personas
    

Estos protocolos humanos siguen reglas implícitas, como turnarse para hablar o responder de cierta forma ante un saludo. De manera similar, los protocolos de red siguen reglas bien definidas para permitir una comunicación ordenada y comprensible entre dispositivos.

Esta analogía ayuda a entender que los protocolos no son exclusivos de las computadoras, sino una forma general de coordinar la comunicación.

---

## 5. Estándares del Internet

Para que el Internet funcione a escala global, es necesario que todos los dispositivos sigan **estándares comunes**. Estos estándares se documentan en los llamados **RFC (Request for Comments)**.

La organización responsable del desarrollo y mantenimiento de estos estándares es la **IETF (Internet Engineering Task Force)**.  
El uso de estándares abiertos garantiza que dispositivos y sistemas de distintos fabricantes puedan comunicarse sin problemas.

---

## 6. Red núcleo (Core Network)

La **core network** es la parte central de la red y constituye el **backbone** del Internet. Su función principal es proporcionar:

- Transferencia de datos a alta velocidad
    
- Comunicación confiable
    
- Capacidad para manejar grandes volúmenes de tráfico
    

La red núcleo conecta diferentes regiones de la red y enlaza múltiples redes de acceso entre sí. En esta parte de la red se utilizan equipos de alto rendimiento y técnicas avanzadas de transmisión.

### Características clave de la core network

El documento menciona como características principales:

- **Interconectividad**: conecta múltiples redes de acceso, redes de borde y otras redes núcleo, incluso entre países o regiones.
    
- **Técnicas de transferencia**: puede utilizar técnicas basadas en paquetes o en circuitos para el reenvío de datos.
    

---

## 7. Red de acceso (Access Network)

La **access network** es la parte de la red que conecta directamente a los **usuarios finales** con la infraestructura del Internet. Se le conoce comúnmente como el **“último kilómetro” o “last mile”**.

Esta red permite que dispositivos como:

- Computadoras
    
- Teléfonos móviles
    
- Sensores
    
- Dispositivos IoT
    

puedan acceder al núcleo de la red.

### Características clave de la red de acceso

El documento indica que la red de acceso se caracteriza por:

- **Dispositivos**: incluye sistemas finales y dispositivos de acceso como puntos de acceso, torres celulares y módems.
    
- **Acceso físico o inalámbrico**: la conexión puede realizarse mediante enlaces cableados o inalámbricos.
    

---

## 8. Tecnologías de acceso cableadas e inalámbricas

El documento distingue entre dos grandes tipos de tecnologías de acceso:

### Acceso cableado

Se menciona específicamente **Ethernet**, con velocidades típicas de:

- 100 Mbps
    
- 1 Gbps
    
- 10 Gbps
    

### Acceso inalámbrico

Se menciona **IEEE 802.11 (Wi-Fi)**, con puntos de acceso que pueden operar a velocidades aproximadas de:

- 11 Mbps
    
- 54 Mbps
    
- 450 Mbps
    

Estas tecnologías permiten la movilidad y flexibilidad en el acceso a la red.

---

## 9. Red de acceso basada en cable: HFC

El documento describe explícitamente la **Cable-based Access Network: HFC (Hybrid Fiber-Coaxial)**.

HFC combina:

- **Fibra óptica** en el backbone
    
- **Cable coaxial** para la conexión del último tramo hacia el usuario
    

Esta arquitectura se utiliza ampliamente para ofrecer servicios de Internet de banda ancha y televisión por cable.

### Características del HFC

- **Ancho de banda**: mayor que el uso exclusivo de coaxial, gracias al backbone de fibra, alcanzando hasta **1.2 Gbps** en muchas implementaciones.
    
- **Distancia**: la fibra permite conexiones de largo alcance, mientras que el cable coaxial cubre el último tramo, aproximadamente **500 metros**.
    
- **Costo**: es más económico que desplegar fibra óptica directamente hasta cada usuario final.
    

---

## 10. Diagramas presentes en el documento

El documento incluye **diagramas visuales** (no textuales) que representan:

- La estructura general del Internet como red de redes
    
- La distinción entre red núcleo y redes de acceso
    
- La arquitectura de una red HFC
    

### Descripción ASCII aproximada de los diagramas

```
[ End Systems ]
       |
   Access Network
       |
------------------- Core Network -------------------
       |
   Access Network
       |
[ End Systems ]
```

```
        Fiber Backbone
   ======================
          |
      Coaxial Cable
          |
       Customer
```

---

## Cierre del módulo

Este módulo introduce los conceptos fundamentales necesarios para comprender el funcionamiento del Internet, incluyendo su estructura como red de redes, el papel central de los protocolos, la importancia de los estándares, y la división entre redes de acceso y red núcleo, junto con tecnologías reales como Ethernet, Wi-Fi y HFC.

---

Si quieres, en el siguiente mensaje puedo:

- 🔹 **Reducir estos apuntes para examen**
    
- 🔹 **Convertirlos en preguntas tipo parcial**
    
- 🔹 **Continuar con el siguiente módulo**
    
- 🔹 **Unificarlos con otros módulos en un solo documento**
    

Tú mandas. Esta vez, **bien hecho** 😌📘