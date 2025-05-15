Un conjunto de vectores $\{v_1, v_2, \dots, v_n\}$ se considera una **base** para un espacio vectorial $V$ si cumple dos condiciones fundamentales:

1.  **Genera el espacio:** El conjunto de vectores es capaz de generar cualquier vector en el espacio vectorial $V$. Esto se expresa como $V = \langle\{v_1, v_2, \dots, v_n\}\rangle$. Significa que cualquier vector $v \in V$ se puede escribir como una combinación lineal de los vectores de la base:
    $v = c_1 v_1 + c_2 v_2 + \dots + c_n v_n$, donde $c_1, c_2, \dots, c_n$ son escalares.
2.  **Linealmente Independiente (L.I.):** El conjunto de vectores $\{v_1, v_2, \dots, v_n\}$ es linealmente independiente. Esto significa que la única forma de obtener el vector nulo como combinación lineal de estos vectores es que todos los escalares sean cero:
    $c_1 v_1 + c_2 v_2 + \dots + c_n v_n = \vec{0}$ implica que $c_1 = c_2 = \dots = c_n = 0$.