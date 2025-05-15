## ¿Qué es?
El algoritmo de Kruskal es un algoritmo voraz (greedy) que encuentra un Árbol de Expansión Mínima (MST) para un grafo ponderado, conexo y no dirigido. Construye el MST seleccionando aristas en orden creciente de peso, siempre que no formen un ciclo con las aristas ya seleccionadas.

## ¿Cómo funciona?
1.  Ordena todas las aristas del grafo por su peso de menor a mayor.
2.  Inicializa el MST como un conjunto vacío de aristas.
3.  Para cada vértice, crea un conjunto disjunto que solo lo contiene a él (usando una estructura Union-Find).
4.  Itera sobre las aristas ordenadas:
    a.  Si los dos vértices de la arista actual pertenecen a conjuntos disjuntos diferentes (es decir, añadir la arista no forma un ciclo), añade la arista al MST.
    b.  Une los conjuntos de estos dos vértices.
5.  El algoritmo termina cuando el MST contiene V-1 aristas (donde V es el número de vértices) o cuando se han considerado todas las aristas.

## Pseudocódigo
```pseudo
KRUSKAL(Grafo G = (V, E, W))
  MST = {} // Conjunto vacío para las aristas del Árbol de Expansión Mínima
  
  PARA CADA vértice v en V:
    CREAR_CONJUNTO(v) // Cada vértice inicia en su propio conjunto (para Union-Find)
    
  Ordenar todas las aristas E por peso W en orden no decreciente
  
  contador_aristas_mst = 0
  indice_arista_actual = 0
  
  MIENTRAS contador_aristas_mst < |V| - 1 Y indice_arista_actual < |E|:
    (u, v, peso_uv) = E[indice_arista_actual] // Obtener la siguiente arista
    indice_arista_actual = indice_arista_actual + 1
    
    conjunto_u = ENCONTRAR_CONJUNTO(u)
    conjunto_v = ENCONTRAR_CONJUNTO(v)
    
    SI conjunto_u != conjunto_v: // Si u y v están en conjuntos diferentes (no forman ciclo)
      Añadir arista (u, v) a MST
      UNIR_CONJUNTOS(u, v) // Unir los conjuntos de u y v
      contador_aristas_mst = contador_aristas_mst + 1
      
  RETORNAR MST
```

## Complejidad

*   Tiempo: `O(E log E)` o `O(E log V)`. La ordenación de aristas toma `O(E log E)`. Las operaciones Union-Find con optimizaciones (unión por rango/tamaño y compresión de caminos) toman casi tiempo constante por operación, resultando en `O(E α(V))`, donde α es la inversa de la función de Ackermann, que es muy lenta creciendo. Por lo tanto, la ordenación suele dominar.
*   Espacio: `O(V + E)` para almacenar el grafo, las aristas ordenadas y la estructura Union-Find.

## Ejemplo de uso

**Input:**
Grafo no dirigido y ponderado:
*   Nodos: A, B, C, D
*   Aristas y pesos: (A,B,1), (A,C,4), (B,C,2), (B,D,5), (C,D,1)

**Output (Aristas del MST):**
1.  Aristas ordenadas: (A,B,1), (C,D,1), (B,C,2), (A,C,4), (B,D,5)
2.  Tomar (A,B,1). MST={(A,B,1)}. Conjuntos: {A,B},{C},{D}
3.  Tomar (C,D,1). MST={(A,B,1),(C,D,1)}. Conjuntos: {A,B},{C,D}
4.  Tomar (B,C,2). MST={(A,B,1),(C,D,1),(B,C,2)}. Conjuntos: {A,B,C,D}
(Se han añadido V-1 = 3 aristas. El algoritmo termina)
*   Peso total del MST: 1 + 1 + 2 = 4

## Cuándo usarlo

*   Diseño de redes (telecomunicaciones, eléctricas, tuberías) para conectar todos los puntos con el mínimo coste total de enlaces, especialmente cuando el grafo es disperso.
*   Algoritmos de clustering (agrupamiento de datos) para formar grupos basados en la "cercanía".
*   Generación de laberintos o en la construcción de mapas de juegos donde se busca una conectividad mínima.
