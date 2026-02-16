## Introducción

En el campo de estudio que respecta al modelado tridimensional, cada uno de los puntos del objeto puede ser descrito a través de una *terna* ($x, y, z$); sin embargo, los dispositivos de salida suelen ser *bidimensionales*, renderizando cada uno de los puntos a manera de *pixeles* en una pantalla plana, mismos que son descritos a través del **par** ($x, y$).

Para lograr el efecto de tridimensionalidad, se genera una secuencia de figuras bidimensionales que produce una ilusión de profundidad. La herramienta matemática para lograr esto, es la **proyección**.

---

## Proyecciones

Una **proyección** es capaz de transformar puntos en un espacio de mayor dimensión a uno menor; en este caso:
  
$f(x,y,z) = (x',y')$

El modelo de *proyección* se encarga de tomar un punto del objeto tridimensional, convirtiéndolo en un punto imagen en el plano de visión (dígase la pantalla). El cambio de tres dimensiones a solo dos provoca una pérdida de información; por ejemplo, en caso de que múltiples puntos con distintas profundidades ($z$) podrían terminar estando en el mismo punto ($x ', y '$).
### Rayos proyectores:

La *proyección* se entiende como el trazo de **rayos imaginarios** que:

1. Salen de un **centro de proyección** (como si fuera una cámara)
    
2. Pasan por puntos del objeto
    
3. Intersectan un **plano de proyección** (plano de visión),
    
4. Forman la imagen 2D.
    

La finalidad de un motor gráfico tridimensional como Unity es transformar la información en 3D a 2D para lograr representarla en pantalla.

![[Pasted image 20260216134302.png]]

---

## Vistas, Clasificación y dos Métodos Principales

Dado un objeto tridimensional (dígase una taza) con diferentes **vistas** y un **punto de referencia** fijo ($P_{ref}$), la *vista* siempre va a cambiar en función desde dónde se observe y cómo se proyecta el plano.

![[Pasted image 20260216134716.png]]

Para proyectar objetos tridimensionales a una visión bidimensional se señalan **dos formas principales**:

1. Proyección paralela
    
2. Proyección en perspectiva
    

Ambas buscan obtener ($x ',y '$), pero difieren en la geometría de los rayos de proyección.

---

## Proyección en perspectiva

Respecto a la **proyección** en perspectiva, las líneas de proyección *convergen* hacia un punto denominado como **centro de proyección** (también conocido como *punto de referencia de proyección*). La vista proyectada se obtiene al calcular la intersección de estas líneas respecto al plano de visión.

Esta proyección imita el punto focal desde un ojo o cámara, en donde los objetos más lejanos tienden a verse más pequeños. 

### Anomalías de la Proyección en Perspectiva

Existen dos fenómenos atípicos conocidos como **anomalías**; esto, debido a que alteran el tamaño y forma respecto a las medidas reales:

### Acortamiento perspectivo:

Aun si dos segmentos u objetos son del mismo tamaño real, el que está más lejos del centro de proyección se observa considerablemente pequeño.

- **Ejemplo:** 

Dado un caso en el que existen dos postes idénticos en una calle, el más lejano se percibe más pequeño a pesar de que físicamente, ambos cuenten con las mismas medidas.

### Puntos de fuga:

Cuando se realiza la proyección de una serie de líneas que no son paralelas al plano de la vista, en la imagen parecen encontrarse en algún punto del propio plano conocido como el **punto de fuga**. Un ejemplo clásico podría ser: los rieles de un tren que parecen unirse en el horizonte.

Los **puntos de fuga** relevantes usualmente suelen derivarse de líneas paralelas a los ejes principales considerados en el espacio tridimensional; es decir, ($x, y, z$). En terminología más simple, el número total de puntos de fuga importantes suele depender de cuántos ejes tienen una profundidad respecto al observador en esa escena.

### Caso 1: Punto de fuga (respecto al eje (Z)):

- Las líneas paralelas al eje (Z) convergen en **un punto de fuga**.
    
- Las líneas paralelas a (X) e (Y) permanecen paralelas en el dibujo.
    
- Se usa para objetos “de frente” (por ejemplo, ver al final un pasillo).
	

![[Pasted image 20260216161342.png]]

### Caso 2: dos puntos de fuga (respecto a (Z) y (X))

- Líneas paralelas a (Z) convergen a un punto, y líneas paralelas a (X) convergen a otro.
    
- Las paralelas a (Y) quedan paralelas.
    
- Útil para objetos vistos desde una esquina (cajas, edificios).
    

![[Pasted image 20260216161516.png]]

### Caso 3: tres puntos de fuga (respecto a (Z), (X) y (Y))

- Líneas paralelas a los tres ejes convergen, cada conjunto hacia su punto de fuga.
    
- Produce sensación más intensa de profundidad y altura (común en dibujo arquitectónico dramático).
    

![[Pasted image 20260216161604.png]]

---

El uso de estos elementos permite representar los entornos bi y tridimensionales de manera realista, estableciendo una profundidad con base en distancias aparentes y creando una composición que guía la mirada de acuerdo con un foco visual.

### Descripción Matemática de la Proyección en Perspectiva:

Se realiza una distinción entre:

- **P**: Punto del objeto (en 3D).
    
- **P'**: Punto imagen (proyección en el plano de visión).
    

La clave matemática consiste en hallar (*P'*) a partir de (*P*) mediante la utilización de *triángulos semejantes* (geometría de la cámara *pinhole*: la razón entre las distancias determina el escalamiento).

```
           Centro de proyección (C)
                    *
                   /|
                  / |
                 /  |
                /   |
               *----+----------------  Plano de visión
             P      P'               (P proyecta en P')
```

### Representación matricial y coordenadas homogéneas:

La representación del elemento debe llevarse a cabo mediante **coordenadas homogéneas**; esto, debido a que permiten expresar la perspectiva a través del uso de matrices (para después aplicar la división por el componente homogéneo). En la práctica, esto facilita los siguientes procedimientos:

- Concatenación de transformaciones (rotación, traslación y escalamiento).

- Aplicación de la proyección perspectiva de manera uniforme a través de multiplicaciones matriciales.

---

## Proyección Paralela

En proyección paralela, las líneas de proyección son **paralelas entre sí**. Se especifica mediante un **vector de proyección** que define la dirección de esas líneas.

Se distinguen dos casos:

1. Proyección paralela ortogonal
    
2. Proyección paralela oblicua
    

### Proyección paralela oblicua:

#### Características:

- El ángulo que existe entre la *línea de proyección* y el *plano de visión* no es de 90°.

- Existe cierta *deformación* debido a que las longitudes no se conservan de manera uniforme para todas las direcciones.

![[Pasted image 20260216165111.png]]

![[Pasted image 20260216165316.png]]

#### Uso típico

Es útil para mostrar simultáneamente:

- caras frontales,
    
- laterales,
    
- superiores,
    

de forma clara, aunque con distorsión en algunas dimensiones.

#### Ventajas y desventajas:

**Ventajas:**

- permite manejar medidas con precisión (en ciertos ejes/planos),
    
- mantiene la misma escala entre vistas.
    

**Desventajas:**

- no es realista como la perspectiva,
    
- con frecuencia requiere varias vistas para entender bien la forma 3D.
    

- **Ejemplo:** 

En dibujo técnico, una pieza mecánica puede presentarse en *oblicua* para ver la cara frontal “sin deformación” y al mismo tiempo sugerir profundidad.

---

### Proyecciones paralelas ortogonales axonométricas:

#### Ideas generales:

Las proyecciones paralelas ortogonales buscan:

- representar objetos 3D en 2D,
    
- conservando proporciones y formas originales en un sentido más “técnico” que artístico (sin el encogimiento por distancia típico de la perspectiva).
    

![[Pasted image 20260216165355.png]]

![[Pasted image 20260216165458.png]]

Dentro de ellas se incluyen las **axonométricas**, subdivididas en:

- Isométrica
    
- Dimétrica
    
- Trimétrica
    

La diferencia entre estas variantes suele entenderse por cómo se orientan los ejes y cómo se “reparte” la escala/ángulos entre ellos.

- **Ejemplo:**

- En isométrica, un cubo suele verse con tres caras visibles y ejes con tratamiento simétrico, muy usado en videojuegos tipo “isometric view” o en planos técnicos simplificados.
    
- En dimétrica y trimétrica, se rompe parte de esa simetría para ajustar mejor la apariencia o destacar una dirección.
    

---

## Conclusiones del tema

Las proyecciones permiten obtener representaciones distintas del mismo objeto:

- La **proyección paralela** tiende a conservar proporciones y ángulos de manera más estable para propósitos técnicos (medición, planos, representación consistente).
    
- La **proyección en perspectiva** puede deformar tamaños y formas aparentes (acortamiento, puntos de fuga), pero logra una representación más cercana a la percepción humana, simulando la distancia y la profundidad.
    

---
