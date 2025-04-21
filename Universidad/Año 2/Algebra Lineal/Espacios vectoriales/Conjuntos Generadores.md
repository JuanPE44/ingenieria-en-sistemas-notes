
**Definición:**
Se dice que un conjunto de vectores $\{\vec{v}_1, \vec{v}_2, \dots, \vec{v}_k\}$ de un espacio vectorial $V$ **genera** a $V$ (o que es un **conjunto de generadores** o **conjunto generador** para $V$) si **todo** vector $\vec{v}$ en el espacio vectorial $V$ puede expresarse como una combinación lineal de los vectores $\{\vec{v}_1, \vec{v}_2, \dots, \vec{v}_k\}$.

**En otras palabras:**
El conjunto $\{\vec{v}_1, \dots, \vec{v}_k\}$ genera a $V$ si se cumple que:
$$ V = \langle \vec{v}_1, \vec{v}_2, \dots, \vec{v}_k \rangle $$
También se usa la notación $V = \text{gen}\{\vec{v}_1, \dots, \vec{v}_k\}$. Esto significa que el subespacio generado por estos vectores no es solo una parte de $V$, sino que es *todo* el espacio $V$. Es decir, para todo $\vec{w} \in V$, existen escalares $\alpha_1, \dots, \alpha_k$ tales que $\vec{w} = \sum_{i=1}^{k} \alpha_i \vec{v}_i$.

**Intuición:**
Piensa en los vectores generadores $\{\vec{v}_1, \dots, \vec{v}_k\}$ como los "ladrillos" o "ingredientes básicos" de tu espacio vectorial $V$. Si este conjunto genera a $V$, significa que puedes construir *cualquier* vector $\vec{w}$ que se te ocurra dentro de $V$ utilizando únicamente combinaciones lineales de estos ladrillos básicos. No hay ningún vector en $V$ que quede "fuera del alcance" de las combinaciones lineales de $\{\vec{v}_1, \dots, \vec{v}_k\}$.

**Ejemplos:**
*   En $\mathbb{R}^2$, el conjunto $\{(1, 0), (0, 1)\}$ genera $\mathbb{R}^2$, porque cualquier vector $(x, y)$ se puede escribir como $x(1, 0) + y(0, 1)$. Este es un conjunto generador.
*   En $\mathbb{R}^2$, el conjunto $\{(1, 1), (2, 2)\}$ *no* genera $\mathbb{R}^2$. Solo genera los vectores que están sobre la línea $y=x$, que es un subespacio propio de $\mathbb{R}^2$. Por ejemplo, el vector $(1, 0)$ no se puede escribir como combinación lineal de $(1, 1)$ y $(2, 2)$. Este *no* es un conjunto generador de $\mathbb{R}^2$.

**Importancia:**
Encontrar un conjunto generador para un espacio vectorial nos da una forma finita y manejable de describir potencialmente infinitos vectores dentro de ese espacio. Si conocemos un conjunto generador, sabemos que cualquier vector del espacio se puede obtener a partir de ellos.

## Propiedades de un Conjunto de Generadores (Relación con L.I./L.D.)

Dado un conjunto generador $\{v_1, \dots, v_k\}$ de $V$, este puede ser Linealmente Independiente (L.I.) o Linealmente Dependiente (L.D.):

1.  **Si es Linealmente Dependiente (L.D.):**
    *   Existe **redundancia**. Al menos un vector del conjunto es combinación lineal de los otros.
    *   Hay vectores que **"sobran"** para generar el espacio: se pueden quitar uno o más vectores (los que son combinación lineal de otros) y el conjunto restante sigue generando $V$.
2.  **Si es Linealmente Independiente (L.I.):**
    *   **No hay redundancia**. Ningún vector del conjunto es combinación lineal de los otros.
    *   Todos los vectores son **"necesarios"**: si se quita cualquier vector del conjunto, el conjunto restante ya *no* genera todo $V$. Cada vector aporta algo único.

## Base

El caso más "eficiente" de un conjunto generador es aquel que no tiene redundancia. Esto nos lleva al concepto de base.

*   **Definición:** Un conjunto de vectores $\{v_1, \dots, v_n\}$ es una **base** de $V$ si cumple **dos condiciones simultáneamente**:
    1.  **Genera V:** $V = \langle \{v_1, \dots, v_n\} \rangle$.
    2.  **Es Linealmente Independiente (L.I.).**
*   **Concepto Clave:** Una base es un conjunto generador que es L.I. Es un conjunto de generadores **mínimo** (sin vectores sobrantes) y **eficiente** para describir todo el espacio vectorial.

## Dimensión

Una propiedad fundamental de los espacios vectoriales es que, aunque puedan tener muchas bases diferentes, todas ellas comparten una característica crucial.

*   **Tamaño de la Base:** **Todas** las bases de un mismo espacio vectorial $V$ (de dimensión finita) tienen la **misma cantidad** de vectores.
*   **Definición de Dimensión:** El número de vectores en *cualquier* base de $V$ se llama la **dimensión** de $V$, y se denota como $\dim(V)$. Es una propiedad intrínseca del espacio vectorial.
    *   $\dim(V) = \text{Cardinalidad (número de vectores) de cualquier base de } V$.
    *   Por ejemplo, como $\{(1, 0), (0, 1)\}$ es una base de $\mathbb{R}^2$ con 2 vectores, $\dim(\mathbb{R}^2) = 2$.

## Observaciones Importantes Finales

*   **Base => Generador:** Toda base de $V$ es, por definición, un conjunto de generadores de $V$.
*   **Generador =/> Base:** Un conjunto de generadores de $V$ **no** es necesariamente una base (podría ser L.D.).
*   **Unicidad de la Base:** La base de un espacio vectorial $V$ **no es única** (pueden existir múltiples conjuntos de vectores diferentes que formen una base para el mismo espacio).