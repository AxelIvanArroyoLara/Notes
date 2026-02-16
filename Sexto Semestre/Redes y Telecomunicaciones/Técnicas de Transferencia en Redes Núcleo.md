## Introducción

En las *redes núcleo*, las *técnicas de transferencia* hacen referencia a la manera en la que los datos se transmiten a través de una red. Existen dos métodos principales:

- **Conmutación de circuitos** (*circuit switching*).

- **Conmutación de paquetes** (*packet switching*).

En donde cada uno opera de manera diferente, manteniendo una serie de ventajas específicas y escenarios de aplicación particulares. 

![[Pasted image 20260216010426.png]]

---

## Conmutación de Circuitos (*circuit switching*)

### Descripción general:

La **conmutación de circuitos** consiste en el establecimiento de un camino de comunicación dedicado entre los dos extremos de la red durante la duración total de la sesión. Absolutamente todos los datos viajan a través de un mismo camino como un flujo continuo de *bits*, sin división de paquetes; es decir, la tasa de datos es fija, garantizando así una conexión consistente y predecible.

Un ejemplo de este sistema, es el *Public Switched Telephone Network* (PSTN), utilizada para los sistemas telefónicos tradicionales, en donde se requiere una calidad constante en la voz.


### Funcionamiento:

El funcionamiento se divide en tres fases fundamentales:

#### 1. Establecimiento de conexión (Connection Establishment):

Previo a comenzar el proceso de comunicación, se reserva un camino particular a través de la red utilizando un proceso conocido como **señalización** (*signaling*), fase durante la cual:

- Cada uno de los *nodos* intermedios almacena información acerca de la conexión.

- Se reservan recursos en todos los *nodos* y *enlaces* que forman parte del camino establecido.

No se lleva a cabo la transmisión de los datos hasta que el circuito se encuentra completamente establecido.

#### 2. Transmisión de datos:

Una vez habiéndose establecido el circuito:

- Los datos se transmiten a manera de un flujo contínuo.

- No es necesario incluir la dirección de destino para cada unidad transmitida.

- Los nodos intermedios, al ya conocer el camino, simplemente se encargan del reenvío de los *bits*.

#### 3. Liberación de conexión (Connection Teardown):

Al finalizar el proceso de comunicación:

- El circuito es liberado.

- Los recursos reservados se liberan.

- La red puede reutilizar el circuito y los recursos para otros usuarios.

---

### Signalling en redes de conmutación de circuitos

El proceso de *señalización* puede definirse como el intercambio de información de control necesario para:

- Establecer las conexiones.

- Mantener las conexiones.

- Finalizar adecuadamente las conexiones.

#### Funciones principales del signalling

1. ***Connection set-up***
    
    - Localiza al receptor.
        
    - Reserva recursos.
        
    - Crea el circuito.
        
2. ***Connection maintenance***
    
    - Supervisa la calidad.
        
    - Gestiona características como llamada en espera.
        
    - Administra el ancho de banda disponible.
        
3. ***Connection teardown***
    
    - Termina la conexión.
        
    - Libera recursos.
        

### *In-band vs Out-of-band Signalling*:

Existen dos formas de señalización:

#### *In-band signalling*:

En este esquema:

- La *señalización* utiliza el mismo canal que los datos del usuario.

- No requiere de canales adicionales.

- Reduce el ancho de banda disponible para datos.

- Puede comprometer la integridad del canal.

Ejemplo: **PSTN**.

![[Pasted image 20260216012631.png]]

En este esquema, tanto la información de control como la información de datos, comparten el mismo camino, utilizando los mismos recursos para establecer el circuito deseado.

#### *Out-of-band signalling*:

En este formato:

- La *señalización* viaja a través de un canal separado.

- El canal principal se dedica exclusivamente a datos.

- Mayor seguridad y confiabilidad.

- Mayor complejidad e infraestructura adicional.

Ejemplo: **GSM**.

![[Pasted image 20260216013002.png]]

El camino de señalización es distinto al de datos. Ambos no comparten recursos.

---

## Multiplexación

La técnica de **multiplexación** permite la combinación de múltiples señales o flujos de datos en un único canal de comunicación, optimizando así el manejo del ancho de banda.

Para el lado del *receptor*, se realiza el proceso inverso, conocido como **demultiplexación**.

![[Pasted image 20260216013333.png]]

---

## *Time Division Multiplexing* (TDM)

El TDM funciona mediante la división de un solo *canal* de comunicación en intervalos de tiempo (*time slots*), asignando cada intervalo a una conexión distinta. De esta manera, se utiliza todo el ancho de banda, pero solo durante intervalos de tiempo pequeños.

### Funcionamiento:

1. El medio se divide en time slots.
    
2. Cada conexión recibe un slot fijo.
    
3. El proceso es cíclico.
    
4. El receptor reconstruye los datos según la posición temporal.
    

### Características:

- La secuencia de *slots* asignados a una fuente se llama *canal*.
    
- Es síncrono porque la asignación es fija.
    
- Los *slots* se reservan incluso si no hay datos.
    
- Puede operar a nivel de *bits* o *bytes*.
    
- No es obligatorio asignar intervalos equitativamente.
    

Ejemplo: **GSM** utiliza TDM para asignar llamadas en la misma frecuencia.

![[Pasted image 20260216082802.png]]

---

## *Frequency Division Multiplexing* (FDM)

El esquema FDM divide el ancho de banda en múltiples bandas de frecuencia no superpuestas, en donde cada una se asigna a una conexión individual.

### Funcionamiento:

1. Se divide el espectro total en sub-bandas.
    
2. Cada conexión recibe una banda fija.
    
3. Cada señal se modula en una frecuencia portadora distinta.
    
4. En el receptor se demodula.
    

### Características:

- Canales activos simultáneamente.
    
- Uso de bandas de guarda (*guard bands*).
    
- Se asigna banda aunque no haya datos.
    

Ejemplo: PSTN analógico.

![[Pasted image 20260216083117.png]]

---

## Ventajas y Desventajas de Circuit Switching

### Ventajas:

- Throughput constante.
    
- No servicio best-effort.
    
- Sin pérdida ni desorden de datos.
    
- No hay headers → baja sobrecarga.
    
- Modelo simple de comunicación.
    

### Desventajas:

- Desperdicio de ancho de banda.
    
- Rechazo de conexiones si no hay recursos.
    
- Tiempo de establecimiento previo.
    
- Los nodos deben mantener estado de conexión.
    

---

## Conmutación de Paquetes (*Packet Switching*)

### Descripción general:

Los datos regularmente se dividen en paquetes con un tamaño aproximado de *1000 bytes* cada uno, conteniendo:

- Payload (datos).
    
- Header (dirección origen/destino, secuencia).
    

En este esquema, no existe un camino dedicado como en la *conmutación de circuitos*.

Ejemplo: Internet (TCP/IP), ATM, MPLS.

### Funcionamiento:

1. Fragmentación.
    
2. Enrutamiento independiente (store and forward).
    
3. Reensamblaje en destino.
    

### Conceptos clave:

#### Packet:

- ***Packet:*** Unidad estructurada que sigue modelo OSI/TCP-IP.

- ***Frame:*** Unidad enviada por el enlace físico. Encapsula el paquete.

Relación:

```
Frame
 └── Packet
      └── Payload
```

---

## Redes enrutadas

Existen dos enfoques:

- Virtual Circuit (packet commutation)
    
- Datagram (packet routing)
    

---

## *Packet Routing* (*Datagram*)

Características:

- Connectionless.
    
- Enrutamiento dinámico (BGP, OSPF).
    
- Dirección completa en el header.
    
- Uso de tabla de enrutamiento.
    

No se mantiene estado de conexión.

---

## *Packet Commutation* (*Virtual Circuits*)

Características:

- Connection-oriented.
    
- Se establece VC mediante *signalling*.
    
- Todos los paquetes siguen mismo camino.
    
- Uso de identificadores (*labels*).
    
- Paquetes de tamaño fijo.
    
- Permite QoS.
    
- Puede reservar recursos.
    

Los nodos mantienen tablas de conmutación con identificadores de entrada y salida.

### Establecimiento de *Virtual Circuit*:

Incluye:

- Creación de entradas en tabla.
    
- Reserva opcional de recursos.
    
- Puede configurarse manualmente o bajo demanda.
    
- Existe un delay de establecimiento.
    
- La ruta se determina durante signalling.
    

---

## Similitudes entre *Virtual Circuit* y *Datagram*

- Ambos dividen datos en paquetes.
    
- Ambos usan store-and-forward.
    
- Ambos requieren buffers.
    
- Ambos pueden *multiplexar* enlaces.
    

---

# Diferencias entre *Virtual Circuit* y *Datagram*

| Aspecto            | Virtual Circuit            | Datagram           |
| ------------------ | -------------------------- | ------------------ |
| Lookup             | Identificador VC           | Dirección completa |
| Inicio transmisión | Requiere signalling previo | Inmediato          |
| Estado en nodos    | Sí                         | No                 |
| QoS                | Posible                    | Difícil            |

---

# Conclusión General

La conmutación de circuitos fue diseñada principalmente para voz, donde se requiere tasa fija y recursos dedicados. Sin embargo, para tráfico de datos variable y bursty, la conmutación de paquetes resulta más eficiente.

La evolución de redes núcleo modernas favorece la conmutación de paquetes por su flexibilidad, eficiencia y escalabilidad, aunque los modelos de circuito virtual permiten combinar ventajas de ambos enfoques mediante mecanismos de QoS y rutas preestablecidas.

---