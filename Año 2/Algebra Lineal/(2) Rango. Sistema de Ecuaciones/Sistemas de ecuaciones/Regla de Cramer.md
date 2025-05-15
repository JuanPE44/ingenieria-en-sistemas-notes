---
sticker: lucide//alarm-clock-off
---

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


## Cálculo de $\det(A_i)$ para la Regla de Cramer

La regla de Cramer se utiliza para resolver sistemas de ecuaciones lineales de la forma $Ax = b$, donde $A$ es la matriz de coeficientes, $x$ es el vector de incógnitas y $b$ es el vector de términos constantes. La solución para la incógnita $x_i$ viene dada por:

$x_i = \frac{\det(A_i)}{\det(A)}$

Donde $A_i$ es la matriz que se obtiene al reemplazar la $i$-ésima columna de la matriz $A$ por el vector $b$.

**Ejemplo:**

Considera el siguiente sistema de ecuaciones lineales:

$2x_1 + 1x_2 - 1x_3 = 8$
$-3x_1 - 1x_2 + 2x_3 = -11$
$-2x_1 + 1x_2 + 2x_3 = -3$

La matriz de coeficientes $A$ y el vector de términos constantes $b$ son:

$A = \begin{pmatrix} 2 & 1 & -1 \\ -3 & -1 & 2 \\ -2 & 1 & 2 \end{pmatrix}$, $b = \begin{pmatrix} 8 \\ -11 \\ -3 \end{pmatrix}$

Supongamos que queremos encontrar el valor de $x_2$. Para ello, necesitamos calcular $\det(A_2)$.

### Paso 1: Construir la matriz $A_2$

Reemplazamos la segunda columna de $A$ con el vector $b$:

$A_2 = \begin{pmatrix} 2 & 8 & -1 \\ -3 & -11 & 2 \\ -2 & -3 & 2 \end{pmatrix}$

### Paso 2: Calcular el determinante de $A_2$

Podemos usar la expansión por cofactores a lo largo de la primera fila:

$\det(A_2) = 2 \cdot \det \begin{pmatrix} -11 & 2 \\ -3 & 2 \end{pmatrix} - 8 \cdot \det \begin{pmatrix} -3 & 2 \\ -2 & 2 \end{pmatrix} + (-1) \cdot \det \begin{pmatrix} -3 & -11 \\ -2 & -3 \end{pmatrix}$

Calculamos los determinantes de las submatrices 2x2:

$\det \begin{pmatrix} -11 & 2 \\ -3 & 2 \end{pmatrix} = (-11)(2) - (2)(-3) = -22 + 6 = -16$

$\det \begin{pmatrix} -3 & 2 \\ -2 & 2 \end{pmatrix} = (-3)(2) - (2)(-2) = -6 + 4 = -2$

$\det \begin{pmatrix} -3 & -11 \\ -2 & -3 \end{pmatrix} = (-3)(-3) - (-11)(-2) = 9 - 22 = -13$

Sustituimos estos valores en la fórmula de expansión:

$\det(A_2) = 2(-16) - 8(-2) + (-1)(-13)$
$\det(A_2) = -32 + 16 + 13$
$\det(A_2) = -16 + 13$
$\det(A_2) = -3$

Por lo tanto, el determinante de la matriz $A_2$ para este sistema es $-3$. Este es el valor que iría en el numerador al calcular $x_2$ usando la regla de Cramer.