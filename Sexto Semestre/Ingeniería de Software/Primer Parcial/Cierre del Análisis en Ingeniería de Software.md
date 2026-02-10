## Desarrollo

En el campo de estudio de la Ingeniería de Software, el cierre del análisis representa una **fase crítica** respecto a la transición entre el marco de comprensión profunda del problema y el comienzo de la ejecución ágil de la solución. Esta etapa es la encargada principal de *producir certeza*, pasando a eliminar ambigüedades previo al ingreso de los marcos de trabajo en un esquema *Scrum*.

El avance hacia un proceso ágil sin la realización previa de un análisis cerrado, no incrementa la velocidad real en la que avanza el desarrollo, sino únicamente la construcción de un sistema incorrecto. La agilidad se encuentra diseñada de manera que sea posible gestionar aspectos tales como la **incertidumbre técnica**, pero jamás compensa la ignorancia respecto al dominio del problema real.

---

## Importancia de Cerrar Correctamente el Análisis

### Riesgo de ambigüedad:

En caso de que los requerimientos no se encuentren claramente comprendidos, un equipo de desarrollo puede comenzar a trabajar con base en *suposiciones*, lo que puede llevar a generar soluciones que, si bien pueden funcionar a nivel técnico, son funcionalmente inútiles. Un proyecto ágil pobremente fundamentado puede llevar a iteraciones rápidas de errores.

### Costo del error

De acuerdo con la denominada **Ley de Bohem**, uno de los errores cometidos más frecuentemente en la fase de análisis de requerimientos, corregirlos puede llegar a costar hasta *cien veces más* durante fases posteriores. Esto, por supuesto, se debe a que los errores en las fases tempranas se propagan hacia el diseño, la implementación, las pruebas integrales y el despliegue. Por tales motivos, resulta de suma importancia recalcar el hecho de que el análisis debe basarse fuertemente en la evidencia observada y no en opiniones o intuiciones subjetivas.

---

## Design Thinking aplicado a la Ingeniería de Software

El **design thinking** se define como un enfoque de resolución de problemas centrado en el usuario, buscando generar soluciones innovadoras con base en el entendimiento profundo de las necesidades reales de las personas, cuestionando los supuestos y experimentando de manera iterativa.

Las principales características de este esquema de diseño son la *empatía*, *creatividad* y *análisis*, y se aplica en campos como el diseño de productos, servicios, educación, negocios e ingeniería. Cabe resaltar que esto no es una metodología rígida, sino una forma de pensar que prioriza entender por completo y correctamente un problema antes de proponer una solución orientada al bienestar del usuario.

De manera general, el *design thinking* es un proceso que se desarrolla de manera iterativa en cinco etapas centrales:

- **Empatizar:** Observar y comprender al usuario, sus contextos, sus problemas y sus motivaciones de manera humanista.
- **Definir:** Se sintetiza la información de manera que sea posible fundamentar la problemática claramente. 
- **Idear:** Se genera una lluvia de ideas con la finalidad de hallar soluciones posibles para la problemática.
- **Prototipar:** Implica la constitución de representaciones simples y visuales para llevar a cabo la evaluación preliminar de la solución.
- **Evaluar:** En esta fase, se prueban los prototipos realizados (con la retroalimentación de los usuarios) con el fin de mejorar la propuesta desarrollada durante la fase previa.

El *design thinking* tiene el objetivo principal de reducir los riesgos de fracaso; esto, ya que las soluciones desarrolladas se basan en las experiencias reales de los usuarios, teniendo como punto focal la innovación práctica y aplicable en el contexto deseado.

![Image](https://images.openai.com/static-rsc-3/iSMswwjcT7bnskIAfzFr6iukLXERQbmxe_fbrAokf0D30wxiq4OciClLdalza8boI0o2LTXi7r2ioRHBHq8BqpLxD5oc27kQnMbnhe9XLMY?purpose=fullsize&v=1)

![Image](https://images.openai.com/static-rsc-3/mORUXnxpQ5rImit3v19RMkNyWv3w9ONNCGvyuGE575JFkNCeR0MhIFZrI9lhRTKs3cz4Zvpke7YqUlQ3rpGnKdBzB72Dt2jCyJD-BBwwF7I?purpose=fullsize&v=1)

![Image](https://media.nngroup.com/media/editor/2020/02/24/faux-journey-map.jpg)

El *design thinking*, en el contexto de la Ingeniería de Software, funge como uno de los pilares fundamentales para la extracción de especificaciones técnicas a partir del comportamiento real de los usuarios respecto a sus necesidades.

Resulta de suma relevancia identificar las causas principales de las problemáticas previo al planteamiento de las soluciones técnicas, ideando las conceptuales primeramente y antes de su implementación.

---

## Artefactos de Formalización del Análisis

Con la finalidad de cerrar adecuadamente el análisis preliminar, se hace uso de artefactos que permiten llevar a cabo la transformación de las observaciones cualitativas en información técnica clara e interpretable.
### Persona (arquetipo de usuario):

La **Persona** se define como un arquetipo diseñado con base en el usuario base sin representar a un individuo real; este tiene la característica principal de que encapsula patrones de comportamiento y problemáticas relevantes a resolver mediante la solución planteada. Este perfil técnico debe incluir:

- **Metas funcionales:** Las cosas que intenta lograr el usuario en su trabajo cotidiano.
- **Frustraciones actuales:** Se relaciona con procesos, sistemas o restricciones que impiden al usuario lograr sus objetivos.
- **Nivel de competencia digital:** Parámetro que indica la capacidad técnica que tiene el usuario para interactuar con el programa, lo que influye en el diseño de la interfaz y la experiencia general del mismo.

Debe enfatizarse la omisión de datos demográficos irrelevantes para el estudio, y concentrarse mayoritariamente en información particular que realmente tenga una aportación técnica.
### Mapa de Empatía:

El **mapa de empatía** es un elemento cuyo propósito principal es dar estructura al contexto psicológico del usuario con la finalidad de hallar contradicciones entre sus palabras y sus acciones. Para ello, se distinguen dos contextos distintos:

- **Contexto externo:** Se toman en cuenta las presiones organizacionales, las exigencias de los superiores y las normativas del entorno del trabajo, mismas que permiten definir las restricciones del sistema.
- **Contexto interno:** Se busca encontrar una brecha entre las palabras y las acciones del usuario; por ejemplo, si este afirma que un sistema le resulta fácil de utilizar, pero constantemente lo evita, esto pasa a generar un *requerimiento no funcional*.

### Customer Journey Map (estado actual):

Un **Jorney Map** es un elemento que permite representar el recorrido total de un usuario a través del proceso actual de trabajo, destacando sus estados emocionales, la duración de las acciones y las fricciones que puedan experimentar. En el mapa se encuentran diversos *valles emocionales*, mismos, que serán de utilidad para encontrar áreas de mejora técnica.

El recorrido se divide en:

- **Antes:** Se analizan los motivos por los que se desencadena el proceso, así como las expectativas iniciales del usuario que lo realiza.
- **Durante:** En donde se identifican los puntos de fricción con el sistema, dígase pérdidas de información o lentitud. En esta fase, suelen emerger las **épicas**.
- **Después:** Lapso en el que se evalúa el nivel de éxito o fracaso respecto al objetivo principal del usuario. Esto define los *criterios de éxito* del sistema.

---
---


---

## Definición formal del problema

### Point of View (POV)

El **Point of View** puede definirse como una estructura canónica cuya utilidad se encuentra en centrar el origen de la problemática mediante la definición de:

- Quién es el usuario.
    
- Qué necesita.
    
- Por qué lo necesita.
    
Esta estructura previene la ideación de soluciones prematuras, manteniendo el punto focal hacia la problemática real del usuario.

### How Might We (HMW):

El **How Might We** es una reformulación del problema en dirección a una oportunidad de solución sin llegar a imponer una respuesta particular; es decir, simplemente plantea una solución alternativa con base en una reescritura de la problemática:

> El estudiante de ingeniería del turno matutino necesita conocer la disponibilidad real de espacios antes de ingresar al campus, porque ha observado que perder 20 minutos buscando lugar en un estacionamiento lleno es la causa principal de sus retardos a la primera clase.

A partir de esto, se plantea:

> ¿Cómo podríamos informar al estudiante sobre la ocupación del estacionamiento en tiempo real antes de que salga de su casa?

---

## Transición del análisis al Product Backlog

La fase de cierre de análisis se erige como un *puente* hacia la metodología *Scrum*, mismo para el que se requiere asumir que el análisis previo ya existe y es, en efecto, sólido. Cada uno de los puntos focales extraidos puede ser directamente traducido:

- Los **puntos de dolor** identificados en el Journey Map se transforman en **épicas o funcionalidades**.
	
- Las **necesidades de la Persona** se convierten en **historias de usuario**.
    
- El **HMW** se traduce en **objetivos de sprint**.
	
---

## Entregables formales del análisis

Al finalizar esta fase, el equipo debe contar con:

- Documento de visión que resuma ejecutivamente el problema.
    
- Arquetipos de usuario (mínimo dos perfiles diferenciados).
    
- Journey Map del estado actual con fricciones y tiempos.
    
- Matriz de requerimientos funcionales y no funcionales.
    
- Glosario del dominio con terminología unificada.
    
- Declaración POV validada del problema central.
    
---

