Sea $V$ un espacio vectorial. Un subconjunto $S \subseteq V$ es un **subespacio vectorial** si cumple las siguientes condiciones:

1.  El vector nulo pertenece a S: $\vec{0} \in S$.
2.  Cerradura bajo la suma: Si $u, v \in S$, entonces la suma $u + v$ también pertenece a $S$ ($u + v \in S$).
3.  Cerradura bajo la multiplicación por escalar: Si $u \in S$ y $\lambda$ es un escalar cualquiera, entonces el producto $\lambda u$ también pertenece a $S$ ($\lambda u \in S$).

## Lema (Condición Equivalente)

Sea $V$ un espacio vectorial y $S \subseteq V$ un subconjunto. Las siguientes afirmaciones son equivalentes:

1.  $S$ es un subespacio de $V$.
2.  Para cada par de vectores $u, v \in S$ y cada par de escalares $\alpha, \beta$, la combinación lineal $\alpha u + \beta v$ también pertenece a $S$ ($\alpha u + \beta v \in S$).

En otras palabras, los subespacios vectoriales son aquellos subconjuntos que son **cerrados bajo combinaciones lineales**.

## Ejemplos (Subespacios Triviales)

Sea $V$ un espacio vectorial cualquiera. Siempre existen al menos dos subespacios, llamados **subespacios triviales**:

*   El subespacio más pequeño posible: el conjunto que contiene únicamente al vector nulo, $\{\vec{0}\}$.
*   El subespacio más grande posible: el propio espacio vectorial completo, $V$.


## Ejemplo: Determinación de Subespacios Vectoriales en R³

## Introducción

Para que un subconjunto $S$ de un espacio vectorial $V$ (en este caso, $\mathbb{R}^3$) sea considerado un **subespacio vectorial**, debe cumplir tres condiciones fundamentales:

1.  **Contener el vector nulo:** El vector $\vec{0}$ del espacio vectorial $V$ debe pertenecer a $S$. Para $\mathbb{R}^3$, el vector nulo es $(0, 0, 0)$.
2.  **Cerrado bajo la suma:** Si $\vec{u} \in S$ y $\vec{v} \in S$, entonces la suma $\vec{u} + \vec{v}$ también debe pertenecer a $S$.
3.  **Cerrado bajo la multiplicación por escalar:** Si $\vec{u} \in S$ y $\lambda$ es un escalar (en este caso, un número real $\lambda \in \mathbb{R}$), entonces el producto $\lambda \vec{u}$ también debe pertenecer a $S$.

Si **alguna** de estas condiciones no se cumple, el subconjunto $S$ **no** es un subespacio vectorial.

## Caso 1: $S = \{(x, y, z) \in \mathbb{R}^3 : 3x + 4y + z = 2\}$

Vamos a verificar si este conjunto $S$ es un subespacio vectorial de $\mathbb{R}^3$.

**Condición 1: Contener el vector nulo $(0, 0, 0)$**

Para que el vector nulo $(0, 0, 0)$ pertenezca a $S$, debe satisfacer la ecuación que define al conjunto: $3x + 4y + z = 2$.
Sustituimos $x=0$, $y=0$, $z=0$:
$3 \cdot 0 + 4 \cdot 0 + 1 \cdot 0 = 0 + 0 + 0 = 0$

El resultado es $0$, pero la condición para pertenecer a $S$ es que la suma sea igual a $2$. Como $0 \neq 2$, el vector nulo $(0, 0, 0)$ **no pertenece** a $S$.

**Conclusión del Caso 1:**
Dado que $S$ no cumple la primera condición (no contiene al vector nulo), podemos concluir inmediatamente que **$S$ no es un subespacio vectorial** de $\mathbb{R}^3$. No es necesario verificar las otras dos condiciones.

## Caso 2: $S' = \{(x, y, z) \in \mathbb{R}^3 : 3x + 4y + z = 0\}$

Ahora, analicemos este segundo conjunto $S'$, definido por una ecuación homogénea (igualada a cero).

**Condición 1 (S1): Contener el vector nulo $(0, 0, 0)$**

Verificamos si $(0, 0, 0)$ satisface la ecuación $3x + 4y + z = 0$:
$3 \cdot 0 + 4 \cdot 0 + 1 \cdot 0 = 0 + 0 + 0 = 0$
Como el resultado es $0$, que es lo requerido por la ecuación, el vector nulo $(0, 0, 0)$ **sí pertenece** a $S'$.

**Condición 2 (S2): Cerrado bajo la suma**

Tomemos dos vectores genéricos que pertenezcan a $S'$:
*   $\vec{u} = (x_1, y_1, z_1) \in S'$. Esto significa que $3x_1 + 4y_1 + z_1 = 0$.
*   $\vec{v} = (x_2, y_2, z_2) \in S'$. Esto significa que $3x_2 + 4y_2 + z_2 = 0$.

Ahora, veamos si su suma $\vec{u} + \vec{v} = (x_1 + x_2, y_1 + y_2, z_1 + z_2)$ pertenece a $S'$. Para ello, debemos verificar si cumple la ecuación $3x + 4y + z = 0$:
$3(x_1 + x_2) + 4(y_1 + y_2) + (z_1 + z_2)$
$= 3x_1 + 3x_2 + 4y_1 + 4y_2 + z_1 + z_2$
Reagrupamos los términos:
$= (3x_1 + 4y_1 + z_1) + (3x_2 + 4y_2 + z_2)$
Sabemos que el primer paréntesis es $0$ (porque $\vec{u} \in S'$) y el segundo paréntesis también es $0$ (porque $\vec{v} \in S'$).
$= 0 + 0 = 0$
Como el resultado es $0$, la suma $\vec{u} + \vec{v}$ **sí pertenece** a $S'$. Por lo tanto, $S'$ es cerrado bajo la suma.

**Condición 3 (S3): Cerrado bajo la multiplicación por escalar**

Tomemos un vector genérico $\vec{u} = (x, y, z) \in S'$ (lo que significa $3x + 4y + z = 0$) y un escalar cualquiera $\lambda \in \mathbb{R}$.
Veamos si el vector $\lambda \vec{u} = (\lambda x, \lambda y, \lambda z)$ pertenece a $S'$. Verificamos si cumple la ecuación $3x + 4y + z = 0$:
$3(\lambda x) + 4(\lambda y) + (\lambda z)$
$= \lambda (3x + 4y + z)$
Sabemos que $(3x + 4y + z) = 0$ porque $\vec{u} \in S'$.
$= \lambda \cdot 0 = 0$
Como el resultado es $0$, el vector $\lambda \vec{u}$ **sí pertenece** a $S'$. Por lo tanto, $S'$ es cerrado bajo la multiplicación por escalar.

**Conclusión del Caso 2:**
Dado que $S'$ cumple las tres condiciones (contiene el vector nulo, es cerrado bajo la suma y es cerrado bajo la multiplicación por escalar), podemos concluir que **$S'$ sí es un subespacio vectorial** de $\mathbb{R}^3$.

**Nota importante:** Geométricamente, la ecuación $3x + 4y + z = 0$ representa un plano que pasa por el origen en $\mathbb{R}^3$. Todos los planos que pasan por el origen son subespacios vectoriales de $\mathbb{R}^3$. La ecuación $3x + 4y + z = 2$ representa un plano que *no* pasa por el origen, y por eso no es un subespacio vectorial (ya que no contiene al vector $(0,0,0)$).


## Subespacios Vectoriales en $\mathbb{R}^2$ y $\mathbb{R}^3$

Recordemos que un subespacio vectorial es un subconjunto de un espacio vectorial que, a su vez, es un espacio vectorial con las mismas operaciones. Esto implica que debe contener al vector nulo, ser cerrado bajo la suma de vectores y cerrado bajo la multiplicación por escalar.

Geométricamente, los subespacios vectoriales en $\mathbb{R}^2$ y $\mathbb{R}^3$ tienen formas muy específicas: siempre deben pasar por el origen.

## Subespacios de $\mathbb{R}^2$

En el plano $\mathbb{R}^2$, los únicos tipos de subconjuntos que cumplen las condiciones de subespacio vectorial son:

1.  **Subespacios Triviales:**
    *   **El conjunto que contiene únicamente al vector nulo:** $S = \{\vec{0}\} = \{(0, 0)\}$. Este es el subespacio más pequeño posible. Siempre es un subespacio en cualquier espacio vectorial. Geométricamente, representa el origen.
    *   **Todo el espacio $\mathbb{R}^2$:** $S = \mathbb{R}^2$. El espacio vectorial completo siempre es un subespacio de sí mismo.

2.  **Rectas que pasan por el origen:**
    *   Cualquier recta en $\mathbb{R}^2$ que pase por el punto $(0, 0)$ es un subespacio vectorial.
    *   **Forma:** Una recta que pasa por el origen puede describirse como el conjunto de todos los múltiplos escalares de un vector director no nulo $\vec{v} = (a, b)$. Es decir, $S = \{ \lambda \vec{v} \mid \lambda \in \mathbb{R} \} = \{ (\lambda a, \lambda b) \mid \lambda \in \mathbb{R} \}$.
    *   **¿Por qué es un subespacio?**
        *   **Contiene al origen:** Si $\lambda = 0$, obtenemos $(0 \cdot a, 0 \cdot b) = (0, 0)$.
        *   **Cerrado bajo la suma:** Si $\vec{u}_1 = \lambda_1 \vec{v} \in S$ y $\vec{u}_2 = \lambda_2 \vec{v} \in S$, entonces $\vec{u}_1 + \vec{u}_2 = \lambda_1 \vec{v} + \lambda_2 \vec{v} = (\lambda_1 + \lambda_2) \vec{v}$. Como $(\lambda_1 + \lambda_2)$ es un escalar, la suma pertenece a $S$.
        *   **Cerrado bajo multiplicación por escalar:** Si $\vec{u} = \lambda_1 \vec{v} \in S$ y $c \in \mathbb{R}$, entonces $c \vec{u} = c (\lambda_1 \vec{v}) = (c \lambda_1) \vec{v}$. Como $(c \lambda_1)$ es un escalar, el resultado pertenece a $S$.
    *   **Nota:** Una recta que *no* pasa por el origen *no* es un subespacio vectorial porque no contiene al vector nulo $(0, 0)$.

## Subespacios de $\mathbb{R}^3$

En el espacio tridimensional $\mathbb{R}^3$, los tipos de subespacios vectoriales son:

1.  **Subespacios Triviales:**
    *   **El conjunto que contiene únicamente al vector nulo:** $S = \{\vec{0}\} = \{(0, 0, 0)\}$. Representa el origen.
    *   **Todo el espacio $\mathbb{R}^3$:** $S = \mathbb{R}^3$.

2.  **Rectas que pasan por el origen:**
    *   Cualquier recta en $\mathbb{R}^3$ que pase por el punto $(0, 0, 0)$ es un subespacio vectorial.
    *   **Forma:** Similar a $\mathbb{R}^2$, se describen como $S = \{ \lambda \vec{v} \mid \lambda \in \mathbb{R} \}$, donde $\vec{v} = (a, b, c)$ es un vector director no nulo en $\mathbb{R}^3$.
    *   La justificación de por qué son subespacios es idéntica a la de las rectas en $\mathbb{R}^2$.

3.  **Planos que pasan por el origen:**
    *   Cualquier plano en $\mathbb{R}^3$ que contenga al punto $(0, 0, 0)$ es un subespacio vectorial.
    *   **Forma:** Un plano que pasa por el origen puede describirse de varias maneras:
        *   Como el conjunto de todas las combinaciones lineales de dos vectores directores linealmente independientes $\vec{u}$ y $\vec{v}$ que pertenecen al plano: $S = \{ \alpha \vec{u} + \beta \vec{v} \mid \alpha, \beta \in \mathbb{R} \}$.
        *   Mediante una ecuación implícita de la forma $ax + by + cz = 0$ (donde $a, b, c$ no son todos cero). El término independiente es cero, lo que garantiza que el plano pasa por el origen $(0, 0, 0)$.
    *   **¿Por qué es un subespacio (usando la ecuación implícita)?**
        *   **Contiene al origen:** $a(0) + b(0) + c(0) = 0$, se cumple la ecuación.
        *   **Cerrado bajo la suma:** Si $\vec{x}_1 = (x_1, y_1, z_1)$ cumple $ax_1 + by_1 + cz_1 = 0$ y $\vec{x}_2 = (x_2, y_2, z_2)$ cumple $ax_2 + by_2 + cz_2 = 0$, entonces para la suma $\vec{x}_1 + \vec{x}_2 = (x_1+x_2, y_1+y_2, z_1+z_2)$:
            $a(x_1+x_2) + b(y_1+y_2) + c(z_1+z_2) = (ax_1 + by_1 + cz_1) + (ax_2 + by_2 + cz_2) = 0 + 0 = 0$. La suma pertenece al plano.
        *   **Cerrado bajo multiplicación por escalar:** Si $\vec{x} = (x, y, z)$ cumple $ax + by + cz = 0$ y $\lambda \in \mathbb{R}$, entonces para $\lambda \vec{x} = (\lambda x, \lambda y, \lambda z)$:
            $a(\lambda x) + b(\lambda y) + c(\lambda z) = \lambda (ax + by + cz) = \lambda (0) = 0$. El múltiplo escalar pertenece al plano.
    *   **Nota:** Un plano que *no* pasa por el origen (ecuación $ax + by + cz = d$ con $d \neq 0$) *no* es un subespacio vectorial porque no contiene al vector nulo $(0, 0, 0)$.

En resumen, los subespacios vectoriales de $\mathbb{R}^2$ y $\mathbb{R}^3$ son siempre el origen, rectas que pasan por el origen, planos que pasan por el origen (solo en $\mathbb{R}^3$), o el espacio completo.