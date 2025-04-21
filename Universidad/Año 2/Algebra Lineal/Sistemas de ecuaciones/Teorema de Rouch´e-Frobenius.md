
Este teorema fundamental proporciona un criterio claro para determinar si un sistema de ecuaciones lineales $A\vec{x} = \vec{b}$ tiene solución, y cuántas, comparando el rango de la matriz de coeficientes $A$ con el rango de la matriz ampliada $(A|\vec{b})$.

## Teorema (Rouché-Frobenius)

Para un sistema lineal $A\vec{x} = \vec{b}$ (donde $A$ es $n \times m$, $\vec{x}$ es $m \times 1$ y $\vec{b}$ es $n \times 1$), las siguientes tres afirmaciones son **equivalentes**:

1.  El sistema $A\vec{x} = \vec{b}$ es **compatible** (es decir, tiene al menos una solución).
2.  El **rango** de la matriz de coeficientes $A$ es **igual** al rango de la matriz ampliada $(A|\vec{b})$:
    $$ \text{rank}(A) = \text{rank}(A|\vec{b}) $$
3.  El vector de términos independientes $\vec{b}$ es **combinación lineal** de los vectores columna de la matriz $A$.

## Clasificación de Sistemas usando Rouché-Frobenius

El teorema no solo indica si hay solución, sino que también permite clasificar el tipo de sistema comparando los rangos con el **número de incógnitas** (denotado aquí como $m$, el número de columnas de $A$):

*   **Sistema Compatible Determinado (SCD - Única Solución):**
    *   Ocurre si $\text{rank}(A) = \text{rank}(A|\vec{b}) = m$ (el rango coincide con el número de incógnitas).

*   **Sistema Compatible Indeterminado (SCI - Infinitas Soluciones):**
    *   Ocurre si $\text{rank}(A) = \text{rank}(A|\vec{b}) < m$ (el rango es menor que el número de incógnitas).
    *   El número de variables libres (parámetros) en la solución es $m - \text{rank}(A)$.

*   **Sistema Incompatible (SI - Sin Solución):**
    *   Ocurre si $\text{rank}(A) < \text{rank}(A|\vec{b})$ (los rangos son diferentes).

**Diagrama Resumen:**
#### Compatibilidad de A * x = b

- **Compatible:** `rank(A) = rank(A|b)`
  - **Única Solución (SCD):** `rank(A) = rank(A|b) = m` (nº incógnitas)
  - **Infinitas Soluciones (SCI):** `rank(A) = rank(A|b) < m` (nº incógnitas)
- **Incompatible (SI):** `rank(A) < rank(A|b)`



## Teorema de Equivalencias para Matrices Cuadradas Invertibles

Para una matriz **cuadrada** $A$ de orden $n$ (tamaño $n \times n$), las siguientes afirmaciones son todas **equivalentes** (si una es verdadera, todas lo son; si una es falsa, todas lo son):

1.  $A$ es **invertible** (existe la matriz inversa $A^{-1}$).
2.  El determinante de $A$ es distinto de cero: $\det(A) \neq 0$.
3.  El sistema $A\vec{x} = \vec{b}$ admite **solución única** para **cualquier** vector $\vec{b} \in \mathbb{R}^n$.
4.  El sistema homogéneo $A\vec{x} = \vec{0}$ admite **únicamente** la **solución trivial** $\vec{x} = \vec{0}$.
5.  El **rango** de la matriz $A$ es igual a su orden $n$: $\text{rank}(A) = n$ (la matriz tiene rango completo).