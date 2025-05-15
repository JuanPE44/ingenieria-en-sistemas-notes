Consideremos una matriz $A$ de tamaño $m \times n$ ( $A \in \mathbb{R}^{m \times n}$ ) y un vector columna $\vec{x}$ de tamaño $n \times 1$ ( $\vec{x} \in \mathbb{R}^n$ ). El producto matriz-vector $A\vec{x}$ resulta en un vector columna de tamaño $m \times 1$.

El sistema de ecuaciones lineales homogéneo se representa como:
$A\vec{x} = \vec{0}$

Donde $\vec{0}$ es el vector nulo de tamaño $m \times 1$. Explícitamente:

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

### Definición del Espacio Nulo

El **Espacio Nulo** (o Núcleo) de la matriz $A$, denotado como $N(A)$, es el conjunto de **todas** las soluciones $\vec{x}$ del sistema homogéneo $A\vec{x} = \vec{0}$.

Formalmente:
$N(A) = \{\vec{x} \in \mathbb{R}^n \mid A\vec{x} = \vec{0}\}$

**Propiedad Fundamental:** El conjunto $N(A)$ es un **subespacio vectorial** del espacio $\mathbb{R}^n$ (el espacio donde viven los vectores $\vec{x}$).

**Nota sobre Notación:**
Aunque en la ecuación $A\vec{x} = \vec{0}$ el vector $\vec{x}$ es un vector columna, es común que al describir los vectores que pertenecen al espacio nulo $N(A)$, estos se escriban como vectores fila (por ejemplo, $(x_1, x_2, \dots, x_n)$) por conveniencia. Sin embargo, conceptualmente siguen siendo las soluciones del sistema con vectores columna.

## Interpretación Geométrica de los Espacios Nulos en $\mathbb{R}^3$

Consideremos un sistema homogéneo de ecuaciones lineales donde las incógnitas son $x, y, z$. Esto corresponde a buscar el espacio nulo $N(A)$ de una matriz $A$ donde los vectores solución $\vec{x} = (x, y, z)$ pertenecen a $\mathbb{R}^3$.

El sistema general tiene la forma:
$A\vec{x} = \vec{0}$

Por ejemplo, para una matriz $A \in \mathbb{R}^{3 \times 3}$:
$$
\begin{cases}
a_{11}x + a_{12}y + a_{13}z = 0 \\
a_{21}x + a_{22}y + a_{23}z = 0 \\
a_{31}x + a_{32}y + a_{33}z = 0
\end{cases}
$$

Sabemos que el espacio nulo $N(A) = \{\vec{x} \in \mathbb{R}^3 \mid A\vec{x} = \vec{0}\}$ es siempre un **subespacio vectorial** de $\mathbb{R}^3$. Los subespacios vectoriales de $\mathbb{R}^3$ tienen interpretaciones geométricas específicas:

1.  **Dimensión 0: El Origen**
    *   $N(A) = \{(0, 0, 0)\}$
    *   Esto ocurre cuando la única solución al sistema homogéneo es la solución trivial $\vec{x} = \vec{0}$. Geométricamente, este subespacio es simplemente el punto origen.

2.  **Dimensión 1: Una Recta que pasa por el Origen**
    *   $N(A) = \langle (x_1, y_1, z_1) \rangle$ (donde $(x_1, y_1, z_1) \neq (0, 0, 0)$)
    *   Esto ocurre cuando todas las soluciones son múltiplos escalares de un único vector no nulo $(x_1, y_1, z_1)$.
    *   Geométricamente, este subespacio es una recta que pasa por el origen y tiene la dirección del vector $(x_1, y_1, z_1)$.

3.  **Dimensión 2: Un Plano que pasa por el Origen**
    *   $N(A) = \langle (x_1, y_1, z_1), (x_2, y_2, z_2) \rangle$ (donde los dos vectores generadores son linealmente independientes).
    *   Esto ocurre cuando las soluciones se pueden expresar como combinaciones lineales de dos vectores linealmente independientes.
    *   Geométricamente, este subespacio es un plano que contiene al origen y está generado (spanned) por los vectores $(x_1, y_1, z_1)$ y $(x_2, y_2, z_2)$.

4.  **Dimensión 3: Todo el Espacio $\mathbb{R}^3$**
    *   $N(A) = \mathbb{R}^3$
    *   Esto ocurre únicamente cuando la matriz $A$ es la matriz nula (todos sus coeficientes son cero). En este caso, cualquier vector $(x, y, z)$ es solución del sistema $A\vec{x} = \vec{0}$.

En resumen, el espacio nulo $N(A)$ de una matriz $A$ con columnas correspondientes a $x, y, z$ siempre será uno de los siguientes objetos geométricos en $\mathbb{R}^3$: el origen, una recta que pasa por el origen, un plano que pasa por el origen, o todo el espacio $\mathbb{R}^3$.