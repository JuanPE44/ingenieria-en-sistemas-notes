
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

## Forma Escalonada (o Escalonada por Filas)

Una matriz $A$ está en **forma escalonada** si cumple las siguientes condiciones:

1.  **Filas de Ceros:** Todas las filas que consisten enteramente de ceros (si las hay) se encuentran en la parte inferior de la matriz.
2.  **Posición de Pivotes:** Por cada fila no nula, el pivote se encuentra en una columna a la **derecha** de la columna del pivote de la fila superior.
3.  **Ceros Debajo de Pivotes:** Todos los elementos en una columna que están **debajo** de un pivote son cero.

*(El primer ejemplo anterior SÍ está en forma escalonada. El segundo NO lo está porque el pivote de la fila 2 no está a la derecha del pivote de la fila 1, y hay un elemento no nulo debajo del pivote de la fila 1)*.

## Forma Escalonada Reducida (o Escalonada Reducida por Filas - RREF)

Una matriz $A$ está en **forma escalonada reducida** si cumple las condiciones de la forma escalonada y **además**:

4.  **Pivotes Iguales a 1:** Todos los pivotes son iguales a 1.
5.  **Ceros Encima de Pivotes:** Todos los elementos en una columna que están **encima** de un pivote también son cero. (Es decir, un pivote es el único elemento no nulo en su columna).

**Ejemplo de Forma Escalonada Reducida:**
$$
\begin{pmatrix}
\boxed{1} & 0 & -5 & 0 \\
0 & \boxed{1} & 2 & 0 \\
0 & 0 & 0 & \boxed{1} \\
0 & 0 & 0 & 0
\end{pmatrix}
$$