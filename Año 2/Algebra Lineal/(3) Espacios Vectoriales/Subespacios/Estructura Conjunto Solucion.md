## Definición

Consideremos un sistema de ecuaciones lineales **no homogéneo**, que se puede escribir en forma matricial como:

$A\vec{x} = \vec{b}$

donde:
*   $A$ es la matriz de coeficientes.
*   $\vec{x}$ es el vector de incógnitas.
*   $\vec{b}$ es el vector de términos constantes, y es **distinto del vector nulo** ($\vec{b} \neq \vec{0}$).

El **conjunto de todas las soluciones** de este sistema no homogéneo, que denotaremos como $S_g$ (Solución general), se puede expresar como la suma de una solución particular del sistema no homogéneo y el conjunto de soluciones del sistema homogéneo asociado. La estructura es:

$S_g = N(A) + S_p$

Desglosemos esta expresión:

1.  **$N(A)$ (Espacio Nulo o Núcleo de A):**
    *   Representa el conjunto de **todas las soluciones** del **sistema homogéneo asociado** $A\vec{x} = \vec{0}$.
    *   El espacio nulo $N(A)$ **sí es un subespacio vectorial** del espacio vectorial donde viven las soluciones $\vec{x}$ (por ejemplo, $\mathbb{R}^n$). Esto significa que $N(A)$ siempre contiene al vector nulo $\vec{0}$, es cerrado bajo la suma y cerrado bajo la multiplicación por escalar.
    *   A las soluciones $\vec{x}_h \in N(A)$ se les llama **soluciones homogéneas**.

2.  **$S_p$ (Solución Particular):**
    *   Representa **una única solución cualquiera**, pero específica, del sistema **no homogéneo** $A\vec{x} = \vec{b}$.
    *   Es decir, $S_p$ es un vector $\vec{x}_p$ tal que al sustituirlo en la ecuación, se cumple: $A\vec{x}_p = \vec{b}$.
    *   Puede haber infinitas soluciones particulares, pero para describir el conjunto solución general $S_g$, basta con encontrar **una** de ellas.

3.  **La Suma $N(A) + S_p$:**
    *   Esta notación significa que la **solución general** $S_g$ se obtiene tomando **cada vector** $\vec{x}_h$ del espacio nulo $N(A)$ y sumándole la **solución particular** $\vec{x}_p$ que hemos encontrado.
    *   Formalmente: $S_g = \{ \vec{x} \mid \vec{x} = \vec{x}_h + \vec{x}_p, \text{ donde } \vec{x}_h \in N(A) \}$
    *   Esto significa que *cualquier* solución del sistema no homogéneo $A\vec{x} = \vec{b}$ se puede escribir como la suma de una solución del sistema homogéneo asociado ($A\vec{x} = \vec{0}$) y una solución particular del sistema no homogéneo ($A\vec{x} = \vec{b}$).

## ¿Por qué $S_g$ no es un Subespacio Vectorial?

El conjunto solución general $S_g$ de un sistema no homogéneo ($A\vec{x} = \vec{b}$ con $\vec{b} \neq \vec{0}$) **nunca es un subespacio vectorial**.

La razón fundamental es que **no contiene al vector nulo $\vec{0}$**. Para que un conjunto sea subespacio vectorial, debe cumplir obligatoriamente la condición de contener al vector nulo.

Veamos por qué $\vec{0}$ no pertenece a $S_g$:
Si $\vec{x} = \vec{0}$ fuera una solución del sistema no homogéneo, entonces debería cumplir $A\vec{0} = \vec{b}$.
Sin embargo, sabemos que para cualquier matriz $A$, $A\vec{0} = \vec{0}$.
Como estamos en un sistema no homogéneo, $\vec{b} \neq \vec{0}$.
Por lo tanto, $A\vec{0} = \vec{0} \neq \vec{b}$, lo que significa que $\vec{x} = \vec{0}$ no es una solución del sistema no homogéneo y, por ende, $\vec{0} \notin S_g$.

**Interpretación Geométrica:**
El conjunto solución $S_g$ puede interpretarse geométricamente como una **traslación** del subespacio vectorial $N(A)$. La solución particular $\vec{x}_p$ actúa como el vector de traslación que "desplaza" el subespacio $N(A)$ (que siempre pasa por el origen) a una nueva posición en el espacio, de forma que ya no pasa por el origen. Por eso se dice que la solución general "se desplaza del origen". El resultado geométrico es un objeto afín (como un punto, una recta, un plano, etc., que no necesariamente pasa por el origen) paralelo al subespacio $N(A)$.