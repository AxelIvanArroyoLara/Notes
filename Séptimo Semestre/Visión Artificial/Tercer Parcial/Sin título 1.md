## Introducción

La visión artificial permite extraer información significativa de imágenes digitales mediante operaciones matemáticas que identifican estructuras, regiones, patrones y características espaciales.

Aunque una imagen puede representarse como una matriz de intensidades, su interpretación requiere estudiar no solamente los valores individuales de los píxeles, sino también las relaciones que existen entre ellos.

Dentro de este contexto, los métodos clásicos de visión artificial pueden dividirse en diferentes familias:

- **Detección de características:** identifica puntos, esquinas, bordes y estructuras geométricas.
- **Segmentación:** divide una imagen en regiones que representan objetos o áreas de interés.
- **Análisis de textura:** describe cómo se distribuyen espacialmente las intensidades.
- **Umbralización:** clasifica píxeles mediante criterios globales o locales de intensidad.
- **Análisis multirresolución:** representa una imagen mediante componentes que describen estructuras a diferentes escalas.

Una característica importante es que cada método utiliza una representación distinta de la información visual.

Por ejemplo, un histograma describe cuántos píxeles tienen determinada intensidad, pero no indica dónde están ubicados. Un detector de esquinas analiza la variación de intensidad en distintas direcciones, mientras que una transformada wavelet separa información de baja y alta frecuencia conservando cierta localización espacial.

Por lo tanto, comprender un algoritmo requiere identificar tres aspectos fundamentales:

1. **Qué información utiliza:** intensidades, gradientes, relaciones espaciales o coeficientes transformados.
2. **Cómo procesa esa información:** operaciones matemáticas, comparaciones, acumulaciones o transformaciones.
3. **En qué condiciones falla:** ruido, iluminación, escala, conectividad, contraste o selección de parámetros.

Estos aspectos permiten explicar por qué dos algoritmos pueden producir resultados diferentes incluso cuando trabajan sobre la misma imagen.

---

## Detección de bordes mediante Canny

### Fundamento de la detección de bordes:

Un borde representa una transición espacial de intensidad dentro de una imagen.

Matemáticamente, estas transiciones pueden detectarse mediante el gradiente:

$$
\nabla I(x,y)=
\begin{bmatrix}
\frac{\partial I}{\partial x}\\
\frac{\partial I}{\partial y}
\end{bmatrix}
$$

El gradiente indica la dirección en la que la intensidad aumenta más rápidamente.

Su magnitud es:

$$
G(x,y)=\sqrt{G_x^2+G_y^2}
$$

Y su orientación puede calcularse mediante:

$$
\theta(x,y)=\operatorname{atan2}(G_y,G_x)
$$

Un gradiente elevado sugiere una transición intensa, pero no necesariamente corresponde a un borde verdadero.

El ruido también puede producir cambios bruscos de intensidad.

Por esta razón, Canny combina diferentes operaciones para reducir falsas detecciones y preservar contornos significativos.

### Etapas del algoritmo Canny:

**Suavizado gaussiano**

Antes de calcular el gradiente, se reduce el ruido de la imagen mediante un filtro gaussiano.

$$
I_s=G_\sigma * I
$$

Donde:

- $I$ es la imagen original.
- $G_\sigma$ es el núcleo gaussiano.
- $*$ representa convolución.
- $\sigma$ controla la intensidad del suavizado.

Un valor elevado de $\sigma$ elimina más variaciones pequeñas, pero también puede borrar detalles finos.

**Cálculo del gradiente**

Se estiman las derivadas horizontales y verticales para determinar la magnitud y orientación de los cambios de intensidad.

**Supresión de no máximos**

Esta operación adelgaza los bordes.

Se compara cada píxel con los vecinos situados aproximadamente sobre la dirección del gradiente. Si su magnitud no es un máximo local, se elimina.

De esta manera, una transición ancha puede reducirse a un contorno delgado.

**Doble umbral e histéresis**

Se establecen dos umbrales:

$$
T_L<T_H
$$

Los píxeles se clasifican en tres grupos:

- **Fuertes:** magnitud superior al umbral alto.
- **Débiles:** magnitud entre ambos umbrales.
- **Descartados:** magnitud inferior al umbral bajo.

Los píxeles fuertes constituyen evidencia confiable de un borde.

Un píxel débil se conserva únicamente cuando está conectado, mediante píxeles candidatos, con un borde fuerte.

Esta última operación recibe el nombre de histéresis.

### Importancia de la histéresis:

Los contornos reales no suelen presentar una magnitud de gradiente constante.

Una misma frontera puede atravesar regiones con diferentes niveles de iluminación, contraste o ruido.

Si únicamente se utiliza el umbral alto, los segmentos débiles desaparecen.

El resultado son contornos fragmentados.

En cambio, si solamente se utiliza el umbral bajo, muchas fluctuaciones producidas por ruido sobreviven como bordes falsos.

La histéresis busca un equilibrio:

- Conserva transiciones confiables.
- Recupera segmentos débiles conectados con ellas.
- Descarta respuestas débiles aisladas.

Es importante distinguir la función de la histéresis de la supresión de no máximos.

La supresión de no máximos determina qué píxeles representan los puntos más intensos de una transición.

La histéresis determina cuáles de esos candidatos forman parte de contornos suficientemente confiables.

**Conclusión:** la supresión de no máximos adelgaza los bordes, mientras que la histéresis contribuye a mantener su continuidad.

---

## Detección de líneas mediante la transformada de Hough

### Problema de la representación tradicional:

Una recta suele expresarse mediante:

$$
y=mx+b
$$

Sin embargo, esta representación presenta una dificultad con las rectas verticales, cuya pendiente no es finita.

La transformada de Hough utiliza una representación alternativa:

$$
\rho=x\cos\theta+y\sin\theta
$$

Donde:

- $\rho$ es la distancia perpendicular con signo de la recta al origen.
- $\theta$ es el ángulo de la normal de la recta.
- $(x,y)$ corresponde a un punto de la imagen.

La normal es un vector perpendicular a la recta.

Por ello, $\theta$ no representa directamente la inclinación de la recta, sino la dirección perpendicular a ella.

### Transformación del espacio de imagen al espacio de parámetros:

La idea central de Hough consiste en transformar el problema de detectar una línea en un problema de encontrar coincidencias entre votos.

Cada píxel considerado como borde puede pertenecer a múltiples rectas.

Para un punto fijo $(x,y)$, diferentes valores de $\theta$ producen diferentes valores de $\rho$.

Por tanto:

$$
\rho(\theta)=x\cos\theta+y\sin\theta
$$

Esta expresión describe una curva sinusoidal en el espacio de parámetros $(\rho,\theta)$.

Si varios píxeles pertenecen a una misma recta, sus curvas coinciden en el par de parámetros que representa esa recta.

La transformada utiliza un acumulador:

$$
A(\rho,\theta)
$$

Cada punto de borde incrementa las celdas correspondientes a las rectas que podrían atravesarlo.

Los máximos locales del acumulador representan candidatos a líneas.

### Ejemplo de cálculo:

Se consideran tres píxeles de borde:

$$
P_1=(1,2)
$$

$$
P_2=(3,2)
$$

$$
P_3=(5,2)
$$

Se evalúan cuatro ángulos:

$$
\theta\in\{0^\circ,45^\circ,90^\circ,135^\circ\}
$$

Para $\theta=0^\circ$:

$$
\rho=x
$$

Por tanto, los valores son:

$$
1,\ 3,\ 5
$$

Para $\theta=45^\circ$:

$$
\rho=0.7071x+0.7071y
$$

Los resultados aproximados son:

$$
2.12,\ 3.54,\ 4.95
$$

Para $\theta=90^\circ$:

$$
\rho=y
$$

Los tres puntos producen:

$$
\rho=2
$$

Finalmente, para $\theta=135^\circ$:

$$
\rho=-0.7071x+0.7071y
$$

Se obtiene:

$$
0.71,\ -0.71,\ -2.12
$$

La tabla resultante es:

| Ángulo | $P_1$ | $P_2$ | $P_3$ |
|---|---:|---:|---:|
| $0^\circ$ | 1.00 | 3.00 | 5.00 |
| $45^\circ$ | 2.12 | 3.54 | 4.95 |
| $90^\circ$ | 2.00 | 2.00 | 2.00 |
| $135^\circ$ | 0.71 | -0.71 | -2.12 |

La coincidencia ocurre en:

$$
(\rho,\theta)=(2,90^\circ)
$$

Sustituyendo:

$$
2=x\cos90^\circ+y\sin90^\circ
$$

Como:

$$
\cos90^\circ=0
$$

$$
\sin90^\circ=1
$$

La ecuación queda:

$$
\boxed{y=2}
$$

Esto representa una recta horizontal.

### Interpretación geométrica:

El ángulo de Hough describe la normal, no la dirección de la propia recta.

Por tanto:

- Una normal vertical corresponde a una recta horizontal.
- Una normal horizontal corresponde a una recta vertical.

Esta distinción es importante porque resulta frecuente asociar incorrectamente $\theta=90^\circ$ con una línea vertical.

### Limitaciones de Hough:

La transformada depende de la discretización del espacio de parámetros.

Si los intervalos de $\rho$ y $\theta$ son demasiado grandes, diferentes rectas pueden acumular votos en la misma celda.

Si son demasiado pequeños, los votos de una misma línea pueden dispersarse.

Además, una imagen con demasiados bordes irrelevantes genera numerosos votos adicionales.

Por ello, Hough suele utilizarse después de una etapa de detección de bordes.

---

## Detección de esquinas mediante Harris

### Diferencia entre una región plana, un borde y una esquina:

El detector Harris analiza cómo cambia la intensidad cuando una pequeña ventana se desplaza en diferentes direcciones.

Existen tres situaciones fundamentales.

**Región plana**

La intensidad permanece aproximadamente constante.

Desplazar la ventana horizontal o verticalmente produce cambios pequeños.

**Borde**

La intensidad cambia principalmente en una dirección.

Un desplazamiento perpendicular al borde produce una variación importante, mientras que uno paralelo genera una variación menor.

**Esquina**

La intensidad cambia significativamente en dos direcciones independientes.

Casi cualquier desplazamiento pequeño modifica la apariencia de la ventana.

Este comportamiento puede describirse mediante una matriz denominada tensor de estructura.

### Tensor de estructura:

El tensor se construye a partir de los gradientes de la imagen:

$$
M=
\sum_{(x,y)\in W}
w(x,y)
\begin{bmatrix}
I_x^2&I_xI_y\\
I_xI_y&I_y^2
\end{bmatrix}
$$

Donde:

- $W$ es la ventana de análisis.
- $I_x$ es el gradiente horizontal.
- $I_y$ es el gradiente vertical.
- $w(x,y)$ permite ponderar los píxeles de la ventana.

La matriz suele representarse como:

$$
M=
\begin{bmatrix}
A&C\\
C&B
\end{bmatrix}
$$

Sus eigenvalores, $\lambda_1$ y $\lambda_2$, representan la intensidad de variación en las dos direcciones principales.

### Interpretación de los eigenvalores:

| $\lambda_1$ | $\lambda_2$ | Clasificación |
|---|---|---|
| Pequeño | Pequeño | Región plana |
| Grande | Pequeño | Borde |
| Pequeño | Grande | Borde |
| Grande | Grande | Esquina |

La idea fundamental es que una esquina presenta variación considerable en ambas direcciones.

No basta con que exista un gradiente intenso.

### Función de respuesta de Harris:

Para evitar calcular los eigenvalores explícitamente en cada ventana, Harris utiliza:

$$
R=\det(M)-k\operatorname{tr}(M)^2
$$

Donde:

$$
\det(M)=AB-C^2
$$

$$
\operatorname{tr}(M)=A+B
$$

La constante utilizada en el material es:

$$
k=0.04
$$

Como:

$$
\det(M)=\lambda_1\lambda_2
$$

Y:

$$
\operatorname{tr}(M)=\lambda_1+\lambda_2
$$

También puede escribirse:

$$
R=\lambda_1\lambda_2-k(\lambda_1+\lambda_2)^2
$$

Esto permite interpretar la fórmula:

- El determinante aumenta cuando ambos eigenvalores son grandes.
- El término de penalización depende de la suma de eigenvalores.
- Una distribución muy desequilibrada suele producir una respuesta negativa.
- Dos eigenvalores grandes y comparables pueden producir una respuesta elevada y positiva.

### Ejemplo con tres ventanas:

Se consideran tres ventanas con las siguientes propiedades.

| Ventana | Determinante | Traza | Respuesta Harris |
|---|---:|---:|---:|
| $W_1$ | 10,000 | 520 | -816 |
| $W_2$ | 82,400 | 580 | 68,944 |
| $W_3$ | 11 | 7 | 9.04 |

Para la primera ventana:

$$
R_1=10000-0.04(520)^2
$$

$$
R_1=10000-10816
$$

$$
\boxed{R_1=-816}
$$

Esta respuesta corresponde a un borde.

Para la segunda ventana:

$$
R_2=82400-0.04(580)^2
$$

$$
R_2=82400-13456
$$

$$
\boxed{R_2=68944}
$$

La respuesta elevada y positiva corresponde a una esquina.

Para la tercera:

$$
R_3=11-0.04(7)^2
$$

$$
R_3=11-1.96
$$

$$
\boxed{R_3=9.04}
$$

Aunque el resultado es positivo, su magnitud es muy pequeña en comparación con la segunda ventana.

Por ello se interpreta como una región prácticamente plana dentro de la escala del ejemplo.

### Por qué la suma de gradientes no es suficiente:

Las ventanas $W_1$ y $W_2$ tienen trazas relativamente parecidas:

$$
520\quad\text{y}\quad580
$$

Sin embargo, representan estructuras distintas.

En la primera, los eigenvalores son aproximadamente:

$$
500,\ 20
$$

En la segunda:

$$
331.2,\ 248.8
$$

La primera concentra la variación en una dirección.

La segunda distribuye la variación entre ambas direcciones principales.

Por eso, observar únicamente la suma no permite distinguir adecuadamente un borde de una esquina.

**Conclusión:** Harris evalúa tanto la magnitud de la variación como su distribución direccional.

---

## Segmentación mediante componentes conexas

### Concepto de conectividad:

Una imagen binaria puede representarse mediante una matriz cuyos elementos toman valores de cero o uno.

Habitualmente:

- $1$ representa un píxel perteneciente al objeto.
- $0$ representa el fondo.

El etiquetado de componentes conexas busca identificar grupos de píxeles de objeto que pueden alcanzarse mediante una secuencia de vecinos permitidos.

La definición de vecindad modifica el resultado.

### Conectividad de cuatro vecinos:

Se consideran las posiciones:

$$
N_4(r,c)=
\{
(r-1,c),
(r+1,c),
(r,c-1),
(r,c+1)
\}
$$

Esto incluye:

- Arriba.
- Abajo.
- Izquierda.
- Derecha.

Los píxeles que solamente se tocan por una esquina no quedan conectados directamente.

### Conectividad de ocho vecinos:

Además de los cuatro vecinos anteriores, se incorporan:

$$
(r-1,c-1)
$$

$$
(r-1,c+1)
$$

$$
(r+1,c-1)
$$

$$
(r+1,c+1)
$$

Por tanto, también se permiten conexiones diagonales.

### Efecto sobre el número de objetos:

En el ejemplo de la presentación, una misma máscara produce:

$$
N_4=6
$$

$$
N_8=2
$$

La diferencia aparece porque diferentes grupos que solamente se tocan diagonalmente permanecen separados con conectividad 4, pero se fusionan con conectividad 8.

Para una misma máscara de primer plano:

$$
\boxed{N_8\leq N_4}
$$

Esta propiedad se debe a que cualquier camino válido con conectividad 4 también es válido con conectividad 8.

La conectividad 8 introduce caminos adicionales, pero no elimina los existentes.

### Importancia práctica:

La elección de conectividad puede modificar:

- El número de objetos detectados.
- El tamaño de las regiones.
- La forma de los componentes.
- Las propiedades geométricas calculadas posteriormente.

Por ejemplo, dos células que se tocan diagonalmente pueden contarse como dos objetos o como uno dependiendo de la regla utilizada.

Por tanto, la conectividad forma parte de la definición operacional de un objeto.

---

## Representación de contornos mediante el código de Freeman

### Fundamento del código de cadena:

El código de Freeman describe un contorno mediante una secuencia de movimientos discretos.

En lugar de almacenar todas las coordenadas absolutas del borde, se almacena un punto inicial y las direcciones utilizadas para recorrerlo.

La convención de ocho direcciones utilizada en el material es:

| Código | Movimiento |
|---|---|
| 0 | Este |
| 1 | Noreste |
| 2 | Norte |
| 3 | Noroeste |
| 4 | Oeste |
| 5 | Suroeste |
| 6 | Sur |
| 7 | Sureste |

Se considera que las filas aumentan hacia abajo.

Por ello, moverse hacia el norte disminuye el índice de fila.

### Estimación del perímetro:

Los movimientos horizontales y verticales tienen longitud unitaria.

Los movimientos diagonales tienen longitud:

$$
\sqrt{2}
$$

Por tanto:

$$
P=n_{\text{rectos}}+\sqrt{2}n_{\text{diagonales}}
$$

En esta convención:

- Los códigos pares representan movimientos rectos.
- Los códigos impares representan movimientos diagonales.

### Ejemplo:

Se considera un contorno con:

$$
n_{\text{rectos}}=6
$$

$$
n_{\text{diagonales}}=2
$$

Entonces:

$$
P=6+2\sqrt{2}
$$

$$
\boxed{P\approx8.828}
$$

El valor es una aproximación discreta del perímetro.

Es importante no contar todos los pasos como si tuvieran la misma longitud, porque ello subestimaría los movimientos diagonales.

---

## Evaluación de segmentaciones mediante IoU y Dice

### Intersección sobre unión:

La métrica Intersection over Union, conocida como IoU, mide qué proporción del área cubierta por dos máscaras corresponde a su intersección.

Sean:

- $A$: máscara de referencia.
- $B$: máscara predicha.

Entonces:

$$
IoU(A,B)=\frac{|A\cap B|}{|A\cup B|}
$$

La unión puede calcularse como:

$$
|A\cup B|=|A|+|B|-|A\cap B|
$$

Por tanto:

$$
IoU=\frac{|A\cap B|}{|A|+|B|-|A\cap B|}
$$

### Coeficiente Dice:

Dice utiliza el doble de la intersección dividido entre la suma de las áreas:

$$
Dice(A,B)=\frac{2|A\cap B|}{|A|+|B|}
$$

Ambas métricas se encuentran entre cero y uno.

Una coincidencia perfecta produce:

$$
IoU=Dice=1
$$

Si no existe intersección y las máscaras tienen unión no vacía:

$$
IoU=Dice=0
$$

### Ejemplo numérico:

Se consideran:

$$
|A|=20
$$

$$
|B|=16
$$

$$
|A\cap B|=14
$$

Primero se calcula la unión:

$$
|A\cup B|=20+16-14
$$

$$
|A\cup B|=22
$$

Entonces:

$$
IoU=\frac{14}{22}
$$

$$
\boxed{IoU\approx0.636}
$$

Para Dice:

$$
Dice=\frac{2(14)}{20+16}
$$

$$
Dice=\frac{28}{36}
$$

$$
\boxed{Dice\approx0.778}
$$

### Relación matemática entre ambas métricas:

Dice e IoU no son medidas independientes.

Existe una transformación exacta:

$$
\boxed{Dice=\frac{2IoU}{1+IoU}}
$$

Y su inversa:

$$
\boxed{IoU=\frac{Dice}{2-Dice}}
$$

Por ejemplo, si:

$$
IoU=0.60
$$

Entonces:

$$
Dice=\frac{1.20}{1.60}
$$

$$
\boxed{Dice=0.75}
$$

Para un mismo par de máscaras, Dice siempre será mayor o igual que IoU.

Esto no significa que la segmentación sea mejor al medirla con Dice.

Ambas describen el mismo traslape utilizando escalas diferentes.

### Sensibilidad a errores:

Cuando un objeto es pequeño, una desviación de pocos píxeles en su contorno puede representar una proporción importante de su área.

En estas condiciones, IoU suele mostrar reducciones numéricas más marcadas que Dice.

Sin embargo, ambas métricas responden de forma monótona al traslape y producen el mismo ordenamiento de predicciones cuando se calculan sobre las mismas máscaras.

**Conclusión:** Dice produce valores numéricos generalmente más altos, pero esto no implica que sea una evaluación objetivamente superior.

---

## Crecimiento de regiones

### Fundamento del algoritmo:

El crecimiento de regiones es un procedimiento de segmentación basado en semillas.

Comienza con uno o varios píxeles iniciales y expande las regiones incorporando vecinos que satisfacen un criterio de similitud.

En la presentación se utiliza una semilla de intensidad:

$$
I_s=124
$$

Y el criterio:

$$
\boxed{|I(r,c)-124|\leq tol}
$$

Además, se utiliza conectividad de cuatro vecinos.

Esto significa que un píxel solamente puede incorporarse si:

1. Es accesible desde la región mediante vecinos permitidos.
2. Su intensidad está dentro del intervalo aceptado.
3. No ha sido incorporado anteriormente.

### Ejemplo con tolerancia de ocho:

Si:

$$
tol=8
$$

El intervalo permitido es:

$$
116\leq I(r,c)\leq132
$$

La región crece por rondas hasta que no quedan vecinos admisibles.

Para la matriz del ejercicio, el resultado final contiene:

$$
\boxed{11\text{ píxeles}}
$$

### Ejemplo con tolerancia de dieciséis:

Ahora se establece:

$$
tol=16
$$

El intervalo se amplía:

$$
108\leq I(r,c)\leq140
$$

Al aceptar más intensidades, aparecen nuevas conexiones posibles.

El resultado final contiene:

$$
\boxed{16\text{ píxeles}}
$$

Además, los cuatro píxeles de una esquina brillante quedan incorporados.

### Importancia de la conectividad:

Un píxel puede cumplir el criterio de intensidad y aun así quedar fuera de la región si no existe un camino de píxeles aceptados que lo conecte con la semilla.

Por tanto, el crecimiento depende simultáneamente de:

- Similitud de intensidad.
- Conectividad espacial.
- Selección de la semilla.
- Tolerancia utilizada.

Es importante señalar que, en este ejercicio, los candidatos se comparan contra la intensidad original de la semilla.

No se comparan contra el último vecino incorporado.

Esta diferencia evita que el criterio de intensidad cambie progresivamente a lo largo del recorrido.

### Limitación del crecimiento de regiones:

Una tolerancia demasiado pequeña puede fragmentar un objeto real.

Una tolerancia demasiado grande puede permitir que la región se extienda a áreas que no pertenecen al objeto.

El fenómeno ocurre cuando existe una ruta conectada que atraviesa una frontera suficientemente similar a la semilla.

Esto explica por qué un cambio relativamente pequeño de tolerancia puede producir una expansión considerable.

**Conclusión:** una frontera solo detiene el crecimiento cuando impide todos los caminos admisibles hacia el exterior.

---

## Umbralización global y adaptativa

### Concepto de umbralización:

La umbralización transforma una imagen de intensidades en una máscara binaria.

Para detectar objetos brillantes, puede utilizarse:

$$
B(x,y)=
\begin{cases}
1,&I(x,y)>T\\
0,&I(x,y)\leq T
\end{cases}
$$

El parámetro $T$ determina la frontera entre objeto y fondo.

Los métodos de umbralización pueden clasificarse en:

- Globales.
- Locales o adaptativos.

### Umbralización global:

Se utiliza un mismo umbral para toda la imagen.

Este procedimiento puede funcionar cuando el fondo y los objetos presentan intensidades claramente separadas.

Sin embargo, se vuelve problemático cuando la iluminación varía espacialmente.

Por ejemplo, un objeto oscuro situado en una región brillante puede confundirse con el fondo si el umbral se selecciona con base en toda la imagen.

### Umbralización adaptativa:

En este procedimiento, el umbral depende de las características de una ventana local.

La regla utilizada en la clase para objetos brillantes es:

$$
\boxed{T(x,y)=m_W(x,y)+C}
$$

Donde:

- $m_W(x,y)$ es la intensidad media de la ventana.
- $C$ es una constante.
- $W$ determina el tamaño de la región local.

La clasificación se realiza mediante:

$$
B(x,y)=1
\quad\text{si}\quad
I(x,y)>m_W(x,y)+C
$$

### Ejemplo de iluminación variable:

Se considera un fondo cuya intensidad aumenta progresivamente:

$$
40\longrightarrow190
$$

Existen dos células brillantes:

- Una de 24 píxeles de ancho.
- Otra de 40 píxeles de ancho.

Ambas presentan una intensidad aproximadamente 70 niveles superior a su fondo local.

La constante utilizada es:

$$
C=10
$$

Con una ventana de 61 píxeles, ambas células se segmentan correctamente en el ejercicio.

Esto ocurre porque la ventana alcanza suficiente fondo alrededor de los objetos.

### Efecto de reducir la ventana:

Se reduce el tamaño de la ventana a:

$$
W=11
$$

En el centro de una célula considerablemente más ancha que la ventana, todos los píxeles observados pertenecen a la propia célula.

Por tanto:

$$
m_W\approx I_{\text{célula}}
$$

El umbral resulta:

$$
T\approx I_{\text{célula}}+C
$$

Como $C$ es positivo:

$$
I_{\text{célula}}<T
$$

Entonces el píxel central no se clasifica como objeto.

En cambio, cerca del borde, la ventana contiene parte de la célula y parte del fondo.

La media local disminuye y algunos píxeles del contorno superan el umbral.

El resultado puede ser una máscara en forma de anillo o con el interior vacío.

En el ejercicio:

$$
\boxed{16\text{ de }64\text{ píxeles detectados}}
$$

Con la ventana pequeña solamente se conservan regiones cercanas a los extremos de las células.

### Selección del tamaño de ventana:

La ventana debe ser suficientemente grande para incluir información del fondo próximo al objeto.

Sin embargo, una ventana excesivamente grande puede volver a introducir problemas relacionados con cambios de iluminación.

Por tanto, existe un compromiso:

- Ventanas pequeñas siguen variaciones locales rápidas, pero pueden producir objetos huecos.
- Ventanas grandes conservan mejor el contraste entre objetos y fondo, pero pueden adaptarse peor a cambios rápidos de iluminación.

La selección debe considerar la escala de los objetos y la escala espacial de las variaciones de iluminación.

---

## Umbralización mediante Otsu

### Fundamento estadístico:

Otsu es un método de umbralización global que selecciona automáticamente un umbral a partir del histograma.

Su objetivo es encontrar una división que produzca una separación elevada entre dos clases.

En la convención utilizada en el material:

$$
C_0=\{i:i<t\}
$$

$$
C_1=\{i:i\geq t\}
$$

La primera clase contiene las intensidades menores que el umbral.

La segunda contiene las intensidades mayores o iguales.

### Pesos y medias de las clases:

Si $p(i)$ representa la probabilidad de intensidad $i$, el peso de cada clase es:

$$
\omega_0=\sum_{i<t}p(i)
$$

$$
\omega_1=\sum_{i\geq t}p(i)
$$

Sus medias son:

$$
\mu_0=\frac{\sum_{i<t}ip(i)}{\omega_0}
$$

$$
\mu_1=\frac{\sum_{i\geq t}ip(i)}{\omega_1}
$$

La varianza entre clases se calcula mediante:

$$
\boxed{
\sigma_B^2=
\omega_0\omega_1(\mu_0-\mu_1)^2
}
$$

El mejor umbral es aquel que maximiza esta expresión:

$$
\boxed{
t^*=\arg\max_t\sigma_B^2(t)
}
$$

### Interpretación de la fórmula:

La varianza entre clases depende de dos factores.

**Separación de medias**

Cuanto mayor sea la diferencia entre $\mu_0$ y $\mu_1$, mayor puede ser la separación estadística.

**Proporciones de las clases**

El producto:

$$
\omega_0\omega_1
$$

penaliza las divisiones extremadamente desbalanceadas.

Por ello, Otsu no busca únicamente el mayor contraste entre dos conjuntos de intensidades.

También considera cuántos píxeles pertenecen a cada conjunto.

### Ejemplo numérico:

Se considera el histograma del ejercicio, con 20 observaciones:

$$
N=20
$$

La suma de intensidades es:

$$
59
$$

Por tanto:

$$
\mu_G=\frac{59}{20}=2.95
$$

Para el umbral:

$$
t=3
$$

La clase oscura contiene 11 píxeles y la clara 9.

Sus medias son aproximadamente:

$$
\mu_0=0.818
$$

$$
\mu_1=5.556
$$

La varianza entre clases es:

$$
\sigma_B^2=
\frac{11}{20}\frac{9}{20}
(5.556-0.818)^2
$$

$$
\boxed{\sigma_B^2\approx5.555}
$$

Ahora se evalúa:

$$
t=4
$$

Las clases contienen 12 y 8 píxeles.

Sus medias son:

$$
\mu_0=1
$$

$$
\mu_1=5.875
$$

Entonces:

$$
\sigma_B^2=
\frac{12}{20}\frac{8}{20}
(5.875-1)^2
$$

$$
\boxed{\sigma_B^2\approx5.704}
$$

Como:

$$
5.704>5.555
$$

El segundo umbral ofrece una mayor separación entre clases.

Para este ejercicio, el máximo ocurre en:

$$
\boxed{t^*=4}
$$

### Medida de separabilidad:

La presentación utiliza:

$$
\boxed{\eta=\frac{\sigma_B^2}{\sigma_G^2}}
$$

Donde:

- $\sigma_B^2$ es la varianza entre clases.
- $\sigma_G^2$ es la varianza global.

Esta proporción indica qué fracción de la variabilidad total queda explicada por la separación seleccionada.

Para el ejemplo:

$$
\boxed{\eta=0.871}
$$

Un valor elevado indica una separación estadística relativamente clara entre las clases obtenidas.

Sin embargo, no garantiza por sí mismo que las clases correspondan a los objetos que se desean detectar.

### Umbralización iterativa:

Otro método consiste en comenzar con un umbral inicial y actualizarlo mediante las medias de las dos clases.

La regla es:

$$
T_{k+1}=\frac{\mu_0(T_k)+\mu_1(T_k)}{2}
$$

El proceso se repite hasta que la partición deja de cambiar o se cumple un criterio de convergencia.

En el material:

$$
2.95\longrightarrow3.187\longrightarrow3.4375
$$

La partición termina estabilizándose.

Este procedimiento no busca explícitamente maximizar la varianza entre clases como Otsu.

Utiliza una actualización basada en medias.

---

## Limitaciones de Otsu ante objetos pequeños

### Problema del desbalance de clases:

Otsu funciona especialmente bien cuando el histograma contiene dos grupos de intensidad suficientemente diferenciados.

Sin embargo, un objeto muy pequeño puede representar una fracción mínima de los píxeles.

Por ejemplo:

$$
P(\text{objeto})=0.01
$$

En este caso, el histograma está dominado por el fondo.

El objeto puede no formar una segunda concentración visible.

Como la varianza entre clases incorpora las proporciones de píxeles, Otsu puede encontrar una separación estadísticamente más atractiva dentro de las propias intensidades del fondo.

El resultado es un umbral que no identifica correctamente el objeto.

### Ejemplo experimental de la presentación:

Para el caso de un objeto pequeño, el notebook de la clase 14 presenta los siguientes resultados:

| Procedimiento | Umbral | $\eta$ | IoU |
|---|---:|---:|---:|
| Otsu con todos los píxeles | 73 | 0.50 | 0.029 |
| Otsu usando píxeles de borde | 104 | 0.92 | 0.844 |
| Umbral de borde aplicado a imagen suavizada | 104 | — | 0.987 |

Estos resultados muestran que la selección de la población de píxeles empleada para calcular el umbral puede modificar significativamente el resultado.

Al utilizar píxeles relacionados con los bordes, se reduce el dominio estadístico del fondo sobre la estimación.

Esto puede ayudar a recuperar la separación entre objeto y fondo.

Sin embargo, el método depende de que los píxeles de borde seleccionados sean representativos.

### Interpretación de la separabilidad:

Un valor bajo de $\eta$ puede indicar que el histograma no presenta una separación clara.

Esto puede suceder por diferentes razones:

- El ruido llena el valle entre las distribuciones.
- Los objetos tienen muy poco peso estadístico.
- Las intensidades de objeto y fondo se superponen.
- La imagen presenta iluminación no uniforme.

Por tanto, $\eta$ describe separabilidad estadística, pero no identifica automáticamente la causa de una mala segmentación.

---

## Umbralización local mediante Niblack y Sauvola

### Fundamento común:

Niblack y Sauvola utilizan estadísticas locales.

Ambos calculan:

- La media de intensidad en una ventana.
- La desviación estándar local.

Esto permite adaptar el umbral a cambios espaciales de iluminación y contraste.

Los métodos son especialmente relevantes para segmentar texto o trazos oscuros sobre fondos relativamente claros.

En este contexto, un píxel se considera tinta cuando su intensidad está por debajo del umbral.

### Método de Niblack:

La formulación utilizada en la clase es:

$$
\boxed{T_N=m-0.2s}
$$

Donde:

- $m$ es la media local.
- $s$ es la desviación estándar local.

La desviación estándar permite ajustar el umbral según la variabilidad de la ventana.

Si la ventana es muy uniforme:

$$
s\approx0
$$

Entonces:

$$
T_N\approx m
$$

Esto puede causar problemas.

### Por qué Niblack produce manchas sobre papel blanco:

En una región de papel aparentemente uniforme, pequeñas fluctuaciones de ruido generan píxeles ligeramente más oscuros que la media.

Como la desviación estándar es pequeña, el umbral queda muy cerca de la media.

Por tanto, algunas fluctuaciones pueden clasificarse como tinta.

Ejemplo:

$$
m=180
$$

$$
s=4
$$

Entonces:

$$
T_N=180-0.2(4)
$$

$$
\boxed{T_N=179.2}
$$

En el ejemplo de la presentación, ocho píxeles del papel se clasifican incorrectamente como tinta.

### Método de Sauvola:

Sauvola utiliza:

$$
\boxed{
T_S=m\left[1+k\left(\frac{s}{R}-1\right)\right]
}
$$

En el ejercicio:

$$
k=0.5
$$

$$
R=128
$$

La diferencia fundamental respecto a Niblack es que la desviación estándar modifica multiplicativamente la media.

Cuando:

$$
s\approx0
$$

El factor se aproxima a:

$$
1-k=0.5
$$

Por tanto:

$$
T_S\approx0.5m
$$

Esto aleja el umbral de las fluctuaciones normales de un fondo uniforme.

### Ejemplo sobre papel blanco:

Se utiliza:

$$
m=180,\quad s=4
$$

Entonces:

$$
T_S=180\left[1+0.5\left(\frac{4}{128}-1\right)\right]
$$

$$
\boxed{T_S\approx92.81}
$$

Este umbral queda mucho más abajo que las intensidades normales del papel.

En el ejemplo, no aparecen píxeles falsamente clasificados como tinta.

### Limitación de Sauvola con trazos tenues:

Aunque Sauvola puede reducir los falsos positivos del fondo, también puede eliminar trazos con poco contraste.

Se considera:

$$
m=170,\quad s=20
$$

Para Niblack:

$$
T_N=170-0.2(20)
$$

$$
\boxed{T_N=166}
$$

Para Sauvola:

$$
T_S=170\left[1+0.5\left(\frac{20}{128}-1\right)\right]
$$

$$
\boxed{T_S\approx98.28}
$$

Un trazo tenue puede ser suficientemente oscuro para quedar por debajo de 166, pero no por debajo de 98.28.

Por tanto, Niblack puede conservarlo mientras Sauvola lo descarta.

### Comparación experimental:

| Ventana | Niblack | Sauvola |
|---|---:|---:|
| Papel blanco, $m=180$, $s=4$ | 179.20 | 92.81 |
| Lápiz tenue, $m=170$, $s=20$ | 166.00 | 98.28 |
| Tinta oscura, $m=150$, $s=60$ | 138.00 | 110.16 |

En el laboratorio:

- Papel blanco: Niblack produce 8 falsos píxeles de tinta; Sauvola produce 0.
- Lápiz tenue: Niblack recupera 5 píxeles; Sauvola recupera 0.
- Tinta oscura: ambos recuperan los 5 píxeles considerados.

### Conclusión comparativa:

Niblack puede conservar trazos de bajo contraste, pero es más vulnerable a fluctuaciones del fondo uniforme.

Sauvola puede mantener limpio el fondo, pero su umbral puede quedar demasiado bajo para detectar trazos tenues.

Esto refleja un compromiso entre sensibilidad y especificidad.

No existe una elección universalmente superior.

---

## Análisis de textura

### Diferencia entre intensidad y textura:

La textura describe cómo se organizan espacialmente las intensidades de una imagen.

Dos imágenes pueden contener exactamente los mismos valores de intensidad y, aun así, presentar apariencias completamente distintas.

Por ejemplo:

- Una imagen puede organizar intensidades en franjas.
- Otra puede distribuirlas aleatoriamente.
- Otra puede formar agrupamientos compactos.
- Otra puede presentar patrones repetitivos.

Si todas utilizan las mismas intensidades con las mismas frecuencias, sus histogramas serán idénticos.

Sin embargo, sus texturas serán diferentes.

### Estadísticas de primer orden:

Las estadísticas de primer orden se calculan a partir de los valores individuales de intensidad o del histograma.

Entre ellas aparecen:

- Media.
- Varianza.
- Uniformidad.
- Entropía del histograma.

Por ejemplo, la media puede calcularse como:

$$
\mu=\sum_i i\,p(i)
$$

Y la varianza como:

$$
\sigma^2=\sum_i(i-\mu)^2p(i)
$$

La entropía del histograma es:

$$
H=-\sum_i p(i)\log_2p(i)
$$

Estas estadísticas no consideran directamente la posición de los píxeles.

### Experimento de permutación:

Si se reorganizan aleatoriamente todos los píxeles de una imagen sin modificar sus intensidades, el histograma permanece idéntico.

Por tanto:

- La media no cambia.
- La varianza no cambia.
- La entropía del histograma no cambia.
- La uniformidad del histograma no cambia.

Sin embargo, las relaciones entre vecinos sí cambian.

Por ello, métodos como GLCM y LBP pueden producir resultados distintos.

**Conclusión:** la información de textura reside en las relaciones espaciales, no solamente en la distribución marginal de intensidades.

---

## Matriz de coocurrencia de niveles de gris

### Concepto de GLCM:

La Gray-Level Co-occurrence Matrix, o GLCM, describe la frecuencia con la que determinados pares de intensidades aparecen separados por un desplazamiento específico.

Se define un desplazamiento:

$$
\Delta=(\Delta r,\Delta c)
$$

La matriz cuenta los pares:

$$
I(r,c)=i
$$

$$
I(r+\Delta r,c+\Delta c)=j
$$

Cada entrada:

$$
C(i,j)
$$

representa el número de veces que ocurre esa relación.

La matriz normalizada es:

$$
p(i,j)=\frac{C(i,j)}{\sum_{a,b}C(a,b)}
$$

De esta manera:

$$
\sum_{i,j}p(i,j)=1
$$

### Importancia de la dirección:

La GLCM depende del desplazamiento seleccionado.

Por ejemplo:

$$
\Delta=(0,1)
$$

analiza vecinos horizontales.

Mientras que:

$$
\Delta=(1,-1)
$$

analiza vecinos en diagonal hacia abajo e izquierda.

Una textura con franjas diagonales puede mostrar una gran similitud en una dirección y grandes diferencias en otra.

Por tanto, una sola GLCM no describe necesariamente todas las propiedades de la textura.

### Contraste:

El contraste mide diferencias de intensidad entre los pares.

$$
\boxed{
Contrast=\sum_{i,j}(i-j)^2p(i,j)
}
$$

Los pares de intensidades iguales contribuyen cero.

Los pares con diferencias grandes contribuyen valores elevados porque la diferencia se eleva al cuadrado.

### Energía:

La energía utilizada en la presentación es:

$$
\boxed{
Energy=\sum_{i,j}p(i,j)^2
}
$$

Esta medida aumenta cuando la probabilidad se concentra en pocas entradas de la matriz.

Disminuye cuando las probabilidades se distribuyen de manera más uniforme.

Debe distinguirse de implementaciones que denominan energía a la raíz cuadrada de esta suma.

### Homogeneidad:

La homogeneidad se calcula como:

$$
\boxed{
Homogeneity=
\sum_{i,j}\frac{p(i,j)}{1+|i-j|}
}
$$

Los pares con intensidades similares reciben una contribución mayor.

Cuando todos los pares tienen intensidades iguales:

$$
Homogeneity=1
$$

### Ejemplo con franjas diagonales:

En el ejercicio, cada fila representa un desplazamiento cíclico del patrón anterior.

Las intensidades siguen:

$$
I(r,c)=(r+c)\bmod4
$$

Esto genera una organización diagonal de cuatro niveles de gris.

Para el desplazamiento:

$$
\Delta=(0,1)
$$

Existen 12 pares válidos.

Los cuatro tipos de pares aparecen tres veces cada uno:

$$
(0,1),\ (1,2),\ (2,3),\ (3,0)
$$

Por tanto, cada tipo tiene probabilidad:

$$
p=\frac{3}{12}=0.25
$$

### Cálculo del contraste horizontal:

Tres tipos de pares tienen diferencia absoluta de uno.

Un tipo presenta diferencia absoluta de tres.

Por tanto:

$$
Contrast=
\frac{9(1)^2+3(3)^2}{12}
$$

$$
Contrast=\frac{9+27}{12}
$$

$$
\boxed{Contrast=3}
$$

### Cálculo de la energía horizontal:

Existen cuatro entradas con probabilidad 0.25.

$$
Energy=4(0.25)^2
$$

$$
\boxed{Energy=0.25}
$$

### Cálculo de la homogeneidad horizontal:

$$
Homogeneity=
\frac{9}{12}\frac{1}{2}
+
\frac{3}{12}\frac{1}{4}
$$

$$
\boxed{Homogeneity=0.4375}
$$

### Comparación con dirección diagonal:

Para:

$$
\Delta=(1,-1)
$$

Existen nueve pares válidos.

Todos conectan intensidades iguales.

Por ello:

$$
\boxed{Contrast=0}
$$

$$
\boxed{Homogeneity=1}
$$

La energía es:

$$
\boxed{Energy=\frac{21}{81}\approx0.2593}
$$

La diferencia entre los desplazamientos demuestra que la textura tiene una estructura direccional.

### Interpretación:

Una GLCM puede revelar:

- Dirección predominante de patrones.
- Repetición espacial.
- Diferencias locales de intensidad.
- Regularidad de las relaciones entre vecinos.

Sin embargo, los resultados dependen del desplazamiento, de la cuantización de niveles de gris y de la normalización empleada.

---

## Patrones binarios locales

### Fundamento de LBP:

Local Binary Patterns, o LBP, describe la estructura local mediante comparaciones entre un píxel central y sus vecinos.

Para cada vecino se define:

$$
s(g_p-g_c)=
\begin{cases}
1,&g_p\geq g_c\\
0,&g_p<g_c
\end{cases}
$$

Donde:

- $g_c$ es la intensidad central.
- $g_p$ es la intensidad del vecino.

El código se construye mediante:

$$
\boxed{
LBP=\sum_{p=0}^{7}s(g_p-g_c)2^p
}
$$

En la convención utilizada en la clase:

- El primer vecino está arriba a la izquierda.
- Los vecinos se recorren en sentido horario.
- La igualdad se clasifica como uno.

### Ejemplo:

Se consideran los valores vecinos:

$$
70,\ 50,\ 65,\ 60,\ 40,\ 80,\ 55,\ 30
$$

Para el píxel central del ejercicio, las comparaciones producen:

$$
1,\ 0,\ 1,\ 1,\ 0,\ 1,\ 0,\ 0
$$

El código decimal es:

$$
LBP=
1(2^0)+0(2^1)+1(2^2)+1(2^3)
+0(2^4)+1(2^5)
$$

$$
LBP=1+4+8+32
$$

$$
\boxed{LBP=45}
$$

### Invariancia ante cambios de iluminación:

Si se agrega una constante a todas las intensidades:

$$
g'_p=g_p+C
$$

$$
g'_c=g_c+C
$$

Entonces:

$$
g'_p-g'_c=g_p-g_c
$$

Por tanto, las comparaciones permanecen iguales.

En el ejemplo, sumar 30 a todos los píxeles conserva:

$$
\boxed{LBP=45}
$$

Esto muestra invariancia ante un cambio aditivo uniforme de iluminación, siempre que no aparezcan efectos como saturación o recorte.

### Patrones uniformes:

Un patrón LBP es uniforme cuando presenta como máximo dos transiciones entre cero y uno al recorrer circularmente sus bits.

Por ejemplo:

$$
00011100
$$

Tiene dos transiciones circulares.

En cambio, el patrón:

$$
10110100
$$

Presenta seis transiciones.

Por tanto, no es uniforme.

Los patrones uniformes suelen utilizarse para simplificar la representación de texturas.

### Rotación de LBP:

Al rotar una imagen, también rota el orden de los vecinos.

Por tanto, el código binario puede cambiar aunque la estructura local sea esencialmente la misma.

En el ejercicio:

$$
LBP_{\text{original}}=45
$$

Después de rotar 90 grados en sentido horario:

$$
\boxed{LBP_{\text{rotado}}=180}
$$

Una estrategia para obtener una representación invariante ante rotaciones consiste en evaluar las rotaciones circulares del patrón binario y seleccionar el código mínimo.

En el ejemplo:

$$
\boxed{LBP_{\text{invariante}}=45}
$$

### Sensibilidad a pequeñas variaciones:

LBP utiliza comparaciones binarias.

Por esta razón, un cambio pequeño puede modificar el resultado si provoca que una intensidad cruce el valor del píxel central.

En el ejercicio, un vecino originalmente igual al centro contribuye:

$$
1
$$

Si su intensidad disminuye ligeramente y queda por debajo del centro, pasa a contribuir:

$$
0
$$

El código cambia de:

$$
45\longrightarrow37
$$

Esto demuestra que LBP es sensible a pequeñas fluctuaciones cerca del límite de comparación.

La debilidad resulta especialmente importante en regiones planas, donde las intensidades vecinas suelen ser muy similares.

---

## Análisis multirresolución mediante wavelets

### Motivación de la representación multirresolución:

Una imagen contiene información visual a diferentes escalas.

Las estructuras grandes representan variaciones lentas de intensidad.

Los detalles pequeños, los bordes y ciertas texturas representan cambios más rápidos.

La transformada wavelet permite separar estas componentes.

A diferencia de una representación puramente global basada en frecuencias, una wavelet utiliza funciones localizadas que permiten relacionar parte de la información transformada con posiciones espaciales.

### Transformada Haar unidimensional:

La transformada Haar es una de las formas más sencillas de análisis wavelet.

Para un par de valores:

$$
x_1,\ x_2
$$

Se calcula un promedio:

$$
a=\frac{x_1+x_2}{2}
$$

Y una diferencia:

$$
d=\frac{x_1-x_2}{2}
$$

El promedio representa la componente de baja frecuencia.

La diferencia representa el detalle local.

La reconstrucción es:

$$
x_1=a+d
$$

$$
x_2=a-d
$$

Por tanto, si se conservan ambos coeficientes, la transformación permite recuperar exactamente los valores originales.

### Transformada Haar bidimensional:

La transformada 2-D opera sobre bloques de:

$$
2\times2
$$

Se considera:

$$
X=
\begin{bmatrix}
a&b\\
c&d
\end{bmatrix}
$$

La descomposición produce cuatro coeficientes.

**Componente de aproximación**

$$
\boxed{
LL=\frac{a+b+c+d}{4}
}
$$

Representa la intensidad promedio del bloque.

**Detalle horizontal en la convención de la clase**

$$
\boxed{
H=\frac{a+b-c-d}{4}
}
$$

Compara la parte superior con la inferior.

**Detalle vertical en la convención de la clase**

$$
\boxed{
V=\frac{a-b+c-d}{4}
}
$$

Compara la parte izquierda con la derecha.

**Detalle diagonal**

$$
\boxed{
D=\frac{a-b-c+d}{4}
}
$$

Representa cambios diagonales dentro del bloque.

Los nombres H y V siguen la convención de la presentación y deben conservarse al realizar los ejercicios.

### Reconstrucción inversa:

Con los cuatro coeficientes puede recuperarse el bloque original:

$$
\boxed{
a=LL+H+V+D
}
$$

$$
\boxed{
b=LL+H-V-D
}
$$

$$
\boxed{
c=LL-H+V-D
}
$$

$$
\boxed{
d=LL-H-V+D
}
$$

Estas ecuaciones demuestran que la transformada conserva la información del bloque mientras se mantengan todos sus coeficientes.

---

## Ejemplo de descomposición y reconstrucción Haar

### Bloque con una transición vertical:

Se considera:

$$
X=
\begin{bmatrix}
100&20\\
100&20
\end{bmatrix}
$$

La aproximación es:

$$
LL=\frac{100+20+100+20}{4}
$$

$$
\boxed{LL=60}
$$

El detalle horizontal es:

$$
H=\frac{100+20-100-20}{4}
$$

$$
\boxed{H=0}
$$

El detalle vertical:

$$
V=\frac{100-20+100-20}{4}
$$

$$
\boxed{V=40}
$$

Y el diagonal:

$$
D=\frac{100-20-100+20}{4}
$$

$$
\boxed{D=0}
$$

Por tanto:

$$
(LL,H,V,D)=(60,0,40,0)
$$

La transición entre las columnas aparece representada en el coeficiente $V$.

### Bloque con un píxel brillante:

Se considera:

$$
X=
\begin{bmatrix}
30&30\\
30&90
\end{bmatrix}
$$

Sus coeficientes son:

$$
\boxed{LL=45}
$$

$$
\boxed{H=-15}
$$

$$
\boxed{V=-15}
$$

$$
\boxed{D=15}
$$

La presencia del píxel brillante genera respuestas en las tres bandas de detalle.

Esto ocurre porque su intensidad modifica las relaciones entre filas, columnas y diagonales.

### Bloques uniformes:

Un bloque uniforme:

$$
X=
\begin{bmatrix}
60&60\\
60&60
\end{bmatrix}
$$

Produce:

$$
LL=60
$$

$$
H=V=D=0
$$

Esto significa que no existe variación interna detectable en ese bloque.

En el ejercicio completo de cuatro bloques, ocho de los doce coeficientes de detalle son cero.

---

## Eliminación de ruido mediante umbralización wavelet

### Idea general:

En una representación wavelet, muchos componentes de ruido aparecen como coeficientes de detalle de baja magnitud.

Esto permite intentar eliminar ruido mediante umbralización de los coeficientes.

Sin embargo, los detalles pequeños de objetos reales también pueden tener magnitudes bajas.

Por tanto, eliminar coeficientes pequeños no equivale necesariamente a eliminar solamente ruido.

### Umbralización dura:

La regla es:

$$
T_{\text{hard}}(x)=
\begin{cases}
0,&|x|\leq\lambda\\
x,&|x|>\lambda
\end{cases}
$$

Los coeficientes pequeños desaparecen.

Los coeficientes que sobreviven conservan su valor original.

### Umbralización suave:

La regla es:

$$
\boxed{
T_{\text{soft}}(x)=
\operatorname{sign}(x)\max(|x|-\lambda,0)
}
$$

Este procedimiento realiza dos operaciones:

1. Elimina los coeficientes cuya magnitud no supera el umbral.
2. Reduce la magnitud de todos los coeficientes que sobreviven.

Por ejemplo, con:

$$
\lambda=20
$$

Los coeficientes:

$$
40,\ -15,\ 15
$$

se transforman en:

$$
20,\ 0,\ 0
$$

### Reconstrucción del bloque con borde:

El bloque original era:

$$
\begin{bmatrix}
100&20\\
100&20
\end{bmatrix}
$$

Sus coeficientes eran:

$$
(60,0,40,0)
$$

Después del umbral suave:

$$
(60,0,20,0)
$$

Al reconstruir:

$$
a=60+20=80
$$

$$
b=60-20=40
$$

$$
c=60+20=80
$$

$$
d=60-20=40
$$

Se obtiene:

$$
\boxed{
\begin{bmatrix}
80&40\\
80&40
\end{bmatrix}
}
$$

El salto original era:

$$
100-20=80
$$

Después del umbralizado:

$$
80-40=40
$$

El contraste del borde se reduce a la mitad.

### Efecto sobre objetos pequeños:

Para el bloque:

$$
\begin{bmatrix}
30&30\\
30&90
\end{bmatrix}
$$

Los tres detalles tienen magnitud 15.

Con:

$$
\lambda=20
$$

Todos desaparecen.

Solamente queda:

$$
LL=45
$$

Al reconstruir:

$$
\boxed{
\begin{bmatrix}
45&45\\
45&45
\end{bmatrix}
}
$$

El píxel brillante desaparece completamente.

**Conclusión:** la umbralización suave puede eliminar ruido, pero también modifica bordes y destruye estructuras pequeñas cuando sus coeficientes se encuentran por debajo del umbral.

---

## Sensibilidad espacial de Haar

### Dependencia de la alineación:

La transformada Haar trabaja con bloques de posiciones fijas.

Por esta razón, una misma estructura puede producir coeficientes distintos dependiendo de su posición respecto a la rejilla de bloques.

Se considera una imagen con una transición entre:

$$
40\longrightarrow200
$$

Si el borde cae exactamente entre dos bloques, cada bloque puede contener intensidades uniformes.

En ese caso, sus detalles internos serán cero.

Aunque visualmente existe un borde intenso, la representación de detalle del bloque no lo detecta.

### Desplazamiento de un píxel:

Ahora se desplaza el borde una columna.

Un bloque contiene:

$$
\begin{bmatrix}
40&200\\
40&200
\end{bmatrix}
$$

El detalle vertical es:

$$
V=\frac{40-200+40-200}{4}
$$

$$
\boxed{V=-80}
$$

El mismo borde que antes podía producir coeficientes de detalle nulos ahora genera una respuesta intensa.

En el ejercicio de la presentación aparecen:

- 16 coeficientes de valor $-80$ en el primer nivel.
- 8 coeficientes de valor $-40$ en el segundo nivel.
- 4 coeficientes de valor $-20$ en el tercer nivel.

### Invariancia a la traslación:

Una transformación es invariante a la traslación, en el sentido relevante para la comparación, cuando desplazar el contenido no cambia sustancialmente su respuesta descriptiva salvo el desplazamiento correspondiente.

La transformada Haar discreta con submuestreo no posee esta propiedad de manera general.

Un desplazamiento pequeño puede cambiar significativamente los coeficientes.

Esto resulta problemático cuando se desea detectar estructuras cuya posición no está alineada con la rejilla.

### Estrategias de mitigación:

Una alternativa consiste en utilizar múltiples desplazamientos de la imagen.

El procedimiento general consiste en:

1. Desplazar la imagen.
2. Aplicar la descomposición wavelet.
3. Procesar los coeficientes.
4. Reconstruir la imagen.
5. Deshacer el desplazamiento.
6. Combinar los resultados de diferentes desplazamientos.

Este tipo de estrategia reduce la dependencia de una única alineación espacial.

---

## Umbral universal y sus limitaciones

### Definición del umbral universal:

Una regla clásica para seleccionar el umbral wavelet es:

$$
\boxed{
\lambda=\sigma\sqrt{2\ln N}
}
$$

Donde:

- $\sigma$ es una estimación de la desviación estándar del ruido.
- $N$ es el número de muestras considerado por la regla.

La idea consiste en establecer un umbral suficientemente elevado para eliminar gran parte de los coeficientes producidos por ruido.

Sin embargo, su resultado depende de las condiciones estadísticas y de la estructura de la imagen.

### Ejemplo experimental:

En el notebook de la clase 14 se comparan diferentes estrategias de eliminación de ruido.

La configuración analizada utiliza una estimación:

$$
\sigma\approx30.2
$$

Y un umbral universal aproximado:

$$
\boxed{\lambda\approx142}
$$

Los resultados reportados son:

| Método | IoU | Células pequeñas conservadas |
|---|---:|---:|
| Wavelet con umbral universal | 0.807 | 4 |
| Suavizado con $\sigma=2$ | 0.957 | 11 |
| Wavelet por banda y 16 desplazamientos | 0.961 | 12 |

La última columna se refiere a las células pequeñas detectadas en el experimento, de un total de doce.

### Por qué el método wavelet tradicional fue inferior:

La primera causa es la magnitud del umbral.

En los primeros niveles, los detalles correspondientes a células pequeñas presentan magnitudes aproximadas de 80 a 140.

Como:

$$
\lambda\approx142
$$

Muchos de esos coeficientes desaparecen.

En el tercer nivel pueden aparecer magnitudes cercanas a 220, que sí sobreviven, aunque disminuidas por el umbral suave.

La segunda causa es la dependencia de Haar respecto a la alineación espacial.

Las células pequeñas pueden caer en posiciones desfavorables respecto a los bloques, produciendo respuestas débiles o fragmentadas.

### Interpretación:

La complejidad de un algoritmo no garantiza que produzca mejores resultados.

En este experimento, un suavizado gaussiano sencillo conserva mejor las estructuras relevantes que una aplicación directa del umbral universal.

La estrategia wavelet mejora cuando se adapta el procesamiento por banda y se reducen los efectos de la alineación mediante desplazamientos.

Sin embargo, este resultado pertenece a las condiciones concretas del experimento.

No demuestra que el suavizado gaussiano sea siempre superior a las wavelets.

---

## Pirámides de imágenes y representación multiescala

### Concepto de pirámide:

Una pirámide representa una imagen a diferentes resoluciones.

En cada nivel se genera una versión reducida, normalmente después de un filtrado adecuado para evitar aliasing.

Para una imagen inicial de tamaño:

$$
W\times H
$$

Los niveles pueden tener aproximadamente:

$$
W\times H
$$

$$
\frac{W}{2}\times\frac{H}{2}
$$

$$
\frac{W}{4}\times\frac{H}{4}
$$

Y así sucesivamente.

### Número de píxeles almacenados:

Si cada dimensión se reduce a la mitad, el número de píxeles se reduce a una cuarta parte.

La cantidad total relativa de píxeles es:

$$
1+\frac14+\frac1{16}+\frac1{64}+\cdots
$$

Esta serie geométrica converge a:

$$
\boxed{\frac43}
$$

Por tanto, una pirámide completa requiere aproximadamente un tercio de almacenamiento adicional respecto a la imagen original, si se almacenan todos sus niveles con el mismo costo por muestra.

### Diferencia respecto a Haar:

La pirámide almacena múltiples representaciones de la imagen a diferentes resoluciones.

Por ello, en este esquema, la representación resulta redundante.

En cambio, una transformada Haar críticamente muestreada reorganiza la información original en coeficientes de aproximación y detalle.

Si se conservan todos los coeficientes, el número total de valores permanece igual al número de píxeles originales.

Esta diferencia es importante:

- La pirámide facilita analizar imágenes en distintas escalas.
- Haar permite representar la información mediante componentes de aproximación y detalle sin aumentar necesariamente el número total de coeficientes.

---

## Comparación entre Fourier y Haar

### Representación de Fourier:

La transformada de Fourier descompone una señal en componentes sinusoidales.

Cada componente representa una frecuencia espacial y posee información de amplitud y fase.

La magnitud describe la intensidad de las diferentes frecuencias.

La fase resulta fundamental para conservar la organización espacial de la señal.

Por ello, no es correcto afirmar que Fourier carece por completo de información de posición.

La transformada completa permite reconstruir la señal y, por tanto, conserva su estructura espacial.

Sin embargo, una representación basada únicamente en las magnitudes de Fourier no permite recuperar de manera única las posiciones de las estructuras.

### Ejemplo de un impulso:

Una señal de longitud ocho contiene una única muestra distinta de cero.

Su transformada discreta de Fourier presenta magnitudes iguales en todas las frecuencias.

Desplazar ese impulso modifica la fase, pero no sus magnitudes.

Por tanto, las magnitudes no indican dónde se encuentra el impulso.

### Representación Haar:

Haar utiliza promedios y diferencias locales.

Sus coeficientes se relacionan con bloques y escalas específicas.

Por ello, ofrece una representación localizada de los cambios de intensidad.

La comparación correcta es:

- Fourier permite analizar la composición en frecuencias globales y conserva información espacial en la fase.
- Haar proporciona una representación conjunta de escala y localización mediante coeficientes asociados con regiones concretas.

### Compromisos:

Fourier resulta útil para analizar estructuras periódicas y contenido frecuencial global.

Haar resulta útil para describir cambios locales y construir representaciones multiescala.

Sin embargo, Haar puede ser sensible a desplazamientos pequeños y a la alineación de sus bloques.

La selección depende del objetivo del análisis.

---

## Evaluación crítica de explicaciones técnicas

### Diferencia entre una afirmación correcta, incorrecta e incompleta:

Una explicación técnica debe evaluarse atendiendo tanto a su conclusión como al mecanismo que presenta.

Una afirmación puede clasificarse como:

**Correcta**

Cuando describe adecuadamente el funcionamiento del método y no contradice las propiedades relevantes.

**Incorrecta**

Cuando contiene una proposición incompatible con el funcionamiento matemático o experimental del algoritmo.

**Incompleta**

Cuando presenta una idea verdadera, pero omite una condición, consecuencia o limitación necesaria para interpretarla correctamente.

### Ejemplo sobre Fourier:

Afirmación:

"Fourier no conserva información de posición."

Esta afirmación es incorrecta si se refiere a la transformada completa.

La información espacial está codificada en las fases.

La magnitud por sí sola no permite localizar de forma única un impulso.

Por tanto, la crítica debe distinguir la transformada completa de su espectro de magnitudes.

### Ejemplo sobre reconstrucción Haar:

Afirmación:

"Los coeficientes LL, H, V y D permiten reconstruir el bloque original."

Es correcta cuando se conservan todos los coeficientes y se utiliza la convención de transformación inversa correspondiente.

La evidencia es el conjunto de ecuaciones de reconstrucción.

### Ejemplo sobre detección de bordes:

Afirmación:

"Haar detecta cualquier borde intenso."

Es incorrecta.

Un borde alineado con los límites entre bloques puede no producir detalles internos en esos bloques.

La intensidad del borde no garantiza una respuesta elevada si su posición es desfavorable respecto a la rejilla.

### Ejemplo sobre umbralización suave:

Afirmación:

"El umbral suave elimina los detalles pequeños."

Es correcta, pero incompleta como explicación del efecto total.

Además de eliminar coeficientes cuya magnitud no supera el umbral, reduce la magnitud de todos los coeficientes que sobreviven.

Esta segunda operación puede reducir el contraste de los bordes reconstruidos.

### Importancia de la evidencia:

Una justificación técnica sólida debe conectar:

$$
\text{Afirmación}
\longrightarrow
\text{Mecanismo}
\longrightarrow
\text{Consecuencia}
\longrightarrow
\text{Evidencia}
$$

Por ejemplo:

"El umbral suave disminuye el contraste porque resta $\lambda$ a la magnitud de los coeficientes que sobreviven. En el bloque analizado, el detalle vertical pasa de 40 a 20 y la diferencia de intensidad reconstruida disminuye de 80 a 40."

Esta explicación es más completa que afirmar únicamente que la imagen se observa más borrosa.

---

## Comparación general de los métodos estudiados

| Método | Información principal | Ventaja | Limitación |
|---|---|---|---|
| Canny | Gradientes y conectividad | Detecta contornos delgados y continuos | Depende de umbrales, suavizado y contraste |
| Hough | Votos en espacio de parámetros | Identifica estructuras geométricas | Sensible a discretización y bordes irrelevantes |
| Harris | Gradientes en dos direcciones | Detecta esquinas | Depende de escala y umbral de respuesta |
| Componentes conexas | Conectividad binaria | Cuenta y etiqueta regiones | Cambia con conectividad 4 u 8 |
| Freeman | Direcciones del contorno | Representación compacta del recorrido | Aproxima geometría sobre una rejilla |
| IoU | Intersección y unión | Evalúa traslape | Sensible proporcionalmente a errores en objetos pequeños |
| Dice | Intersección y suma de áreas | Evalúa traslape con otra escala | Puede mostrar cifras más altas para la misma máscara |
| Crecimiento de regiones | Semilla, similitud y vecindad | Segmenta áreas conectadas | Depende de semilla y tolerancia |
| Umbral adaptativo | Media local | Compensa iluminación variable | Puede producir objetos huecos con ventanas pequeñas |
| Otsu | Varianza entre clases | Selección automática de umbral | Puede fallar con objetos pequeños |
| Niblack | Media y desviación local | Recupera trazos tenues | Puede generar manchas en fondos uniformes |
| Sauvola | Media y contraste local | Reduce falsas detecciones del fondo | Puede eliminar trazos débiles |
| GLCM | Coocurrencia entre vecinos | Describe textura direccional | Depende de desplazamiento y cuantización |
| LBP | Comparaciones locales binarias | Describe patrones de vecindad | Sensible a fluctuaciones cerca de la igualdad |
| Haar | Promedios y diferencias locales | Descomposición espacial y multiescala | Sensible a traslaciones |
| Umbral wavelet | Magnitud de coeficientes | Reduce determinados componentes de ruido | Puede eliminar detalles reales |
| Pirámide | Escalas de resolución | Facilita análisis multiescala | Almacena representaciones redundantes |

---

## Conclusiones

Los métodos clásicos de visión artificial muestran que la representación seleccionada determina qué información puede extraerse de una imagen.

Los detectores de bordes y esquinas utilizan gradientes, pero responden a propiedades diferentes. Canny busca contornos y su continuidad, mientras que Harris identifica variaciones significativas en dos direcciones. Hough utiliza los puntos previamente detectados para identificar estructuras geométricas mediante coincidencias en un espacio de parámetros.

Los algoritmos de segmentación dependen de decisiones que afectan directamente la definición de los objetos. La conectividad modifica el número de componentes, el crecimiento de regiones depende de semillas y tolerancias, y los métodos de umbralización utilizan diferentes criterios estadísticos para distinguir objetos del fondo.

Las técnicas de textura muestran que la distribución de intensidades no basta para describir la apariencia visual. La GLCM analiza relaciones entre pares de píxeles, mientras que LBP describe patrones locales de comparación. Ambos pueden identificar diferencias espaciales que un histograma no detecta.

Por su parte, el análisis multirresolución permite separar información de aproximación y detalle. Haar facilita estudiar cambios locales a diferentes escalas, pero su respuesta depende de la alineación espacial. Además, la eliminación de ruido mediante umbralización puede afectar las estructuras reales cuando sus coeficientes se confunden con los del ruido.

De manera general, la calidad de un método no depende únicamente de su complejidad matemática. Un procedimiento sencillo puede superar a uno sofisticado cuando sus supuestos se ajustan mejor a las características de la imagen.

Por ello, una evaluación adecuada debe contemplar tanto las métricas cuantitativas como el mecanismo que produce los resultados.

La comprensión de estos mecanismos permite seleccionar algoritmos, explicar sus fallas y diseñar estrategias de procesamiento más adecuadas para cada problema de visión artificial.