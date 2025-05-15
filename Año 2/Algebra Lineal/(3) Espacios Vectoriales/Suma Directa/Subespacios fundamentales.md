Sea $A$ una matriz de tamaño $m \times n$:

$$
A =
\begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn}
\end{pmatrix}
= (C_1, \dots, C_n) % Representación por columnas
= \begin{pmatrix} F_1 \\ \vdots \\ F_m \end{pmatrix} % Representación por filas
$$

Donde $C_j$ representa la $j$-ésima columna (un vector en $\mathbb{R}^m$) y $F_i$ representa la $i$-ésima fila (un vector en $\mathbb{R}^n$).

Podemos definir cuatro subespacios vectoriales fundamentales asociados a la matriz $A$:

1.  **Espacio Nulo de A ($N(A)$):**
    *   Definición: Es el conjunto de todos los vectores $\vec{x}$ en $\mathbb{R}^n$ que son solución del sistema homogéneo $A\vec{x} = \vec{0}$.
    *   $N(A) = \{\vec{x} \in \mathbb{R}^n \mid A\vec{x} = \vec{0}\}$
    *   Es un subespacio de $\mathbb{R}^n$.

2.  **Espacio Fila de A ($Fi(A)$ o $R(A)$):**
    *   Definición: Es el subespacio de $\mathbb{R}^n$ generado por los vectores fila de $A$.
    *   $Fi(A) = \langle F_1, \dots, F_m \rangle$
    *   Es un subespacio de $\mathbb{R}^n$.

3.  **Espacio Columna de A ($Co(A)$):**
    *   Definición: Es el subespacio de $\mathbb{R}^m$ generado por los vectores columna de $A$.
    *   $Co(A) = \langle C_1, \dots, C_n \rangle$
    *   Es un subespacio de $\mathbb{R}^m$. (También se conoce como la *imagen* o *rango* de la transformación lineal definida por $A$).

4.  **Espacio Nulo de la Transpuesta de A ($N(A^t)$):**
    *   Definición: Es el espacio nulo de la matriz transpuesta $A^t$. Es el conjunto de todos los vectores $\vec{y}$ en $\mathbb{R}^m$ tales que $A^t\vec{y} = \vec{0}$.
    *   $N(A^t) = \{\vec{y} \in \mathbb{R}^m \mid A^t\vec{y} = \vec{0}\}$
    *   Es un subespacio de $\mathbb{R}^m$. (También se conoce como el *espacio nulo izquierdo* de $A$, ya que la condición $A^t\vec{y} = \vec{0}$ es equivalente a $\vec{y}^t A = \vec{0}^t$).

Estos cuatro subespacios capturan información esencial sobre la matriz $A$ y la transformación lineal que representa.