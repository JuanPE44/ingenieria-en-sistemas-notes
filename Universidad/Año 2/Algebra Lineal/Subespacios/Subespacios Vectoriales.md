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

**En resumen:** Un subespacio vectorial es una "parte" de un espacio vectorial que conserva la estructura de espacio vectorial en sí misma. Debe contener al vector cero y ser cerrada bajo las operaciones básicas de suma de vectores y multiplicación por un escalar (o equivalentemente, cerrada bajo combinaciones lineales).