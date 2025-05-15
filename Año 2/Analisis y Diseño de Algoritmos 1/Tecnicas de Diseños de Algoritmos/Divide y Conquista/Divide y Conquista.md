Es una técnica de diseño de algoritmos que resuelve un problema descomponiéndolo recursivamente en subproblemas más pequeños del mismo tipo. Luego, combina las soluciones de estos subproblemas para obtener la solución del problema original.

## Conceptos Clave
*   **Divide:** El problema se descompone en subproblemas independientes.
*   **Conquista:** Los subproblemas se resuelven recursivamente (o directamente si son triviales).
*   **Combina:** Las soluciones de los subproblemas se fusionan para la solución final.
*   **Recursión:** Es la base de la implementación de esta técnica.
*   **Caso Base:** Condición que detiene la recursión (subproblema suficientemente pequeño).

## Explicación
La estrategia de "Divide y Conquista" aborda problemas complejos dividiéndolos en partes más manejables. Primero, se identifica cómo fraccionar el problema principal en instancias más pequeñas de sí mismo. Cada una de estas instancias se resuelve, idealmente de forma recursiva, hasta llegar a un punto donde la solución es obvia o muy simple (el caso base). Finalmente, las soluciones obtenidas para cada subproblema se integran o combinan de manera inteligente para construir la solución completa del problema inicial. La eficiencia de esta técnica a menudo depende de cuán equilibrada sea la división y cuán eficiente sea la etapa de combinación.

## Ejemplo
El algoritmo de ordenamiento **Mergesort** es un ejemplo clásico:
1.  **Divide:** El arreglo `A` se divide en dos mitades `A1` y `A2`.
2.  **Conquista:** Se llama recursivamente a `Mergesort(A1)` y `Mergesort(A2)`.
3.  **Combina:** Se fusionan (merge) las dos mitades ordenadas `A1` y `A2` para obtener el arreglo `A` ordenado.

```pseudocode
MERGE-SORT(A, inicio, fin)
  SI inicio < fin ENTONCES
    medio = (inicio + fin) / 2
    MERGE-SORT(A, inicio, medio)
    MERGE-SORT(A, medio + 1, fin)
    MERGE(A, inicio, medio, fin)
  FIN SI
```

## Aplicaciones
*   **Algoritmos de ordenamiento:** [[Mergesort]], [[Quicksort]].
*   **Búsqueda:** [[Universidad/Año 2/Analisis y Diseño de Algoritmos 1/Tecnicas de Diseños de Algoritmos/Divide y Conquista/Busqueda Binaria|Busqueda Binaria]].
*   **Procesamiento de imágenes:** Multiplicación de matrices (algoritmo de [[Strassen]]), transformada rápida de Fourier ([[FFT]]).

