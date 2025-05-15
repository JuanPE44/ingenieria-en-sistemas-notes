## ¿Qué es?
Mergesort es un algoritmo de ordenamiento eficiente y estable que utiliza la técnica de "Divide y Conquista". Divide recursivamente la lista a ordenar en sublistas más pequeñas hasta que cada sublista contenga un solo elemento, y luego las fusiona (merge) de manera ordenada.

## ¿Cómo funciona?
1.  **Divide:** Si la lista tiene más de un elemento, se divide en dos mitades aproximadamente iguales.
2.  **Conquista:** Se llama recursivamente a Mergesort para ordenar cada una de las dos mitades. Si una mitad tiene un solo elemento, se considera ordenada (caso base).
3.  **Combina (Merge):** Una vez que las dos mitades están ordenadas, se fusionan en una única lista ordenada. Esto se hace comparando los elementos de ambas mitades secuencialmente y colocando el menor en la nueva lista, repitiendo hasta que todos los elementos de ambas mitades se hayan copiado.

## Pseudocódigo
```pseudo
MERGESORT(arr, inicio, fin)
  SI inicio < fin ENTONCES
    medio = piso((inicio + fin) / 2)
    
    MERGESORT(arr, inicio, medio)       // Ordena la primera mitad
    MERGESORT(arr, medio + 1, fin)    // Ordena la segunda mitad
    
    MERGE(arr, inicio, medio, fin)      // Fusiona las dos mitades ordenadas

MERGE(arr, inicio, medio, fin)
  // Crear arreglos temporales para las dos mitades
  n1 = medio - inicio + 1
  n2 = fin - medio
  
  IZQ = nuevo arreglo de tamaño n1
  DER = nuevo arreglo de tamaño n2
  
  // Copiar datos a los arreglos temporales IZQ[] y DER[]
  PARA i = 0 HASTA n1 - 1
    IZQ[i] = arr[inicio + i]
  PARA j = 0 HASTA n2 - 1
    DER[j] = arr[medio + 1 + j]
    
  // Fusionar los arreglos temporales de nuevo en arr[inicio..fin]
  i = 0     // Índice inicial de la primera sublista
  j = 0     // Índice inicial de la segunda sublista
  k = inicio // Índice inicial de la sublista fusionada
  
  MIENTRAS i < n1 Y j < n2
    SI IZQ[i] <= DER[j] ENTONCES
      arr[k] = IZQ[i]
      i = i + 1
    SINO
      arr[k] = DER[j]
      j = j + 1
    FIN SI
    k = k + 1
    
  // Copiar los elementos restantes de IZQ[], si hay alguno
  MIENTRAS i < n1
    arr[k] = IZQ[i]
    i = i + 1
    k = k + 1
    
  // Copiar los elementos restantes de DER[], si hay alguno
  MIENTRAS j < n2
    arr[k] = DER[j]
    j = j + 1
    k = k + 1
```

## Complejidad

*   Tiempo: `O(N log N)` en el peor, mejor y caso promedio. (N es el número de elementos a ordenar).
*   Espacio: `O(N)` debido a la necesidad de un arreglo auxiliar del mismo tamaño que el original para la etapa de fusión.

## Ejemplo de uso

**Input:**
Arreglo: `[38, 27, 43, 3, 9, 82, 10]`

**Output (Arreglo ordenado):**
`[3, 9, 10, 27, 38, 43, 82]`

**Pasos intermedios (simplificado):**
1.  Divide: `[38, 27, 43, 3]` y `[9, 82, 10]`
2.  Divide más: `[38, 27]`, `[43, 3]` y `[9, 82]`, `[10]`
3.  Divide más: `[38]`, `[27]`, `[43]`, `[3]` y `[9]`, `[82]`, `[10]`
4.  Merge: `[27, 38]`, `[3, 43]` y `[9, 82]`, `[10]`
5.  Merge: `[3, 27, 38, 43]` y `[9, 10, 82]`
6.  Merge final: `[3, 9, 10, 27, 38, 43, 82]`

## Cuándo usarlo

*   Cuando se necesita un algoritmo de ordenamiento estable (mantiene el orden relativo de elementos iguales).
*   Cuando la complejidad `O(N log N)` en el peor caso es un requisito crucial.
*   Para ordenar grandes conjuntos de datos que pueden no caber completamente en la memoria principal (ordenamiento externo), ya que su naturaleza secuencial de acceso a datos es ventajosa.
