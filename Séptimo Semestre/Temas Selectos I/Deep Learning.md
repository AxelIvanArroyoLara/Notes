El **deep learning** forma parte del **machine learning** y no es un paradigma, ni tampoco un nuevo tipo de aprendizaje, sino una combinación de los enfoques principales (supervisado, no supervisado y refuerzo). Su funcionamiento se basa en el uso de redes neuronales con múltiples capas para aprender representaciones de utilidad: se conocen como **deep neural networks**.

Todo sistema de deep-learning es machine learning, pero no todo sistema machine learning es deep learning.

---
## Profundidad

La **profundidad** significa aprendizaje a través de múltiples capas. Existe una capa de entrada, capas ocultas (patrones simples y después complejos combinados), llevando todos a una misma salida. Cada capa transforma la representación previa de manera que llega como dato a la siguiente, en donde nodo en la representación representa una neurona o perceptrón. La combinación de todo este sistema se conoce como **red neuronal**. Cabe destacar que una neurona no es (generalmente) capaz de enviar su salida a alguna de las neuronas de su misma capa.

---
## Redes Neuronales

Téngase una neurona cuya entrada $x$ es multiplicada por un peso (parámetro) $\theta_1$, sumada a un sesgo $\theta_0$. La expresión se ve representada en:

$$
\theta_1 * \theta_0 x
$$

Esta se corresponde con la ecuación de la recta, y permite clasificar una serie de puntos en la gráfica.

$g(z)$ retorna una probabilidad y $y$ sombrero representa una predicción o decisión dada por el resultado de $g$. La función que transforma los valores para lograr los finales, se conoce como *sigmoide* y se representa por $\sum$. 
