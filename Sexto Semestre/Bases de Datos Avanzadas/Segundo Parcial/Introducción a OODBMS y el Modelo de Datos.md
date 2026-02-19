
---

## Object Oriented Data Base Management System

Un **Object Oriented Database Management System**, **OODBMS** por sus siglas, es un gestor de base de datos que se rige con base en los principios del paradigma orientado a objetos que permite almacenar y manipular información persistente. La idea central de su uso, es reducir la brecha entre las obligaciones de un programa (objetos, atributos y métodos) y las de una base de datos tradicional (principalmente tablas y consultas); esto, integrando los datos junto con el comportamiento dentro de una misma unidad conceptual: el **objeto**.

---

## Relational DBMS

Los **Sistemas Gestores de Bases de Datos Relacionales** (**RDBMS**) han sido utilizados muy frecuentemente en la industria durante décadas; esto, gracias a su funcionamiento simple mediante *tablas* y la separación clara que existe entre *paradigmas* y *datos*. Teóricamente, sus bases se encuentran en las *relaciones n-arias* definidas por ($R \subseteq D_1 \times D_2 \times \cdots \times D_n$), el Álgebra Relacional, el Cálculo Relacional y la utilización de las dependencias funcionales para hacer la captura entre relaciones semánticas.

### Fortalezas:

Estos sistemas son ampliamente considerados como una tecnología madura dada su inclusión de la optimización de consultas, mecanismos de indexación, control de la concurrencia y las transacciones con propiedades *ACID*, así como componentes de seguridad operacional como las recuperaciones ante fallos. En acceso (transparente a datos) se apoya de la *persistencia sistemática* automática del sistema, mientras que *SQL*, por otro lado, se enfoca en ser declarativo; es decir, que especifica *qué* se quiere obtener, mas no *como* obtenerlo.

### Limitaciones:

El modelo relacional, a pesar de su madurez, presenta fuertes limitaciones al momento de crear estructuras ricas y cercanas al mundo real; esto, debido a su pobre semántica, en donde los tipos pueden llegar a ser restrictivos y las operaciones no se encuentran naturalmente ligadas a los datos. Así bien, destaca por tener una falta de extensibilidad al no permitir la existencia de tipos complejos, tratándose el DBMS como una caja negra complicada de extender respecto a sus funcionalidades internas.

Otra de las desventajas importantes es que, a pesar de que los *DML* (particularmente SQL) son excelentes en el campo de las consultas, no son lenguajes de programación completos, por lo que no cuentan con la capacidad de crear lógica procedural en las aplicaciones. El punto de quiebre suele ser el llamado **problema de impedancia** (*impedance mismatch*) entre el lenguaje de consulta y el de programación, en donde se contraponen los paradigmas *declarativo* y *procedural*, al igual que las estructuras de *conjuntos* y *elementos*, lo que obliga a realizar constantes conversiones entre los tipos de elementos.

---

## Lenguajes de Programación

Los **lenguajes de programación** (PL) integran el uso de los datos y la lógica de manera natural, ofreciendo además una fuerte expresividad a través de conceptos como la modularidad, la herencia y los sistemas de tipos. Igualmente, permiten optimizar la ejecución a través del manejo directo de la memoria central, los cachés y los recolectores de basura; sin embargo, la *persistencia* con regularidad requiere del uso de mecanismos explícitos; es decir, escribir variables a bloques persistentes para leerlas después; esto no equivale a une gestión transaccional completa como en un DBMS. Otro de los contrastes es el hecho de que los PL operan a un único nivel de abstracción, mientras que los gestores tradicionales se manejan en niveles internos y externos (como ANSI/SPARC).

### El problema práctico entre PL y DML:

Cuando una aplicación utiliza al mismo tiempo un PL y un RDDBMS, se tienen una serie de desventajas particulares:

- Deben aprenderse dos lenguajes y estilos de programación distintos.
	
- Se realizan conversiones continuas entre el espacio de trabajo de la base de datos y el programa.
	
- Se debe tener cuidado al elegir las operaciones que se ejecutan en el DBMS y en el programa. 
	
- Se tiene una comunicación muy frecuente entre el cliente y el servidor.

Para solventar estas problemáticas, el OODBMS permite que los objetos se trasladen directamente desde el disco hacia la pantalla, integrando el manejo de los *datos* y el *comportamiento*, soportando un lenguaje de consulta orientado a objetos como **OQL**.

---

## Bases de Datos Orientadas a Objetos

Las **bases de datos orientadas a objetos** llevan a cabo la aplicación de los conceptos propios del paradigma orientado a objetos al almacenamiento persistente. Por desgracia, no existe un soporte técnico matemático consolidado como en el mundo relacional (salvo el sustento proveniente de los mismos lenguajes de programación). Sus orígenes están asociados a:

- Inteligencia Artificial.

- Lenguajes orientados a objetos.

- Investigación en alrededor de conceptos como objetos, clases y modelos semánticos, incluyendo herencias, generalización y composición en bases de datos. 

### Requisitos generales y reglas OO

Entre los requisitos generales, pueden encontrarse muchas de las normativas básicas de cualquier DBMS, como pueden ser:

- Persistencia

- Manejo de disco

- Confiabilidad

- Seguridad

- Compartición de datos.

- Soporte de consultas *ad-hoc*.

Partiendo desde esa base, las reglas particulares de los DBMS orientados a objetos:

- Manejo de **objetos complejos** con identidad

- Soporte para *tipos* o *clases*

- Encapsulación

- Herencia

- Mecanismos de carga y enlace dinámico (*loading and dynamic linked*).

Todo esto, con el objetivo de lograr un DBMS completo y extensible.

### Modelos en un OO DBMS:

En el actual enfoque, un sistema orientado a objetos se describe a través de diversos modelos complementarios:

---
---

1. **Modelo de datos (estructura / parte estática):** define cómo se representan los objetos y sus valores, incluyendo colecciones y estructuras complejas.
    
2. **Modelo de comportamiento (operaciones / parte dinámica):** define qué operaciones pueden ejecutarse sobre los objetos.
    
3. **Modelo de nombres (puntos de entrada):** describe cómo se localizan y referencian los objetos dentro de la base.
    
4. **Modelo de persistencia (qué es persistente y qué no):** determina qué entidades sobreviven a la ejecución del programa y cómo se gestionan.
    

---

## ODMG: estandarización para bases de datos orientadas a objetos

El **Object Database Management Group (ODMG)** surge como un grupo para definir estándares de bases de datos orientadas a objetos, asociado en cierta medida a OMG (Object Management Group). Se indica su creación a mediados de 1991, con especificaciones como ODMG-93, y revisiones posteriores (95, 97 como ODMG 2.0, 99 como ODMG 3.0 con incorporación de Java).

El objetivo es asegurar **portabilidad** entre productos, normalizando un modelo de datos y lenguajes orientados a objetos. La especificación abarca: **Object Model**, **ODL** (Object Data Definition Language), **OML** (Object Manipulation Language), **OQL** (Object Query Language) e interfaces para **C++**, **Smalltalk** y **Java**.

---

## Modelo de datos orientado a objetos: conceptos clave

El modelo de datos OO incorpora:

- **Objetos complejos:** no solo valores atómicos, sino tuplas/estructuras, bolsas (bags), conjuntos (sets), listas (lists), etc.
    
- **Asociaciones entre objetos:** relaciones 1:1, 1:N y N:M.
    
- **Identidad de objeto:** independencia respecto al valor, referencias y compartición de objetos.
    
- **Clases y tipos:** para caracterizar objetos de la misma naturaleza.
    
- **Herencia:** relación de especialización “is a”, que induce un orden parcial sobre tipos/clases.
    
- **Independencia entre modelos lógico y físico:** la estructura conceptual no debe depender de cómo se almacena físicamente.
    

---

## Objetos como “datos + comportamiento”: encapsulación e interfaz

Un objeto integra **estado (datos)** y **comportamiento (métodos)**. La encapsulación implica que el valor interno se considera privado, y que el acceso o modificación se realiza mediante métodos (por ejemplo, `getName`, `setName`, `getCapital`, `addCity`). Además, los valores pueden ser complejos (estructuras anidadas y colecciones), y cada objeto posee un **identificador único**. Los métodos constituyen la **interfaz del objeto**; en términos OO, el objeto recibe mensajes y ejecuta operaciones.

**Aviso de diagrama en las diapositivas:** en el material se muestra un esquema donde un objeto “Country” con identificador (por ejemplo `c1`) ofrece métodos como `setName/getName/getCapital/addCity` y contiene una estructura con atributos `name`, `capital` y `cities` que incluye referencias a otros objetos (por ejemplo `t1, t2, t3`). A continuación se describe en ASCII una versión fiel a la intención del diagrama.

```text
Objeto Country (id: c1)
  Métodos (interfaz):
    setName(), getName(), getCapital(), addCity(), ...
  Estado (valor complejo):
    struct(
      name: "México",
      capital: t1,
      cities: Set<t1, t2, t3>
    )
```

---

## Valores complejos: estructuras y colecciones anidadas

Una característica central es la posibilidad de representar valores complejos sin “aplanarlos” a tablas. Se ejemplifica con una estructura tipo persona que contiene un conjunto de nombres y una dirección que, a su vez, es otra estructura. Este tipo de modelado permite capturar jerarquías de información de forma directa.

Ejemplo conceptual (mismo estilo del material):

- Una persona puede modelarse como `struct(name, first_names, birth_date, address)`.
    
- `first_names` puede ser un `set<string>`.
    
- `address` puede ser un `struct(number, street, zip_code, town)` anidado.
    

---

## Objetos y valores: formalización con identidad

Se diferencia entre **objeto** y **valor** de manera explícita. Un objeto puede verse como un par ((i, v)), donde (i) es el identificador y (v) el valor (que puede ser atómico o complejo). El valor puede adoptar distintas formas: átomo (integer, float, char, string, etc.), tupla (atributos), conjunto (set) o lista (list). Esta visión permite representar que dos objetos distintos pueden tener valores iguales pero identidades distintas.

**Aviso de diagrama en las diapositivas:** se muestra un esquema que clasifica “atom / struct / set / list” como formas del valor asociado a un identificador. A continuación se resume en ASCII.

```text
Objeto = (id, valor)

valor puede ser:
  atom   -> integer | float | bit | char | string | ...
  tuple  -> tuple(a1: v1, a2: v2, ... an: vn)
  set    -> set(v1, v2, ... vn)
  list   -> list(v1, v2, ... vn)

(En el esquema original se visualizan las formas: list / struct / atom / set)
```

---

## Identificador (OID): referencia, compartición y diferencia entre identidad e igualdad

El **identificador** de un objeto funciona como referencia única (al menos dentro del alcance definido por el sistema, y en ODMG se enfatiza “dentro de la base”). Este identificador es **independiente** de los valores de atributos, lo que habilita la **compartición** (varios objetos pueden referenciar al mismo objeto) y permite construir **grafos de composición**, incluso con ciclos. Se remarca que **identidad** (ser el mismo objeto) y **igualdad** (tener el mismo valor) son conceptos diferentes.

---

## Ejemplo: México y sus ciudades como objetos relacionados

Se presenta un ejemplo con un objeto que representa a “México” y objetos que representan ciudades importantes. El país (por ejemplo `c1`) referencia a su capital (`t1`) y a un conjunto de ciudades (`t1, t2, t3`). Cada ciudad referencia de vuelta al país, mostrando enlaces bidireccionales a nivel conceptual (aunque el mecanismo exacto depende del modelo/ODL).

La idea esencial es que el país no almacena “copias” planas de ciudades; mantiene **referencias** a objetos ciudad, y esas ciudades pueden compartirse o relacionarse sin duplicación.

---

## Grafo de composición: representación estructural de referencias

**Aviso de diagrama en las diapositivas:** se muestra un grafo donde `c1` apunta a `t1` como capital y a un conjunto `{t1, t2, t3}` como ciudades; cada ciudad apunta al país mediante `country`, y almacena su `name` y `population`. Esto se representa en ASCII como grafo dirigido de composición/referencias.

```text
c1 (Country)
 |-- name = "México"
 |-- capital --> t1
 |-- cities  --> Set{ t1, t2, t3 }

t1 (Town)
 |-- name = "D.F."
 |-- population = 19.3
 |-- country --> c1

t2 (Town)
 |-- name = "Guadalajara"
 |-- population = 4.1
 |-- country --> c1

t3 (Town)
 |-- name = "Monterrey"
 |-- population = 3.8
 |-- country --> c1
```

---

## Clase vs. tipo; instancia de clase vs. instancia de tipo

En el enfoque OO, **un objeto es instancia de una clase**, mientras que **un valor es instancia de un tipo**. La clase define la estructura (por ejemplo, `name: String`, `capital: City`, `cities: Set<City>`) y además define las operaciones (métodos) disponibles para las instancias. Esta distinción separa el mundo de los valores (tipos) del mundo de los objetos con identidad y comportamiento (clases).

**Aviso de diagrama en las diapositivas:** se contrasta una instancia concreta `Country` con su definición de clase/tipo. A continuación se refleja la idea en ASCII.

```text
Clase Country:
  struct(
    name: String,
    capital: City,
    cities: Set<City>
  )
  Métodos: setName(), getName(), getCapital(), addCity(), ...

Instancia (objeto):
  struct(
    name: "México",
    capital: t1,
    cities: Set{t1, t2, t3}
  )
```

---

## Ejemplo de definición de clases y su grafo de tipos

Se ilustra la relación entre `Country` y `Town` (o “Town/City” según el ejemplo) mediante clases con atributos y referencias (relaciones). Por ejemplo, `Country` puede tener `towns: set<Town>`, y `Town` puede tener `town_state: Country` junto con su `population`. Esta estructura produce un grafo de referencias entre clases, reflejando la composición y asociación.

---

## ODMG: modelo de objetos

En el modelo ODMG:

- Un **OBJECT** está caracterizado por un **tipo (CLASS)** que asocia **estado** y **comportamiento**; un objeto es instancia de una clase.
    
- El **estado** se define por un conjunto de valores almacenados en **propiedades** (atributos); dichos valores pueden cambiar con el tiempo.
    
- El **comportamiento** se define por un conjunto de operaciones ejecutables sobre el objeto.
    
- La base de datos se entiende mediante intención/extensión: las **interfaces y clases** definidas en ODL (intención) y los **valores/objetos** almacenados (extensión).
    

---

## Clase e interfaz en ODMG: especificación externa e implementación

ODMG distingue entre:

- **CLASS:** contiene una especificación externa (propiedades, operaciones, excepciones) y una o más implementaciones (aspectos internos).
    
- **INTERFACE:** especificación abstracta del comportamiento; en la presentación también se menciona como especificación abstracta del comportamiento y del estado, enfatizando que describe “qué existe” sin imponer una implementación concreta.
    

**Aviso de diagrama en las diapositivas:** se presenta una organización conceptual que relaciona Interface/Class/Literal y separa “Operations” y “State (Properties)”. A continuación se describe en ASCII.

```text
INTERFACE / CLASS / LITERAL
   |         |
Operations   State (Properties)
```

---

## Literal en ODMG: valores sin identidad propia

Un **literal** es un valor que **no tiene identificador**, no actúa como referencia y se encuentra **incluido** dentro de un objeto (como parte de su estado). Se enumeran categorías:

- **Atomic_literal:** long, float, boolean, char, string, short, etc.
    
- **Collection_literal:** set, bag, list, array, dictionary.
    
- **Structured_literal:** date, interval, time, timestamp.
    
- **Structure:** estructuras definidas por el usuario (por ejemplo, `struct Address { ... }`).
    

La consecuencia práctica es que, al copiar un literal, se copia el valor; no se preserva una identidad compartida como sí ocurre con objetos referenciables.

---

## Objeto en ODMG: identidad dentro de la base y formas de objeto

En ODMG, un **objeto** sí tiene un identificador único **dentro de la base de datos**. Se contemplan objetos atómicos definidos por el usuario y objetos de colección (`Set`, `Bag`, `List`, `Array`, `Dictionary`) donde el tipo interno (t) puede ser a su vez un objeto o un literal. También se incluyen objetos estructurados para conceptos temporales como `Date`, `Interval`, `Time`, `TimeStamp`.

---

## Tipos en ODMG: mapa completo de literales y objetos

ODMG organiza los tipos en dos grandes familias:

1. **Literal type**
    

- Atómicos: long/short, float, char, string, boolean, enum<>
    
- Colecciones: set<>, bag<>, list<>, array<>, dictionary<>
    
- Estructurados: date, time, timestamp, interval, structure<>
    

2. **Object type**
    

- Atomic_object (definido por el usuario)
    
- Collection_object: Set/Bag/List/Array/Dictionary
    
- Structured_object: Date/Time/Timestamp/Interval
    

Se advierte prestar atención a la diferencia entre `date` y `Date` (distinción de tipo literal vs. tipo objeto/estructurado en la convención mostrada).

---

## Interfaz ODMG: ejemplo “Student-IF” (atributos, relaciones, operaciones y excepciones)

Se presenta una interfaz `Student-IF` como ejemplo de cómo una interfaz puede especificar:

- **Atributos** (por ejemplo, `name`, `student_id`, `address`).
    
- **Relaciones** con otros tipos de objetos, incluyendo especificación de inversa (por ejemplo, `takes` inversa de `Section::is_taken_by`).
    
- **Operaciones** con parámetros de entrada.
    
- **Excepciones** que pueden ser lanzadas por operaciones (por ejemplo, prerrequisitos no satisfechos, sección llena, curso lleno).
    

Este ejemplo muestra que el modelo OO en bases de datos no solo describe estructura, sino reglas operacionales y contratos de uso (incluyendo manejo explícito de condiciones de error).

---

## Atributos ODMG: valores literales, almacenamiento opcional y atributos calculados

Un **atributo** toma un **valor literal** y tiene nombre y tipo asociado. Un punto relevante es que un atributo **no necesariamente está almacenado**: puede derivarse o calcularse, como el caso típico de `age`, que puede implementarse como método a partir de la fecha de nacimiento. También se menciona que no existe referencia “a través de atributos” en el sentido de que el atributo, como tal, está pensado para literales; los enlaces entre objetos se gestionan a través de **relaciones**.

---

## Relaciones ODMG: enlaces entre objetos, inversas e integridad referencial

Una **relación** enlaza objetos con cardinalidades 1:1, 1:N o N:M. Se enfatiza que son binarias y bidireccionales, implementadas mediante dos funciones (encabezados) en ambas direcciones, y que se declaran como **inversas** entre sí (por ejemplo, `teaches` en `Professor` y `is_taught_by` en `Section`). El sistema gestiona la **integridad referencial**, es decir, mantiene consistentes los enlaces al insertar, borrar o modificar asociaciones.

**Aviso de diagrama en las diapositivas:** se muestra un enlace bidireccional entre `Section` y `Professor` con las funciones inversas. En ASCII:

```text
Professor  --teaches-->   Section
Professor  <--is_taught_by-- Section
(inversas; el sistema mantiene integridad referencial)
```

---

## Clase ODMG: ejemplo “Professor” (atributos, enums y relaciones)

Una **clase** define la estructura de sus instancias (datos) y los métodos que operan sobre esas estructuras. El ejemplo `Professor` incluye atributos como `name`, `faculty_id`, `annual_salary` y un atributo `rank` como enumeración (`full`, `associate`, `assistant`). También incluye una relación `teaches` hacia un conjunto de `Section`, declarada como inversa de `Section::is_taught_by`.

---

## Clase ODMG: ejemplo “Section” y el tipo estructurado “salary”

Se muestra una clase `Section` con un atributo `number` y una relación hacia `Professor` llamada `is_taught_by`, inversa de `Professor::teaches`. Además, se define un `struct salary` con campos `base`, `overtime` y `bonus` como ejemplo de tipo estructurado que puede usarse en atributos.

---

## Conclusión conceptual: por qué OO DBMS y qué aporta ODMG

El enfoque OO DBMS busca resolver fricciones prácticas y conceptuales entre programas y bases de datos al tratar la información como **objetos persistentes con identidad, estructura compleja y comportamiento encapsulado**. ODMG, como estándar, intenta estabilizar este ecosistema con un modelo de objetos, lenguajes de definición/manipulación/consulta (ODL/OML/OQL) y reglas claras sobre tipos, literales, clases, interfaces y relaciones inversas con integridad referencial administrada por el sistema. En conjunto, la propuesta apunta a un DBMS más **extensible**, más cercano a los modelos de software OO y más natural para dominios donde la complejidad estructural y la semántica de relaciones entre entidades son centrales.