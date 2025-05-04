### *Indice*
- [[Base]] 
- [[Coordenadas]]
- [[Dimension de un Espacio Vectorial]]
- [[Matriz Cambio de Base]]

## Definicion

Un mismo espacio vectorial puede tener muchas bases diferentes. Por ejemplo, en $\mathbb{R}^2$, tanto $B_1 = \{(1, 0), (0, 1)\}$ (la base canónica) como $B_2 = \{(1, 1), (1, -1)\}$ son bases válidas.

El **cambio de base** es el proceso de encontrar las coordenadas de un vector respecto a una nueva base, conociendo sus coordenadas respecto a la base original.

Si tenemos un vector $v$ y conocemos sus coordenadas respecto a una base $B = \{v_1, \dots, v_n\}$, es decir, conocemos $[v]_B$, y queremos encontrar sus coordenadas respecto a otra base $B' = \{w_1, \dots, w_n\}$, es decir, $[v]_{B'}$, necesitamos una forma de "traducir" entre las bases.

Esto se logra mediante la **matriz de cambio de base** (o matriz de transición) de $B$ a $B'$. Si llamamos $P_{B' \leftarrow B}$ a esta matriz, la relación es:

$[v]_{B'} = P_{B' \leftarrow B} [v]_B$

La matriz $P_{B' \leftarrow B}$ se construye expresando cada vector de la base original $B$ como una combinación lineal de los vectores de la nueva base $B'$, y usando las coordenadas resultantes como columnas de la matriz.


### Algunas consideraciones

*   El vector de coordenadas en una base depende del orden de los vectores en dicha base. La base $\{(1, 0), (1, -1)\}$ es distinta a la base $\{(1, -1), (1, 0)\}$.
*   Considerando la base canónica $C$ en $\mathbb{R}^n$, para todo $v \in \mathbb{R}^n$ se tiene que $[v]_C = v^t$.
*   Si $v, w$ son vectores de $V$ y $k$ un escalar, entonces:
    *   $[v + w]_B = [v]_B + [w]_B$
    *   $[kv]_B = k[v]_B$