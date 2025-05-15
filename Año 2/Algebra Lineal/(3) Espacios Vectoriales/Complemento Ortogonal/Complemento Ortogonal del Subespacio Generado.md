Consideremos $V$ un espacio vectorial y $S$ el subespacio generado por un conjunto de vectores $\{v_1, \dots, v_k\}$. Esto se escribe como:
$S = \langle v_1, \dots, v_k \rangle$

Un vector $v$ pertenece a $S$ si y solo si $v$ se puede expresar como una combinación lineal de los vectores generadores:
$v \in S \iff v = \alpha_1 v_1 + \dots + \alpha_k v_k$ para algunos escalares $\alpha_1, \dots, \alpha_k$.

Ahora, consideremos qué significa que un vector $w \in V$ pertenezca al complemento ortogonal $S^\perp$. Por definición:
$w \in S^\perp \iff w \cdot v = 0$ para todo $v \in S$.

Sustituyendo la expresión de $v$ como combinación lineal:
$w \in S^\perp \iff w \cdot (\alpha_1 v_1 + \dots + \alpha_k v_k) = 0$ para *cualquier* elección de escalares $\alpha_1, \dots, \alpha_k$.

Usando la propiedad de linealidad del producto escalar:
$w \cdot (\alpha_1 v_1 + \dots + \alpha_k v_k) = \alpha_1 (w \cdot v_1) + \dots + \alpha_k (w \cdot v_k)$

Entonces, la condición se convierte en:
$w \in S^\perp \iff \alpha_1 (w \cdot v_1) + \dots + \alpha_k (w \cdot v_k) = 0$ para *todos* los $\alpha_1, \dots, \alpha_k$.

Esta última condición nos lleva a un teorema fundamental.

### Teorema

Sea $V$ un espacio vectorial y $S = \langle v_1, \dots, v_k \rangle$. Las siguientes afirmaciones son equivalentes:

1.  $w \in S^\perp$ ( $w$ es ortogonal a *todo* vector en $S$)
2.  $w \cdot v_i = 0$ para todo $i$ desde $1$ hasta $k$ ( $w$ es ortogonal a *cada uno* de los vectores generadores de $S$)

**Explicación de la Equivalencia:**

*   **$(1 \implies 2)$:** Si $w \in S^\perp$, entonces $w$ es ortogonal a *todos* los vectores de $S$. Como cada vector generador $v_i$ pertenece a $S$ (tomando $\alpha_i=1$ y los demás $\alpha_j=0$), se sigue directamente que $w \cdot v_i = 0$ para cada $i$.
*   **$(2 \implies 1)$:** Si $w \cdot v_i = 0$ para todos los generadores $v_1, \dots, v_k$, entonces consideremos un vector genérico $v = \alpha_1 v_1 + \dots + \alpha_k v_k$ en $S$. Calculamos el producto escalar:
    $w \cdot v = w \cdot (\alpha_1 v_1 + \dots + \alpha_k v_k)$
    $w \cdot v = \alpha_1 (w \cdot v_1) + \dots + \alpha_k (w \cdot v_k)$
    Como por hipótesis cada término $w \cdot v_i = 0$, la suma completa es:
    $w \cdot v = \alpha_1 (0) + \dots + \alpha_k (0) = 0$
    Dado que esto se cumple para cualquier $v \in S$, concluimos que $w \in S^\perp$.

**En resumen:** Para verificar si un vector $w$ pertenece al complemento ortogonal de un subespacio $S$ generado por $\{v_1, \dots, v_k\}$, **basta con comprobar que $w$ es ortogonal a cada uno de los vectores generadores $v_i$**.