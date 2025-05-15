## ¿Qué es?
El algoritmo de Prim es un algoritmo voraz (greedy) que encuentra un Árbol de Expansión Mínima (MST, por sus siglas en inglés) para un grafo ponderado, conexo y no dirigido. Esto significa que encuentra un subconjunto de aristas que conecta todos los vértices sin formar ciclos y con el mínimo peso total posible.

## ¿Cómo funciona?
1.  Comienza eligiendo un vértice arbitrario para iniciar el MST (este vértice es el único en el MST inicialmente).
2.  Mantiene un conjunto de vértices ya incluidos en el MST y otro con los que aún no lo están.
3.  En cada paso, selecciona la arista de menor peso que conecta un vértice del MST con un vértice que aún no está en el MST.
4.  Añade esta arista y el nuevo vértice al MST.
5.  Repite el proceso hasta que todos los vértices del grafo original estén incluidos en el MST.
6.  Para evitar ciclos, solo se consideran aristas que conectan un vértice dentro del MST con uno fuera de él.

## Pseudocódigo
```pseudo
PRIM(Grafo G, Nodo_origen S)
  PARA CADA Nodo U en G:
    costo_min[U] = INFINITO  // Costo mínimo para conectar U al MST
    padre_en_MST[U] = NULO   // Vértice a través del cual U se conecta al MST
    en_MST[U] = FALSO

  costo_min[S] = 0

  ColaPrioridad Q // Contiene todos los nodos de G, priorizados por costo_min[]

  MIENTRAS Q no esté vacía:
    U = Q.extraer_min() // Extrae el nodo con el menor costo_min que no esté en el MST
    en_MST[U] = VERDADERO

    PARA CADA Vecino V de U:
      SI en_MST[V] == FALSO Y peso_arista(U, V) < costo_min[V]:
        padre_en_MST[V] = U
        costo_min[V] = peso_arista(U, V)
        // (Actualizar la prioridad de V en Q con el nuevo costo_min[V])
  
  // El MST está formado por las aristas (padre_en_MST[V], V) para cada V != S
  // y padre_en_MST[V] != NULO
  RETORNAR padre_en_MST[] // o el conjunto de aristas del MST
```

## Complejidad

*   Tiempo:
    *   `O(V^2)` con matriz de adyacencia y búsqueda lineal del mínimo.
    *   `O(E log V)` o `O((V+E) log V)` con lista de adyacencia y cola de prioridad (heap binario).
    *   `O(E + V log V)` con lista de adyacencia y cola de prioridad (heap de Fibonacci).
    (V = número de vértices, E = número de aristas)
*   Espacio: `O(V + E)` para almacenar el grafo, costos y punteros a padres.

## Ejemplo de uso

**Input:**
Grafo no dirigido y ponderado:
*   Nodos: A, B, C, D
*   Aristas: (A,B,1), (A,C,4), (B,C,2), (B,D,5), (C,D,1)

**Output (Aristas del MST, suponiendo que se empieza en A):**
*   (A,B) con peso 1
*   (B,C) con peso 2
*   (C,D) con peso 1
*   Peso total del MST: 1 + 2 + 1 = 4

## Cuándo usarlo

*   Diseño de redes de comunicación, eléctricas o de transporte para conectar múltiples puntos con el mínimo coste de cableado o infraestructura.
*   Generación de laberintos o en algoritmos de clustering.
*   Aproximación para problemas NP-difíciles, como el problema del viajante de comercio (en algunas de sus variantes).
