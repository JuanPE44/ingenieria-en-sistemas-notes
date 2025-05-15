## Concepto Principal (Teorema de Extensión de la Base)

Dado un espacio vectorial $V$ de dimensión finita $\dim(V) = n$:

*   **Situación Inicial:** Se tiene un conjunto de $k$ vectores $\{\vec{v}_1, \dots, \vec{v}_k\}$ que es **Linealmente Independiente (L.I.)**, donde $k < n$.
*   **Problema:** Este conjunto es L.I. pero es "demasiado pequeño" para generar todo $V$ (genera un subespacio $W \subset V$). No es una base de $V$.
*   **Solución (Garantía del Teorema):** **Siempre es posible** encontrar $n-k$ vectores adicionales $\{\vec{v}_{k+1}, \dots, \vec{v}_n\}$ tales que el conjunto "extendido" o "completado":
    $$ B = \{\vec{v}_1, \dots, \vec{v}_k, \vec{v}_{k+1}, \dots, \vec{v}_n\} $$
    sea una **base** para todo el espacio $V$.
*   **Propiedades del Conjunto Extendido B:**
    *   Contiene $n$ vectores.
    *   Es Linealmente Independiente (L.I.).
    *   Genera todo el espacio $V$ ($V = \langle B \rangle$).

## Método General

1.  Empezar con el conjunto L.I. inicial $\{\vec{v}_1, \dots, \vec{v}_k\}$.
2.  Buscar un vector $\vec{v}_{k+1} \in V$ tal que $\vec{v}_{k+1}$ **no** sea combinación lineal de $\{\vec{v}_1, \dots, \vec{v}_k\}$. Añadirlo al conjunto. (Esto asegura que el nuevo conjunto $\{\vec{v}_1, \dots, \vec{v}_k, \vec{v}_{k+1}\}$ sigue siendo L.I.).
3.  Repetir el paso 2, añadiendo en cada paso un vector que no sea combinación lineal de los ya seleccionados, hasta tener un total de $n$ vectores.
4.  El conjunto final de $n$ vectores será una base de $V$.

## Ejemplo Práctico: Extensión en $\mathbb{R}^3$

**Problema:**
Consideremos el vector $\vec{v} = (1, 2, -1)$. Este vector es L.I. (cualquier vector no nulo lo es) y genera una recta en $\mathbb{R}^3$ que pasa por el origen. Queremos extender el conjunto $\{\vec{v}\}$ para obtener una base completa de $\mathbb{R}^3$.
Como $\dim(\mathbb{R}^3) = 3$ y tenemos $k=1$ vector inicial, necesitamos añadir $n-k = 3-1 = 2$ vectores más, digamos $\vec{v}_2$ y $\vec{v}_3$, tales que $B = \{\vec{v}, \vec{v}_2, \vec{v}_3\}$ sea una base de $\mathbb{R}^3$.

**Paso 1: Añadir el primer vector ($\vec{v}_2$).**
*   Necesitamos encontrar un vector $\vec{v}_2$ que sea L.I. con $\vec{v} = (1, 2, -1)$. Esto significa que $\vec{v}_2$ no debe ser un múltiplo escalar de $\vec{v}$.
*   Podemos elegir un vector sencillo que cumpla esto. El ejemplo propone $\vec{v}_2 = (1, 0, 0)$. Claramente, $(1, 0, 0)$ no es múltiplo de $(1, 2, -1)$, por lo que son L.I.
*   Ahora tenemos el conjunto L.I. $\{(1, 2, -1), (1, 0, 0)\}$.

**Paso 2: Añadir el segundo vector ($\vec{v}_3$).**
*   Necesitamos encontrar un tercer vector $\vec{v}_3 = (x, y, z)$ tal que el conjunto completo $\{(1, 2, -1), (1, 0, 0), (x, y, z)\}$ sea L.I.
*   Para que 3 vectores en $\mathbb{R}^3$ sean L.I., la matriz formada por ellos (como filas o columnas) debe tener rango 3 (o, equivalentemente, su determinante debe ser no nulo).
*   Formemos la matriz $A$ con los vectores como columnas (el ejemplo usa filas, pero el rango es el mismo y el cálculo es idéntico):
    $$ A = \begin{pmatrix} 1 & 1 & x \\ 2 & 0 & y \\ -1 & 0 & z \end{pmatrix} $$
*   Para que los vectores sean L.I., necesitamos que $\text{rank}(A) = 3$. Realizamos eliminación gaussiana para encontrar la condición sobre $x, y, z$:
    $$
    \begin{pmatrix} 1 & 1 & x \\ 2 & 0 & y \\ -1 & 0 & z \end{pmatrix}
    \xrightarrow[F_3 \to F_3 + F_1]{F_2 \to F_2 - 2F_1}
    \begin{pmatrix} 1 & 1 & x \\ 0 & -2 & y-2x \\ 0 & 1 & z+x \end{pmatrix}
    \xrightarrow{F_2 \leftrightarrow F_3}
    \begin{pmatrix} 1 & 1 & x \\ 0 & 1 & z+x \\ 0 & -2 & y-2x \end{pmatrix}
    \xrightarrow{F_3 \to F_3 + 2F_2}
    \begin{pmatrix} 1 & 1 & x \\ 0 & 1 & z+x \\ 0 & 0 & (y-2x) + 2(z+x) \end{pmatrix}
    =
    \begin{pmatrix} 1 & 1 & x \\ 0 & 1 & z+x \\ 0 & 0 & y+2z \end{pmatrix}
    $$
    *(Nota: El resultado de la eliminación gaussiana coincide con el del texto original)*.
*   La matriz tendrá rango 3 si y sólo si el último elemento pivote es distinto de cero, es decir, si $y + 2z \neq 0$.

**Paso 3: Elegir un vector $\vec{v}_3$ válido.**
*   Cualquier vector $(x, y, z)$ que cumpla la condición $y + 2z \neq 0$ hará que el conjunto sea L.I.
*   El ejemplo elige $\vec{v}_3 = (1, 1, 1)$. Verifiquemos: para $(x,y,z)=(1,1,1)$, tenemos $y+2z = 1 + 2(1) = 3 \neq 0$. Por lo tanto, esta es una elección válida.

**Conclusión:**
Hemos extendido el conjunto inicial $\{\vec{v}\}$ añadiendo $\vec{v}_2 = (1, 0, 0)$ y $\vec{v}_3 = (1, 1, 1)$. El conjunto resultante:
$$ B = \{(1, 2, -1), (1, 0, 0), (1, 1, 1)\} $$
es un conjunto de 3 vectores L.I. en $\mathbb{R}^3$, y por lo tanto, es una **base** de $\mathbb{R}^3$.