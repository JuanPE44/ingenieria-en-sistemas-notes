## ¿Qué es?
El algoritmo de Dijkstra es un algoritmo voraz (greedy) que encuentra el camino más corto desde un nodo de origen único hacia todos los demás nodos en un grafo ponderado, siempre y cuando los pesos de las aristas no sean negativos.

## ¿Cómo funciona?
1.  Inicializa las distancias a todos los nodos como infinito y la distancia al nodo de origen como 0.
2.  Crea un conjunto de nodos visitados (inicialmente vacío) y un conjunto de nodos no visitados (inicialmente todos los nodos).
3.  Mientras haya nodos no visitados:
    a.  Selecciona el nodo no visitado con la distancia tentativa más pequeña (el nodo actual).
    b.  Para cada vecino del nodo actual: calcula la distancia desde el origen hasta este vecino pasando por el nodo actual. Si esta nueva distancia es menor que la distancia previamente registrada para el vecino, actualízala.
    c.  Marca el nodo actual como visitado y lo elimina del conjunto de no visitados.
4.  Una vez que todos los nodos alcanzables han sido visitados, el algoritmo termina y se conocen las distancias más cortas desde el origen.

## Pseudocódigo
```pseudo
DIJKSTRA(Grafo G, Nodo origen S)
  PARA CADA Nodo V en G:
    distancia[V] = INFINITO
    previo[V] = INDEFINIDO
  distancia[S] = 0

  ColaPrioridad Q // Todos los nodos de G, priorizados por distancia[]

  MIENTRAS Q no esté vacía:
    U = Q.extraer_min() // Nodo en Q con la menor distancia[]

    PARA CADA Vecino V de U:
      alternativa = distancia[U] + peso_arista(U, V)
      SI alternativa < distancia[V]:
        distancia[V] = alternativa
        previo[V] = U
        // (Si V está en Q, actualizar su prioridad)
  RETORNAR distancia[], previo[]
```

## Complejidad

*   Tiempo:
    *   `O(V^2)` con una matriz de adyacencia y búsqueda lineal para el mínimo.
    *   `O((V + E) log V)` con una lista de adyacencia y una cola de prioridad basada en un heap binario (donde V es el número de vértices y E el número de aristas).
    *   `O(E + V log V)` con una lista de adyacencia y una cola de prioridad basada en un heap de Fibonacci.
*   Espacio: `O(V + E)` para almacenar el grafo, las distancias y los predecesores.

## Ejemplo de uso

**Input:**
Grafo:
*   Nodos: A, B, C, D
*   Aristas: (A,B,1), (A,C,4), (B,C,2), (B,D,5), (C,D,1)
*   Origen: A

**Output (distancias más cortas desde A):**
*   A: 0
*   B: 1 (A -> B)
*   C: 3 (A -> B -> C)
*   D: 4 (A -> B -> C -> D)

## Cuándo usarlo

*   Encontrar la ruta más corta en redes de computadoras (protocolos de enrutamiento como OSPF).
*   Sistemas de navegación GPS para calcular la ruta más rápida entre dos puntos.
*   Análisis de redes sociales para encontrar el "grado de separación" más corto entre personas.
