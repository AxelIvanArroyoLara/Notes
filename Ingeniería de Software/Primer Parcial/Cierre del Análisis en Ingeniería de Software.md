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

---
---
---

### Persona (arquetipo de usuario)

La Persona define al actor principal del sistema. No representa a un individuo real, sino a un **perfil sintetizado** que encapsula patrones de comportamiento relevantes.

Un perfil técnico adecuado debe incluir:

- **Metas funcionales**, es decir, qué intenta lograr el usuario en su trabajo cotidiano.
    
- **Frustraciones actuales**, relacionadas con procesos, sistemas o restricciones que le impiden alcanzar sus objetivos.
    
- **Nivel de competencia digital**, ya que este factor impacta directamente en decisiones de diseño de interfaz y experiencia de usuario.
    

Se deben evitar datos demográficos irrelevantes y concentrarse exclusivamente en información que tenga **impacto técnico**.

---

### Mapa de Empatía

El mapa de empatía estructura el **contexto psicológico del usuario** y permite identificar contradicciones entre lo que el usuario dice y lo que realmente hace.

- En el **contexto externo (ve y oye)** se analizan presiones organizacionales, exigencias de superiores y normativas, las cuales definen restricciones del sistema.
    
- En el **contexto interno (piensa y siente)** se busca la brecha entre discurso y acción. Por ejemplo, si el usuario afirma que un sistema es “fácil”, pero duda constantemente al usarlo, esto evidencia un **requerimiento no funcional de usabilidad**.
    

---

### Customer Journey Map (estado actual)

El Journey Map representa el recorrido del usuario a lo largo del proceso actual, destacando sus estados emocionales, tiempos y fricciones.

Cada **valle emocional** identificado en este mapa constituye una **oportunidad de mejora técnica**.

El recorrido se divide en:

- **Antes**, donde se analiza el detonante que inicia el proceso y las expectativas iniciales del usuario.
    
- **Durante**, donde se identifican puntos de fricción, pérdidas de información y lentitud del sistema. En esta fase suelen emerger las **épicas**.
    
- **Después**, donde se evalúa si el usuario alcanzó su objetivo o quedó frustrado, lo cual define el **criterio de éxito del sistema**.
    

---

## Definición formal del problema

### Point of View (POV)

El POV es una estructura canónica que permite centrar el alcance del problema. Define claramente:

- Quién es el usuario.
    
- Qué necesita.
    
- Por qué lo necesita.
    

El POV evita soluciones prematuras y mantiene el enfoque en el problema real.

### How Might We (HMW)

El HMW reformula el problema hacia una oportunidad de solución sin imponer una respuesta específica. Por ejemplo:

> El estudiante de ingeniería del turno matutino necesita conocer la disponibilidad real de espacios antes de ingresar al campus, porque ha observado que perder 20 minutos buscando lugar en un estacionamiento lleno es la causa principal de sus retardos a la primera clase.

A partir de esto, se plantea:

> ¿Cómo podríamos informar al estudiante sobre la ocupación del estacionamiento en tiempo real antes de que salga de su casa?

---

## Transición del análisis al Product Backlog

El cierre del análisis funciona como un **puente metodológico** hacia Scrum. Scrum asume que el análisis previo ya existe y que es sólido.

La relación entre artefactos es directa:

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

## Actividad práctica en clase

Durante el taller de formalización, el equipo debe:

1. Sintetizar la información obtenida previamente.
    
2. Visualizar el proceso mediante un Journey Map.
    
3. Definir el POV del problema principal.
    
4. Presentar el hallazgo principal al grupo.
    

---

## Criterios de evaluación

La evaluación del análisis se basa en:

- **Trazabilidad**, verificando que cada problema tenga evidencia observada.
    
- **Profundidad**, evaluando si se identifican causas raíz y no solo síntomas.
    
- **Viabilidad**, asegurando que el problema sea resoluble dentro del tiempo del curso.
    

---

> _“Un problema bien entendido es medio sistema resuelto.”_  
> — Adaptación de Charles Kettering

---

### Próxima sesión

User Story Mapping e inicio de sprints.

Si quieres, puedo **resumir estos apuntes para repaso rápido**, **convertirlos en preguntas tipo examen**, o **extraer solo lo más importante en una hoja de estudio** 📘✨