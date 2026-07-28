Los **algoritmos de búsqueda** son parte fundamental del proceso de localizar un elemento particular dentro de una colección de datos que puede tomar varias formas como arreglos, listas, árboles u otras estructuras.

## Algoritmos Básicos

Las formas más básicas de búsqueda vienen dadas en la forma de los siguientes algoritmos:

### Búsqueda Lineal ($O(n)$ & $O(1)$):

Esta es la forma más sencilla de búsqueda y consiste en revisar cada elemento de manera secuencial hasta hallar el objetivo o haber recorrido toda la estructura de datos. Es útil para datos organizados y no organizados.

##### Ejemplo:

Considérese el arreglo `arr[] = {10, 50, 30, 70, 80, 20, 90, 40}` en donde `key = 30`.

1. Primero, se compara el valor de cada índice con la key establecida, comenzando por el primer elemento. 
2. Después se compara con los índices subsecuentes.
3. Si se encuentra, el programa se detiene; si no, marca que no se halló la key deseada. 

```
#include <stdio.h>

int search(int arr[], int n, int x) {
    
    // Iterate over the array in order to
    // find the key x
    for (int i = 0; i < n; i++)
        if (arr[i] == x)
            return i;
    return -1;
}

// Driver code
int main(void) {
    int arr[] = { 2, 3, 4, 10, 40 };
    int x = 10;
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    int result = search(arr, n, x);
    (result == -1)
        ? printf("Element is not present in array")
        : printf("Element is present at index %d", result);
    return 0;
}
```

