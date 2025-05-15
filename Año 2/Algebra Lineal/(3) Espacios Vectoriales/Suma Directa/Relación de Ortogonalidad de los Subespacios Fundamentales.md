Existe una relación fundamental de ortogonalidad entre los cuatro subespacios asociados a una matriz $A \in \mathbb{R}^{m \times n}$.

Recordemos las definiciones:
*   **Espacio Fila ($Fi(A)$):** Subespacio de $\mathbb{R}^n$ generado por las filas de $A$. $Fi(A) = \langle F_1, \dots, F_m \rangle$.
*   **Espacio Nulo ($N(A)$):** Subespacio de $\mathbb{R}^n$ de las soluciones de $A\vec{x} = \vec{0}$. $N(A) = \{\vec{x} \in \mathbb{R}^n \mid A\vec{x} = \vec{0}\}$.
*   **Espacio Columna ($Co(A)$):** Subespacio de $\mathbb{R}^m$ generado por las columnas de $A$. $Co(A) = \langle C_1, \dots, C_n \rangle$.
*   **Espacio Nulo Izquierdo ($N(A^t)$):** Subespacio de $\mathbb{R}^m$ de las soluciones de $A^t\vec{y} = \vec{0}$. $N(A^t) = \{\vec{y} \in \mathbb{R}^m \mid A^t\vec{y} = \vec{0}\}$.

### Ortogonalidad entre $N(A)$ y $Fi(A)$

Consideremos la condición para que un vector $\vec{x} = (x_1, \dots, x_n)$ pertenezca al espacio nulo $N(A)$:
$A\vec{x} = \vec{0}$

$$
\begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn}
\end{pmatrix}
\begin{pmatrix}
x_1 \\
\vdots \\
x_n
\end{pmatrix}
=
\begin{pmatrix}
0 \\
\vdots \\
0
\end{pmatrix}
$$

Recordemos que la multiplicación matriz-vector se puede ver como una serie de productos escalares entre las filas de la matriz y el vector columna:

$$
\begin{pmatrix}
F_1 \cdot \vec{x} \\
F_2 \cdot \vec{x} \\
\vdots \\
F_m \cdot \vec{x}
\end{pmatrix}
=
\begin{pmatrix}
0 \\
\vdots \\
0
\end{pmatrix}
$$

Por lo tanto, un vector $\vec{x}$ está en $N(A)$ si y solo si su producto escalar con **cada una** de las filas $F_i$ de $A$ es cero:
$\vec{x} \in N(A) \iff F_i \cdot \vec{x} = 0$ para todo $i = 1, \dots, m$.

Sabemos que el espacio fila $Fi(A)$ es el espacio generado por estas filas: $Fi(A) = \langle F_1, \dots, F_m \rangle$.
También sabemos que un vector es ortogonal a un subespacio si y solo si es ortogonal a todos los vectores de un conjunto generador de ese subespacio.

Entonces, la condición $F_i \cdot \vec{x} = 0$ para todo $i$ significa que $\vec{x}$ es ortogonal a todos los generadores de $Fi(A)$, lo cual implica que $\vec{x}$ es ortogonal a **todo** el espacio fila $Fi(A)$.

Por definición de complemento ortogonal, el conjunto de todos los vectores $\vec{x}$ que son ortogonales a $Fi(A)$ es precisamente $Fi(A)^\perp$.

Hemos demostrado que:
$\vec{x} \in N(A) \iff \vec{x} \in Fi(A)^\perp$

Por lo tanto, concluimos:
$N(A) = Fi(A)^\perp$

Utilizando la propiedad de que $(S^\perp)^\perp = S$, también obtenemos la relación inversa:
$N(A)^\perp = (Fi(A)^\perp)^\perp = Fi(A)$

### Ortogonalidad entre $N(A^t)$ y $Co(A)$

De manera análoga, aplicando el mismo razonamiento a la matriz transpuesta $A^t$, se puede demostrar que:
*   El espacio nulo de $A^t$ ($N(A^t)$) es el complemento ortogonal del espacio fila de $A^t$.
*   Pero el espacio fila de $A^t$ es precisamente el espacio columna de $A$ ($Fi(A^t) = Co(A)$).

Por lo tanto, obtenemos la segunda relación fundamental de ortogonalidad:
$N(A^t) = Co(A)^\perp$
y
$N(A^t)^\perp = Co(A)$

**En resumen:** El espacio nulo izquierdo y el espacio columna son complementos ortogonales el uno del otro dentro de $\mathbb{R}^m$.
## Relación de Ortogonalidad de los Subespacios Fundamentales (Continuación y Resumen)

### Demostración de $Co(A)^\perp = N(A^t)$

Sabemos por la sección anterior, aplicando la relación entre el espacio nulo y el espacio fila a la matriz transpuesta $A^t$, que:
$N(A^t) = Fi(A^t)^\perp$

Ahora, recordemos que las filas de la matriz transpuesta $A^t$ son las columnas de la matriz original $A$. Por lo tanto, el espacio fila de $A^t$ es idéntico al espacio columna de $A$:
$Fi(A^t) = Co(A)$

Sustituyendo esta identidad en la primera ecuación, obtenemos directamente:
$N(A^t) = Co(A)^\perp$

Que es equivalente a:
$Co(A)^\perp = N(A^t)$

### Resumen de las Relaciones Fundamentales

Dada una matriz $A \in \mathbb{R}^{m \times n}$:

$$
A =
\begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn}
\end{pmatrix}
$$

Los cuatro subespacios fundamentales se agrupan y relacionan de la siguiente manera:

**Subespacios de $\mathbb{R}^n$:**

*   **Espacio Fila:** $Fi(A) = \langle F_1, \dots, F_m \rangle$
*   **Espacio Nulo:** $N(A) = \{\vec{x} \in \mathbb{R}^n \mid A\vec{x} = \vec{0}\}$

**Subespacios de $\mathbb{R}^m$:**

*   **Espacio Columna:** $Co(A) = \langle C_1, \dots, C_n \rangle$
*   **Espacio Nulo Izquierdo:** $N(A^t) = \{\vec{y} \in \mathbb{R}^m \mid A^t\vec{y} = \vec{0}\}$

**Relaciones de Ortogonalidad:**

1.  Dentro de $\mathbb{R}^n$: El espacio fila y el espacio nulo son complementos ortogonales.
    *   $Fi(A)^\perp = N(A)$
    *   $N(A)^\perp = Fi(A)$

2.  Dentro de $\mathbb{R}^m$: El espacio columna y el espacio nulo izquierdo son complementos ortogonales.
    *   $Co(A)^\perp = N(A^t)$
    *   $N(A^t)^\perp = Co(A)$

**Descomposición del Espacio (Suma Directa):**

Como estos pares de subespacios son complementos ortogonales, su intersección es solo el vector nulo y su suma genera todo el espacio correspondiente. Esto significa que forman una suma directa:

1.  $\mathbb{R}^n = Fi(A) \oplus N(A)$
    *   Cualquier vector en $\mathbb{R}^n$ se puede descomponer de forma única como la suma de un vector en el espacio fila y un vector en el espacio nulo.

2.  $\mathbb{R}^m = Co(A) \oplus N(A^t)$
    *   Cualquier vector en $\mathbb{R}^m$ se puede descomponer de forma única como la suma de un vector en el espacio columna y un vector en el espacio nulo izquierdo.