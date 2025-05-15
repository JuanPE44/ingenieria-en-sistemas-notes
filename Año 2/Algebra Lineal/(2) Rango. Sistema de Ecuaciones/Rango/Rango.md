Dada una matriz $A \in \mathbb{R}^{m \times n}$, sus filas pueden considerarse como vectores en $\mathbb{R}^n$ y sus columnas como vectores en $\mathbb{R}^m$.

### Definición

**Teorema:** Para cualquier matriz A, el [[Rango por Filas]] es igual al [[Rango por Columnas]]. Este valor común se denomina simplemente el **rango** de A, y se denota como $Rg(A)$.
$$Rg(A) = Rg_f(A) = Rg_c(A)$$

*Nota: El rango también representa la dimensión del espacio vectorial generado por las filas (espacio fila) y la dimensión del espacio vectorial generado por las columnas (espacio columna).*

### Ejemplo

Sea la matriz:
$$ A = \begin{pmatrix} 2 & -1 & 1 \\ 1 & 0 & 1 \\ 2 & -1 & 4 \end{pmatrix} $$

Para calcular el rango, escalonamos la matriz mediante operaciones elementales por filas:

1.  $F_2 \leftarrow F_2 - \frac{1}{2}F_1$
2.  $F_3 \leftarrow F_3 - F_1$

$$
\begin{pmatrix} 2 & -1 & 1 \\ 1 & 0 & 1 \\ 2 & -1 & 4 \end{pmatrix}
\xrightarrow{F_2 \leftarrow F_2 - \frac{1}{2}F_1}
\begin{pmatrix} 2 & -1 & 1 \\ 0 & \frac{1}{2} & \frac{1}{2} \\ 2 & -1 & 4 \end{pmatrix}
\xrightarrow{F_3 \leftarrow F_3 - F_1}
\begin{pmatrix} 2 & -1 & 1 \\ 0 & \frac{1}{2} & \frac{1}{2} \\ 0 & 0 & 3 \end{pmatrix}
$$

La matriz escalonada resultante tiene 3 filas no nulas. Por lo tanto, el rango de A es 3.

$$ Rg(A) = 3 $$
