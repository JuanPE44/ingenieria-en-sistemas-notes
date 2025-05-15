## ¿Qué es?
El algoritmo de Strassen es un algoritmo eficiente para la multiplicación de matrices que utiliza la técnica de "Divide y Conquista".  Reduce el número de multiplicaciones necesarias en comparación con el algoritmo clásico, mejorando la complejidad temporal para matrices grandes.

## ¿Cómo funciona?
1.  **Divide:** Divide las matrices de entrada A y B (de tamaño n x n, donde n es una potencia de 2) en cuatro submatrices de tamaño (n/2) x (n/2).
2.  **Calcula 7 productos:** Define 7 nuevas matrices (M1 a M7) que son el resultado de multiplicaciones de combinaciones específicas de las submatrices de A y B.  Esta es la parte clave donde se reduce el número de multiplicaciones.
3.  **Combina:** Calcula las cuatro submatrices (C11, C12, C21, C22) de la matriz resultante C (de tamaño n x n) utilizando sumas y restas de las matrices M1 a M7.
4.  **Recursión:** Si las submatrices (n/2) x (n/2) son lo suficientemente grandes, aplica recursivamente el algoritmo de Strassen para calcular los productos M1 a M7. Si son pequeñas, se puede usar la multiplicación de matrices clásica.

## Pseudocódigo
```pseudo
STRASSEN(A, B)
  // A y B son matrices n x n, donde n es una potencia de 2
  SI n <= umbral ENTONCES
    RETORNAR MultiplicacionClasica(A, B) // Usar multiplicación clásica para matrices pequeñas

  // Dividir A y B en submatrices de tamaño (n/2) x (n/2)
  A11, A12, A21, A22 = Dividir(A)
  B11, B12, B21, B22 = Dividir(B)

  // Calcular las 7 matrices producto
  M1 = STRASSEN(A11 + A22, B11 + B22)
  M2 = STRASSEN(A21 + A22, B11)
  M3 = STRASSEN(A11, B12 - B22)
  M4 = STRASSEN(A22, B21 - B11)
  M5 = STRASSEN(A11 + A12, B22)
  M6 = STRASSEN(A21 - A11, B11 + B12)
  M7 = STRASSEN(A12 - A22, B21 + B22)

  // Calcular las submatrices de la matriz resultante C
  C11 = M1 + M4 - M5 + M7
  C12 = M3 + M5
  C21 = M2 + M4
  C22 = M1 - M2 + M3 + M6

  // Combinar las submatrices para formar la matriz resultante C
  C = Combinar(C11, C12, C21, C22)
  RETORNAR C
```

## Complejidad

*   Tiempo: `O(n^log2(7))` ≈ `O(n^2.81)`, donde n es la dimensión de las matrices.  Esto es mejor que la multiplicación clásica, que es O(n^3).
*   Espacio: `O(n^2)` debido a la creación de matrices temporales durante la recursión.

## Ejemplo de uso

**Input:**
```
A = [[1, 2], [3, 4]]
B = [[5, 6], [7, 8]]
```

**Output:**
```
C = [[19, 22], [43, 50]]
```

(El algoritmo realizaría las operaciones de división, multiplicación de las M1-M7 y combinación como se describe arriba, recursivamente si fuera necesario).

## Cuándo usarlo

*   Para multiplicar matrices muy grandes donde la eficiencia es crítica. El algoritmo de Strassen supera a la multiplicación clásica para matrices de tamaño suficientemente grande (el "umbral" depende de la implementación y la arquitectura).
*   En bibliotecas de álgebra lineal y software científico donde la multiplicación de matrices es una operación fundamental.
