	Dadas dos bases $B_1 = \{v_1, \dots, v_n\}$ y $B_2 = \{u_1, \dots, u_n\}$ de un espacio vectorial $V$ de dimensión finita $n$.

**Objetivo:** Determinar un procedimiento que nos permita conocer las coordenadas de un vector $v$ en la base $B_2$ (la "base de llegada") si conocemos las coordenadas de dicho vector en la base $B_1$ (la "base de partida").

*   Conocemos: $[v]_{B_1} = \begin{pmatrix} c_1 \\ \vdots \\ c_n \end{pmatrix}$ (Coordenadas de $v$ respecto a $B_1$)
*   Queremos hallar: $[v]_{B_2} = \begin{pmatrix} d_1 \\ \vdots \\ d_n \end{pmatrix}$ (Coordenadas de $v$ respecto a $B_2$)

---

**Definición: Matriz de Cambio de Base**

Sean $B_1 = \{v_1, \dots, v_n\}$ y $B_2 = \{u_1, \dots, u_n\}$ dos bases de $V$.

La matriz $I_{B_1 B_2}$ cuyas columnas son los vectores de coordenadas de los vectores de la base $B_1$ expresados en términos de la base $B_2$:

$I_{B_1 B_2} = \begin{pmatrix} | & | & & | \\ [v_1]_{B_2} & [v_2]_{B_2} & \dots & [v_n]_{B_2} \\ | & | & & | \end{pmatrix}$

se llama **matriz cambio de base** (o matriz de transición) de la base $B_1$ a la base $B_2$.

---

**Teorema: Transformación de Coordenadas**

Para cada vector $v \in V$, la relación entre sus coordenadas en la base $B_1$ y sus coordenadas en la base $B_2$ viene dada por:

$[v]_{B_2} = I_{B_1 B_2} \cdot [v]_{B_1}$

**En resumen:** Para pasar de coordenadas en $B_1$ a coordenadas en $B_2$, se multiplica el vector de coordenadas $[v]_{B_1}$ por la izquierda por la matriz de cambio de base $I_{B_1 B_2}$.

**Propiedad Importante:** La matriz de cambio de base $I_{B_1 B_2}$ es siempre invertible, y su inversa realiza el cambio de base opuesto: $I_{B_2 B_1} = (I_{B_1 B_2})^{-1}$.

### Observación 

Si $B_1 = \{v_1, \dots, v_n\}$ y $B_2 = \{u_1, \dots, u_n\}$ son bases de un espacio vectorial $V$, entonces se puede probar lo siguiente:

1.  **Las columnas son bases de $\mathbb{R}^n$:**
    *   El conjunto de vectores de coordenadas $\{ [v_1]_{B_2}, \dots, [v_n]_{B_2} \}$ (las columnas de $I_{B_1 B_2}$) forma una base para $\mathbb{R}^n$.
    *   El conjunto de vectores de coordenadas $\{ [u_1]_{B_1}, \dots, [u_n]_{B_1} \}$ (las columnas de $I_{B_2 B_1}$) forma una base para $\mathbb{R}^n$.

2.  **Invertibilidad:** Como consecuencia directa del punto anterior, las matrices de cambio de base $I_{B_1 B_2}$ y $I_{B_2 B_1}$ son siempre **invertibles**.

3.  **Relación Inversa:** Las dos matrices de cambio de base entre $B_1$ y $B_2$ son **inversas** la una de la otra:
    *   $I_{B_1 B_2} = (I_{B_2 B_1})^{-1}$
    *   $I_{B_2 B_1} = (I_{B_1 B_2})^{-1}$

4.  **Fórmulas de Transformación:** Esto nos permite expresar el cambio de coordenadas en ambas direcciones:
    *   $[v]_{B_2} = I_{B_1 B_2} [v]_{B_1}$ (Cambio de $B_1$ a $B_2$)
    *   $[v]_{B_1} = I_{B_2 B_1} [v]_{B_2} = (I_{B_1 B_2})^{-1} [v]_{B_2}$ (Cambio de $B_2$ a $B_1$)