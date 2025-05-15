Para entender el complemento ortogonal, primero repasamos el concepto de **producto escalar**.

### Producto Escalar

Dados dos vectores $u = (u_1, \dots, u_n)$ y $v = (v_1, \dots, v_n)$ en $\mathbb{R}^n$, su producto escalar se define como:
$u \cdot v = \sum_{i=1}^n u_i v_i$

**Propiedades del Producto Escalar:**

Sean $u, v \in \mathbb{R}^n$. El producto escalar cumple las siguientes propiedades:

1.  **Conmutatividad:** $u \cdot v = v \cdot u$
2.  **Relación con la norma:** $u \cdot u = ||u||^2$ (donde $||u||$ es la norma o longitud del vector $u$)
3.  **Linealidad:** $u \cdot (\alpha_1 v_1 + \dots + \alpha_n v_n) = \alpha_1 (u \cdot v_1) + \dots + \alpha_n (u \cdot v_n)$ (Es distributivo respecto a la suma de vectores y compatible con la multiplicación por escalar).
4.  **Relación con el ángulo:** $u \cdot v = ||u|| \cdot ||v|| \cdot \cos \theta$, donde $\theta$ es el ángulo formado entre los vectores $u$ y $v$.
5.  **Ortogonalidad:** Dos vectores $u$ y $v$ son ortogonales (perpendiculares), denotado como $u \perp v$, si y solo si su producto escalar es cero: $u \cdot v = 0$.

### Definición de Complemento Ortogonal

Sea $V$ un espacio vectorial (como $\mathbb{R}^n$) y $S$ un subconjunto de $V$ ( $S \subseteq V$ ). El **complemento ortogonal** de $S$, denotado como $S^\perp$, es el conjunto de *todos* los vectores $w$ en $V$ que son ortogonales a *cada uno* de los vectores $v$ que pertenecen al conjunto $S$.

Formalmente:
$S^\perp = \{w \in V \mid w \cdot v = 0 \text{ para todo } v \in S\}$

En esencia, $S^\perp$ agrupa a todos los vectores de $V$ que son "perpendiculares" a todo el conjunto $S$. Si un vector $w$ está en $S^\perp$, significa que al calcular su producto escalar con cualquier vector $v$ de $S$, el resultado siempre será 0.

### Ejemplo

Consideremos la recta $r$ generada por el vector $(1, 1, 1)$, es decir:
$r = \langle(1, 1, 1)\rangle$

Sabemos que un vector $(a, b, c)$ pertenece a la recta $r$ si y solo si es un múltiplo escalar del vector generador:
$(a, b, c) = \lambda(1, 1, 1)$ para algún escalar $\lambda \in \mathbb{R}$.

Ahora, buscamos el complemento ortogonal $r^\perp$. Un vector $(x, y, z)$ pertenece a $r^\perp$ si y solo si es ortogonal a *todos* los vectores de $r$. Es decir, su producto escalar con cualquier vector de $r$ debe ser cero:
$(x, y, z) \cdot (a, b, c) = 0$ para todo $(a, b, c) \in r$.

Sustituyendo $(a, b, c)$ por $\lambda(1, 1, 1)$:
$(x, y, z) \cdot (\lambda(1, 1, 1)) = 0$

Utilizando las propiedades del producto escalar (podemos sacar el escalar $\lambda$):
$\lambda ((x, y, z) \cdot (1, 1, 1)) = 0$

Para que esta igualdad se cumpla para cualquier valor de $\lambda$ (incluyendo $\lambda \neq 0$), es necesario que el producto escalar sea cero:
$(x, y, z) \cdot (1, 1, 1) = 0$

Calculando el producto escalar:
$x \cdot 1 + y \cdot 1 + z \cdot 1 = 0$
$x + y + z = 0$

Por lo tanto, el complemento ortogonal de la recta $r$ es el conjunto de todos los vectores $(x, y, z)$ en $\mathbb{R}^3$ que satisfacen la ecuación $x + y + z = 0$. Geométricamente, esto representa un plano que pasa por el origen y cuyo vector normal es $(1, 1, 1)$.

$r^\perp = \{(x, y, z) \in \mathbb{R}^3 \mid x + y + z = 0\}$


## Propiedades del Complemento Ortogonal

Sea $V$ un espacio vectorial de dimensión $\dim(V) = n$ y $S$ un subespacio vectorial de $V$ ($S \subseteq V$). El complemento ortogonal $S^\perp$ tiene las siguientes propiedades importantes:

1.  **$S^{\perp \perp} = S$**
    *   El complemento ortogonal del complemento ortogonal de $S$ es el propio subespacio $S$. Esto significa que si primero encuentras todos los vectores ortogonales a $S$ (formando $S^\perp$), y luego encuentras todos los vectores ortogonales a $S^\perp$, vuelves a obtener el subespacio original $S$.

2.  **$V = S \oplus S^\perp$**
    *   El espacio vectorial $V$ es la **suma directa** del subespacio $S$ y su complemento ortogonal $S^\perp$. Esto implica dos cosas fundamentales:
        *   Cualquier vector $v \in V$ se puede escribir de forma **única** como la suma de un vector $s \in S$ y un vector $w \in S^\perp$: $v = s + w$.
        *   La intersección de $S$ y $S^\perp$ es solo el vector nulo (ver propiedad 3).
    *   Dimensionalmente, esto significa que $\dim(V) = \dim(S) + \dim(S^\perp)$.

3.  **$S \cap S^\perp = \{0\}$**
    *   El único vector que pertenece tanto a $S$ como a su complemento ortogonal $S^\perp$ es el vector nulo ($0$). Si un vector $v$ estuviera en ambos conjuntos, tendría que ser ortogonal a sí mismo ($v \cdot v = 0$), lo cual solo es posible si $v$ es el vector nulo ($||v||^2 = 0 \implies v = 0$).

4.  **Bases Combinadas**
    *   Si $B = \{v_1, \dots, v_k\}$ es una base para el subespacio $S$ (por lo tanto, $\dim(S) = k$), y $B' = \{v_{k+1}, \dots, v_n\}$ es una base para el complemento ortogonal $S^\perp$ (por lo tanto, $\dim(S^\perp) = n-k$), entonces la unión de estas dos bases, $B \cup B' = \{v_1, \dots, v_k, v_{k+1}, \dots, v_n\}$, forma una base para todo el espacio vectorial $V$. Esto es una consecuencia directa de que $V$ sea la suma directa de $S$ y $S^\perp$.

---

**Aplicación al Ejemplo Anterior:**

Recordemos el ejemplo:
*   $S = \langle(1, 1, 1)\rangle$ (una recta en $\mathbb{R}^3$, $\dim(S)=1$)
*   $S^\perp = \{(x, y, z) \in \mathbb{R}^3 \mid x + y + z = 0\}$ (un plano en $\mathbb{R}^3$, $\dim(S^\perp)=2$)

Vemos que:
*   $\dim(S) + \dim(S^\perp) = 1 + 2 = 3 = \dim(\mathbb{R}^3)$, lo cual concuerda con la propiedad 2 ($V = S \oplus S^\perp$).
*   El único vector que está en la recta $S$ (múltiplo de $(1,1,1)$) y también en el plano $S^\perp$ (satisface $x+y+z=0$) es el vector $(0,0,0)$, verificando la propiedad 3 ($S \cap S^\perp = \{0\}$).
*   Si tomamos una base para $S$, por ejemplo $\{(1, 1, 1)\}$, y una base para $S^\perp$, por ejemplo $\{(1, -1, 0), (1, 0, -1)\}$, la unión $\{(1, 1, 1), (1, -1, 0), (1, 0, -1)\}$ forma una base para $\mathbb{R}^3$, verificando la propiedad 4.