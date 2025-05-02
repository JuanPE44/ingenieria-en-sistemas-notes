---
sticker: lucide//air-vent
---
Consideremos el sistema lineal en su forma matricial $A\vec{x} = \vec{b}$.

## Interpretación Clave
Podemos interpretar esta ecuación desde la perspectiva de los vectores columna de la matriz $A$. Si $A = [\vec{a}_1 | \vec{a}_2 | \dots | \vec{a}_m]$, donde $\vec{a}_j$ es la $j$-ésima columna de $A$, y $\vec{x} = (x_1, x_2, \dots, x_m)^T$, entonces el producto $A\vec{x}$ es equivalente a la combinación lineal de las columnas de $A$ con los elementos de $\vec{x}$ como coeficientes:
$$ A\vec{x} = x_1 \vec{a}_1 + x_2 \vec{a}_2 + \dots + x_m \vec{a}_m $$

## Ecuación Vectorial Equivalente
Por lo tanto, el sistema $A\vec{x} = \vec{b}$ es equivalente a la ecuación vectorial:
$$ x_1 \vec{a}_1 + x_2 \vec{a}_2 + \dots + x_m \vec{a}_m = \vec{b} $$

## Significado
*   **Resolver el sistema $A\vec{x} = \vec{b}$ es equivalente a determinar si el vector $\vec{b}$ puede expresarse como una combinación lineal de los vectores columna de $A$.**
*   **Existencia de Solución:** El sistema tiene solución si y sólo si $\vec{b}$ pertenece al **espacio generado** (span) por las columnas de $A$: $\vec{b} \in \langle \vec{a}_1, \vec{a}_2, \dots, \vec{a}_m \rangle$.
*   **Encontrar una Solución:** Si existe, una solución $(x_1, x_2, \dots, x_m)$ proporciona los **coeficientes** específicos de la combinación lineal de las columnas de $A$ que igualan a $\vec{b}$.

## Ejemplo
Afirmar que $\begin{pmatrix} 2 \\ -1 \\ 3 \end{pmatrix}$ es combinación lineal de $\begin{pmatrix} -2 \\ 1 \\ -1 \end{pmatrix}$, $\begin{pmatrix} 1 \\ 3 \\ 2 \end{pmatrix}$, $\begin{pmatrix} 4 \\ -2 \\ -3 \end{pmatrix}$ es lo mismo que decir que el sistema:
$$ \begin{pmatrix} -2 & 1 & 4 \\ 1 & 3 & -2 \\ -1 & 2 & -3 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \\ x_3 \end{pmatrix} = \begin{pmatrix} 2 \\ -1 \\ 3 \end{pmatrix} $$
tiene (al menos) una solución.