## La Equivalencia Fundamental para Matrices Cuadradas

Tenemos una propiedad muy importante que aplica **específicamente a matrices cuadradas** $A$ de tamaño $n \times n$ (con componentes en los números reales, $A \in \mathbb{R}^{n \times n}$). Esta propiedad establece que las siguientes dos condiciones son **equivalentes**:

1.  **El determinante de la matriz A es distinto de cero:**
$\det(A) \neq 0$

2.  **El sistema de ecuaciones lineales homogéneo $A\vec{x} = \vec{0}$ tiene una única solución, y esa solución es el vector nulo:**
$\vec{x} = \vec{0}$ (donde $\vec{0}$ es el vector con todas sus componentes iguales a cero).

*   **"Equivalentes"** significa que si una de las condiciones se cumple, la otra automáticamente también se cumple. Y si una es falsa, la otra también lo es.
*   Si $\det(A) \neq 0$, entonces *sabemos* que la única solución de $A\vec{x} = \vec{0}$ es $\vec{x} = \vec{0}$.
*   Si sabemos que la única solución de $A\vec{x} = \vec{0}$ es $\vec{x} = \vec{0}$, entonces *sabemos* que $\det(A) \neq 0$.
*   Del mismo modo, si $\det(A) = 0$, entonces el sistema $A\vec{x} = \vec{0}$ tendrá *infinitas* soluciones (además de la trivial $\vec{x} = \vec{0}$).

## ¿Para Qué Sirve Saber Esto?

La utilidad principal que se menciona aquí es que esta equivalencia nos da una **herramienta práctica para analizar la independencia lineal** de un conjunto de vectores.

La idea es que la definición de independencia lineal está directamente relacionada con si un sistema homogéneo específico tiene solo la solución trivial. Como ahora sabemos que esto está ligado al valor del determinante (para matrices cuadradas), podremos **usar el cálculo del determinante** para concluir si un conjunto de vectores es linealmente independiente o no.

En resumen: El determinante se convierte en un test para la independencia lineal cuando trabajamos con $n$ vectores en $\mathbb{R}^n$.

## Ejemplos de Aplicación

Veamos cómo se utiliza esta herramienta en la práctica.

### Ejemplo 1: Vectores Linealmente Independientes (L.I.)

**Problema:** Determinar si el conjunto de vectores $S = \{(1, 0, 1), (0, 1, 1), (-1, 1, -1)\}$ en $\mathbb{R}^3$ es L.I.

**Paso 1: Plantear la ecuación de dependencia lineal.**
Buscamos si la única solución de la ecuación:
$\alpha_1(1, 0, 1) + \alpha_2(0, 1, 1) + \alpha_3(-1, 1, -1) = (0, 0, 0)$
es la trivial: $\alpha_1 = 0, \alpha_2 = 0, \alpha_3 = 0$.

**Paso 2: Formar el sistema homogéneo.**
Esta ecuación vectorial es equivalente al sistema $A\vec{\alpha} = \vec{0}$, donde $A$ es la matriz con los vectores como columnas:
$$
A = \begin{pmatrix}
1 & 0 & -1 \\
0 & 1 & 1 \\
1 & 1 & -1
\end{pmatrix}
$$
El sistema es:
$$
\begin{pmatrix}
1 & 0 & -1 \\
0 & 1 & 1 \\
1 & 1 & -1
\end{pmatrix}
\begin{pmatrix}
\alpha_1 \\
\alpha_2 \\
\alpha_3
\end{pmatrix} =
\begin{pmatrix}
0 \\
0 \\
0
\end{pmatrix}
$$
Necesitamos saber si este sistema tiene **única solución** (la trivial).

**Paso 3: Calcular el determinante de A.**
Como tenemos 3 vectores en $\mathbb{R}^3$, la matriz $A$ es cuadrada (3x3). Podemos usar el determinante:
$$
\det(A) = \left| \begin{matrix}
1 & 0 & -1 \\
0 & 1 & 1 \\
1 & 1 & -1
\end{matrix} \right| = 1(1(-1)-1(1)) - 0(...) + (-1)(0(1)-1(1)) = 1(-2) - 1(-1) = -2 + 1 = -1
$$

**Paso 4: Concluir.**
Dado que $\det(A) = -1 \neq 0$, por la equivalencia que vimos, el sistema homogéneo $A\vec{\alpha} = \vec{0}$ tiene **única solución**, que es $\vec{\alpha} = (0, 0, 0)$.
Por lo tanto, el conjunto de vectores $\{(1, 0, 1), (0, 1, 1), (-1, 1, -1)\}$ es **linealmente independiente (L.I.)**.

---

### Ejemplo 2: Vectores Linealmente Dependientes (L.D.)

**Problema:** Determinar si los vectores $\{(1, 0, 1), (1, 1, 1), (-1, -1, -1)\}$ son L.I o L.D.

**Paso 1: Plantear el sistema homogéneo.**
Formamos la matriz $A$ con los vectores como columnas y consideramos el sistema $A\vec{\alpha} = \vec{0}$:
$$
A = \begin{pmatrix}
1 & 1 & -1 \\
0 & 1 & -1 \\
1 & 1 & -1
\end{pmatrix}
$$
$$
\begin{pmatrix}
1 & 1 & -1 \\
0 & 1 & -1 \\
1 & 1 & -1
\end{pmatrix}
\begin{pmatrix}
\alpha_1 \\
\alpha_2 \\
\alpha_3
\end{pmatrix} =
\begin{pmatrix}
0 \\
0 \\
0
\end{pmatrix}
$$
Debemos estudiar si tiene única solución (L.I.) o infinitas soluciones (L.D.).

**Paso 2: Calcular el determinante de A.**
La matriz es cuadrada (3x3):
$$
\det(A) = \left| \begin{matrix}
1 & 1 & -1 \\
0 & 1 & -1 \\
1 & 1 & -1
\end{matrix} \right|
$$
Podemos notar que la tercera fila es igual a la primera fila. Una propiedad de los determinantes es que si una matriz tiene dos filas (o columnas) iguales, su determinante es 0.
(Calculando: $1(1(-1)-(-1)(1)) - 1(0(-1)-(-1)(1)) + (-1)(0(1)-1(1)) = 1(0) - 1(1) - 1(-1) = 0 - 1 + 1 = 0$)

**Paso 3: Concluir.**
Dado que $\det(A) = 0$, el sistema homogéneo $A\vec{\alpha} = \vec{0}$ **no** tiene solución única. Como es un sistema homogéneo, esto implica que tiene **infinitas soluciones**.
Esto significa que existen escalares $\alpha_1, \alpha_2, \alpha_3$, **no todos cero**, tales que la combinación lineal da el vector nulo.
Por lo tanto, los vectores $\{(1, 0, 1), (1, 1, 1), (-1, -1, -1)\}$ son **linealmente dependientes (L.D.)**.

---

### Ejemplo 3: Caso No Cuadrado

**Problema:** Determinar si el conjunto de vectores $\{(1, 1, 1), (0, 1, 1)\}$ en $\mathbb{R}^3$ es L.I.

**Paso 1: Plantear la ecuación de dependencia lineal.**
$\alpha_1(1, 1, 1) + \alpha_2(0, 1, 1) = (0, 0, 0)$

**Paso 2: Formar el sistema de ecuaciones.**
Esto lleva al sistema:
$$
\begin{cases}
\alpha_1 + 0\alpha_2 = 0 \\
\alpha_1 + \alpha_2 = 0 \\
\alpha_1 + \alpha_2 = 0
\end{cases}
\implies
\begin{cases}
\alpha_1 = 0 \\
\alpha_1 + \alpha_2 = 0
\end{cases}
$$

**Paso 3: Resolver el sistema.**
De la primera ecuación, $\alpha_1 = 0$. Sustituyendo en la segunda: $0 + \alpha_2 = 0 \implies \alpha_2 = 0$.

**Paso 4: Concluir.**
La única solución es $\alpha_1 = 0, \alpha_2 = 0$. Por lo tanto, los vectores son **linealmente independientes (L.I.)**.

**Nota Importante:** En este caso, tenemos 2 vectores en $\mathbb{R}^3$. Si intentáramos formar una matriz $A$ con ellos como columnas, sería:
$$
A = \begin{pmatrix}
1 & 0 \\
1 & 1 \\
1 & 1
\end{pmatrix}
$$
Esta matriz **no es cuadrada** (es 3x2). Por lo tanto, **no podemos usar la herramienta del determinante** para analizar la independencia lineal en este caso. Debemos resolver el sistema directamente.

---

## ¿Cómo Descartar los Vectores L.D. de un Conjunto?

Si un conjunto de vectores es L.D., significa que al menos uno de ellos se puede escribir como combinación lineal de los otros. A menudo queremos encontrar un subconjunto L.I. "máximo" dentro del conjunto original.

**Método usando Eliminación Gaussiana:**

Consideremos el conjunto $S = \{(1, 0, 1), (1, 1, -1), (2, 1, 0)\}$.

**Paso 1: Plantear el sistema homogéneo.**
Formamos la matriz $A$ con los vectores como columnas y consideramos el sistema $A\vec{\alpha} = \vec{0}$:
$$
A = \begin{pmatrix}
1 & 1 & 2 \\
0 & 1 & 1 \\
1 & -1 & 0
\end{pmatrix}
$$
$$
\begin{pmatrix}
1 & 1 & 2 \\
0 & 1 & 1 \\
1 & -1 & 0
\end{pmatrix}
\begin{pmatrix}
\alpha_1 \\
\alpha_2 \\
\alpha_3
\end{pmatrix} =
\begin{pmatrix}
0 \\
0 \\
0
\end{pmatrix}
$$

**Paso 2: Llevar la matriz A a su forma escalonada por filas (usando Eliminación Gaussiana).**
Trabajamos con la matriz aumentada del sistema homogéneo (aunque los ceros de la última columna no cambiarán):
$$
\begin{pmatrix}
1 & 1 & 2 & | & 0 \\
0 & 1 & 1 & | & 0 \\
1 & -1 & 0 & | & 0
\end{pmatrix}
\xrightarrow{F_3 \to F_3 - F_1}
\begin{pmatrix}
1 & 1 & 2 & | & 0 \\
0 & 1 & 1 & | & 0 \\
0 & -2 & -2 & | & 0
\end{pmatrix}
\xrightarrow{F_3 \to F_3 + 2F_2}
\begin{pmatrix}
1 & 1 & 2 & | & 0 \\
0 & 1 & 1 & | & 0 \\
0 & 0 & 0 & | & 0
\end{pmatrix}
$$

**Paso 3: Analizar la matriz escalonada.**
*   La matriz escalonada tiene una fila de ceros. Esto confirma que el sistema tiene infinitas soluciones (el rango de A es 2, menor que el número de incógnitas 3), y por lo tanto, los vectores son **L.D.**
*   Identificamos las **columnas pivote**: son las columnas que contienen el primer elemento no nulo (pivote) de alguna fila en la matriz escalonada. En este caso, las columnas 1 y 2 son columnas pivote.
    $$
    \begin{pmatrix}
    \boxed{1} & 1 & 2 \\
    0 & \boxed{1} & 1 \\
    0 & 0 & 0
    \end{pmatrix}
    $$
*   Las **columnas no pivote** corresponden a las variables libres del sistema y a los vectores que son combinación lineal de los anteriores. Aquí, la columna 3 no es pivote.

**Paso 4: Concluir qué vectores son L.I. y cuáles son L.D.**
*   Los **vectores originales** que corresponden a las **columnas pivote** forman un conjunto linealmente independiente. En este caso, los vectores de las columnas 1 y 2 de la matriz *original* $A$: $\{(1, 0, 1), (1, 1, -1)\}$ son L.I.
*   El vector original que corresponde a la **columna no pivote** es linealmente dependiente de los vectores correspondientes a las columnas pivote que están a su izquierda. Aquí, el vector de la columna 3, $(2, 1, 0)$, es L.D. con respecto a los dos primeros.

**Verificación:**
El sistema escalonado representa:
$$
\begin{cases}
\alpha_1 + \alpha_2 + 2\alpha_3 = 0 \\
\alpha_2 + \alpha_3 = 0
\end{cases}
$$
Si tomamos $\alpha_3$ como variable libre (por ejemplo, $\alpha_3 = t$), entonces $\alpha_2 = -t$ y $\alpha_1 = -\alpha_2 - 2\alpha_3 = -(-t) - 2t = t - 2t = -t$.
Una solución no trivial es (tomando $t=1$): $\alpha_1 = -1, \alpha_2 = -1, \alpha_3 = 1$.
Esto significa:
$-1(1, 0, 1) -1(1, 1, -1) + 1(2, 1, 0) = (0, 0, 0)$
Reordenando:
$(2, 1, 0) = 1(1, 0, 1) + 1(1, 1, -1)$
Esto confirma que el tercer vector es combinación lineal de los dos primeros.