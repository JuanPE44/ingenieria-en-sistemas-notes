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