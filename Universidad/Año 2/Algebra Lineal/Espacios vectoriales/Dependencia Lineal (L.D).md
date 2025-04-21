
**Idea Intuitiva:** Un conjunto de vectores es linealmente dependiente si existe cierta "redundancia" entre ellos. Es decir, si al menos uno de los vectores puede ser expresado como una combinación lineal de los otros. Esto significa que ese vector no aporta "información direccional" nueva que no estuviera ya contenida en los demás.

**Definición Formal:**
Sea $V$ un espacio vectorial sobre un cuerpo $\mathbb{K}$ (por ejemplo, $\mathbb{R}$).
Un conjunto finito de vectores $\{\mathbf{v}_1, \mathbf{v}_2, \dots, \mathbf{v}_n\}$ en $V$ se dice que es **Linealmente Dependiente (L.D.)** si existen escalares $\alpha_1, \alpha_2, \dots, \alpha_n \in \mathbb{K}$, **no todos iguales a cero**, tales que su combinación lineal es igual al vector nulo:

$$ \alpha_1 \mathbf{v}_1 + \alpha_2 \mathbf{v}_2 + \dots + \alpha_n \mathbf{v}_n = \mathbf{0} $$

**Puntos Clave de la Definición:**

1.  **Combinación Lineal Nula:** Buscamos una forma de "combinar" los vectores (sumándolos después de multiplicarlos por escalares) para obtener el vector cero.
2.  **Escalares No Todos Nulos:** ¡Esta es la parte crucial! Siempre podemos obtener el vector cero si usamos *todos* los escalares iguales a cero (la llamada **combinación lineal trivial**: $0\mathbf{v}_1 + \dots + 0\mathbf{v}_n = \mathbf{0}$). La dependencia lineal requiere que encontremos una combinación lineal que dé cero **sin** que todos los escalares sean cero (una **combinación lineal no trivial**).

**¿Qué significa si son L.D.?**
Si $\alpha_1 \mathbf{v}_1 + \dots + \alpha_n \mathbf{v}_n = \mathbf{0}$ y al menos un escalar, digamos $\alpha_i$, es distinto de cero, entonces podemos despejar $\mathbf{v}_i$:
$$ \alpha_i \mathbf{v}_i = -\alpha_1 \mathbf{v}_1 - \dots - \alpha_{i-1} \mathbf{v}_{i-1} - \alpha_{i+1} \mathbf{v}_{i+1} - \dots - \alpha_n \mathbf{v}_n $$
Y como $\alpha_i \neq 0$, podemos dividir por él:
$$ \mathbf{v}_i = \left(-\frac{\alpha_1}{\alpha_i}\right)\mathbf{v}_1 + \dots + \left(-\frac{\alpha_{n}}{\alpha_i}\right)\mathbf{v}_n $$
Esto demuestra que $\mathbf{v}_i$ es una combinación lineal de los otros vectores del conjunto.

---

### Ejemplo 1

Considera el conjunto de vectores en $\mathbb{R}^3$: $S = \{(1, 0, 0), (0, 1, 0), (1, 1, 0)\}$.
Llamemos $\mathbf{v}_1 = (1, 0, 0)$, $\mathbf{v}_2 = (0, 1, 0)$, $\mathbf{v}_3 = (1, 1, 0)$.

**¿Por qué es L.D.?**
Necesitamos encontrar escalares $\alpha_1, \alpha_2, \alpha_3$, no todos cero, tales que:
$$ \alpha_1 (1, 0, 0) + \alpha_2 (0, 1, 0) + \alpha_3 (1, 1, 0) = (0, 0, 0) $$
Esto se traduce en el sistema de ecuaciones:
$$ (\alpha_1 + \alpha_3, \alpha_2 + \alpha_3, 0) = (0, 0, 0) $$
$$ \begin{cases} \alpha_1 + \alpha_3 = 0 \\ \alpha_2 + \alpha_3 = 0 \\ 0 = 0 \end{cases} $$
De la primera ecuación, $\alpha_1 = -\alpha_3$. De la segunda, $\alpha_2 = -\alpha_3$.
Podemos elegir un valor no nulo para $\alpha_3$. Por ejemplo, si $\alpha_3 = 1$, entonces $\alpha_1 = -1$ y $\alpha_2 = -1$.
Los escalares son $\alpha_1 = -1, \alpha_2 = -1, \alpha_3 = 1$. **No son todos cero**.
Verifiquemos la combinación:
$$ (-1)(1, 0, 0) + (-1)(0, 1, 0) + (1)(1, 1, 0) = (-1, 0, 0) + (0, -1, 0) + (1, 1, 0) = (-1+0+1, 0-1+1, 0+0+0) = (0, 0, 0) $$
Como encontramos escalares no todos nulos que hacen la combinación lineal igual a cero, el conjunto $S$ es **Linealmente Dependiente**.

*Observación:* También podemos ver directamente que $\mathbf{v}_3 = \mathbf{v}_1 + \mathbf{v}_2$, lo que implica $1\mathbf{v}_1 + 1\mathbf{v}_2 - 1\mathbf{v}_3 = \mathbf{0}$. Los escalares son $1, 1, -1$, no todos nulos.

---

### Ejemplo 2

Considera el conjunto de vectores en $\mathbb{R}^3$: $S = \{(1, 2, 1), (1, 0, -1), (1, 4, 3)\}$.
Llamemos $\mathbf{v}_1 = (1, 2, 1)$, $\mathbf{v}_2 = (1, 0, -1)$, $\mathbf{v}_3 = (1, 4, 3)$.

El texto ya nos da la respuesta: el conjunto es L.D. porque se encontró la siguiente combinación lineal no trivial que da el vector nulo:
$$ (-2)(1, 2, 1) + (1)(1, 0, -1) + (1)(1, 4, 3) = (-2, -4, -2) + (1, 0, -1) + (1, 4, 3) = (-2+1+1, -4+0+4, -2-1+3) = (0, 0, 0) $$
Los escalares son $\alpha_1 = -2, \alpha_2 = 1, \alpha_3 = 1$. Como **no son todos cero**, el conjunto es **Linealmente Dependiente**.

**Conexión con Sistemas de Ecuaciones Homogéneos:**

Buscar los escalares $\alpha_1, \alpha_2, \alpha_3$ tales que $\alpha_1 \mathbf{v}_1 + \alpha_2 \mathbf{v}_2 + \alpha_3 \mathbf{v}_3 = \mathbf{0}$ es equivalente a resolver el sistema de ecuaciones lineales homogéneo $A\mathbf{x} = \mathbf{0}$, donde las columnas de la matriz $A$ son los vectores $\mathbf{v}_1, \mathbf{v}_2, \mathbf{v}_3$ y $\mathbf{x} = (\alpha_1, \alpha_2, \alpha_3)^T$:

$$ \begin{pmatrix} 1 & 1 & 1 \\ 2 & 0 & 4 \\ 1 & -1 & 3 \end{pmatrix} \begin{pmatrix} \alpha_1 \\ \alpha_2 \\ \alpha_3 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \\ 0 \end{pmatrix} $$

Un conjunto de vectores es **Linealmente Dependiente** si y solo si el sistema homogéneo $A\mathbf{x} = \mathbf{0}$ tiene **soluciones no triviales** (es decir, soluciones donde $\mathbf{x} \neq \mathbf{0}$).

En este ejemplo, la solución $\mathbf{x} = (-2, 1, 1)^T$ es una solución no trivial, lo que confirma que los vectores columna (y por tanto el conjunto $S$) son linealmente dependientes.

---

**En Resumen:**

*   **L.D.:** Existe una combinación lineal *no trivial* (al menos un escalar no es cero) que da el vector nulo. Implica redundancia. Al menos un vector es combinación lineal de los otros. El sistema $A\mathbf{x}=\mathbf{0}$ tiene soluciones no triviales.
*   **L.I. (Linealmente Independiente):** La *única* forma de obtener el vector nulo como combinación lineal es usando *todos* los escalares iguales a cero (la solución trivial). No hay redundancia. Ningún vector es combinación lineal de los otros. El sistema $A\mathbf{x}=\mathbf{0}$ solo tiene la solución trivial $\mathbf{x}=\mathbf{0}$.


## Dependencia Lineal: Una Equivalencia Fundamental

Hemos visto que un conjunto de vectores $\{\mathbf{v}_1, \dots, \mathbf{v}_n\}$ es Linealmente Dependiente (L.D.) si existe una combinación lineal *no trivial* (con escalares no todos cero) que resulta en el vector nulo. Existe una forma alternativa y equivalente de entender la dependencia lineal:

**Definición (Equivalencia):**
Dado un conjunto de vectores $\{\mathbf{v}_1, \dots, \mathbf{v}_n\}$ en un espacio vectorial $V$, las siguientes dos afirmaciones son **equivalentes** (si una es verdadera, la otra también lo es, y viceversa):

1.  El conjunto $\{\mathbf{v}_1, \dots, \mathbf{v}_n\}$ es **Linealmente Dependiente (L.D.)**.
(Es decir, existen escalares $\alpha_1, \dots, \alpha_n$, no todos nulos, tales que $\alpha_1 \mathbf{v}_1 + \dots + \alpha_n \mathbf{v}_n = \mathbf{0}$).

2.  **Existe al menos un vector** $\mathbf{v}_j$ en el conjunto que **es combinación lineal (CL) de los *otros* vectores** del conjunto.
(Es decir, existe algún $j \in \{1, \dots, n\}$ tal que $\mathbf{v}_j \in \langle \{\mathbf{v}_i : i \in \{1, \dots, n\} \setminus \{j\}\} \rangle$, lo que se escribe como $\mathbf{v}_j = \sum_{i \neq j} \beta_i \mathbf{v}_i$ para algunos escalares $\beta_i$).

**¿Por qué son equivalentes?**

*   **(1 ⇒ 2):** Si el conjunto es L.D., sabemos que $\alpha_1 \mathbf{v}_1 + \dots + \alpha_n \mathbf{v}_n = \mathbf{0}$ con al menos un $\alpha_j \neq 0$. Podemos despejar ese $\mathbf{v}_j$:
$$ \alpha_j \mathbf{v}_j = - \sum_{i \neq j} \alpha_i \mathbf{v}_i $$
Como $\alpha_j \neq 0$, dividimos por $\alpha_j$:
$$ \mathbf{v}_j = \sum_{i \neq j} \left(-\frac{\alpha_i}{\alpha_j}\right) \mathbf{v}_i $$
Esto muestra que $\mathbf{v}_j$ es una combinación lineal de los otros vectores.

*   **(2 ⇒ 1):** Si existe un $\mathbf{v}_j$ que es combinación lineal de los otros, $\mathbf{v}_j = \sum_{i \neq j} \beta_i \mathbf{v}_i$. Podemos reordenar esto para obtener el vector nulo:
$$ \sum_{i \neq j} \beta_i \mathbf{v}_i - 1 \cdot \mathbf{v}_j = \mathbf{0} $$
Esta es una combinación lineal de *todos* los vectores $\{\mathbf{v}_1, \dots, \mathbf{v}_n\}$ igualada a cero. El escalar que multiplica a $\mathbf{v}_j$ es $-1$, que es distinto de cero. Por lo tanto, hemos encontrado una combinación lineal no trivial que da el vector nulo, lo que significa que el conjunto es L.D.

**En resumen:** Un conjunto es L.D. si y solo si hay "redundancia", es decir, al menos un vector puede ser "construido" a partir de los demás.

---

### Análisis del Ejemplo

Consideremos el conjunto $S = \{(1, 0, 1), (2, 0, 2)\}$ en $\mathbb{R}^3$.
Llamemos $\mathbf{v}_1 = (1, 0, 1)$ y $\mathbf{v}_2 = (2, 0, 2)$.

*   **Verificación (1): ¿Es L.D. según la primera definición?**
Sí, porque como muestra el texto, podemos encontrar escalares no todos nulos (específicamente $2$ y $-1$) tales que la combinación lineal es cero:
$$ 2(1, 0, 1) + (-1)(2, 0, 2) = (2, 0, 2) + (-2, 0, -2) = (0, 0, 0) $$
Como $2 \neq 0$ (y también $-1 \neq 0$), el conjunto es L.D.

*   **Verificación (2): ¿Se cumple la segunda definición?**
Sí. De la ecuación $2\mathbf{v}_1 - \mathbf{v}_2 = \mathbf{0}$, podemos despejar:
*   $\mathbf{v}_2 = 2\mathbf{v}_1$. Esto muestra que $\mathbf{v}_2$ es combinación lineal de $\{\mathbf{v}_1\}$. Es decir, $\mathbf{v}_2 \in \langle \mathbf{v}_1 \rangle$.
*   También podríamos despejar $\mathbf{v}_1 = \frac{1}{2}\mathbf{v}_2$. Esto muestra que $\mathbf{v}_1$ es combinación lineal de $\{\mathbf{v}_2\}$. Es decir, $\mathbf{v}_1 \in \langle \mathbf{v}_2 \rangle$.
En ambos casos, encontramos un vector que es CL del otro (o de los otros, si hubiera más).

*   **Interpretación del Span:**
El texto dice $S = \langle (1, 0, 1), (2, 0, 2) \rangle = \langle (1, 0, 1) \rangle$. Esto es correcto porque $\mathbf{v}_2$ es simplemente un múltiplo de $\mathbf{v}_1$ ($\mathbf{v}_2 = 2\mathbf{v}_1$). Añadir $\mathbf{v}_2$ al conjunto generador no aporta ninguna dirección nueva que no estuviera ya dada por $\mathbf{v}_1$. Cualquier combinación lineal de $\mathbf{v}_1$ y $\mathbf{v}_2$, como $a\mathbf{v}_1 + b\mathbf{v}_2$, se puede reescribir usando solo $\mathbf{v}_1$: $a\mathbf{v}_1 + b(2\mathbf{v}_1) = (a+2b)\mathbf{v}_1$, que sigue siendo solo un múltiplo de $\mathbf{v}_1$.
Por lo tanto, el subespacio generado por ambos vectores es el mismo que el generado solo por $\mathbf{v}_1$, que es la recta en $\mathbb{R}^3$ que pasa por el origen y tiene como vector director a $(1, 0, 1)$.

---

### ¿Cómo Saber si un Conjunto Dado es L.D.?

La forma más sistemática es usar la primera definición y convertir el problema en resolver un sistema de ecuaciones lineales homogéneo:

1.  **Plantea la Ecuación:** Escribe la combinación lineal genérica igualada al vector nulo:
$$ \alpha_1 \mathbf{v}_1 + \alpha_2 \mathbf{v}_2 + \dots + \alpha_n \mathbf{v}_n = \mathbf{0} $$
2.  **Forma el Sistema:** Si los vectores $\mathbf{v}_i$ están en $\mathbb{R}^m$, esta ecuación vectorial se convierte en un sistema de $m$ ecuaciones lineales con $n$ incógnitas ($\alpha_1, \dots, \alpha_n$). Este sistema siempre será **homogéneo** (los términos constantes son cero).
$$ A \boldsymbol{\alpha} = \mathbf{0} $$
donde $A$ es la matriz cuyas columnas son los vectores $\mathbf{v}_1, \dots, \mathbf{v}_n$, y $\boldsymbol{\alpha} = (\alpha_1, \dots, \alpha_n)^T$.
3.  **Resuelve el Sistema:** Utiliza métodos como la eliminación gaussiana para encontrar las soluciones del sistema.
4.  **Analiza la Solución:**
*   Si la **única solución** es la **trivial** ($\alpha_1 = 0, \alpha_2 = 0, \dots, \alpha_n = 0$), entonces el conjunto $\{\mathbf{v}_1, \dots, \mathbf{v}_n\}$ es **Linealmente Independiente (L.I.)**.
*   Si existen **soluciones no triviales** (al menos un $\alpha_i \neq 0$), entonces el conjunto $\{\mathbf{v}_1, \dots, \mathbf{v}_n\}$ es **Linealmente Dependiente (L.D.)**.

**Atajo (para $n$ vectores en $\mathbb{R}^n$):** Si tienes exactamente $n$ vectores en $\mathbb{R}^n$, puedes formar una matriz cuadrada $A$ con esos vectores como columnas (o filas). El conjunto es L.D. si y solo si $\det(A) = 0$. Si $\det(A) \neq 0$, el conjunto es L.I.

## Ejemplo: Determinar si un Conjunto es L.D.

**Problema:** Determinar si el siguiente conjunto de vectores en $\mathbb{R}^3$ es Linealmente Dependiente (L.D.):
$$ S = \{(1, 1, 1), (-1, 0, 1), (2, 1, 0)\} $$
Llamemos $\mathbf{v}_1 = (1, 1, 1)$, $\mathbf{v}_2 = (-1, 0, 1)$, $\mathbf{v}_3 = (2, 1, 0)$.

**Paso 1: Aplicar la Definición de L.D.**
Por definición, el conjunto $S$ es L.D. si existen escalares $\alpha_1, \alpha_2, \alpha_3$, **no todos iguales a cero**, tales que:
$$ \alpha_1 \mathbf{v}_1 + \alpha_2 \mathbf{v}_2 + \alpha_3 \mathbf{v}_3 = \mathbf{0} $$
Sustituyendo los vectores:
$$ \alpha_1 (1, 1, 1) + \alpha_2 (-1, 0, 1) + \alpha_3 (2, 1, 0) = (0, 0, 0) $$

**Paso 2: Convertir la Ecuación Vectorial en un Sistema de Ecuaciones Lineales**
Realizando las operaciones vectoriales (producto por escalar y suma) en el lado izquierdo, obtenemos:
$$ (\alpha_1 - \alpha_2 + 2\alpha_3, \quad \alpha_1 + 0\alpha_2 + \alpha_3, \quad \alpha_1 + \alpha_2 + 0\alpha_3) = (0, 0, 0) $$
Igualando componente a componente, obtenemos el siguiente sistema de ecuaciones lineales homogéneo:
$$ \begin{cases} 1\alpha_1 - 1\alpha_2 + 2\alpha_3 = 0 \\ 1\alpha_1 + 0\alpha_2 + 1\alpha_3 = 0 \\ 1\alpha_1 + 1\alpha_2 + 0\alpha_3 = 0 \end{cases} $$

**Paso 3: Representar el Sistema en Forma Matricial**
Este sistema es equivalente a la ecuación matricial $A \boldsymbol{\alpha} = \mathbf{0}$, donde $A$ es la matriz cuyas columnas son los vectores $\mathbf{v}_1, \mathbf{v}_2, \mathbf{v}_3$, y $\boldsymbol{\alpha} = (\alpha_1, \alpha_2, \alpha_3)^T$:
$$ \begin{pmatrix} 1 & -1 & 2 \\ 1 & 0 & 1 \\ 1 & 1 & 0 \end{pmatrix} \begin{pmatrix} \alpha_1 \\ \alpha_2 \\ \alpha_3 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \\ 0 \end{pmatrix} $$

**Paso 4: Analizar la Existencia de Soluciones No Triviales**
La pregunta ahora es: ¿Tiene este sistema homogéneo soluciones **distintas de la trivial** ($\alpha_1=0, \alpha_2=0, \alpha_3=0$)? Si la respuesta es sí, los vectores son L.D. Si la única solución es la trivial, son Linealmente Independientes (L.I.).

**Paso 5: Usar Eliminación Gaussiana**
Para determinar si existen soluciones no triviales, aplicamos eliminación gaussiana a la matriz aumentada del sistema $[A | \mathbf{0}]$:
$$ \left(\begin{array}{ccc|c} 1 & -1 & 2 & 0 \\ 1 & 0 & 1 & 0 \\ 1 & 1 & 0 & 0 \end{array}\right) $$
Aplicamos operaciones de fila para obtener la forma escalonada:
1.  $R_2 \leftarrow R_2 - R_1$
2.  $R_3 \leftarrow R_3 - R_1$
$$ \left(\begin{array}{ccc|c} 1 & -1 & 2 & 0 \\ 0 & 1 & -1 & 0 \\ 0 & 2 & -2 & 0 \end{array}\right) $$
3.  $R_3 \leftarrow R_3 - 2R_2$
$$ \left(\begin{array}{ccc|c} 1 & -1 & 2 & 0 \\ 0 & 1 & -1 & 0 \\ 0 & 0 & 0 & 0 \end{array}\right) $$
Esta es la forma escalonada (REF).

**Paso 6: Interpretar la Forma Escalonada**
*   **Rango:** El número de filas no nulas en la REF de la matriz de coeficientes $A$ es 2. Por lo tanto, el rango de $A$, $rg(A) = 2$. El rango de la matriz aumentada $[A|\mathbf{0}]$ también es 2.
*   **Número de Variables:** Tenemos 3 variables ($\alpha_1, \alpha_2, \alpha_3$).
*   **Teorema de Rouché-Frobenius:** Para un sistema homogéneo $A\boldsymbol{\alpha} = \mathbf{0}$, si el rango de la matriz $A$ es *menor* que el número de variables ($rg(A) < n$), entonces el sistema tiene **infinitas soluciones** (es decir, existen soluciones no triviales).
*   **Conclusión:** En nuestro caso, $rg(A) = 2$ y el número de variables es $n=3$. Como $2 < 3$, el sistema tiene infinitas soluciones. Esto significa que existen escalares $\alpha_1, \alpha_2, \alpha_3$, no todos cero, que satisfacen la ecuación original.

**Resultado Final:**
Dado que el sistema homogéneo asociado tiene soluciones no triviales, el conjunto de vectores $S = \{(1, 1, 1), (-1, 0, 1), (2, 1, 0)\}$ es **Linealmente Dependiente (L.D.)**.


**Análisis de la Nota sobre los Pivotes:**

La forma escalonada es:
$$ \left(\begin{array}{ccc|c} \boxed{1} & -1 & 2 & 0 \\ 0 & \boxed{1} & -1 & 0 \\ 0 & 0 & 0 & 0 \end{array}\right) $$
Los pivotes (los primeros elementos no nulos de las filas no nulas) están en las columnas 1 y 2. La columna 3 no tiene pivote.

*   **Columnas Pivote (1 y 2):** Corresponden a los vectores $\mathbf{v}_1 = (1, 1, 1)$ y $\mathbf{v}_2 = (-1, 0, 1)$.
*   **Columna No Pivote (3):** Corresponde al vector $\mathbf{v}_3 = (2, 1, 0)$.

La teoría nos dice que los vectores correspondientes a las **columnas sin pivote** pueden expresarse como combinación lineal de los vectores correspondientes a las **columnas con pivote** que están a su izquierda.

En este caso, $\mathbf{v}_3$ (columna 3, sin pivote) debe ser combinación lineal de $\mathbf{v}_1$ y $\mathbf{v}_2$ (columnas 1 y 2, con pivotes).

Para encontrar esa combinación, resolvemos el sistema a partir de la REF:
$$ \begin{cases} \alpha_1 - \alpha_2 + 2\alpha_3 = 0 \\ \alpha_2 - \alpha_3 = 0 \end{cases} $$
La variable asociada a la columna sin pivote ($\alpha_3$) es la variable libre. Sea $\alpha_3 = t$.
De la segunda ecuación: $\alpha_2 = \alpha_3 = t$.
De la primera ecuación: $\alpha_1 = \alpha_2 - 2\alpha_3 = t - 2t = -t$.
La solución general es $(-t, t, t)$. Si tomamos $t=1$, una solución no trivial es $(-1, 1, 1)$.
Esto significa:
$$ (-1)\mathbf{v}_1 + (1)\mathbf{v}_2 + (1)\mathbf{v}_3 = \mathbf{0} $$
Reordenando para expresar $\mathbf{v}_3$ (el vector de la columna sin pivote) en términos de $\mathbf{v}_1$ y $\mathbf{v}_2$ (los vectores de las columnas con pivote):
$$ \mathbf{v}_3 = 1\mathbf{v}_1 - 1\mathbf{v}_2 $$
$$ (2, 1, 0) = 1(1, 1, 1) - 1(-1, 0, 1) = (1, 1, 1) - (-1, 0, 1) = (2, 1, 0) $$
¡Funciona!

La nota "Los pivotes me indican los vectores que NO son L.D" es una forma un poco imprecisa de decirlo. Es más exacto decir que los vectores correspondientes a las **columnas con pivote** forman un conjunto **linealmente independiente** que genera el mismo subespacio que el conjunto original. Los vectores de las **columnas sin pivote** son los que causan la dependencia lineal, ya que pueden escribirse como combinación lineal de los vectores "pivote" anteriores.