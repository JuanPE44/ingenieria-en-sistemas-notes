
# Divide y consquista

Es una técnica de diseño de algoritmos que consiste en resolver un problema complejo dividiéndolo en subproblemas más pequeños y manejables. El proceso general sigue tres pasos:

1.  **Dividir:** Se descompone el problema original en uno o varios subproblemas del mismo tipo, pero de menor tamaño. Idealmente, estos subproblemas son independientes entre sí.
2.  **Conquistar:** Se resuelven los subproblemas de forma recursiva. Si un subproblema es lo suficientemente pequeño (caso base), se resuelve directamente sin más división.
3.  **Combinar:** Se combinan las soluciones de los subproblemas para obtener la solución del problema original.

## Características Principales

*   **Recursividad:** La naturaleza de "conquistar" los subproblemas suele llevar a implementaciones recursivas.
*   **Eficiencia:** A menudo conduce a algoritmos eficientes, con complejidades temporales como $O(n \log n)$ o $O(\log n)$.
*   **Paralelismo:** Los subproblemas independientes pueden resolverse en paralelo, lo que hace a esta técnica adecuada para arquitecturas multi-núcleo.

## Análisis de Complejidad

La complejidad de los algoritmos de Divide y Conquista se analiza comúnmente mediante **relaciones de recurrencia**. Una herramienta útil para resolver estas recurrencias es el **Teorema Maestro**.

## Ejemplos Clásicos

*   **Mergesort:**
    *   *Dividir:* Divide la secuencia a ordenar en dos mitades.
    *   *Conquistar:* Ordena recursivamente cada mitad.
    *   *Combinar:* Mezcla (merge) las dos mitades ordenadas para obtener la secuencia completa ordenada.
*   **Quicksort:**
    *   *Dividir:* Elige un pivote y particiona la secuencia en dos sub-secuencias: elementos menores que el pivote y elementos mayores que el pivote.
    *   *Conquistar:* Ordena recursivamente las dos sub-secuencias.
    *   *Combinar:* No requiere un paso explícito de combinación, ya que la ordenación se logra durante la partición.
*   **Búsqueda Binaria:**
    *   *Dividir:* Compara el elemento buscado con el elemento central de la secuencia ordenada. Esto divide la secuencia en (como máximo) una mitad relevante.
    *   *Conquistar:* Busca recursivamente en la mitad relevante.
    *   *Combinar:* No requiere combinación; el resultado de la conquista es el resultado final.
*   **Multiplicación de matrices (Algoritmo de Strassen):** Divide las matrices en submatrices y realiza multiplicaciones y sumas recursivas de forma optimizada.

En resumen, Divide y Conquista es una estrategia poderosa para abordar problemas que pueden descomponerse en partes más simples, resolviendo estas partes y luego uniendo sus soluciones de manera eficiente.