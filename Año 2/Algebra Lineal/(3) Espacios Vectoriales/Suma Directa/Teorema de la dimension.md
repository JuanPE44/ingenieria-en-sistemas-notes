Sea $V$ un espacio vectorial de dimensión finita $n$. Sean $S_1$ y $S_2$ dos subespacios de $V$. El Teorema de la Dimensión (también conocido como Fórmula de Grassmann) establece una relación fundamental entre las dimensiones de estos subespacios, su suma y su intersección.

### Enunciado del Teorema

La dimensión de la suma de los subespacios $S_1$ y $S_2$ es igual a la suma de sus dimensiones individuales menos la dimensión de su intersección:

$\dim(S_1 + S_2) = \dim(S_1) + \dim(S_2) - \dim(S_1 \cap S_2)$

### Interpretación

Este teorema nos dice que si simplemente sumamos las dimensiones de $S_1$ y $S_2$, estamos contando "dos veces" la contribución de los vectores que pertenecen a ambos subespacios (es decir, los vectores de la intersección $S_1 \cap S_2$). Por lo tanto, para obtener la dimensión correcta de la suma $S_1 + S_2$, debemos restar la dimensión de la intersección una vez.

### Caso Especial: Suma Directa

Un caso particular importante ocurre cuando la intersección de los subespacios es únicamente el vector nulo:
$S_1 \cap S_2 = \{\vec{0}\}$

En esta situación, la dimensión de la intersección es cero:
$\dim(S_1 \cap S_2) = 0$

Sustituyendo esto en la fórmula general del Teorema de la Dimensión, obtenemos:
$\dim(S_1 + S_2) = \dim(S_1) + \dim(S_2) - 0$
$\dim(S_1 + S_2) = \dim(S_1) + \dim(S_2)$

Esto coincide con la condición de la suma directa. Si la suma es directa ($S_1 \oplus S_2$), la dimensión de la suma es simplemente la suma de las dimensiones.