## Definición
Un **sistema de $n$ ecuaciones lineales con $m$ incógnitas** es un conjunto de $n$ ecuaciones lineales que deben satisfacerse simultáneamente. Su forma general es:

$$
\begin{cases}
a_{11}x_1 + a_{12}x_2 + \dots + a_{1m}x_m = b_1 \\
a_{21}x_1 + a_{22}x_2 + \dots + a_{2m}x_m = b_2 \\
\vdots \\
a_{n1}x_1 + a_{n2}x_2 + \dots + a_{nm}x_m = b_n
\end{cases}
$$

Donde:
*   $x_1, x_2, \dots, x_m$ son las **incógnitas** o variables.
*   $a_{ij}$ (con $1 \le i \le n$, $1 \le j \le m$) son los **coeficientes** del sistema (constantes conocidas). El subíndice $i$ indica la ecuación (fila) y $j$ indica la incógnita (columna) a la que multiplica.
*   $b_1, b_2, \dots, b_n$ son los **términos independientes** (constantes conocidas).
*   $n$ es el número de ecuaciones.
*   $m$ es el número de incógnitas.

Una **solución** del sistema es una $m$-tupla de valores $(s_1, s_2, \dots, s_m)$ que, al sustituir $x_1=s_1, \dots, x_m=s_m$, satisface **todas** las $n$ ecuaciones.

## Sistema Homogéneo
Un sistema de ecuaciones lineales se llama **homogéneo** si todos sus términos independientes son cero, es decir, $b_1 = b_2 = \dots = b_n = 0$.
$$
\begin{cases}
a_{11}x_1 + a_{12}x_2 + \dots + a_{1m}x_m = 0 \\
a_{21}x_1 + a_{22}x_2 + \dots + a_{2m}x_m = 0 \\
\vdots \\
a_{n1}x_1 + a_{n2}x_2 + \dots + a_{nm}x_m = 0
\end{cases}
$$
*   **Nota:** Todo sistema homogéneo admite siempre, al menos, la **solución trivial** $(x_1=0, x_2=0, \dots, x_m=0)$.

## Número de Soluciones de un Sistema de Ecuaciones Lineales

Al resolver un sistema de ecuaciones lineales, nos podemos encontrar con tres posibles escenarios respecto a la cantidad de soluciones que admite:

1.  **Sistema Compatible Determinado (SCD):**
    *   El sistema tiene **exactamente una única solución**.
    *   Existe un solo conjunto de valores para las incógnitas que satisface todas las ecuaciones simultáneamente.

2.  **Sistema Compatible Indeterminado (SCI):**
    *   El sistema tiene un **número infinito de soluciones**.
    *   Existe más de una solución, y de hecho, una infinidad de conjuntos de valores para las incógnitas que satisfacen todas las ecuaciones. A menudo, estas soluciones se pueden expresar en términos de una o más variables libres (parámetros).

3.  **Sistema Incompatible (SI):**
    *   El sistema **no tiene ninguna solución**.
    *   No existe ningún conjunto de valores para las incógnitas que pueda satisfacer todas las ecuaciones del sistema al mismo tiempo. Las ecuaciones presentan alguna contradicción entre sí.

**En resumen:** Un sistema de ecuaciones lineales solo puede tener:
*   **Una solución** (Compatible Determinado)
*   **Infinitas soluciones** (Compatible Indeterminado)
*   **Ninguna solución** (Incompatible)

No es posible, por ejemplo, que un sistema de ecuaciones *lineales* tenga exactamente dos o tres soluciones.
