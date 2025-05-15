## ¿Qué es?
Quicksort es un algoritmo de ordenamiento altamente eficiente que utiliza la técnica de "Divide y Conquista". Funciona seleccionando un elemento como 'pivote' y particionando los demás elementos del arreglo alrededor de este pivote.

## ¿Cómo funciona?
1.  **Divide (Partición):**
    a.  Elige un elemento del arreglo, llamado pivote (estrategias comunes: primer, último, medio o elemento aleatorio).
    b.  Reorganiza el arreglo de tal manera que todos los elementos menores que el pivote se coloquen antes que él, y todos los elementos mayores se coloquen después. Los elementos iguales pueden ir a cualquier lado. Después de esta partición, el pivote está en su posición final ordenada.
2.  **Conquista:** Llama recursivamente a Quicksort para ordenar el sub-arreglo de elementos a la izquierda del pivote y el sub-arreglo de elementos a la derecha del pivote.
3.  **Combina:** No se necesita una fase de combinación explícita, ya que el ordenamiento se realiza "in-place" durante la partición. Una vez que los sub-arreglos están ordenados, el arreglo completo está ordenado.

## Pseudocódigo
```pseudo
QUICKSORT(arr, bajo, alto)
  SI bajo < alto ENTONCES
    // pi es el índice de partición, arr[pi] está ahora en el lugar correcto
    indice_pivote = PARTICION(arr, bajo, alto)
    
    QUICKSORT(arr, bajo, indice_pivote - 1)  // Ordena recursivamente el sub-arreglo izquierdo
    QUICKSORT(arr, indice_pivote + 1, alto) // Ordena recursivamente el sub-arreglo derecho

// Función para realizar la partición (ejemplo: esquema de Lomuto)
PARTICION(arr, bajo, alto)
  pivote = arr[alto] // Elegir el último elemento como pivote
  i = bajo - 1       // Índice del elemento más pequeño encontrado hasta ahora
  
  PARA j = bajo HASTA alto - 1
    // Si el elemento actual es menor o igual al pivote
    SI arr[j] <= pivote ENTONCES
      i = i + 1
      INTERCAMBIAR(arr[i], arr[j])
  FIN PARA
  
  INTERCAMBIAR(arr[i + 1], arr[alto]) // Colocar el pivote en su posición correcta
  RETORNAR i + 1                     // Retornar el índice del pivote
```

## Complejidad

*   Tiempo:
    *   Peor caso: `O(N^2)` (ocurre con particiones muy desbalanceadas, ej. arreglo ya ordenado y mal pivote).
    *   Caso promedio y mejor caso: `O(N log N)`.
*   Espacio:
    *   `O(log N)` en promedio (para la pila de llamadas recursivas).
    *   `O(N)` en el peor caso (para la pila de llamadas recursivas si las particiones son muy desbalanceadas).

## Ejemplo de uso

**Input:**
Arreglo: `[7, 2, 1, 6, 8, 5, 3, 4]`

**Output (Arreglo ordenado):**
`[1, 2, 3, 4, 5, 6, 7, 8]`

**Un paso de partición (ej. pivote = 4, último elemento):**
Original: `[7, 2, 1, 6, 8, 5, 3, 4]`
Después de particionar alrededor de 4: `[2, 1, 3, 4, 8, 5, 6, 7]` (el 4 está en su lugar, elementos menores a la izquierda, mayores a la derecha).

## Cuándo usarlo

*   Cuando se necesita un algoritmo de ordenamiento rápido en promedio y el uso de memoria adicional es una preocupación (es un algoritmo in-place).
*   Es una buena opción para ordenamiento de propósito general y es la base de muchas funciones de ordenamiento en bibliotecas estándar (a menudo con mejoras como Introsort para evitar el peor caso).
*   Cuando la estabilidad del ordenamiento (mantener el orden relativo de elementos iguales) no es un requisito crítico, ya que Quicksort no es inherentemente estable.
