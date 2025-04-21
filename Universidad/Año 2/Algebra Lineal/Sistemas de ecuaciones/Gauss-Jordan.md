
## La Idea Central
El objetivo es transformar un sistema de ecuaciones lineales original, $A\vec{x} = \vec{b}$, en un **sistema equivalente**, $E\vec{x} = \vec{d}$, que tenga **exactamente las mismas soluciones** que el original, pero que sea mucho más **sencillo de resolver** (idealmente, donde la solución sea evidente).

## El Método: Trabajar con la Matriz Ampliada
En lugar de manipular directamente las ecuaciones (lo cual puede ser tedioso), se trabaja con la **matriz ampliada** $(A|\vec{b})$ asociada al sistema. Se aplican operaciones específicas a las filas de esta matriz para simplificarla y obtener una nueva matriz ampliada $(E|\vec{d})$ que representa el sistema simplificado.

$$ (A | \vec{b}) \xrightarrow{\text{Operaciones Elementales por Filas}} (E | \vec{d}) $$

## Operaciones Elementales por Filas
Las operaciones que se pueden realizar sobre las filas de la matriz ampliada (y que garantizan que el sistema resultante sea equivalente al original) son:

| Operación sobre las Ecuaciones del Sistema | Operación Equivalente sobre las Filas de $(A|\vec{b})$ |
| :----------------------------------------- | :----------------------------------------------------- |
| 1. Intercambiar dos ecuaciones             | 1. Intercambiar dos filas ($F_i \leftrightarrow F_j$)  |
| 2. Multiplicar una ecuación por $c \neq 0$ | 2. Multiplicar una fila por $c \neq 0$ ($F_i \to cF_i$)  |
| 3. Sumar un múltiplo de una ecuación a otra | 3. Sumar un múltiplo de una fila a otra fila ($F_i \to F_i + kF_j$) |

**Ejemplo (Sistema 3x3):**
El sistema:
$$
\begin{cases}
a_{11}x + a_{12}y + a_{13}z = b_1 \\
a_{21}x + a_{22}y + a_{23}z = b_2 \\
a_{31}x + a_{32}y + a_{33}z = b_3
\end{cases}
$$
Se representa por la matriz ampliada:
$$ (A | \vec{b}) = \begin{pmatrix} a_{11} & a_{12} & a_{13} & | & b_1 \\ a_{21} & a_{22} & a_{23} & | & b_2 \\ a_{31} & a_{32} & a_{33} & | & b_3 \end{pmatrix} $$
Aplicar las operaciones elementales por filas a esta matriz permite simplificar el sistema hasta encontrar su solución o determinar su naturaleza (compatible determinado, indeterminado o incompatible). Este es el fundamento del método de **Eliminación Gaussiana** y **Gauss-Jordan**.