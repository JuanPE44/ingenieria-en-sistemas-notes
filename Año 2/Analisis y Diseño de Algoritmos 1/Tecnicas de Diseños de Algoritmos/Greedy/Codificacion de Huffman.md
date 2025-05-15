## ¿Qué es?
La Codificación de Huffman es un algoritmo voraz (greedy) utilizado para la compresión de datos sin pérdida. Asigna códigos de longitud variable a los caracteres de entrada basándose en sus frecuencias: los caracteres más frecuentes obtienen códigos más cortos y los menos frecuentes, códigos más largos.

## ¿Cómo funciona?
1.  Calcula la frecuencia de aparición de cada carácter en el texto de entrada.
2.  Crea un nodo hoja para cada carácter, con su frecuencia como "peso".
3.  Utiliza una cola de prioridad (min-heap) para almacenar estos nodos.
4.  Mientras haya más de un nodo en la cola de prioridad:
    a.  Extrae los dos nodos con las frecuencias (pesos) más bajas.
    b.  Crea un nuevo nodo interno cuya frecuencia es la suma de las frecuencias de los dos nodos extraídos.
    c.  Establece el primer nodo extraído como hijo izquierdo y el segundo como hijo derecho del nuevo nodo.
    d.  Inserta este nuevo nodo interno de nuevo en la cola de prioridad.
5.  El único nodo que queda en la cola es la raíz del árbol de Huffman.
6.  Recorre el árbol desde la raíz para asignar los códigos: asigna '0' a las aristas izquierdas y '1' a las aristas derechas. El código de cada carácter es la secuencia de 0s y 1s desde la raíz hasta su hoja.

## Pseudocódigo
```pseudo
HUFFMAN(C) // C es un conjunto de caracteres con sus frecuencias
  n = |C|
  Q = C // Cola de prioridad (min-heap) basada en frecuencias

  PARA i = 1 HASTA n-1:
    asignar nuevo_nodo z
    z.izquierda = EXTRAER-MIN(Q)
    z.derecha = EXTRAER-MIN(Q)
    z.frecuencia = z.izquierda.frecuencia + z.derecha.frecuencia
    INSERTAR(Q, z)
  
  RETORNAR EXTRAER-MIN(Q) // La raíz del árbol de Huffman
  // (Los códigos se obtienen recorriendo el árbol)
```

## Complejidad

*   Tiempo: `O(N log N)` o más precisamente `O(M + C log C)`, donde `M` es la longitud total del texto de entrada (para calcular frecuencias) y `C` es el número de caracteres únicos (para construir el árbol). Si `C` es pequeño y fijo, puede ser `O(M)`. Si se considera `N` como el número de caracteres únicos, entonces `O(N log N)` para la construcción del árbol.
*   Espacio: `O(C)` para almacenar el árbol de Huffman y la tabla de frecuencias/códigos, donde `C` es el número de caracteres únicos.

## Ejemplo de uso

**Input:**
Texto: "AAAAABBBCCCDDE"
Frecuencias: A:5, B:3, C:3, D:2, E:1

**Output (un posible conjunto de códigos Huffman):**
*   A: 0
*   B: 100
*   C: 101
*   D: 110
*   E: 111

Texto codificado (ejemplo): `00000100100100101101101110111` (mucho más corto que la representación original si cada carácter usara, por ejemplo, 8 bits).

## Cuándo usarlo

*   Compresión de archivos de texto o datos donde algunos símbolos son significativamente más frecuentes que otros (ej. formatos ZIP, GZIP).
*   Transmisión eficiente de datos, reduciendo el ancho de banda necesario.
*   Parte de algoritmos de compresión más complejos, como en formatos de imagen (JPEG) y audio/video (MP3, MPEG).
