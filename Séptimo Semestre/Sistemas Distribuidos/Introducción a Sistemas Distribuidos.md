## Sistemas

Previo a comprender el funcionamiento de los sistemas distribuidos, resulta importante entender el significado de los **sistemas**, que pueden definirse como un conjunto de elementos capaces de interactuar entre sí para cumplir una función dentro de un ambiente determinado. Por ejemplo, una computadora puede ser entendida como un sistema, en el que trabajan juntos:

- CPU
- RAM
- Disco
- I/O
- OS

Y todos juntos, son capaces de ejecutar programas.

### Sistemas informáticos:

Un **sistema informático**, por su parte, actúa como un intermediario entre las aplicaciones y el hardware; por ejemplo, una app como Spotify requiere de la interacción con el sistema operativo para lograr hacer trabajar a la tarjeta de sonido. En este ejemplo, la aplicación no necesita conocer cómo hacer funcionar a las bocinas directamente, sino que el propio sistema operativo se encarga de hacerlo tras haberse llamado a una función particular. 

### Funciones de un sistema:

Primeramente, un sistema es capaz de ofrecer una interfaz de más alto nivel para operar al hardware más fácilmente que su lenguaje puro. Por ejemplo, al escribir una línea de código, no se requiere controlar directamente ninguno de los componentes internos o externos relacionados con las funciones de esta. 

Todo equipo computacional cuenta con una serie de recursos limitados (dígase sus componentes internos); aquí, el sistema operativo es el que se encarga de gestionarlos. Asumiendo un caso en el que se tienen muchas aplicaciones abiertas, el OS decide a cuál darle prioridad en el momento, así como proteger los recursos utilizados por cada uno.

Así bien, los sistemas proporcionan una serie de funciones comunes que pueden ser accedidos por las aplicaciones: 

- Comunicación
- Acceso a archivos
- Identificación de recursos
- Seguridad
- Composición de servicios

De esta manera, se evita que cada programa tenga que reinventar la manera en la que utiliza los recursos del equipo.

Finalmente, los sistemas operativos buscan mantener una serie particular de propiedades:

- Buen desempeño
- Seguridad
- Tolerancia a fallas

---
## Sistemas Distribuidos

Estrictamente, un **sistema distribuido** está formado por una serie de programas ejecutados en procesos diferentes, aunque comunicándose entre ellos y colaborando para llegar a una misma finalidad:

```
Programa A ───┐
              │
Programa B ───┼──→ trabajan juntos
              │
Programa C ───┘
```

Estos a su vez, pueden trabajar dentro de una misma computadora, o en una serie de ellas. 

Bajo el segundo precepto, un sistema distribuido puede definirse como una colección de computadoras autónomas, dando la ilusión de ser un único sistema homogéneo. Dígase un e-commerce, detrás del que se erigen:

```
              ┌─ servidor usuarios
              │
              ├─ servidor productos
Usuario ──────┼─ servidor pagos
              │
              ├─ servidor recomendaciones
              │
              └─ servidor imágenes
```

Pero parecen integrados como un solo sistema. 

### Computadoras autónomas:

Cada computadora, sin excepción, cuenta con sus propios recursos; es decir, no se comparten entre sí. Cada máquina debe existir y operar de manera independiente, conectándose entre sí a través de una red. 

Por ejemplo:

```
Cliente
  |
  | "dame el usuario 53"
  v
Servidor
  |
  | consulta
  v
Base de datos
```

Y posteriormente:

```
Base de datos
     ↓
Servidor
     ↓
Cliente
```

A esto se le conoce como **interacción cliente-servidor**, en donde el *cliente* envía una petición y el *servidor* devuelve una respuesta.

### Cliente - servidor:

Este es uno de los modelos más utilizados dentro de los sistemas distribuidos. Aquí se tiene:

```
CLIENTE
   |
   | petición
   ↓
SERVIDOR
   |
   | respuesta
   ↓
CLIENTE
```

Al escribir un URL, el navegador envía una petición similar a `GET /video/123`, en donde el servidor responde con la información del video. En este caso, se puede destilar la siguiente equivalencia:

```
Navegador = cliente
Servidor de YouTube = servidor
```

### Business to business:

También conocidas como **B2B**, aquí ya no se tiene una estructura básica cliente - servidor, sino que se prioriza la comunicación entre sistemas empresariales. Por ejemplo, una tienda es capaz de comunicarse directamente con un empresa de paquetería:

```
Amazon
   |
   | crear envío
   ↓
DHL
```

---

## Recursos locales y remotos

Dentro de un sistema distribuido, un recurso puede encontrarse dentro de una máquina cualquiera o dentro de cualquier servidor. Dentro de un sistema local los archivos se almacenan dentro del disco y pueden ser accesados inmediatamente:

```
Mi computadora
 └── archivo.txt
```

Por otro lado, un recurso remoto va a encontrarse dentro de un servidor que será accesado a través de internet:

```
Mi computadora
      │
      │ Internet
      ↓
Servidor
 └── archivo.txt
```

Una infraestructura distribuida intenta permitir utilizar ambas maneras de almacenamiento.

### Ventajas de los sistemas distribuidos:

Utilizar sistemas distribuidos cuenta con una serie de ventajas específicas; por ejemplo, aprovechar recursos que pueden estar repartidos en distintas partes del mundo:

```
Servidor A → usuarios
Servidor B → archivos
Servidor C → base de datos
Servidor D → IA
```

Presentando esto al usuario en forma de una misma aplicación

---
## Multiprocesadores

Existe una diferencia conceptual entre multiprocesadores, multicomputadoras y sistemas distribuidos de información.

Un **multiprocesador** se define como una computadora con múltiples procesadores o núcleos, por ejemplo, un CPU de 8 núcleos:

```
        RAM
         |
 ┌───────┼───────┐
CPU 1  CPU 2   CPU 3
```

Por otra parte, los sistemas distribuidos fungen como máquinas completamente independientes entre sí, siendo dependientes de la infraestructura de red.

---
## La "Metodología Sistema"

Los sistemas deben ser pensados en dos maneras diferentes: no basta con estudiar el funcionamiento de cada componente aislado, sino la manera en la que este interactúa con los demás; por ejemplo:

```
Hardware
   ↕
Sistema operativo
   ↕
Aplicación
   ↕
Usuario
   ↕
Red
   ↕
Otros sistemas
```

Esta metodología se basa en el análisis de:

### Interacciones:

Por ejemplo, la manera en la que se conecta el hardware con el software, la aplicación con el sistema o el sistema con la red:

```
software ↔ hardware
aplicación ↔ sistema
sistema ↔ red
```

### Arquitectura:

La manera en la que están organizados los componentes del sistema:

```
         Frontend
             |
             v
          Backend
         /       \
        v         v
      Cache      DB
```

La arquitectura debe ser capaz de responder preguntas como:

- ¿Qué componentes existen?
- ¿Qué responsabilidad tienen los componentes?
- ¿Cómo se comunican entre sí las partes?
- ¿Dónde se ejecutan los componentes?

### Evaluación:

Es posible analizar el sistema de manera cuantitativa:

```
latencia = 20 ms
throughput = 5000 req/s
CPU = 70 %
```

o cualitativa:

```
¿es fácil de mantener?
¿es robusto?
¿qué problemas encontramos?
```

### Evolución: 

Un sistema normalmente evoluciona con el tiempo; por ejemplo, en el número de usuarios al pasar del tiempo:

```
100 usuarios
    ↓
10 000 usuarios
    ↓
1 000 000 usuarios
```

La arquitectura debe ser capaz de adaptarse a estos cambios.

---

## Paralelismo, Concurrencia y Distribución

A continuación se enlistan parte de los principios fundamentales del campo de estudio que comprende los Sistemas Distribuidos:

- Paralelismo
- Gestión de información
- Arquitectura
- Composición

Estos tópicos se estudiarán a profundidad posteriormente.

### Paralelismo:

Varias tareas se ejecutan simultáneamente al aprovechar diferentes núcleos al mismo tiempo.

```
CPU 1 → tarea A

CPU 2 → tarea B
```

### Concurrencia:

Define la capacidad para ejecutar varias tareas durante un mismo periodo:

```
Tarea A ────┐
Tarea B ───────┐
Tarea C ──┐    │
          tiempo →
```

Cabe destacar, que no necesariamente ocurren exactamente en un mismo instante.

### Distribución:

Dos o más tareas se ejecutan de manera simultánea, pero no en máquinas distintas:

```
Máquina A → tarea A
     ↕
Máquina B → tarea B
```

--- 
## Quality of Service

Por sus siglas QoS, el **Quality of Service** hace referencia a la capacidad de un sistema para cumplir adecuadamente cierto esquema de garantías como:

- Latencia
- Disponibilidad
- Rendimiento
- Seguridad
- Fiabilidad

De manera particular, no solo se desea que un sistema funcione, sino que lo haga correctamente.

--- 
## Tolerancia a Fallas

Un sistema distribuido costa de muchos componentes que trabajan en conjunto para llegar a una misma finalidad; esto, de manera inherente, lleva a un mayor potencial de falla:

```
Servidor A ✅
Servidor B ❌
Servidor C ✅
Red       ✅
DB        ✅
```

La **tolerancia a fallas** es la capacidad que tiene un sistema para mantenerse funcionando incluso a pesar de fallas en sus componentes, ya sea mediante redundancia o con una capacidad limitada.

---
