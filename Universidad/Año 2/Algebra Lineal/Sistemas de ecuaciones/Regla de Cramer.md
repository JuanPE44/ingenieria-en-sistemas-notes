
Este método se aplica a sistemas de ecuaciones lineales $A\vec{x} = \vec{b}$ donde el número de ecuaciones es igual al número de incógnitas ($n \times n$), es decir, la matriz de coeficientes $A$ es cuadrada.

## Caso 1: Solución Única ($\det(A) \neq 0$)

*   **Condición:** El determinante de la matriz de coeficientes $A$ es distinto de cero.
*   **Resultado:** El sistema tiene **una única solución** (Sistema Compatible Determinado).
*   **Fórmula:** El valor de cada incógnita $x_i$ viene dado por:
 $$ x_i = \frac{\det(A_i)}{\det(A)} \quad \text{para } i = 1, 2, \dots, n $$
*   **Definición de $A_i$:** Es la matriz que se obtiene al reemplazar la **$i$-ésima columna** de la matriz $A$ por el vector de términos independientes $\vec{b}$.

## Caso 2: Sin Solución Única ($\det(A) = 0$)

*   **Condición:** El determinante de la matriz de coeficientes $A$ es igual a cero.
*   **Resultado:** El sistema no tiene solución única. Puede ser compatible indeterminado (infinitas soluciones) o incompatible (sin solución). La regla ayuda a clasificarlo:
    1.  **Sistema Compatible Indeterminado (SCI):** Ocurre si $\det(A) = 0$ y **además** $\det(A_i) = 0$ para **todos** los $i = 1, 2, \dots, n$.
    2.  **Sistema Incompatible (SI):** Ocurre si $\det(A) = 0$ y **existe al menos un** $i$ tal que $\det(A_i) \neq 0$.