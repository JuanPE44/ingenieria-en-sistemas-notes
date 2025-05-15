Es una técnica de diseño de algoritmos que construye una solución a un problema tomando, en cada paso, la decisión que parece ser la mejor en ese momento (óptima local). Espera que una secuencia de óptimos locales conduzca a una solución óptima global.

## Conceptos Clave
*   **Elección Localmente Óptima:** En cada etapa, se selecciona la opción más prometedora sin considerar futuras consecuencias.
*   **Irrevocable:** Una vez que se toma una decisión, no se reconsidera.
*   **Construcción Paso a Paso:** La solución se arma de forma incremental.
*   **Función de Selección:** Criterio para elegir la "mejor" opción en cada paso.
*   **No Siempre Óptimo Global:** Puede no encontrar la mejor solución global para todos los problemas.

## Explicación
La técnica Greedy, o Voraz, aborda los problemas tomando decisiones que parecen las más ventajosas de forma inmediata. En cada paso del algoritmo, se evalúan las opciones disponibles y se elige aquella que maximiza o minimiza algún criterio local, sin preocuparse por el impacto a largo plazo de esa elección. Es como si en cada bifurcación del camino, eligiéramos la ruta que parece más corta en ese instante, esperando que esto nos lleve al destino más rápido. Si bien esta estrategia es simple y a menudo eficiente, no garantiza la solución óptima global para todos los tipos de problemas, pero sí para una clase específica donde la propiedad de "elección voraz" se cumple.

## Ejemplo
**Problema de las Monedas (Cambio)**: Dar el cambio con la menor cantidad de monedas, usando un conjunto de denominaciones disponibles (ej. 25, 10, 5, 1 centavos).
1.  **Elección Voraz:** En cada paso, tomar la moneda de mayor valor posible que no exceda la cantidad restante a dar.
2.  **Proceso:** Si se deben dar 36 centavos:
    *   Tomar una moneda de 25 (restan 11).
    *   Tomar una moneda de 10 (resta 1).
    *   Tomar una moneda de 1 (restan 0).
    *   Total: 3 monedas.

## Aplicaciones
*   **Algoritmo de [[Dijkstra]]:** Para encontrar el camino más corto en un grafo con pesos no negativos.
*   **Algoritmo de [[Prim]] y [[Kruskal]]:** Para encontrar el árbol de expansión mínima en un grafo.
*   **[[Codificacion de Huffman]]**:Para compresión de datos.
