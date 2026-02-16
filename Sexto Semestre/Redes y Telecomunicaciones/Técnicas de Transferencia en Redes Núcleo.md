A continuación se presentan los **apuntes explicados y extendidos** del documento _“Transfer techniques in Core networks”_ , redactados en tercera persona, en estilo formal y priorizando la prosa, integrando toda la información de las diapositivas e incluyendo la descripción de los diagramas cuando corresponde.

---

# Transfer Techniques in Core Networks

## 1. Introducción a las técnicas de transferencia en redes núcleo

En las redes núcleo (core networks), las técnicas de transferencia hacen referencia a la forma en que los datos se transmiten a través de la red. Existen dos métodos principales: **circuit switching (conmutación de circuitos)** y **packet switching (conmutación de paquetes)**. Cada uno posee mecanismos distintos de operación, ventajas específicas y escenarios de aplicación particulares.

El esquema general presentado en el documento muestra que:

- La **conmutación de circuitos** se relaciona con tecnologías como **PSTN** (Public Switched Telephone Network) y **GSM**, utilizando técnicas de multiplexación como **FDM** (Frequency Division Multiplexing) y **TDM** (Time Division Multiplexing).
    
- La **conmutación de paquetes** se asocia con redes como **Internet (TCP/IP)** y tecnologías como **ATM** y **MPLS**, operando bajo dos modelos: **Virtual Circuit** y **Datagram**.
    

---

# 2. Circuit Switching (Conmutación de Circuitos)

## 2.1. Descripción general

La conmutación de circuitos consiste en establecer un camino de comunicación dedicado entre dos extremos de la red durante toda la duración de la sesión. Todos los datos viajan por ese mismo camino como un flujo continuo de bits, sin división en paquetes.

No existe el concepto de paquete durante la transmisión; el flujo es continuo y la tasa de datos es fija, lo que garantiza una conexión consistente y predecible.

Un ejemplo clásico es la **Public Switched Telephone Network (PSTN)**, utilizada en sistemas telefónicos tradicionales, donde se requiere calidad constante de voz.

---

## 2.2. Funcionamiento del Circuit Switching

El funcionamiento se divide en tres fases fundamentales:

### 1. Establecimiento de conexión (Connection Establishment)

Antes de iniciar la comunicación, se reserva un camino a través de la red mediante un proceso llamado **signalling (señalización)**.

Durante esta fase:

- Cada nodo intermedio almacena información sobre la conexión.
    
- Se reservan recursos en todos los nodos y enlaces que forman parte del camino.
    

No hay transmisión de datos hasta que el circuito esté completamente establecido.

### 2. Transmisión de datos

Una vez establecido el circuito:

- Los datos fluyen como un flujo continuo.
    
- No es necesario incluir dirección de destino en cada unidad transmitida.
    
- Los nodos intermedios ya conocen el camino, por lo que simplemente reenvían los bits.
    

### 3. Liberación de conexión (Connection Teardown)

Al finalizar la comunicación:

- Se libera el circuito.
    
- Se liberan los recursos reservados.
    
- La red puede reutilizarlos para otros usuarios.
    

---

## 2.3. Signalling en redes de conmutación de circuitos

La señalización es el intercambio de información de control necesario para:

- Establecer la conexión.
    
- Mantenerla.
    
- Finalizarla correctamente.
    

### Funciones principales del signalling

1. **Connection set-up**
    
    - Localiza al receptor.
        
    - Reserva recursos.
        
    - Crea el circuito.
        
2. **Connection maintenance**
    
    - Supervisa la calidad.
        
    - Gestiona características como llamada en espera.
        
    - Administra el ancho de banda disponible.
        
3. **Connection teardown**
    
    - Termina la conexión.
        
    - Libera recursos.
        

---

## 2.4. In-band vs Out-of-band Signalling

Existen dos formas de señalización:

### A) In-band signalling

En este esquema:

- La señalización utiliza el mismo canal que los datos del usuario.
    
- No requiere canales adicionales.
    
- Reduce el ancho de banda disponible para datos.
    
- Puede comprometer la integridad del canal.
    

Ejemplo: **PSTN**.

**Descripción del diagrama (página 9):**

Se observa que la información de control y la información de datos viajan exactamente por el mismo camino y utilizan los mismos recursos para establecer el circuito.

Representación simplificada:

```
Origen ----[Nodo]----[Nodo]---- Destino
      (Datos + Señalización por el mismo camino)
```

---

### B) Out-of-band signalling

En este caso:

- La señalización viaja por un canal separado.
    
- El canal principal se dedica exclusivamente a datos.
    
- Mayor seguridad y confiabilidad.
    
- Mayor complejidad e infraestructura adicional.
    

Ejemplo: **GSM**.

**Descripción del diagrama (página 11):**

El camino de señalización es distinto al de datos. Ambos no comparten recursos.

Representación simplificada:

```
Camino datos:        A ----- B ----- C
Camino señalización: A == S == S == C
```

---

# 3. Multiplexing

La multiplexación es una técnica que permite combinar múltiples señales o flujos de datos en un único canal de comunicación, optimizando el uso del ancho de banda.

En el receptor, se realiza el proceso inverso llamado **demultiplexación**.

**Descripción del diagrama (página 12):**

Se muestra un bloque MUX con múltiples entradas y una sola salida (1 link, n channels), y un bloque DEMUX que separa nuevamente las señales.

```
Entradas → [MUX] → Canal único → [DEMUX] → Salidas
```

---

# 4. Time Division Multiplexing (TDM)

## 4.1. Concepto

TDM divide el canal de comunicación en intervalos de tiempo (time slots), asignando cada intervalo a una conexión distinta.

El ancho de banda completo se utiliza, pero sólo durante pequeños intervalos de tiempo.

---

## 4.2. Funcionamiento

1. El medio se divide en time slots.
    
2. Cada conexión recibe un slot fijo.
    
3. El proceso es cíclico.
    
4. El receptor reconstruye los datos según la posición temporal.
    

---

## 4.3. Características

- La secuencia de slots asignados a una fuente se llama canal.
    
- Es síncrono porque la asignación es fija.
    
- Los slots se reservan incluso si no hay datos.
    
- Puede operar a nivel de bits o bytes.
    
- No es obligatorio asignar intervalos equitativamente.
    

Ejemplo: **GSM** utiliza TDM para asignar llamadas en la misma frecuencia.

---

# 5. Frequency Division Multiplexing (FDM)

## 5.1. Concepto

FDM divide el ancho de banda en múltiples bandas de frecuencia no superpuestas, cada una asignada a una conexión.

---

## 5.2. Funcionamiento

1. Se divide el espectro total en sub-bandas.
    
2. Cada conexión recibe una banda fija.
    
3. Cada señal se modula en una frecuencia portadora distinta.
    
4. En el receptor se demodula.
    

---

## 5.3. Características

- Canales activos simultáneamente.
    
- Uso de bandas de guarda (guard bands).
    
- Se asigna banda aunque no haya datos.
    

Ejemplo: PSTN analógico.

---

# 6. Ventajas y Desventajas de Circuit Switching

## Ventajas

- Throughput constante.
    
- No servicio best-effort.
    
- Sin pérdida ni desorden de datos.
    
- No hay headers → baja sobrecarga.
    
- Modelo simple de comunicación.
    

## Desventajas

- Desperdicio de ancho de banda.
    
- Rechazo de conexiones si no hay recursos.
    
- Tiempo de establecimiento previo.
    
- Los nodos deben mantener estado de conexión.
    

---

# 7. Packet Switching (Conmutación de Paquetes)

## 7.1. Descripción general

Los datos se dividen en paquetes (~1000 bytes), cada uno con:

- Payload (datos).
    
- Header (dirección origen/destino, secuencia).
    

No existe camino dedicado.

Ejemplo: Internet (TCP/IP), ATM, MPLS.

---

## 7.2. Funcionamiento

1. Fragmentación.
    
2. Enrutamiento independiente (store and forward).
    
3. Reensamblaje en destino.
    

---

## 7.3. Conceptos clave

### Packet

Unidad estructurada que sigue modelo OSI/TCP-IP.

### Frame

Unidad enviada directamente por el enlace físico.  
Encapsula al paquete.

Relación:

```
Frame
 └── Packet
      └── Payload
```

---

# 8. Redes enrutadas

Existen dos enfoques:

- Virtual Circuit (packet commutation)
    
- Datagram (packet routing)
    

---

# 9. Packet Routing (Datagram)

Características:

- Connectionless.
    
- Enrutamiento dinámico (BGP, OSPF).
    
- Dirección completa en el header.
    
- Uso de tabla de enrutamiento.
    

No se mantiene estado de conexión.

---

# 10. Packet Commutation (Virtual Circuits)

Características:

- Connection-oriented.
    
- Se establece VC mediante signalling.
    
- Todos los paquetes siguen mismo camino.
    
- Uso de identificadores (labels).
    
- Paquetes de tamaño fijo.
    
- Permite QoS.
    
- Puede reservar recursos.
    

Los nodos mantienen tablas de conmutación con identificadores de entrada y salida.

---

# 11. Establecimiento de Virtual Circuit

Incluye:

- Creación de entradas en tabla.
    
- Reserva opcional de recursos.
    
- Puede configurarse manualmente o bajo demanda.
    
- Existe un delay de establecimiento.
    
- La ruta se determina durante signalling.
    

---

# 12. Similitudes entre VC y Datagram

- Ambos dividen datos en paquetes.
    
- Ambos usan store-and-forward.
    
- Ambos requieren buffers.
    
- Ambos pueden multiplexar enlaces.
    

---

# 13. Diferencias entre VC y Datagram

|Aspecto|Virtual Circuit|Datagram|
|---|---|---|
|Lookup|Identificador VC|Dirección completa|
|Inicio transmisión|Requiere signalling previo|Inmediato|
|Estado en nodos|Sí|No|
|QoS|Posible|Difícil|

---

# Conclusión General

La conmutación de circuitos fue diseñada principalmente para voz, donde se requiere tasa fija y recursos dedicados. Sin embargo, para tráfico de datos variable y bursty, la conmutación de paquetes resulta más eficiente.

La evolución de redes núcleo modernas favorece la conmutación de paquetes por su flexibilidad, eficiencia y escalabilidad, aunque los modelos de circuito virtual permiten combinar ventajas de ambos enfoques mediante mecanismos de QoS y rutas preestablecidas.

---

Si lo deseas, puedo ahora:

- Convertir estos apuntes a PDF.
    
- Hacer un mapa conceptual.
    
- Generar una tabla comparativa más detallada para estudiar.
    
- Crear preguntas tipo examen.