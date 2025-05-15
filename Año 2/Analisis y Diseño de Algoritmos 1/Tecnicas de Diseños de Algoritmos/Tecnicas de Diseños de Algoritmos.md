Son enfoques o metodologías generales y sistemáticas utilizadas para desarrollar algoritmos eficientes y efectivos. Estas técnicas proporcionan un marco para abordar problemas computacionales, guiando la creación de soluciones estructuradas.

## Conceptos Clave
*   **Estrategia General:** No son algoritmos específicos, sino "recetas" para crearlos.
*   **Eficiencia:** Buscan optimizar el uso de recursos (tiempo y espacio).
*   **Estructura del Problema:** La elección de la técnica depende de la naturaleza del problema.
*   **Descomposición:** A menudo implican dividir el problema en subproblemas más simples.
*   **Patrones de Solución:** Ofrecen soluciones probadas para clases de problemas.

## Explicación
Las técnicas de diseño de algoritmos son fundamentales en la informática para resolver problemas complejos de manera organizada. En lugar de inventar una solución desde cero cada vez, estas técnicas ofrecen plantillas de pensamiento. Por ejemplo, "[[Divide y Conquista]]" es ideal para problemas que se pueden fraccionar; "[[Greedy]]" (Voraz) toma la mejor decisión local en cada paso; y "Programación Dinámica" resuelve subproblemas que se superponen, almacenando sus resultados para evitar recálculos. Conocer estas técnicas permite seleccionar el enfoque más adecuado para un problema dado, llevando a soluciones más rápidas, con menor consumo de memoria y más fáciles de entender y mantener.

## Ejemplo
Un ejemplo de aplicación de una técnica de diseño es el algoritmo **Mergesort**, que utiliza la técnica de **Divide y Conquista**:
1.  **Divide:** El arreglo a ordenar se divide recursivamente por la mitad hasta obtener subarreglos de un solo elemento (que se consideran ordenados).
2.  **Conquista:** (Implícito, ya que los subarreglos de un elemento están ordenados).
3.  **Combina:** Los subarreglos ordenados se fusionan (merge) de manera ordenada para producir un arreglo ordenado más grande.

## Aplicaciones
*   **Ordenamiento y Búsqueda:** Algoritmos como Quicksort (Divide y Conquista) o Búsqueda Binaria.
*   **Optimización de Rutas:** Problemas como el del viajante de comercio (puede usar Programación Dinámica o algoritmos Greedy para aproximaciones).
*   **Procesamiento de Datos:** Compresión de datos (algoritmos Greedy como Huffman).