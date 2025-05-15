Dada una matriz $A$ de tamaño $m \times n$ ( $A \in \mathbb{R}^{m \times n}$ ), podemos identificar sus vectores fila y sus vectores columna:

$$
A =
\begin{array}{c}
\vec{f}_1 \rightarrow \\
\vec{f}_2 \rightarrow \\
\vdots \\
\vec{f}_m \rightarrow
\end{array}
\begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn}
\end{pmatrix}
\\
\begin{array}{cccc}
\uparrow & \uparrow & & \uparrow \\
\vec{c}_1 & \vec{c}_2 & \cdots & \vec{c}_n
\end{array}
$$

Donde:
*   $\vec{f}_i = (a_{i1}, a_{i2}, \dots, a_{in})$ es el $i$-ésimo vector fila (pertenece a $\mathbb{R}^n$).
*   $\vec{c}_j = \begin{pmatrix} a_{1j} \\ a_{2j} \\ \vdots \\ a_{mj} \end{pmatrix}$ es el $j$-ésimo vector columna (pertenece a $\mathbb{R}^m$).

### Definiciones

1.  **Espacio Columna (Co(A))**
    *   El **espacio columna** de $A$, denotado como $Co(A)$, es el **subespacio vectorial de $\mathbb{R}^m$** generado por los vectores columna de $A$.
    *   $Co(A) = \langle \vec{c}_1, \vec{c}_2, \dots, \vec{c}_n \rangle$
    *   Este espacio contiene todas las posibles combinaciones lineales de las columnas de $A$.

2.  **Espacio Fila (Fi(A) o R(A))**
    *   El **espacio fila** de $A$, denotado como $Fi(A)$ o $R(A)$ (del inglés *Row Space*), es el **subespacio vectorial de $\mathbb{R}^n$** generado por los vectores fila de $A$.
    *   $Fi(A) = R(A) = \langle \vec{f}_1, \vec{f}_2, \dots, \vec{f}_m \rangle$
    *   Este espacio contiene todas las posibles combinaciones lineales de las filas de $A$.