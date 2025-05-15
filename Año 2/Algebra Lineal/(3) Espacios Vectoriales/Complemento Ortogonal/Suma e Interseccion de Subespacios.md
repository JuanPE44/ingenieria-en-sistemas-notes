Sea $V$ un espacio vectorial, y sean $S_1$ y $S_2$ dos subespacios de $V$. Podemos definir dos operaciones principales entre ellos:

### Intersección ($S_1 \cap S_2$)

La intersección de $S_1$ y $S_2$ es el conjunto de vectores que pertenecen a **ambos** subespacios simultáneamente.

$S_1 \cap S_2 = \{v \in V \mid v \in S_1 \land v \in S_2\}$

**¿Es $S_1 \cap S_2$ un subespacio?**

Sí, la intersección de dos subespacios es siempre un subespacio.

**¿Por qué?** Para que un conjunto sea un subespacio, debe cumplir tres condiciones:
1.  Contener al vector nulo ($0$). Como $S_1$ y $S_2$ son subespacios, ambos contienen a $0$, por lo tanto $0 \in S_1 \cap S_2$.
2.  Ser cerrado bajo la suma. Si $u, v \in S_1 \cap S_2$, entonces $u, v$ pertenecen a $S_1$ y también a $S_2$. Como $S_1$ y $S_2$ son subespacios, son cerrados bajo la suma, así que $u+v \in S_1$ y $u+v \in S_2$. Por lo tanto, $u+v \in S_1 \cap S_2$.
3.  Ser cerrado bajo la multiplicación por escalar. Si $u \in S_1 \cap S_2$ y $\alpha$ es un escalar, entonces $u \in S_1$ y $u \in S_2$. Como $S_1$ y $S_2$ son subespacios, son cerrados bajo la multiplicación por escalar, así que $\alpha u \in S_1$ y $\alpha u \in S_2$. Por lo tanto, $\alpha u \in S_1 \cap S_2$.

**Propiedad:** La intersección $S_1 \cap S_2$ es el **mayor** subespacio vectorial que está contenido simultáneamente en $S_1$ y $S_2$.

###  Suma ($S_1 + S_2$)

La suma de $S_1$ y $S_2$ es el conjunto de todos los vectores que se pueden expresar como la suma de un vector de $S_1$ y un vector de $S_2$.

$S_1 + S_2 = \{v_1 + v_2 \mid v_1 \in S_1, v_2 \in S_2\}$

Si $B_1$ es una base de $S_1$ y $B_2$ es una base de $S_2$, entonces la suma $S_1 + S_2$ es igual al subespacio generado por la unión de las bases $B_1$ y $B_2$.

$S_1 + S_2 = \langle B_1 \cup B_2 \rangle$

**¿Es $S_1 + S_2$ un subespacio?**

Sí, la suma de dos subespacios es siempre un subespacio.

**¿Por qué?**
Una forma de verlo es que $S_1 + S_2 = \langle B_1 \cup B_2 \rangle$. El espacio generado (span) por cualquier conjunto de vectores es, por definición, un subespacio vectorial. Contiene al vector nulo, es cerrado bajo la suma y bajo la multiplicación por escalar.

**Propiedad:** La suma $S_1 + S_2$ es el **menor** subespacio vectorial que contiene tanto a $S_1$ como a $S_2$.

---

En resumen:
*   Las operaciones de **intersección** y **suma** entre subespacios ($S_1, S_2$) producen nuevos **subespacios** ($S_1 \cap S_2$, $S_1 + S_2$).
*   Si $S_1 = \langle B_1 \rangle$ y $S_2 = \langle B_2 \rangle$, entonces $S_1 + S_2 = \langle B_1 \cup B_2 \rangle$.