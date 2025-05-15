Un teorema importante derivado de la definición de base es:

**Teorema:** Si $B = \{v_1, v_2, \dots, v_n\}$ es una base para un espacio vectorial $V$, entonces cada vector $v \in V$ se puede escribir de **una y sólo una forma** como combinación lineal de los vectores de $B$.

$v = c_1 v_1 + c_2 v_2 + \dots + c_n v_n$

Los escalares $(c_1, c_2, \dots, c_n)$ son únicos para cada vector $v$ y se llaman las **coordenadas** del vector $v$ respecto a la base $B$. Se suelen representar como un vector columna:
$[v]_B = \begin{pmatrix} c_1 \\ c_2 \\ \vdots \\ c_n \end{pmatrix}$

### Coordenadas de un vector en la base canónica

Cuando trabajamos con la **base canónica** $C$ en $\mathbb{R}^n$, nos referimos a la base formada por los vectores que tienen un 1 en una posición y 0 en todas las demás:

$C = \{ e_1, e_2, e_3, \dots, e_n \}$

donde:
*   $e_1 = (1, 0, 0, \dots, 0)$
*   $e_2 = (0, 1, 0, \dots, 0)$
*   $e_3 = (0, 0, 1, \dots, 0)$
*   $\vdots$
*   $e_n = (0, 0, 0, \dots, 1)$

Para cualquier vector $v = (v_1, v_2, \dots, v_n) \in \mathbb{R}^n$, podemos expresarlo como una combinación lineal de los vectores de la base canónica de la siguiente manera:

$v = (v_1, v_2, \dots, v_n) = v_1 e_1 + v_2 e_2 + v_3 e_3 + \dots + v_n e_n$

**Vector de Coordenadas en la Base Canónica**

Las coordenadas del vector $v$ respecto a la base canónica $C$, denotadas como $[v]_C$, son precisamente las componentes del vector $v$ escritas como un vector columna:

$[v]_C = \begin{pmatrix} v_1 \\ v_2 \\ \vdots \\ v_n \end{pmatrix} = v^t$

**Importancia y Simplicidad**

La base canónica es fundamental porque simplifica muchos cálculos. Las coordenadas de un vector en esta base son directamente sus componentes. Por esta razón, a menudo se trabaja implícitamente con la base canónica sin mencionarla explícitamente.

**Ejemplo en $\mathbb{R}^3$**

Si $v = (3, -1, 4) \in \mathbb{R}^3$, la base canónica es $C = \{ (1, 0, 0), (0, 1, 0), (0, 0, 1) \}$.
Entonces:
$v = 3(1, 0, 0) + (-1)(0, 1, 0) + 4(0, 0, 1)$
Y el vector de coordenadas de $v$ en la base canónica es:
$[v]_C = \begin{pmatrix} 3 \\ -1 \\ 4 \end{pmatrix}$
