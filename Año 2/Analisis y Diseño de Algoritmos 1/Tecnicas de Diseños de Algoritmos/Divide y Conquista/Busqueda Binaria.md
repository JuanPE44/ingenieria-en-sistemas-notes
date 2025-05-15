## ¿Qué es?
La Búsqueda Binaria es un algoritmo eficiente para encontrar un elemento específico dentro de una lista ordenada. Divide repetidamente la porción de la lista que podría contener el elemento, reduciendo a la mitad el espacio de búsqueda en cada paso.

## ¿Cómo funciona?
1.  Comienza examinando el elemento central de la lista ordenada.
2.  Si el elemento central es el elemento buscado, la búsqueda termina con éxito.
3.  Si el elemento buscado es menor que el elemento central, la búsqueda continúa en la mitad izquierda de la lista.
4.  Si el elemento buscado es mayor que el elemento central, la búsqueda continúa en la mitad derecha de la lista.
5.  Repite los pasos 1-4 hasta que el elemento sea encontrado o la porción de la lista a buscar esté vacía (en cuyo caso, el elemento no está presente).

## Pseudocódigo
```pseudo
BUSQUEDA_BINARIA(lista, elemento_buscado)
  inicio = 0
  fin = longitud(lista) - 1

  MIENTRAS inicio <= fin:
    medio = piso((inicio + fin) / 2)  // Calcula el índice del elemento central

    SI lista[medio] == elemento_buscado:
      RETORNAR medio  // Elemento encontrado en el índice 'medio'
    SINO SI elemento_buscado < lista[medio]:
      fin = medio - 1  // Buscar en la mitad izquierda
    SINO:
      inicio = medio + 1 // Buscar en la mitad derecha

  RETORNAR -1  // Elemento no encontrado
```

## Complejidad

*   Tiempo: `O(log N)` (logarítmica), donde N es el número de elementos en la lista.
*   Espacio: `O(1)` (constante) para la versión iterativa. `O(log N)` para la versión recursiva debido a la pila de llamadas.

## Ejemplo de uso

**Input:**
*   Lista ordenada: `[2, 5, 7, 8, 11, 12]`
*   Elemento buscado: `11`

**Output:**
*   Índice: `4` (el elemento 11 se encuentra en el índice 4 de la lista).

**Pasos:**
1.  Medio = (0 + 5) / 2 = 2. lista[2] = 7. 11 > 7, buscar en la mitad derecha.
2.  Inicio = 3, Fin = 5. Medio = (3 + 5) / 2 = 4. lista[4] = 11. ¡Encontrado!

## Cuándo usarlo

*   Para buscar rápidamente elementos en listas o arreglos que ya están ordenados.
*   En diccionarios o bases de datos indexadas para encontrar registros específicos.
*   Implementación de algoritmos más complejos que requieren búsquedas eficientes en rangos ordenados.
