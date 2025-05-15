La **dimensión** de un espacio vectorial $V$ (que no sea el espacio nulo $\{\vec{0}\}$) es el **número de vectores** que contiene cualquiera de sus bases.

Se utiliza la notación $\dim(V)$ para representar la dimensión de $V$.

### Observaciones Importantes

*   **Unicidad del número de vectores:** Una propiedad fundamental es que todas las bases de un mismo espacio vectorial tienen exactamente la **misma cantidad de vectores**. Esto asegura que la dimensión esté bien definida, sin importar qué base elijamos para contar sus vectores.
*   **Dimensión del espacio nulo:** El espacio vectorial que solo contiene al vector nulo, $V = \{\vec{0}\}$, es un caso especial. Como el conjunto $\{\vec{0}\}$ es linealmente dependiente (ya que $c \cdot \vec{0} = \vec{0}$ para cualquier $c \neq 0$), no puede formar una base. Por convención, se define que la dimensión del espacio vectorial $\{\vec{0}\}$ es **cero**:
    $\dim(\{\vec{0}\}) = 0$.

### Ejemplos

*   **Dimensión de $\mathbb{R}^n$:** El espacio vectorial $\mathbb{R}^n$ (vectores de $n$ componentes reales) tiene dimensión $n$.
    $\dim(\mathbb{R}^n) = n$.
    Una de sus bases más comunes es la **base canónica**:
    $B = \{ (1, 0, \dots, 0), (0, 1, \dots, 0), \dots, (0, 0, \dots, 1) \}$. Esta base tiene $n$ vectores.

*   **Dimensión de $P_n$:** El espacio vectorial $P_n$ de los polinomios de grado menor o igual a $n$ con coeficientes reales tiene dimensión $n+1$.
    $\dim(P_n) = n + 1$.
    La **base estándar** (o canónica) para $P_n$ es:
    $B = \{1, t, t^2, \dots, t^n\}$. Esta base contiene $n+1$ "vectores" (polinomios).