
La independencia lineal es el concepto opuesto a la dependencia lineal. Si la dependencia lineal significa que hay "redundancia" en un conjunto de vectores (al menos uno se puede escribir a partir de los otros), la independencia lineal significa que **no hay redundancia**; cada vector aporta información direccional única.

**Definición Formal:**

Un conjunto de vectores $\{\mathbf{v}_1, \mathbf{v}_2, \dots, \mathbf{v}_n\}$ en un espacio vectorial $V$ se dice que es **Linealmente Independiente (L.I.)** si **no** es Linealmente Dependiente (L.D.).

De forma más explícita y útil, esto significa que la **única** manera de que una combinación lineal de estos vectores sea igual al vector nulo es que **todos** los escalares sean cero. Formalmente:

Para todos los escalares $\alpha_1, \alpha_2, \dots, \alpha_n \in \mathbb{K}$ (usualmente $\mathbb{R}$), se cumple la siguiente implicación:
$$ \alpha_1 \mathbf{v}_1 + \alpha_2 \mathbf{v}_2 + \dots + \alpha_n \mathbf{v}_n = \mathbf{0} \quad \implies \quad \alpha_1 = \alpha_2 = \dots = \alpha_n = 0 $$

En palabras simples: la única forma de "combinar" vectores L.I. para obtener el vector cero es la **combinación lineal trivial** (todos los coeficientes cero). No existe ninguna combinación *no trivial* que dé como resultado el vector cero.


**Teorema (Equivalencia para L.I.)**

Al igual que con la dependencia lineal, existe una condición equivalente muy útil para entender la independencia lineal:

Dado un conjunto de vectores $\{\mathbf{v}_1, \dots, \mathbf{v}_n\}$, las siguientes afirmaciones son **equivalentes**:

1.  El conjunto $\{\mathbf{v}_1, \dots, \mathbf{v}_n\}$ es **Linealmente Independiente (L.I.)**.

2.  **Ningún vector** $\mathbf{v}_j$ del conjunto puede expresarse como una combinación lineal de los **otros** vectores del conjunto.
(Formalmente: para todo $j \in \{1, \dots, n\}$, se cumple que $\mathbf{v}_j \notin \langle \{\mathbf{v}_i : i \in \{1, \dots, n\} \setminus \{j\}\} \rangle$. El vector $\mathbf{v}_j$ *no* pertenece al subespacio generado por los demás vectores).

**¿Por qué son equivalentes?**
Esta equivalencia es la negación lógica directa de la equivalencia para L.D.
*   Ser L.D. $\iff$ Al menos un vector es CL de los otros.
*   Negando ambas partes: No ser L.D. (ser L.I.) $\iff$ Ningún vector es CL de los otros.

**En Resumen:**

Un conjunto de vectores es L.I. si cumple cualquiera de estas condiciones (que implican la otra):
*   La única combinación lineal que da el vector nulo es la trivial (todos los escalares cero).
*   Ningún vector del conjunto se puede "construir" a partir de los demás vectores del mismo conjunto.


## Ejemplo: ¿Cómo Saber si un Conjunto de Vectores es L.I.?

**Problema:** Determinar si el siguiente conjunto de vectores en $\mathbb{R}^3$ es Linealmente Independiente (L.I.):
$$ S = \{(1, 0, 1), (1, 1, 1), (0, 1, 1)\} $$
Llamemos $\mathbf{v}_1 = (1, 0, 1)$, $\mathbf{v}_2 = (1, 1, 1)$, $\mathbf{v}_3 = (0, 1, 1)$.

**Paso 1: Aplicar la Definición de L.I.**
Por definición, el conjunto $S$ es L.I. si la única forma de obtener el vector nulo como combinación lineal de sus vectores es usando exclusivamente escalares iguales a cero. Es decir, debemos verificar si la siguiente implicación es verdadera:
$$ \text{Si } \alpha_1 \mathbf{v}_1 + \alpha_2 \mathbf{v}_2 + \alpha_3 \mathbf{v}_3 = \mathbf{0}, \quad \text{ entonces necesariamente } \alpha_1 = 0, \alpha_2 = 0, \alpha_3 = 0 $$

**Paso 2: Plantear la Ecuación Vectorial (Suponer el Antecedente)**
Seguimos la lógica de la implicación: **suponemos** que la primera parte (el antecedente) es verdadera. Es decir, asumimos que *existe* una combinación lineal que da el vector nulo:
$$ \alpha_1 (1, 0, 1) + \alpha_2 (1, 1, 1) + \alpha_3 (0, 1, 1) = (0, 0, 0) $$

**Paso 3: Convertir a Sistema de Ecuaciones y Forma Matricial**
Esta ecuación vectorial se traduce en un sistema de ecuaciones lineales homogéneo, como vimos antes:
$$ \begin{cases} 1\alpha_1 + 1\alpha_2 + 0\alpha_3 = 0 \\ 0\alpha_1 + 1\alpha_2 + 1\alpha_3 = 0 \\ 1\alpha_1 + 1\alpha_2 + 1\alpha_3 = 0 \end{cases} $$
Y esto, a su vez, es equivalente a la ecuación matricial $A \boldsymbol{\alpha} = \mathbf{0}$:
$$ \begin{pmatrix} 1 & 1 & 0 \\ 0 & 1 & 1 \\ 1 & 1 & 1 \end{pmatrix} \begin{pmatrix} \alpha_1 \\ \alpha_2 \\ \alpha_3 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \\ 0 \end{pmatrix} $$
Donde $A = \begin{pmatrix} 1 & 1 & 0 \\ 0 & 1 & 1 \\ 1 & 1 & 1 \end{pmatrix}$ y $\boldsymbol{\alpha} = (\alpha_1, \alpha_2, \alpha_3)^T$.

**Paso 4: El Objetivo: Probar la Unicidad de la Solución Trivial**
Ahora, el objetivo es **demostrar** que la única solución posible para este sistema homogéneo (es decir, los únicos valores de $\alpha_1, \alpha_2, \alpha_3$ que satisfacen las ecuaciones) es la solución trivial $\alpha_1 = 0, \alpha_2 = 0, \alpha_3 = 0$.

Si logramos probar que la única solución es la trivial, entonces la implicación del Paso 1 será verdadera, y concluiremos que el conjunto $S$ es **Linealmente Independiente (L.I.)**.

Si, por el contrario, encontramos que existen otras soluciones además de la trivial (soluciones no triviales), entonces la implicación del Paso 1 sería falsa, y concluiríamos que el conjunto es Linealmente Dependiente (L.D.).

**Paso 5: Resolver el Sistema Homogéneo usando Eliminación Gaussiana**

Habíamos llegado al sistema $A \boldsymbol{\alpha} = \mathbf{0}$ con la matriz aumentada:
$$ \left(\begin{array}{ccc|c} 1 & 1 & 0 & 0 \\ 0 & 1 & 1 & 0 \\ 1 & 1 & 1 & 0 \end{array}\right) $$
Aplicamos eliminación gaussiana para llevarla a la forma escalonada:
1.  $R_3 \leftarrow R_3 - R_1$
$$ \left(\begin{array}{ccc|c} 1 & 1 & 0 & 0 \\ 0 & 1 & 1 & 0 \\ 0 & 0 & 1 & 0 \end{array}\right) $$
¡Ya está en forma escalonada (de hecho, es casi la forma escalonada reducida)!

**Paso 6: Interpretar la Forma Escalonada y Encontrar la Solución**

La matriz escalonada corresponde al siguiente sistema de ecuaciones:
$$ \begin{cases} 1\alpha_1 + 1\alpha_2 + 0\alpha_3 = 0 & \implies \alpha_1 + \alpha_2 = 0 \\ 0\alpha_1 + 1\alpha_2 + 1\alpha_3 = 0 & \implies \alpha_2 + \alpha_3 = 0 \\ 0\alpha_1 + 0\alpha_2 + 1\alpha_3 = 0 & \implies \alpha_3 = 0 \end{cases} $$

Ahora, podemos resolver este sistema fácilmente usando sustitución hacia atrás:
1.  De la tercera ecuación, obtenemos directamente:
$$ \alpha_3 = 0 $$
2.  Sustituimos $\alpha_3 = 0$ en la segunda ecuación:
$$ \alpha_2 + (0) = 0 \implies \alpha_2 = 0 $$
3.  Sustituimos $\alpha_2 = 0$ en la primera ecuación:
$$ \alpha_1 + (0) = 0 \implies \alpha_1 = 0 $$

**Paso 7: Conclusión Final**

Hemos partido de la suposición de que $\alpha_1 \mathbf{v}_1 + \alpha_2 \mathbf{v}_2 + \alpha_3 \mathbf{v}_3 = \mathbf{0}$. Al resolver el sistema de ecuaciones resultante, hemos encontrado que la **única solución posible** es $\alpha_1 = 0$, $\alpha_2 = 0$, y $\alpha_3 = 0$.

Esto confirma que la implicación que define la independencia lineal es verdadera:
$$ \alpha_1 \mathbf{v}_1 + \alpha_2 \mathbf{v}_2 + \alpha_3 \mathbf{v}_3 = \mathbf{0} \quad \implies \quad \alpha_1 = \alpha_2 = \alpha_3 = 0 $$

Por lo tanto, el conjunto de vectores $S = \{(1, 0, 1), (1, 1, 1), (0, 1, 1)\}$ es **Linealmente Independiente (L.I.)**.

**Observación Adicional (Rango y Determinante):**
*   La matriz escalonada tiene 3 filas no nulas. El rango de la matriz $A$ es $rg(A) = 3$.
*   El número de variables (escalares) también es $n=3$.
*   Como $rg(A) = n$, el sistema homogéneo $A \boldsymbol{\alpha} = \mathbf{0}$ tiene una única solución, que es la trivial. Esto confirma que los vectores son L.I.
*   Alternativamente, podríamos calcular el determinante de la matriz original $A$:
$$ \det(A) = \begin{vmatrix} 1 & 1 & 0 \\ 0 & 1 & 1 \\ 1 & 1 & 1 \end{vmatrix} = 1(1-1) - 1(0-1) + 0(0-1) = 0 + 1 + 0 = 1 $$
Como $\det(A) = 1 \neq 0$, esto también confirma que la única solución del sistema homogéneo es la trivial y, por lo tanto, los vectores columna son **Linealmente Independientes (L.I.)**.


