- Definir un problema con significado.
- Inspeccionar y preparar datos.
- Entrenar y evaluar un modelo.
- Interpretar resultados y riesgos.

La metodología de la clase parte de la modificación de notebooks, explicando las decisiones tomadas y cuestionando los resultados. 

## Patrones en ML

La programación tradicional se caracteriza por ejecutar acciones con base en reglas escritas por el desarrollador; se espera una entrada, y se otorga una salida final.

Por otra parte, en el campo del Machine Learning, se establecen ejemplos y resultados conocidos, los cuales son aprendidos a través de algoritmos, que eventualmente general modelos para trabajar con nuevas entradas. 

Este paradigma se utiliza cuando las reglas son complejas de establecer, pero existen ejemplos situacionales.

---

## Tipos de aprendizaje

En el aprendizaje automático, se tienen tres tipos principales de aprendizaje:

### Aprendizaje supervisado:

Los datos incluyen etiquetas; es decir, ejemplos ya categorizados con base en labels específicos. Esta estrategia permite *clasificar* los datos (Regresión Lineal y Logística).

Las dos categorías básicas de esta metodología son la *clasificación* (predicción de categorías) y la *regresión* (predicción de valores numéricos o categorías).

Por ejemplo, dado el caso de que un estudiante $x$ tenga cierto tiempo de estudio y asistencia a clases, se puede predecir $y$: aprueba o no aprueba la clase.

Aquí, los ejemplos ya incluyen la respuesta correcta 
### Aprendizaje no supervisado:

Aquí solo existen los ejemplos, pero vienen sin ninguna clase de etiqueta de apoyo. Aquí, se efectúa *agrupación* para hallar los patrones útiles. Este proceso se lleva a cabo mediante:

- **Clustering:** Identifica grupos con características similares.
- **Reducción de dimensionalidad:** Representa los mismos datos con menos variables.
- **Exploración de anomalías:** Encuentra observaciones inusuales.

Esto permite, de manera general, agrupar con base en similaridades. Un algoritmo puede descubrir las consecuencias de ciertas acciones con base en los datos ingresados.

Los grupos descubiertos no son iguales o significativos por naturaleza.

Para determinar la cercanía entre grupos y entre los elementos dentro de uno mismo, se hace uso del *silhouette score*.



### Aprendizaje por refuerzo:

El aprendizaje llega a través de un sistema de recompensas acumulativas con base en acciones correctas. De manera general, esta metodología permite a un agente mejorar por su cuenta a través de interacciones con el ambiente, que representa los casos reales. 

Un detalle a destacar, es que las recompensas no deben ser tratadas de forma consecutiva, sino acumulativa, tratando en de mejorar iterativamente.

El funcionamiento de un sistema agéntico de ese tipo se basa en la secuencia a continuación:

---
## Riesgos

Todo sistema de inteligencia artificial está sumamente propenso a caer en sesgos o desarrollar tendencias maliciosas. 

### Riesgos en el modelo y los datos:

Los datos se erigen como el componente central para todo aprendizaje autónomo; de no ser tratados correctamente previo a la implementación, pueden llevar a consecuencias severas.

- Información sesgada o incompleta
- Fugas de datos
- Dist shift
- Métricas mal seleccionadas

### Riesgos en el despliegue:

- Automatización maliciosa
- Confianza injustificada
- Impacto desigual de los errores
- Falta de supervisión humana