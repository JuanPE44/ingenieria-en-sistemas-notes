El proceso de escalonamiento transforma una matriz en una forma más simple (forma escalonada o escalonada reducida) mediante operaciones elementales por filas, lo cual es fundamental para resolver sistemas de ecuaciones lineales, calcular rangos, determinantes e inversas.

## Pivote

*   **Definición:** Un **pivote** de una fila en una matriz es el **primer elemento distinto de cero** (leyendo de izquierda a derecha) en esa fila.
*   Si una fila está compuesta enteramente por ceros, no tiene pivote.

**Ejemplos de Pivotes (marcados con \boxed{}):**

1.  $$
    \begin{pmatrix}
    \boxed{2} & 0 & -1 & 3 \\
    0 & 0 & \boxed{-3} & 5 \\
    0 & 0 & 0 & \boxed{6}
    \end{pmatrix}
    $$
    *   Fila 1: Pivote es 2 (en columna 1).
    *   Fila 2: Pivote es -3 (en columna 3).
    *   Fila 3: Pivote es 6 (en columna 4).

2.  $$
    \begin{pmatrix}
    \boxed{-3} & 0 & 0 & 4 & -7 & 1 \\
    \boxed{8} & -2 & 6 & 0 & 0 & -4 \\
    0 & 0 & \boxed{3} & -2 & 1 & 6 \\
    0 & 0 & 0 & 0 & \boxed{-2} & 3
    \end{pmatrix}
    $$
    *   Fila 1: Pivote es -3 (en columna 1).
    *   Fila 2: Pivote es 8 (en columna 1). *(Nota: Esta matriz NO está escalonada aún)*.
    *   Fila 3: Pivote es 3 (en columna 3).
    *   Fila 4: Pivote es -2 (en columna 5).


## [[Forma Escalonada]]
## [[Forma Escalonada Reducida]]
