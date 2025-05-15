### Menores de una Matriz

**Definición:**
Dada una matriz $A \in \mathbb{R}^{m \times n}$, una **sub matriz cuadrada** de orden $h$ (donde $1 \le h \le \min(m, n)$) se obtiene al seleccionar $h$ filas y $h$ columnas de $A$ (o equivalentemente, eliminando $m-h$ filas y $n-h$ columnas).
El **determinante** de esta submatriz cuadrada se denomina **menor de orden $h$** de la matriz $A$.

**Ejemplo:**
Sea la matriz $A = \begin{pmatrix} 2 & 1 & 3 & 1 \\ 0 & 2 & 0 & 2 \\ 1 & 2 & 1 & 3 \end{pmatrix} \in \mathbb{R}^{3 \times 4}$.
Se pueden calcular menores de orden 1, 2 y 3 (ya que $\min(3, 4) = 3$).

*   **Menor de orden 1:** Cualquier elemento de la matriz. Ejemplo: $|2| = 2$.
*   **Menor de orden 2:** Determinante de una submatriz 2x2. Ejemplo (eliminando fila 3, columnas 3 y 4):
    $\begin{vmatrix} 2 & 1 \\ 0 & 2 \end{vmatrix} = 4$.
*   **Menor de orden 3:** Determinante de una submatriz 3x3. Ejemplo (eliminando columna 4):
    $\begin{vmatrix} 2 & 1 & 3 \\ 0 & 2 & 0 \\ 1 & 2 & 1 \end{vmatrix} = 2(2-0) - 1(0-0) + 3(0-2) = 4 - 0 - 6 = -2$.

### Rango en Términos de Menores

A veces, es más fácil calcular el rango de una matriz en función de sus menores.
z
**Definición:**
Se define el **rango** de una matriz $A$, denotado $Rg(A)$, como el orden $k$ del mayor menor no nulo de $A$.
Formalmente, $Rg(A) = k$ si se cumplen dos condiciones:
1.  Existe al menos un menor de orden $k$ distinto de cero.
2.  Todos los menores de orden $h$ son nulos para cualquier $h > k$.

**Ejemplo:**
Consideremos la misma matriz $A = \begin{pmatrix} 2 & 1 & 3 & 1 \\ 0 & 2 & 0 & 2 \\ 1 & 2 & 1 & 3 \end{pmatrix}$.

Hemos encontrado un menor de orden 3:
$M = \begin{vmatrix} 2 & 1 & 3 \\ 0 & 2 & 0 \\ 1 & 2 & 1 \end{vmatrix} = -2$.
Dado que este menor es distinto de cero ($M \neq 0$) y el orden máximo posible para un menor en esta matriz es 3, concluimos que el rango de la matriz es 3.
$Rg(A) = 3$.

### Lema (Propiedad Importante)

Si $A$ es una matriz cuadrada de orden $n$ (es decir, $A \in \mathbb{R}^{n \times n}$), entonces las siguientes afirmaciones son equivalentes:
1.  $\det(A) \neq 0$ (La matriz es invertible o no singular).
2.  $Rg(A) = n$ (El rango de la matriz es igual a su orden).

---