## Machine Learning

### ¿Qué es Machine Learning?

Machine Learning es una rama de la inteligencia artificial que permite que una computadora **aprenda patrones a partir de datos** sin tener que programar manualmente todas las reglas posibles. En vez de decirle al sistema exactamente qué hacer en cada caso, se le muestran ejemplos para que detecte regularidades y use ese aprendizaje para hacer predicciones o tomar decisiones.

La idea central es que un modelo recibe datos de entrada, encuentra relaciones internas entre ellos y luego usa esas relaciones para responder ante datos nuevos. Por ejemplo, si se le muestran muchos correos ya clasificados como spam o no spam, puede aprender qué características suelen aparecer en cada tipo y después clasificar correos que nunca había visto.

Esto lo diferencia de la programación tradicional. En la programación clásica se escriben reglas explícitas. En Machine Learning, el sistema **aprende esas reglas implícitamente** a partir de los datos.

#### Idea clave

Machine Learning no consiste en “memorizar respuestas”, sino en **aprender patrones generalizables**. Cuando el aprendizaje es bueno, el modelo puede responder correctamente ante casos nuevos, no solo ante los ejemplos con los que fue entrenado.

---

## Tipos principales de aprendizaje

### Aprendizaje supervisado

El aprendizaje supervisado se utiliza cuando los datos de entrenamiento ya incluyen la respuesta correcta. A esa respuesta se le llama **etiqueta**. El objetivo del modelo es aprender la relación entre las entradas y esas etiquetas para luego predecir la salida correcta en casos nuevos.

Por ejemplo, si se quiere detectar si un correo es spam, se entrena al modelo con muchos correos etiquetados previamente como “spam” o “no spam”. El modelo observa patrones en los textos, remitentes, palabras frecuentes y otros atributos para aprender a clasificar.

#### Características principales

- Hay datos de entrada y una salida conocida.
    
- El modelo aprende una correspondencia entre ambas.
    
- Se usa mucho para clasificación y regresión.
    

#### Ejemplos

- Clasificación de imágenes con etiquetas.
    
- Detección de spam.
    
- Predicción del precio de una casa.
    
- Diagnóstico asistido por computadora a partir de ejemplos ya clasificados.
    

### Aprendizaje no supervisado

El aprendizaje no supervisado se utiliza cuando los datos **no tienen etiquetas**. En este caso, el modelo no recibe la respuesta correcta, sino que debe explorar los datos para descubrir estructuras internas, patrones ocultos o agrupaciones naturales.

Aquí no se le dice al sistema qué categoría tiene cada dato. Más bien, el modelo intenta identificar similitudes y diferencias entre los ejemplos.

#### Características principales

- No hay respuesta correcta conocida durante el entrenamiento.
    
- Se buscan patrones, grupos o representaciones internas.
    
- Se usa mucho en clustering y reducción de dimensión.
    

#### Ejemplos

- Agrupar clientes según comportamientos similares.
    
- Detectar segmentos de mercado.
    
- Reducir variables para representar mejor un conjunto de datos.
    
- Encontrar estructuras ocultas en grandes bases de información.
    

### Diferencia principal entre ambos

La diferencia central es que en el **aprendizaje supervisado sí existen etiquetas**, mientras que en el **no supervisado no existen**. Esa es la distinción más importante que suele evaluarse en exámenes introductorios.

---

## Tareas básicas del aprendizaje supervisado

### Clasificación

La clasificación consiste en asignar una entrada a una **categoría o clase**. La salida no es un número continuo, sino una etiqueta.

#### Ejemplos

- Spam o no spam.
    
- Gato o perro.
    
- Aprobado o reprobado.
    
- Fraude o no fraude.
    

En una tarea de clasificación, el modelo aprende a distinguir entre clases con base en ejemplos ya etiquetados.

### Regresión

La regresión consiste en predecir un **valor numérico continuo**. A diferencia de la clasificación, aquí la salida no es una categoría, sino una cantidad.

#### Ejemplos

- Precio de una casa.
    
- Temperatura del día siguiente.
    
- Ingreso mensual esperado.
    
- Tiempo estimado de entrega.
    

#### Diferencia entre clasificación y regresión

La clasificación responde preguntas del tipo “¿a qué grupo pertenece esto?”, mientras que la regresión responde preguntas del tipo “¿qué valor numérico debería tener esto?”.

---

## Modelos clásicos: árbol de decisión

### ¿Qué es un árbol de decisión?

Un árbol de decisión es un modelo que toma decisiones mediante una estructura jerárquica de preguntas o reglas. Cada nodo del árbol representa una condición sobre una característica del dato, y dependiendo del resultado, se sigue una rama distinta.

Por eso se considera un **modelo basado en reglas**.

#### Ejemplo conceptual

Supóngase que se quiere decidir si una persona obtendrá un crédito. El árbol podría comenzar con una pregunta como:

- ¿Tiene ingresos mayores a cierto umbral?
    

Si la respuesta es sí, pasa por una rama; si es no, pasa por otra. Después podrían venir más preguntas como:

- ¿Tiene historial crediticio bueno?
    
- ¿Tiene deudas activas?
    
- ¿Tiene empleo estable?
    

Finalmente, al llegar a una hoja del árbol, se produce una decisión, como “aprobar” o “rechazar”.

### Ventajas del árbol de decisión

- Es fácil de interpretar.
    
- Se parece al razonamiento humano basado en decisiones sucesivas.
    
- Permite visualizar claramente el proceso de decisión.
    

### Limitaciones

- Puede sobreajustarse si crece demasiado.
    
- Puede ser inestable si cambian un poco los datos.
    
- A veces no generaliza tan bien como otros métodos más robustos.
    

---

## Generalización y sobreajuste

### ¿Qué significa generalizar?

Generalizar significa que un modelo no solo funciona bien con los datos que ya vio, sino también con **datos nuevos**. Este es uno de los objetivos más importantes del aprendizaje automático.

Un modelo útil no es el que memoriza el conjunto de entrenamiento, sino el que puede responder correctamente ante ejemplos diferentes pero similares en estructura.

### ¿Qué es el sobreajuste?

El **sobreajuste** u **overfitting** ocurre cuando el modelo aprende demasiado específicamente los datos de entrenamiento. En lugar de captar patrones generales, termina memorizando detalles, ruido o particularidades que solo existen en ese conjunto.

Como resultado, el modelo obtiene muy buen desempeño en entrenamiento, pero falla cuando se enfrenta a datos nuevos.

#### Idea intuitiva

Es como si un estudiante se aprendiera un examen de memoria pregunta por pregunta, pero no entendiera realmente los conceptos. Si el examen cambia un poco, ya no sabe responder.

### Señales de sobreajuste

- Muy alta precisión en entrenamiento.
    
- Mucho peor rendimiento en validación o prueba.
    
- El modelo es excesivamente complejo para la cantidad de datos disponible.
    

### Contraste con subajuste

El subajuste ocurre cuando el modelo es demasiado simple y no logra aprender ni siquiera los patrones básicos. En ese caso falla tanto en entrenamiento como en prueba.

#### Resumen conceptual

- **Subajuste:** el modelo aprende muy poco.
    
- **Buen ajuste:** el modelo aprende lo necesario y generaliza bien.
    
- **Sobreajuste:** el modelo memoriza demasiado y generaliza mal.
    

---

## Evaluación del modelo

### ¿Para qué sirve la validación cruzada?

La validación cruzada sirve para **evaluar el modelo correctamente** y obtener una estimación más confiable de su capacidad de generalización.

En lugar de dividir los datos una sola vez en entrenamiento y prueba, se hacen varias divisiones. Así, el modelo se entrena y evalúa múltiples veces usando diferentes particiones. Esto reduce la dependencia de una sola separación de datos y permite una evaluación más estable.

### Idea general del proceso

Un método común es dividir el conjunto en varias partes. En cada iteración:

- se entrenan varias partes,
    
- se deja una parte para validar,
    
- y luego se rota cuál parte queda fuera.
    

Al final se promedian los resultados.

### Ventajas

- Da una evaluación más robusta.
    
- Reduce el sesgo por una partición afortunada o desafortunada.
    
- Ayuda a comparar modelos de forma más justa.
    

### Importancia para el examen

Cuando se pregunte por validación cruzada, la idea central que debe recordarse es que **sirve para evaluar mejor el modelo**, no para aumentar datos, no para reducir dimensiones y no para cambiar el tipo de modelo.

---

## Deep Learning

### ¿Qué es Deep Learning?

Deep Learning es una subárea del Machine Learning basada en redes neuronales con **muchas capas**. La palabra “deep” se refiere precisamente a la profundidad de la red, es decir, al número de capas intermedias que transforman la información.

Estas capas permiten que el sistema aprenda representaciones cada vez más complejas. Las primeras capas suelen detectar rasgos simples, mientras que las capas posteriores combinan esos rasgos para formar estructuras más abstractas.

### Idea intuitiva

En una imagen, una red profunda puede aprender primero bordes y líneas, luego formas más complejas, después partes de objetos, y finalmente el objeto completo.

### Por qué es importante

Deep Learning ha sido especialmente exitoso en problemas complejos como:

- visión por computadora,
    
- procesamiento de lenguaje natural,
    
- reconocimiento de voz,
    
- generación de contenido.
    

### Diferencia con modelos simples

Los modelos más tradicionales suelen requerir mayor ingeniería manual de características. En Deep Learning, gran parte de esas representaciones se aprenden automáticamente a partir de los datos.

---

## Redes neuronales para imágenes

### CNN: redes convolucionales

Las **CNN** o **Convolutional Neural Networks** son redes diseñadas especialmente para trabajar con imágenes.

Su fuerza principal es que pueden detectar patrones espaciales locales, como bordes, texturas, esquinas y formas, y luego combinar esos elementos en representaciones más complejas.

### ¿Por qué funcionan bien en imágenes?

Las imágenes tienen estructura espacial. Los píxeles cercanos suelen estar relacionados entre sí. Las CNN aprovechan esa propiedad al aplicar filtros que recorren la imagen y extraen características relevantes.

### Qué suelen aprender

- Bordes
    
- Contornos
    
- Texturas
    
- Formas
    
- Partes de objetos
    
- Objetos completos
    

### Idea importante para examen

Cuando se pregunte qué tipo de red se usa principalmente para imágenes, la respuesta clásica esperada es **CNN**.

---

## Redes neuronales para secuencias

### RNN: redes recurrentes

Las **RNN** o **Recurrent Neural Networks** se diseñaron para procesar datos secuenciales. En este tipo de datos, el orden importa. Cada elemento depende, al menos en parte, de los anteriores.

#### Ejemplos de secuencias

- Texto
    
- Audio
    
- Series de tiempo
    
- Señales
    
- Secuencias biológicas
    

### ¿Cómo funcionan en esencia?

A diferencia de una red convencional, una RNN mantiene una especie de estado interno que arrastra información de pasos anteriores. Así puede incorporar contexto pasado al procesar el elemento actual de la secuencia.

### Importancia histórica

Las RNN fueron fundamentales antes del auge de los Transformers y aún son muy relevantes para entender la evolución del campo.

### Problema principal de las RNN tradicionales

Las RNN clásicas sufren el problema de **vanishing gradient**.

#### ¿Qué es el vanishing gradient?

Durante el entrenamiento, los gradientes se propagan hacia atrás para ajustar los pesos del modelo. En secuencias largas, esos gradientes pueden hacerse muy pequeños. Cuando eso ocurre, el aprendizaje de relaciones lejanas en el tiempo se vuelve muy difícil.

#### Consecuencias

- La red olvida información antigua.
    
- Le cuesta captar dependencias largas.
    
- Su entrenamiento se vuelve problemático en secuencias extensas.
    

### Soluciones parciales

Para reducir este problema surgieron arquitecturas como:

- **LSTM**
    
- **GRU**
    

Estas variantes introducen mecanismos que permiten conservar mejor la información importante a lo largo del tiempo.

---

## Mecanismo de atención

### ¿Qué hace la atención?

El mecanismo de atención permite que el modelo **seleccione información relevante** en lugar de tratar toda la entrada con la misma importancia.

La idea es que, en muchos problemas, no todas las partes del dato son igual de útiles para tomar una decisión o generar una salida. La atención permite enfocarse en las partes más importantes en cada momento.

### Ejemplo intuitivo en lenguaje

Si una oración larga se está traduciendo, puede que para traducir una palabra concreta sea necesario concentrarse solo en ciertas palabras de la entrada original. La atención ayuda justamente a hacer esa selección dinámica.

### Ventaja clave

La atención mejora la capacidad del modelo para manejar relaciones importantes incluso cuando están lejos en la secuencia. En lugar de depender únicamente de un estado acumulado como en las RNN, puede acceder más directamente a elementos relevantes.

---

## Transformers

### ¿Qué es un Transformer?

Un Transformer es una arquitectura de red neuronal **basada en atención**, especialmente en el mecanismo llamado **self-attention**.

A diferencia de las RNN, los Transformers no dependen de procesar la secuencia estrictamente paso a paso con una memoria recurrente. En cambio, pueden analizar relaciones entre distintos elementos de la secuencia de manera más directa.

### ¿Qué significa self-attention?

Significa que cada elemento de la secuencia puede “mirar” a otros elementos de la misma secuencia para decidir cuáles son relevantes en su representación.

Por ejemplo, una palabra en una frase puede relacionarse con otra palabra lejana para entender correctamente el significado.

### Ventajas de los Transformers

- Captan dependencias largas con más facilidad.
    
- Permiten procesamiento más paralelo.
    
- Han sido extremadamente exitosos en lenguaje natural.
    
- También se han extendido a visión, audio y otras áreas.
    

### Importancia moderna

Gran parte de los modelos actuales de lenguaje, incluyendo muchos sistemas generativos, se basan en Transformers.

---

## Modelos generativos y discriminativos

### Modelo discriminativo

Un modelo discriminativo aprende a distinguir entre clases o a predecir directamente una salida a partir de una entrada. Su enfoque principal es separar correctamente categorías o mapear entradas a respuestas.

#### Ejemplos

- Clasificar una imagen como gato o perro.
    
- Decidir si un correo es spam o no.
    
- Determinar si una transacción es fraudulenta.
    

### Modelo generativo

Un modelo generativo aprende la estructura o distribución de los datos y puede **generar nuevos ejemplos** similares a los vistos durante el entrenamiento.

#### Ejemplos

- Generar texto.
    
- Generar imágenes.
    
- Crear audio sintético.
    
- Producir nuevas muestras parecidas a las reales.
    

### Diferencia esencial

La diferencia más importante es:

- el **modelo discriminativo** distingue o clasifica,
    
- el **modelo generativo** crea o genera datos.
    

### Ejemplo para fijar la diferencia

Si se tiene un conjunto de imágenes de gatos:

- Un modelo discriminativo puede decir: “esta imagen sí es un gato”.
    
- Un modelo generativo puede producir una nueva imagen que parezca un gato.
    

### Qué caracteriza a un modelo generativo

La palabra clave que debe recordarse para examen es: **genera nuevos datos**.

---

## Relación entre los conceptos del examen

### Conexión general del tema

Todos estos conceptos forman una línea lógica dentro de la inteligencia artificial moderna.

Primero aparece la idea general de Machine Learning: aprender patrones a partir de datos. Después se distinguen dos grandes formas de aprendizaje: supervisado y no supervisado. Dentro del supervisado aparecen tareas como clasificación y regresión. Luego se estudian modelos concretos, como árboles de decisión. Más adelante se analizan problemas de entrenamiento, como el sobreajuste y la necesidad de evaluar bien el modelo con validación cruzada. Finalmente se introduce Deep Learning, junto con arquitecturas especializadas como CNN, RNN y Transformers, y se cierra con la diferencia entre modelos generativos y discriminativos.

### Mapa mental resumido

#### Machine Learning

Aprender patrones a partir de datos.

#### Aprendizaje supervisado

Aprende con etiquetas.

#### Aprendizaje no supervisado

Aprende sin etiquetas.

#### Clasificación

Predice categorías.

#### Regresión

Predice valores continuos.

#### Árbol de decisión

Modelo basado en reglas.

#### Overfitting

Memoriza entrenamiento y generaliza mal.

#### Validación cruzada

Evalúa mejor la capacidad de generalización.

#### Deep Learning

Redes neuronales con muchas capas.

#### CNN

Redes para imágenes.

#### RNN

Redes para secuencias.

#### Vanishing gradient

Problema clásico de RNN tradicionales.

#### Atención

Selecciona información relevante.

#### Transformer

Arquitectura basada en atención.

#### Modelo generativo

Genera nuevos datos.

#### Modelo discriminativo

Distingue o clasifica.

---

## Errores típicos que no deben confundirse en el examen

### Confundir clasificación con regresión

Esto pasa mucho. La clasificación trabaja con etiquetas discretas. La regresión trabaja con valores continuos.

### Pensar que no supervisado significa “menos importante”

No supervisado no significa más simple ni menos útil. Solo significa que no hay etiquetas.

### Decir que el árbol de decisión es una red neuronal

No lo es. Es un modelo basado en reglas y divisiones sucesivas.

### Creer que overfitting significa que el modelo “aprendió muy bien”

No exactamente. Aprender demasiado el entrenamiento puede ser malo si el modelo deja de generalizar.

### Pensar que validación cruzada cambia el modelo

No. Su propósito principal es evaluarlo mejor.

### Confundir CNN con RNN

- CNN: imágenes.
    
- RNN: secuencias.
    

### Decir que el problema de las RNN es que “no pueden clasificar”

Sí pueden clasificar. Su problema clásico es el vanishing gradient.

### Confundir atención con clasificación

La atención no clasifica por sí sola. Su función es enfocar el procesamiento en la información relevante.

### Creer que Transformer es una CNN

No. El Transformer es una arquitectura basada en atención.

### Confundir generativo con discriminativo

El generativo crea ejemplos. El discriminativo separa categorías o predice salidas.

---

## Mini resumen de memorización rápida

### Definiciones clave

**Machine Learning:** aprender patrones a partir de datos.  
**Supervisado:** usa etiquetas.  
**No supervisado:** no usa etiquetas.  
**Clasificación:** predice clases.  
**Regresión:** predice valores continuos.  
**Árbol de decisión:** modelo basado en reglas.  
**Overfitting:** memoriza entrenamiento.  
**Validación cruzada:** evalúa mejor el modelo.  
**Deep Learning:** muchas capas.  
**CNN:** imágenes.  
**RNN:** secuencias.  
**Problema RNN:** vanishing gradient.  
**Atención:** selecciona información relevante.  
**Transformer:** basado en atención.  
**Modelo generativo:** genera nuevos datos.  
**Modelo discriminativo:** clasifica o distingue.

---

## Preguntas de repaso para autoevaluación

### Conceptuales

#### ¿Qué distingue a Machine Learning de la programación tradicional?

Que en lugar de escribir todas las reglas manualmente, el sistema aprende patrones a partir de datos.

#### ¿Qué diferencia principal existe entre supervisado y no supervisado?

La presencia o ausencia de etiquetas.

#### ¿Cuál es la diferencia entre clasificación y regresión?

Clasificación predice clases; regresión predice valores continuos.

#### ¿Por qué un árbol de decisión se considera un modelo basado en reglas?

Porque toma decisiones mediante condiciones sucesivas.

#### ¿Por qué el overfitting es un problema?

Porque el modelo funciona bien en entrenamiento, pero mal en datos nuevos.

#### ¿Para qué sirve la validación cruzada?

Para evaluar de forma más confiable la capacidad de generalización del modelo.

#### ¿Qué hace especial al Deep Learning?

Que utiliza redes neuronales profundas con muchas capas.

#### ¿Por qué las CNN son buenas para imágenes?

Porque detectan patrones espaciales locales.

#### ¿Cuál es el problema clásico de las RNN tradicionales?

El vanishing gradient.

#### ¿Qué hace el mecanismo de atención?

Permite enfocarse en la información relevante.

#### ¿Qué define a un Transformer?

Que es una arquitectura basada en atención.

#### ¿Cuál es la diferencia entre un modelo generativo y uno discriminativo?

El generativo crea datos nuevos; el discriminativo distingue categorías o predice salidas.

---

## Cierre

Para un examen como este, lo más importante no es memorizar palabras aisladas, sino entender la lógica entre los conceptos. Si se comprende que todo parte de aprender con datos, luego distinguir si hay etiquetas o no, después identificar qué tipo de tarea se resuelve, cómo se evalúa un modelo y qué arquitecturas se usan según el tipo de información, entonces las preguntas se vuelven mucho más fáciles de responder.

Lo esencial para fijar bien este bloque es dominar estas asociaciones:

- **supervisado -> etiquetas**
    
- **regresión -> valor continuo**
    
- **clasificación -> categoría**
    
- **CNN -> imágenes**
    
- **RNN -> secuencias**
    
- **RNN tradicional -> vanishing gradient**
    
- **atención -> información relevante**
    
- **Transformer -> atención**
    
- **generativo -> crea datos**
    