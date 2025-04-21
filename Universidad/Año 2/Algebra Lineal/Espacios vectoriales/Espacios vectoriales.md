## Operaciones en $\mathbb{R}^2$ (Conceptos Previos a Espacios Vectoriales)

Recordemos el conjunto de vectores en el plano: $\mathbb{R}^2 = \{ (v_1, v_2) \mid v_1, v_2 \in \mathbb{R} \}$.
Dados dos vectores $\mathbf{v} = (v_1, v_2)$ y $\mathbf{u} = (u_1, u_2)$ en $\mathbb{R}^2$, y un escalar (número real) $\lambda \in \mathbb{R}$, definimos dos operaciones fundamentales:

### 1. Suma de Vectores

La suma de dos vectores se define componente a componente:
$$ \mathbf{v} + \mathbf{u} = (v_1, v_2) + (u_1, u_2) = (v_1 + u_1, v_2 + u_2) $$
El resultado es otro vector en $\mathbb{R}^2$.

### 2. Producto de un Vector por un Escalar

El producto de un escalar por un vector se define multiplicando cada componente del vector por el escalar:
$$ \lambda \mathbf{v} = \lambda (v_1, v_2) = (\lambda v_1, \lambda v_2) $$
El resultado es también un vector en $\mathbb{R}^2$.

Con estas dos operaciones, dotamos al conjunto $\mathbb{R}^2$ de una estructura algebraica, que podemos denotar como $\langle \mathbb{R}^2, +_{\mathbb{R}^2}, \cdot_{\mathbb{R}} \rangle$.

### Propiedades de las Operaciones

Estas operaciones cumplen una serie de propiedades importantes:

**Propiedades de la Suma de Vectores** (para $\mathbf{u}, \mathbf{v}, \mathbf{w} \in \mathbb{R}^2$):

*   **S1 (Asociativa):** $\mathbf{u} + (\mathbf{v} + \mathbf{w}) = (\mathbf{u} + \mathbf{v}) + \mathbf{w}$
*   **S2 (Conmutativa):** $\mathbf{u} + \mathbf{v} = \mathbf{v} + \mathbf{u}$
*   **S3 (Elemento Neutro):** Existe un vector $\mathbf{0} = (0, 0) \in \mathbb{R}^2$ (el vector nulo) tal que $\mathbf{v} + \mathbf{0} = \mathbf{v}$ para todo $\mathbf{v} \in \mathbb{R}^2$.
*   **S4 (Inverso Aditivo):** Para cada $\mathbf{v} = (v_1, v_2) \in \mathbb{R}^2$, existe un vector $-\mathbf{v} = (-v_1, -v_2) \in \mathbb{R}^2$ tal que $\mathbf{v} + (-\mathbf{v}) = \mathbf{0}$.

**Propiedades del Producto por un Escalar y Distributivas** (para $\mathbf{u}, \mathbf{v} \in \mathbb{R}^2$ y escalares $\lambda, \beta \in \mathbb{R}$):

*   **P1 (Asociativa escalar):** $(\lambda \beta) \cdot \mathbf{v} = \lambda \cdot (\beta \cdot \mathbf{v})$
*   **P2 (Neutro multiplicativo escalar):** Existe el escalar $1 \in \mathbb{R}$ tal que $1 \cdot \mathbf{v} = \mathbf{v}$.
*   **P3 (Distributiva respecto a la suma de escalares):** $(\lambda + \beta) \cdot \mathbf{v} = (\lambda \cdot \mathbf{v}) + (\beta \cdot \mathbf{v})$
*   **P4 (Distributiva respecto a la suma de vectores):** $\lambda \cdot (\mathbf{u} + \mathbf{v}) = (\lambda \cdot \mathbf{u}) + (\lambda \cdot \mathbf{v})$

Estas 8 propiedades (S1-S4 y P1-P4) son fundamentales y son las que se exigirán para definir la estructura más general de **Espacio Vectorial**.

## ¿Qué es un Espacio Vectorial?

Imagina que tienes un conjunto de objetos (que llamaremos "vectores") y quieres poder hacer dos cosas básicas con ellos de una manera coherente y útil: **sumarlos entre sí** y **"escalarlos"** (multiplicarlos por números). Un **espacio vectorial** es precisamente un marco matemático que formaliza esta idea.

Más formalmente:

**Definición:**
Un **espacio vectorial** sobre un **cuerpo** $\mathbb{K}$ (piensa en $\mathbb{K}$ como el conjunto de los "números" que usaremos para escalar, usualmente los números reales $\mathbb{R}$ o los complejos $\mathbb{C}$) es una estructura algebraica formada por:

1.  Un conjunto no vacío $V$, cuyos elementos se llaman **vectores**.
2.  Una operación llamada **suma de vectores** (`+`), que toma dos vectores de $V$ y devuelve otro vector en $V$:
$$ + : V \times V \to V $$
$$ (\mathbf{u}, \mathbf{v}) \mapsto \mathbf{u} + \mathbf{v} $$
3.  Una operación llamada **producto por escalar** (`·`), que toma un escalar de $\mathbb{K}$ y un vector de $V$, y devuelve otro vector en $V$:
$$ \cdot : \mathbb{K} \times V \to V $$
$$ (\lambda, \mathbf{v}) \mapsto \lambda \cdot \mathbf{v} $$

Esta estructura, denotada como $(V, +, \cdot)$, debe cumplir **obligatoriamente** las siguientes 10 propiedades (axiomas) para cualesquiera vectores $\mathbf{u}, \mathbf{v}, \mathbf{w} \in V$ y cualesquiera escalares $\lambda, \beta \in \mathbb{K}$:

**Axiomas relativos a la Suma de Vectores**
(Estos axiomas aseguran que $(V, +)$ sea un *grupo abeliano*, lo que significa que la suma es "bien comportada"):

*   **S1 (Asociatividad):** La forma de agrupar la suma de tres vectores no importa.
$$ \mathbf{u} + (\mathbf{v} + \mathbf{w}) = (\mathbf{u} + \mathbf{v}) + \mathbf{w} $$
*   **S2 (Conmutatividad):** El orden en que sumas dos vectores no importa.
$$ \mathbf{u} + \mathbf{v} = \mathbf{v} + \mathbf{u} $$
*   **S3 (Elemento Neutro Aditivo):** Existe un vector especial, llamado **vector nulo** ($\mathbf{0}$), tal que sumarlo a cualquier vector no lo cambia.
$$ \text{Existe } \mathbf{0} \in V \text{ tal que } \mathbf{v} + \mathbf{0} = \mathbf{v} \text{ para todo } \mathbf{v} \in V $$
*   **S4 (Inverso Aditivo):** Cada vector tiene un "opuesto" que, al sumarlo, da el vector nulo.
$$ \text{Para cada } \mathbf{v} \in V, \text{ existe } -\mathbf{v} \in V \text{ tal que } \mathbf{v} + (-\mathbf{v}) = \mathbf{0} $$

**Axiomas relativos al Producto por Escalar y la Distributividad**
(Estos axiomas conectan la multiplicación por escalar con la suma de vectores y las operaciones del cuerpo $\mathbb{K}$):

*   **P1 (Asociatividad Mixta):** Escalar un vector por un producto de escalares es lo mismo que escalar sucesivamente.
$$ (\lambda \beta) \cdot \mathbf{v} = \lambda \cdot (\beta \cdot \mathbf{v}) $$
*   **P2 (Elemento Neutro Escalar):** Escalar por el número $1$ (el neutro multiplicativo del cuerpo $\mathbb{K}$) no cambia el vector.
$$ 1 \cdot \mathbf{v} = \mathbf{v} $$
*   **P3 (Distributividad respecto a la suma de vectores):** Escalar una suma de vectores es lo mismo que sumar los vectores escalados individualmente.
$$ \lambda \cdot (\mathbf{u} + \mathbf{v}) = (\lambda \cdot \mathbf{u}) + (\lambda \cdot \mathbf{v}) $$
*   **P4 (Distributividad respecto a la suma de escalares):** Escalar un vector por una suma de escalares es lo mismo que sumar el vector escalado por cada escalar.
$$ (\lambda + \beta) \cdot \mathbf{v} = (\lambda \cdot \mathbf{v}) + (\beta \cdot \mathbf{v}) $$

**En resumen:**

Un espacio vectorial es un conjunto donde podemos sumar sus elementos (vectores) y multiplicarlos por escalares (números de un cuerpo $\mathbb{K}$), de manera que estas operaciones se comporten de la forma "natural" y consistente a la que estamos acostumbrados, por ejemplo, con los vectores en $\mathbb{R}^2$ o $\mathbb{R}^3$. Los 10 axiomas simplemente formalizan este "comportamiento natural".

La belleza de esta definición abstracta es que muchos conjuntos diferentes (como $\mathbb{R}^n$, conjuntos de matrices, conjuntos de polinomios, conjuntos de funciones continuas) pueden ser espacios vectoriales si definimos adecuadamente la suma y el producto por escalar y verificamos que cumplen estos axiomas. Esto permite estudiar sus propiedades de forma unificada.

## Ejemplos Clásicos de Espacios Vectoriales

Una característica clave de los espacios vectoriales es que son **cerrados bajo combinaciones lineales**. Esto significa que si tomas cualquier conjunto de vectores del espacio y los combinas usando la suma vectorial y el producto por escalar, el resultado *siempre* será otro vector dentro del mismo espacio. Veamos cómo funciona esto en ejemplos concretos:

### Ejemplo 1: Los Espacios $\mathbb{R}^n$

Estos son quizás los espacios vectoriales más intuitivos.

*   **El Conjunto (V):** Es $\mathbb{R}^n$, el conjunto de todas las **n-tuplas** (listas ordenadas de $n$ números) de números reales.
$$ V = \mathbb{R}^n = \{ (x_1, x_2, \dots, x_n) \mid x_1, x_2, \dots, x_n \in \mathbb{R} \} $$
*   Si $n=2$, tenemos los vectores del plano $\mathbb{R}^2 = \{(x, y) \mid x, y \in \mathbb{R}\}$.
*   Si $n=3$, tenemos los vectores del espacio tridimensional $\mathbb{R}^3 = \{(x, y, z) \mid x, y, z \in \mathbb{R}\}$.

*   **Los Vectores:** Son las propias n-tuplas, como $\mathbf{x} = (x_1, \dots, x_n)$.

*   **Los Escalares (Cuerpo $\mathbb{K}$):** Son los números reales, $\mathbb{K} = \mathbb{R}$.

*   **Operación Suma (+):** Se define componente a componente. Si $\mathbf{x} = (x_1, \dots, x_n)$ y $\mathbf{y} = (y_1, \dots, y_n)$:
$$ \mathbf{x} + \mathbf{y} = (x_1 + y_1, x_2 + y_2, \dots, x_n + y_n) $$
*Importante:* La suma de dos vectores de $\mathbb{R}^n$ sigue siendo un vector de $\mathbb{R}^n$ (la tupla resultante tiene $n$ componentes reales).

*   **Operación Producto por Escalar (·):** Se define multiplicando cada componente por el escalar. Si $\lambda \in \mathbb{R}$:
$$ \lambda \cdot \mathbf{x} = \lambda \cdot (x_1, \dots, x_n) = (\lambda x_1, \lambda x_2, \dots, \lambda x_n) $$
*Importante:* El resultado de multiplicar un vector de $\mathbb{R}^n$ por un escalar real sigue siendo un vector de $\mathbb{R}^n$.

*   **¿Por qué es un Espacio Vectorial?** Porque el conjunto $\mathbb{R}^n$ con estas dos operaciones cumple **todos los 10 axiomas** de espacio vectorial (S1-S4, P1-P4). Por ejemplo:
*   El vector nulo es $\mathbf{0} = (0, 0, \dots, 0)$.
*   El inverso aditivo de $\mathbf{x}=(x_1, \dots, x_n)$ es $-\mathbf{x}=(-x_1, \dots, -x_n)$.
*   La conmutatividad, asociatividad y distributividad se heredan directamente de las propiedades de los números reales en cada componente.

---

### Ejemplo 2: El Espacio de Polinomios de Grado $\le n$, $P_n(\mathbb{R})$

Este es un ejemplo menos geométrico pero igualmente importante. (Usaremos la notación $P_n(\mathbb{R})$ o $P_n[X]$ para ser más precisos que $P[X]$).

*   **El Conjunto (V):** Es $P_n(\mathbb{R})$, el conjunto de todos los **polinomios con coeficientes reales de grado como máximo $n$**, incluyendo el polinomio nulo.
$$ V = P_n(\mathbb{R}) = \{ a_n x^n + a_{n-1} x^{n-1} + \dots + a_1 x + a_0 \mid a_i \in \mathbb{R} \} $$
*   Por ejemplo, si $n=2$, $V = P_2(\mathbb{R}) = \{ ax^2 + bx + c \mid a, b, c \in \mathbb{R} \}$. Polinomios como $3x^2 - 5$, $x+1$, $7$, y $0$ están en $P_2(\mathbb{R})$.

*   **Los Vectores:** Son los propios polinomios, como $p(x) = a_n x^n + \dots + a_0$.

*   **Los Escalares (Cuerpo $\mathbb{K}$):** Son los números reales, $\mathbb{K} = \mathbb{R}$.

*   **Operación Suma (+):** Es la suma habitual de polinomios, sumando los coeficientes de los términos del mismo grado. Si $p(x) = \sum_{i=0}^n a_i x^i$ y $q(x) = \sum_{i=0}^n b_i x^i$:
$$ (p+q)(x) = p(x) + q(x) = \sum_{i=0}^n (a_i + b_i) x^i $$
*Importante:* La suma de dos polinomios de grado $\le n$ da como resultado otro polinomio cuyo grado también es $\le n$ (o el polinomio nulo). El grado no puede aumentar más allá de $n$.

*   **Operación Producto por Escalar (·):** Es la multiplicación habitual de un polinomio por un número real, multiplicando cada coeficiente por el escalar. Si $\lambda \in \mathbb{R}$:
$$ (\lambda \cdot p)(x) = \lambda \cdot p(x) = \lambda \cdot \sum_{i=0}^n a_i x^i = \sum_{i=0}^n (\lambda a_i) x^i $$
*Importante:* Multiplicar un polinomio de grado $\le n$ por un escalar real da como resultado otro polinomio de grado $\le n$ (o el polinomio nulo si $\lambda=0$ o $p(x)=0$).

*   **¿Por qué es un Espacio Vectorial?** Porque el conjunto $P_n(\mathbb{R})$ con estas operaciones de suma y producto por escalar cumple **todos los 10 axiomas** de espacio vectorial.
*   El vector nulo es el polinomio cero: $\mathbf{0} = 0x^n + \dots + 0x + 0$.
*   El inverso aditivo de $p(x) = \sum a_i x^i$ es $-p(x) = \sum (-a_i) x^i$.
*   Las demás propiedades (asociatividad, conmutatividad, distributividad) se derivan de las propiedades de la suma y producto de números reales aplicadas a los coeficientes.

Estos ejemplos muestran cómo la estructura abstracta de espacio vectorial puede aplicarse tanto a objetos geométricos (como $\mathbb{R}^n$) como a objetos algebraicos (como los polinomios $P_n(\mathbb{R})$).

## Dependencia Lineal (L.D)

[[Dependencia Lineal (L.D)]]

## Vector Perteneciente al Subespacio Generado

[[Vector Perteneciente al Subespacio Generado]]

## Conjunto de Generadores 

[[Conjuntos Generadores]]
## Independencia Lineal (L.I)

[[Independencia Lineal (L.I)]]

## Independencia Lineal y Determinante

[[Independencia Lineal y Determinante]]

## Extension a una base

[[Extension a una base]]

