Sea $V$ un espacio vectorial (como $\mathbb{R}^n$, por ejemplo) y sea $S = \{\vec{v}_1, \vec{v}_2, \dots, \vec{v}_k\}$ un conjunto finito de vectores pertenecientes a $V$.

Se define el **subespacio generado por el conjunto $S$**, denotado como $\langle \vec{v}_1, \vec{v}_2, \dots, \vec{v}_k \rangle$ o también como $gen(S)$ o $span(S)$, como el conjunto de **todas las posibles combinaciones lineales** que se pueden formar utilizando los vectores de $S$.

Formalmente:

$\langle \vec{v}_1, \dots, \vec{v}_k \rangle = \{ \lambda_1 \vec{v}_1 + \lambda_2 \vec{v}_2 + \dots + \lambda_k \vec{v}_k \mid \lambda_1, \lambda_2, \dots, \lambda_k \in \mathbb{R} \}$

Donde $\lambda_1, \lambda_2, \dots, \lambda_k$ son escalares cualesquiera (números reales en este caso).

## Terminología

*   **Conjunto de Generadores:** El conjunto original de vectores $\{\vec{v}_1, \dots, \vec{v}_k\}$ se denomina **conjunto de generadores** del subespacio $\langle \vec{v}_1, \dots, \vec{v}_k \rangle$. Esto significa que cualquier vector dentro de este subespacio puede ser "construido" o "generado" a partir de una combinación lineal de estos vectores generadores.

*   **Combinaciones Lineales:** La expresión $\lambda_1 \vec{v}_1 + \lambda_2 \vec{v}_2 + \dots + \lambda_k \vec{v}_k$ es una **combinación lineal** de los vectores $\vec{v}_1, \dots, \vec{v}_k$. El subespacio generado es, por definición, el conjunto que abarca *todas* estas combinaciones lineales posibles.

## Propiedad Fundamental

El conjunto $\langle \vec{v}_1, \dots, \vec{v}_k \rangle$ **siempre es un subespacio vectorial** del espacio vectorial original $V$. Se puede demostrar que cumple las tres condiciones:

1.  **Contiene al vector nulo:** Tomando todos los escalares $\lambda_i = 0$, la combinación lineal resulta $0\vec{v}_1 + \dots + 0\vec{v}_k = \vec{0}$. Por lo tanto, $\vec{0} \in \langle \vec{v}_1, \dots, \vec{v}_k \rangle$.
2.  **Cerrado bajo la suma:** Si $\vec{u} = \sum \alpha_i \vec{v}_i$ y $\vec{w} = \sum \beta_i \vec{v}_i$ son dos vectores en el subespacio generado, su suma $\vec{u} + \vec{w} = \sum (\alpha_i + \beta_i) \vec{v}_i$ también es una combinación lineal de los $\vec{v}_i$, por lo que pertenece al subespacio generado.
3.  **Cerrado bajo multiplicación por escalar:** Si $\vec{u} = \sum \alpha_i \vec{v}_i$ está en el subespacio generado y $c$ es un escalar, entonces $c\vec{u} = \sum (c\alpha_i) \vec{v}_i$ sigue siendo una combinación lineal de los $\vec{v}_i$, por lo que pertenece al subespacio generado.

De hecho, el subespacio generado $\langle \vec{v}_1, \dots, \vec{v}_k \rangle$ es el **subespacio vectorial más pequeño** de $V$ que contiene a todos los vectores del conjunto $\{\vec{v}_1, \dots, \vec{v}_k\}$.

## Ejemplos Geométricos

*   **En $\mathbb{R}^2$ o $\mathbb{R}^3$:** Si tomamos un solo vector no nulo $\vec{v}_1 \neq \vec{0}$, el subespacio generado $\langle \vec{v}_1 \rangle = \{ \lambda_1 \vec{v}_1 \mid \lambda_1 \in \mathbb{R} \}$ es la **recta** que pasa por el origen y tiene a $\vec{v}_1$ como vector director.
*   **En $\mathbb{R}^3$:** Si tomamos dos vectores linealmente independientes $\vec{v}_1, \vec{v}_2$, el subespacio generado $\langle \vec{v}_1, \vec{v}_2 \rangle = \{ \lambda_1 \vec{v}_1 + \lambda_2 \vec{v}_2 \mid \lambda_1, \lambda_2 \in \mathbb{R} \}$ es el **plano** que pasa por el origen y contiene a los vectores $\vec{v}_1$ y $\vec{v}_2$.
*   **En $\mathbb{R}^n$:** Si los vectores $\{\vec{v}_1, \dots, \vec{v}_k\}$ generan todo el espacio $\mathbb{R}^n$, entonces $\langle \vec{v}_1, \dots, \vec{v}_k \rangle = \mathbb{R}^n$.