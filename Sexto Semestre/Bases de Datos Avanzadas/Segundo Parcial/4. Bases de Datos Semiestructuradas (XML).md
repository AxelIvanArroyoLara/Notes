Las bases de datos semiestructuradas surgen como una respuesta a las limitaciones de los modelos tradicionales de gestión de datos cuando la información ya no se encuentra siempre perfectamente tabulada, rígidamente definida o confinada a esquemas estáticos. En el contexto de la Web y de los sistemas distribuidos, comenzó a ser cada vez más frecuente trabajar con documentos, intercambios entre aplicaciones heterogéneas y estructuras de datos flexibles. En ese escenario, XML se convirtió en una pieza clave para representar, intercambiar y organizar información.

El enfoque semiestructurado resulta especialmente importante porque no obliga a que todos los datos sigan exactamente la misma estructura interna, como sí sucede en los modelos relacionales clásicos. En lugar de eso, permite que la estructura esté embebida en los propios datos, lo cual facilita la interoperabilidad, la integración y la evolución de sistemas complejos.

---

## Introducción a las bases de datos semiestructuradas

El estudio de las bases de datos semiestructuradas puede entenderse mejor si primero se observa la evolución histórica de los modelos de bases de datos. En una primera etapa, entre las décadas de 1970 y 1980, predominaban los modelos de red y jerárquicos. Posteriormente, entre 1980 y 1990, el modelo relacional se consolidó como el paradigma dominante. Más adelante surgieron los sistemas objeto-relacionales, que ampliaron las capacidades del modelo relacional tradicional.

Sin embargo, la llegada de la Web modificó profundamente la naturaleza de los datos y de las aplicaciones. La Web introdujo un entorno distribuido, vasto, débilmente acoplado y orientado a documentos. Esto significa que los datos ya no se generan únicamente dentro de una base de datos centralizada, sino que pueden estar dispersos entre distintos servidores, aplicaciones y plataformas. Además, ya no siempre presentan una estructura uniforme y predecible.

### Problemas que introduce la Web en el manejo de datos

La Web provoca varios desafíos para los sistemas de bases de datos tradicionales. Entre ellos, se menciona la pérdida o debilidad de ciertas conexiones rígidas entre datos, el uso de servidores de aplicaciones poco acoplados entre sí, la naturaleza distribuida del entorno web, la existencia de una estructuración débil o flexible y la creciente orientación documental de la información.

Todo esto implica que ya no basta con almacenar registros en tablas bien normalizadas. Ahora es necesario representar documentos completos, estructuras jerárquicas, contenido mixto y relaciones que no siempre siguen una forma predefinida y fija.

---

## XML como fundamento del modelo semiestructurado

XML ocupa un lugar central en este tema porque representa una forma estándar de estructurar datos dentro de documentos. Su relevancia radica en que permite integrar datos y metadatos dentro de un mismo formato, lo que favorece el intercambio entre sistemas distintos.

Las bases de datos no pueden permanecer indiferentes ante XML, porque deben ser capaces de almacenar documentos XML, consultarlos y decidir si su incorporación representa una simple evolución tecnológica o una transformación más profunda del paradigma de manejo de datos.

### Preguntas fundamentales que plantea XML

La aparición de XML obliga a reflexionar sobre varias cuestiones esenciales. Primero, qué modelo de datos debe utilizarse para representar información semiestructurada. Segundo, qué lenguaje de consulta debe emplearse para recuperar información de esos documentos. Tercero, cómo integrar las nuevas soluciones basadas en XML con los sistemas previos, especialmente con las bases de datos relacionales y orientadas a objetos.

Estas preguntas muestran que XML no solo es un formato de marcado, sino también un punto de transición entre distintas formas de concebir la información.

---

## Modelos internos y productos relacionados con XML

Las diapositivas describen varias formas en que los productos y sistemas pueden manejar XML. Esto es importante porque no existe un único enfoque técnico para incorporar documentos semiestructurados a un entorno de bases de datos.

### Middleware XML DB

Una primera opción consiste en usar middleware XML por encima de un DBMS tradicional. En este enfoque, XML no se almacena necesariamente de manera nativa, sino que se traduce o mapea hacia estructuras internas del sistema gestor subyacente. Para ello se requieren técnicas sofisticadas de mapeo, pues los documentos XML suelen ser jerárquicos, mientras que muchas bases de datos tradicionales trabajan con estructuras tabulares.

### Sistemas nativos

Otra alternativa son los sistemas nativos XML. Estos sistemas están diseñados específicamente para almacenar, indexar, buscar y manipular documentos XML sin convertirlos forzosamente a otro modelo. Para ello utilizan técnicas especializadas de investigación y almacenamiento, orientadas al manejo directo de árboles, nodos, rutas y documentos.

### Extensiones de sistemas relacionales

También existen extensiones de DBMS relacionales que añaden tipos de datos nativos y soporte para tipos documentales extendidos. Aquí el sistema relacional se adapta parcialmente para manejar contenido XML, manteniendo parte de la infraestructura relacional clásica.

### Bases de datos orientadas a objetos

Finalmente, las bases de datos orientadas a objetos pueden intervenir en este contexto mediante modelos basados en el paradigma orientado a objetos. Dado que este paradigma permite representar estructuras anidadas y complejas, puede resultar útil para modelar información semiestructurada.

---

## Panorama general del contenido del tema

El material se organiza en torno a varios bloques principales. Primero, los modelos de datos semiestructurados y su justificación conceptual. Después, una introducción a XML. Más adelante, las bases de datos XML, sus conceptos fundamentales, los DTD y XML Schema, y finalmente herramientas de consulta como XPath y XQuery. En esta primera parte del documento, el contenido se concentra principalmente en la racionalidad del modelo semiestructurado, la introducción a XML y los fundamentos de DTD y XML Schema.

---

## Introducción formal a XML

XML se presenta como un **metalenguaje universal** para datos en la Web. El término metalenguaje implica que XML no define por sí mismo un conjunto fijo de etiquetas para todos los casos, sino que proporciona las reglas para construir lenguajes de marcado especializados según las necesidades de cada dominio.

XML permite el intercambio de contenido entre aplicaciones y también entre navegadores. Su importancia radica en que estandariza la manera en que la información es procesada.

### Funciones que XML ayuda a estandarizar

Dentro del ecosistema XML, distintas tecnologías complementarias cubren diferentes necesidades:

- **Exchange (XML):** intercambio de datos.
    
- **Presentation (XSL):** presentación y transformación visual o estructural.
    
- **Retrieval (XQuery):** recuperación y consulta de información.
    
- **Security (Encryption, Authentication):** protección y validación de identidad.
    
- **Linking (XLink):** vinculación entre recursos.
    

Esto demuestra que XML no opera de forma aislada, sino dentro de una constelación tecnológica que soporta múltiples procesos en la Web.

---

## La galaxia de estándares alrededor de XML

El material muestra una “galaxia” de estándares relacionados con XML. Esta representación ilustra que XML funciona como núcleo alrededor del cual giran otras especificaciones.

### Principales estándares relacionados

#### XML Schema

Sirve para definir el esquema o estructura permitida de los documentos XML. Es una evolución más potente y expresiva que los DTD.

#### XSL

Corresponde a las hojas de estilo usadas para transformar o presentar documentos XML. Permite separar contenido de presentación.

#### SAX

Es una API de programación orientada a eventos. Resulta útil cuando se necesita procesar documentos XML de forma secuencial y eficiente en memoria.

#### DOM

Es una API orientada a objetos que representa el documento XML como un árbol manipulable. Facilita el acceso estructurado a nodos, atributos y contenido.

#### SOAP

Es un protocolo asociado a servicios web, históricamente muy importante para el intercambio estructurado de mensajes.

#### RDF

Se emplea para la descripción de recursos web, especialmente en contextos de metadatos y Web semántica.

#### ebXML

Es un conjunto de estándares relacionado con comercio electrónico.

#### Otros estándares de negocio

El material también alude a otros lenguajes o estándares especializados para sectores empresariales concretos.

### Descripción del diagrama de la “galaxia de estándares”

En la diapositiva correspondiente aparece un diagrama en el que **XML** se ubica en el centro, rodeado por tecnologías como **XMLSchema**, **DOM**, **SAX**, **SOAP**, **XSL**, **XQuery**, **RDF** y **ebXML**. El diagrama comunica visualmente que XML es el núcleo del ecosistema y que las demás tecnologías orbitan alrededor de él como extensiones o herramientas complementarias.

Una representación ASCII simplificada del diagrama sería la siguiente:

```text
              ebXML
                |
      RDF --- XMLSchema --- DOM
        \         |         /
         \       XML      SAX
          \       |       /
             XSL --- SOAP
                  |
                XQuery
```

Esta representación no reproduce exactamente la forma gráfica original, pero sí conserva la idea conceptual principal: XML como centro integrador de estándares.

---

## Objetivos de XML

XML puede entenderse como un nuevo lenguaje de intercambio basado en etiquetas. Fue diseñado para ser más simple que SGML, pero más complejo y eficiente que HTML en términos de representación estructural de datos.

### Relación entre XML, SGML y HTML

SGML era un metalenguaje poderoso, pero demasiado complejo para muchos usos prácticos en la Web. HTML, por su parte, era muy útil para presentación, pero insuficiente para representar semánticamente datos complejos y estructurados. XML aparece como un punto intermedio: más manejable que SGML y más expresivo que HTML para la representación de datos.

### Contexto histórico

XML fue desarrollado por el XML Working Group bajo la dirección del W3C desde 1996, y XML 1.0 fue adoptado como recomendación oficial del W3C en 1998. Este dato histórico es importante porque muestra que XML no nació como una solución improvisada, sino como una estandarización formal para responder a necesidades reales de interoperabilidad.

---

## Elementos XML

El elemento es la unidad básica de XML. Todo documento XML está compuesto, esencialmente, por elementos delimitados por etiquetas. Un elemento puede contener texto, otros elementos o ambos.

### Estructura básica de un elemento

Un ejemplo simple consiste en un elemento `person` que contiene los subelementos `name`, `age` y `email`. Esta estructura muestra cómo XML representa información de forma jerárquica.

```xml
<person>
  <name>Alan</name>
  <age>42</age>
  <email>alan@abc.com</email>
</person>
```

Aquí, `person` es el elemento raíz del fragmento, mientras que `name`, `age` y `email` son subelementos. Esto permite distinguir claramente el significado de cada dato.

### Ejemplo extendido con varias personas

Más adelante se presenta un documento más amplio con un elemento `table`, una descripción y un conjunto de personas dentro de `people`. La idea importante es que XML no solo guarda datos aislados, sino también su contexto y agrupación lógica.

```xml
<table>
  <description>People on the fourth floor</description>
  <people>
    <person>
      <name>Alan</name>
      <age>42</age>
      <email>alan@abc.com</email>
    </person>
    <person>
      <name>Ryan</name>
      <age>36</age>
      <email>ryan@abc.com</email>
    </person>
    <person>
      <name>Patsy</name>
      <age>58</age>
      <email>patsy@abc.com</email>
    </person>
  </people>
</table>
```

Este ejemplo permite observar que XML expresa mejor la estructura semántica de la información que una simple presentación visual.

---

## Diferencia entre XML y HTML

La comparación con HTML resulta muy reveladora. En HTML se presenta la misma información, pero organizada para visualización:

```html
<h1>People on the fourth floor</h1>
<p><b>Alan</b>, 42 years, <i>alan@abc.com</i></p>
<p><b>Ryan</b>, 58 years, <i>ryan@abc.com</i></p>
<p><b>Patsy</b>, 36 years, <i>patsy@abc.com</i></p>
```

En este caso, HTML indica cómo mostrar los datos, pero no expresa con la misma claridad la estructura lógica interna. XML, en cambio, no se enfoca en la presentación, sino en la representación significativa del contenido.

### Consecuencias de esta diferencia

En XML, nombres, edades y correos se encuentran claramente separados y pueden ser interpretados con facilidad por aplicaciones. No existe información sobre cómo debe presentarse visualmente el contenido, porque ese no es su propósito principal. El texto del documento se considera **PCDATA**, es decir, _Parser Character Data_.

---

## Elementos vacíos

XML permite elementos vacíos, es decir, etiquetas que no contienen contenido interno. Pueden escribirse de dos maneras equivalentes:

```xml
<married></married>
```

o bien

```xml
<married/>
```

Estos elementos resultan útiles para representar la presencia de una propiedad o una marca sin necesidad de contenido textual adicional.

---

## Atributos XML

Un atributo es una propiedad expresada mediante una relación nombre-valor. Se utiliza para añadir información complementaria a un elemento, como idioma, moneda, formato u otros metadatos.

### Ejemplo de atributos

```xml
<product>
  <name language="Spanish">flauta transversal</name>
  <price currency="Pesos">4200.12</price>
</product>
```

Aquí, `language="Spanish"` y `currency="Pesos"` son atributos. El contenido principal sigue estando dentro de los elementos, pero los atributos añaden propiedades adicionales.

---

## Atributos versus elementos

Una parte importante del diseño XML consiste en decidir cuándo conviene usar atributos y cuándo elementos.

### Diferencia en frecuencia

Un atributo solo puede aparecer una vez dentro de un elemento con un nombre dado. En cambio, un elemento puede repetirse múltiples veces. Esto hace que los elementos sean más adecuados cuando se necesita modelar colecciones o listas.

### Diferencia en contenido

El valor de un atributo siempre es una cadena de texto. Un elemento, por el contrario, puede contener subelementos y estructuras internas más complejas. Por ello, cuando se necesita mayor riqueza estructural, los elementos suelen ser la mejor opción.

### Problemas de ambigüedad

Las diapositivas muestran que la misma información puede escribirse de distintas maneras:

```xml
<person>
  <name>Alan</name>
  <age>42</age>
  <email>alan@abc.com</email>
</person>
```

```xml
<person name="Alan" age="42" email="alan@abc.com"/>
```

```xml
<person age="42">
  <name>Alan</name>
  <email>alan@abc.com</email>
</person>
```

Esto demuestra que XML permite múltiples representaciones para la misma información, lo cual da flexibilidad, pero también introduce ambigüedad de modelado. La elección entre atributos y elementos afecta la claridad, la extensibilidad y el procesamiento posterior.

---

## Documentos bien formados

Un documento XML bien formado es aquel que respeta las reglas sintácticas básicas del lenguaje.

### Reglas fundamentales

#### Etiquetas correctamente anidadas

Las etiquetas deben abrirse y cerrarse respetando la jerarquía. No pueden cruzarse de manera incorrecta.

#### Atributos únicos

Dentro de un mismo elemento, un atributo no debe repetirse con el mismo nombre.

#### Relevancia del orden

El orden de los subelementos es importante. Esto significa que dos documentos con los mismos datos pero con distinto orden pueden ser considerados diferentes en términos estructurales.

---

## Namespaces

Los _namespaces_ o espacios de nombres resuelven un problema importante: cómo combinar etiquetas provenientes de distintos contextos sin generar colisiones de nombres.

### Motivación de los namespaces

Si dos vocabularios XML diferentes utilizan una etiqueta llamada `name`, surge la duda de si ambas etiquetas significan lo mismo. Los namespaces permiten distinguirlas mediante prefijos asociados a identificadores universales.

### Principio básico

A cada etiqueta o atributo se le puede asociar un URI que la identifica de forma única. Este URI actúa como identificador global, evitando ambigüedades entre vocabularios distintos.

### Ejemplo conceptual

Se muestra un caso donde `Guide:Nom` y `Annuaire:Nom` pertenecen a espacios diferentes. Aunque ambas etiquetas se llaman `Nom`, el prefijo indica que provienen de taxonomías distintas.

### Declaración de namespaces

#### Con prefijo explícito

```xml
<table xmlns:SD="http://www.SellsDepartment.hp.org">
  <SD:people>
    <SD:person>
      <SD:name>Alan</SD:name>
      <SD:age>42</SD:age>
      <SD:email>alan@abc.com</SD:email>
    </SD:person>
  </SD:people>
</table>
```

#### Con namespace por defecto

```xml
<table>
  <people xmlns="http://www.SellsDepartment.hp.org">
    <person>
      <name>Alan</name>
      <age>42</age>
      <email>alan@abc.com</email>
    </person>
  </people>
</table>
```

En el primer caso se utiliza un prefijo explícito (`SD`). En el segundo, se define un espacio de nombres por defecto para todos los elementos contenidos dentro del bloque correspondiente.

---

## Modelo XML basado en grafos

El material introduce la idea de representar XML mediante un modelo basado en grafos, lo cual se relaciona directamente con la noción de datos semiestructurados.

### Equivalencia entre XML y una expresión semiestructurada

Se presenta el siguiente ejemplo XML:

```xml
<person>
  <name>Alan</name>
  <age>42</age>
  <email>alan@abc.com</email>
</person>
```

Y se muestra una expresión equivalente en términos de datos semiestructurados:

```text
{person: {name: "Alan", age: 42, email: "alan@abc.com"}}
```

Esto permite ver que XML puede interpretarse como una estructura etiquetada y anidada, parecida a un árbol o grafo. Esa es precisamente la base conceptual de los datos semiestructurados: la estructura está integrada en el propio documento.

---

## Referencias en XML

XML también permite asociar identificadores a los elementos mediante atributos específicos. Esto posibilita representar relaciones entre distintos fragmentos del documento sin necesidad de duplicar toda la información.

### Ejemplo de referencia

```xml
<state id="s2">
  <scode>PUE</scode>
  <sname>Puebla</sname>
</state>

<city id="c2">
  <cname>Ciudad de Puebla</cname>
  <state-of idref="s2"/>
</city>
```

Aquí, la ciudad no repite toda la información del estado, sino que apunta a él mediante una referencia. Esto es importante porque introduce enlaces internos similares a relaciones entre entidades.

---

## Importancia del orden en XML

El orden de aparición de los elementos puede cambiar el significado o, al menos, la estructura del documento.

### Ejemplos de orden

```xml
<person>
  <firstname>John</firstname>
  <lastname>Smith</lastname>
</person>
```

no es estructuralmente igual a

```xml
<person>
  <lastname>Smith</lastname>
  <firstname>John</firstname>
</person>
```

De manera parecida, también puede variar el orden de los atributos:

```xml
<person firstname="John" lastname="Smith"/>
```

```xml
<person lastname="Smith" firstname="John"/>
```

En el caso de los atributos, normalmente el orden no tiene relevancia semántica fuerte. Pero en los subelementos, el orden sí puede ser impuesto por la definición del documento o por su esquema.

---

## Otros constructores de XML

Además de elementos, atributos y namespaces, XML dispone de otras construcciones complementarias.

### Comentarios

Se escriben así:

```xml
<!-- this is a comment -->
```

Sirven para insertar anotaciones legibles por humanos que no forman parte del contenido estructural procesable.

### Instrucciones de procesamiento

Ejemplos:

```xml
<?xml version="1.0"?>
<?xml-stylesheet href="book.css" type="text/css"?>
```

Estas instrucciones permiten proporcionar información al procesador XML, por ejemplo, la versión del estándar o la hoja de estilo a utilizar.

### CDATA

Se usa para incluir texto que de otra manera podría confundirse con marcado:

```xml
<![CDATA[<start> an incorrect element </end>]]>
```

Con CDATA, el contenido se interpreta literalmente y no como etiquetas XML.

### Entidades y macros

Para representar ciertos caracteres reservados, se emplean secuencias especiales. Por ejemplo, el carácter `<` se representa como:

```xml
&lt;
```

### Declaración DTD

También puede aparecer una declaración de tipo de documento:

```xml
<!DOCTYPE name [markupdeclarations]>
```

---

## Estructura completa de un documento XML

Un documento XML completo puede incluir, en este orden general:

1. Declaración XML.
    
2. Declaración DOCTYPE.
    
3. Elemento raíz con su contenido.
    

### Ejemplo

```xml
<?xml version="1.0"?>
<!DOCTYPE db SYSTEM "person.dtd">
<db>
  <person> ... </person>
</db>
```

Esto indica que el documento XML puede apoyarse en una definición externa de estructura contenida en un archivo DTD.

---

## DTD: definición de tipo de documento

DTD significa **Document Type Definition**. Su función es actuar como una especie de gramática para documentos XML. Permite definir qué elementos son válidos, en qué orden deben aparecer, cuántas veces pueden repetirse y qué tipo básico de contenido contienen.

### Expresiones regulares en DTD

Los DTD usan operadores similares a expresiones regulares para describir estructuras:

- $e^*$: cualquier número de ocurrencias.
    
- $e^+$: una o más ocurrencias.
    
- $e?$: cero o una ocurrencia.
    
- $e \mid e'$: alternancia.
    
- $e, e'$: concatenación.
    

Estas construcciones permiten modelar secuencias, alternativas y repeticiones.

---

## DTD como gramática

### Ejemplo básico de gramática

```xml
<!DOCTYPE db [
<!ELEMENT db (person*)>
<!ELEMENT person (name,age,email)>
<!ELEMENT name (#PCDATA)>
<!ELEMENT age (#PCDATA)>
<!ELEMENT email (#PCDATA)>
]>
```

Este DTD establece que:

- `db` contiene cero o más elementos `person`.
    
- Cada `person` debe contener exactamente `name`, `age` y `email`, en ese orden.
    
- `name`, `age` y `email` contienen texto parseable.
    

### Ejemplo recursivo

Se muestra también una definición recursiva:

```xml
<!DOCTYPE recursiva [
<!ELEMENT node (leaf | (node,node))>
<!ELEMENT leaf (#PCDATA)>
]>
```

Este ejemplo ilustra que un nodo puede ser una hoja o bien contener dos nodos, permitiendo estructuras recursivas tipo árbol binario.

---

## DTD como esquema para representar información

El material también muestra cómo un esquema relacional puede expresarse en XML con ayuda de un DTD.

### Esquema relacional de partida

Se parte de dos relaciones:

- $R1(A:D1, B:D2, C:D3)$
    
- $R2(C:D3, D:D4)$
    

Después, se genera una representación XML con elementos `r1` y `r2`.

### DTD correspondiente

```xml
<!DOCTYPE db [
<!ELEMENT db (r1*, r2*)>
<!ELEMENT r1 (a,b,c)>
<!ELEMENT r2 (c,d)>
<!ELEMENT a (#PCDATA)>
<!ELEMENT b (#PCDATA)>
<!ELEMENT c (#PCDATA)>
<!ELEMENT d (#PCDATA)>
]>
```

Esto muestra que XML puede utilizarse para representar información relacional, aunque la correspondencia no siempre es tan natural como en el caso de datos jerárquicos o documentales.

### Mezcla de elementos y componentes opcionales

DTD también permite expresar estructuras más flexibles. Por ejemplo:

```xml
<!ELEMENT db ((r1|r2)*)>
```

indica que `db` puede contener una secuencia arbitraria de elementos `r1` o `r2` mezclados.

Asimismo:

```xml
<!ELEMENT r1 (a,b?,c+)>
```

indica que `a` es obligatorio, `b` es opcional y `c` debe aparecer una o más veces.

### DTD externo

El esquema puede almacenarse fuera del documento:

```xml
<!DOCTYPE db SYSTEM "schema.dtd">
```

o incluso en una ubicación remota:

```xml
<!DOCTYPE db SYSTEM "http://.../schema.dtd">
```

---

## DTD y atributos

DTD también permite declarar atributos mediante `ATTLIST`.

### Ejemplo

```xml
<!ATTLIST name language CDATA #REQUIRED
               department CDATA #IMPLIED>
<!ATTLIST price currency CDATA #IMPLIED>
```

Esto significa que el elemento `name` debe tener obligatoriamente el atributo `language`, mientras que `department` es opcional. De forma similar, `price` puede incluir opcionalmente el atributo `currency`.

### Significado de las palabras clave

#### `CDATA`

Indica que el valor del atributo es texto.

#### `#REQUIRED`

Significa que el atributo es obligatorio.

#### `#IMPLIED`

Significa que el atributo es opcional.

---

## DTD y referencias

DTD también puede manejar identificadores y referencias entre elementos. Se ejemplifica con una estructura familiar en la que varias personas se enlazan entre sí mediante atributos como `mother`, `father` y `children`.

El punto importante aquí es que XML puede representar vínculos internos sin necesidad de anidar toda la información. Esto se relaciona directamente con ideas de normalización y modelado relacional.

### Problema de redundancia

Cuando la información se representa por anidamiento, puede repetirse innecesariamente. Las referencias ayudan a evitar esa redundancia.

### Relación con el producto cartesiano

En una representación normalizada, la información puede combinarse posteriormente mediante identificadores, en lugar de repetirse en todos los nodos donde se necesita. Esto recuerda al uso de claves y joins en bases de datos relacionales.

---

## Documentos XML válidos

Un documento XML válido debe cumplir dos condiciones simultáneamente:

### Ser bien formado

Debe respetar las reglas sintácticas básicas de XML.

### Conformarse a un DTD

Además de estar bien escrito, debe ajustarse a la gramática definida en el DTD correspondiente.

### Restricciones de validez

Los identificadores deben representar valores distintos entre sí, y las referencias deben apuntar a identificadores existentes. En otras palabras, no basta con que el documento tenga buena sintaxis; también debe respetar las restricciones estructurales y referenciales declaradas.

---

## Limitaciones de DTD

Aunque DTD fue una herramienta muy importante, presenta varias limitaciones.

### Impone orden

DTD fuerza un orden específico de elementos, salvo que se use alternancia con `|`. Esto puede ser demasiado rígido para algunos escenarios.

### Carece de tipos atómicos ricos

Solo dispone esencialmente de `#PCDATA`, por lo que no distingue formalmente entre números, fechas, cadenas, listas u otros tipos más específicos.

### Limitaciones en referencias

No puede restringir con precisión ciertos tipos de referencias más especializadas. Aunque maneja ideas como identificadores y referencias, su expresividad es limitada.

### Alcance global de etiquetas

Las etiquetas son globales, por lo que pueden surgir conflictos de nombres. Para ello se recomienda el uso de namespaces mediante `xmlns`.

---

## XML Schema

XML Schema surge como una respuesta a muchas de las deficiencias de DTD. Se trata de un lenguaje de especificación de esquemas más sofisticado.

### Ventajas iniciales frente a DTD

Permite restringir elementos mediante tipos de datos específicos, como `xsd:string` y `xsd:decimal`. También posibilita indicar el número mínimo y máximo de ocurrencias de subelementos mediante `minOccurs` y `maxOccurs`.

Por defecto:

- `minOccurs="1"`
    
- `maxOccurs="1"`
    

Esto significa que, salvo que se indique lo contrario, cada elemento debe aparecer exactamente una vez.

---

## Ejemplo comparativo entre DTD y XML Schema

Las diapositivas comparan una definición DTD con una definición XML Schema del mismo caso.

### Ejemplo XML Schema

```xml
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <xsd:element name="db" type="Empleados"/>
  <xsd:element name="person">
    <xsd:element name="name" type="xsd:string"/>
    <xsd:element name="age" type="xsd:decimal"/>
    <xsd:element name="email" type="xsd:string"/>
  </xsd:element>
  <xsd:complexType name="Empleados">
    <xsd:sequence>
      <xsd:element ref="person"
                   minOccurs="0"
                   maxOccurs="unbounded"/>
    </xsd:sequence>
  </xsd:complexType>
</xsd:schema>
```

Aunque el ejemplo del material es esquemático y no necesariamente perfecto en términos de sintaxis estricta moderna, su intención didáctica es clara: mostrar que XML Schema introduce tipos de datos explícitos y control detallado de cardinalidades.

---

## Ventajas de XML Schema

XML Schema posee varias ventajas importantes frente a DTD.

### Tipos definidos por el usuario

Permite crear tipos personalizados, lo que hace posible modelar dominios específicos con mayor precisión.

### Restricción de textos a tipos específicos

Los elementos pueden restringirse a tipos concretos, como numéricos, cadenas, listas y otros.

### Especialización de tipos

Es posible imponer valores mínimos y máximos, así como otras restricciones más precisas.

### Extensión de tipos complejos

Permite extender tipos complejos mediante un mecanismo parecido a la herencia. Esto acerca XML Schema a ideas propias de la orientación a objetos.

### Restricciones de unicidad y claves foráneas

Se pueden establecer restricciones equivalentes a claves únicas y claves foráneas, lo cual fortalece mucho el control de integridad.

### Integración con namespaces

XML Schema se integra con namespaces, permitiendo que distintas partes de un documento se adapten a diferentes esquemas sin conflictos de nombres.

---

## Interpretación general del tema

Las bases de datos semiestructuradas representan una transición desde modelos rígidos hacia formas más flexibles de representación. XML es la tecnología central de esta transición porque permite describir datos y estructura dentro de un mismo documento. A partir de XML, se vuelve posible manejar información jerárquica, documentos complejos, integración entre aplicaciones y modelos menos dependientes de un esquema tabular fijo.

DTD y XML Schema aparecen como mecanismos para formalizar esa estructura. DTD ofrece una primera aproximación gramatical, mientras que XML Schema aporta un control mucho más poderoso sobre tipos, cardinalidades, extensibilidad y restricciones.

---

## Conclusiones

Las bases de datos semiestructuradas surgen como una respuesta natural a las exigencias de la Web, de los entornos distribuidos y de la información orientada a documentos. Frente a la rigidez del modelo relacional clásico, este paradigma introduce estructuras flexibles donde los datos pueden organizarse de forma jerárquica y parcialmente irregular.

XML se convierte en la herramienta central de este enfoque porque permite representar información con significado estructural, independientemente de su presentación visual. A través de elementos, atributos, namespaces, referencias y otras construcciones, XML proporciona una sintaxis capaz de modelar documentos complejos e interoperables.

DTD y XML Schema intentan imponer orden y validez sobre esos documentos. El primero lo hace mediante una gramática relativamente sencilla, mientras que el segundo amplía considerablemente la expresividad al incorporar tipos de datos, restricciones, herencia estructural y control de integridad. En conjunto, estos conceptos sientan las bases para comprender posteriormente cómo consultar, transformar y almacenar documentos XML dentro de sistemas de bases de datos.

---
