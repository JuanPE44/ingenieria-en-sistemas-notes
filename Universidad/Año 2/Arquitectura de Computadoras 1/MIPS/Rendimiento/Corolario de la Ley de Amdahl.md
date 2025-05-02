El **Corolario de la Ley de Amdahl** es una consecuencia directa de la Ley de Amdahl que establece un **límite superior teórico** a la aceleración que se puede lograr al mejorar solo una parte de un sistema.

Este corolario se deriva de la Ley de Amdahl cuando consideramos el caso extremo en el que la parte mejorada se vuelve *infinitamente rápida*. En otras palabras, el tiempo de ejecución de la parte mejorada tiende a cero.

Recordemos la fórmula de la Ley de Amdahl:

$$
Acc_G = \frac{1}{(1 - F_m) + \frac{F_m}{Acc_m}}
$$

Donde:

*   $Acc_G$ es la aceleración global del sistema.
*   $F_m$ es la fracción del tiempo original que se puede mejorar.
*   $Acc_m$ es la aceleración de la parte mejorada.

Ahora, imaginemos que hacemos que la parte mejorada sea *infinitamente* rápida. Esto significa que $Acc_m$ tiende a infinito ($Acc_m \to \infty$). En este caso, el término $\frac{F_m}{Acc_m}$ tiende a cero:

$$
\lim_{Acc_m \to \infty} \frac{F_m}{Acc_m} = 0
$$

Sustituyendo esto en la fórmula de la Ley de Amdahl, obtenemos:

$$
Acc_{G_{máx}} = \frac{1}{(1 - F_m) + 0} = \frac{1}{1 - F_m}
$$

Esta fórmula nos da la **aceleración máxima teórica** que se puede lograr, independientemente de cuánto aceleremos la parte mejorada.

### Interpretación

El corolario nos dice que, incluso si logramos que una parte de la tarea se ejecute instantáneamente (tiempo cero), la aceleración global del sistema estará limitada por la fracción del trabajo que *no* se puede mejorar ($1 - F_m$).

En palabras de Amdahl:

> "Si una mejora es utilizable en una fracción de una tarea, no podemos aumentar la velocidad de la tarea más que el recíproco de 1 menos esa fracción."

### Implicaciones Prácticas

*   **Rendimientos Decrecientes:** A medida que nos acercamos al límite de aceleración impuesto por el corolario, los esfuerzos adicionales para mejorar la parte optimizada dan rendimientos cada vez menores en términos de aceleración global.
*   **Identificar Cuellos de Botella:** El corolario resalta la importancia de identificar y abordar los cuellos de botella en el sistema. Si una gran parte del trabajo no se puede mejorar (es decir, $1 - F_m$ es grande), entonces la aceleración global estará severamente limitada, sin importar cuánto optimicemos otras partes.
*   **Optimización Holística:** Para lograr mejoras significativas en el rendimiento, a menudo es necesario adoptar un enfoque holístico y optimizar múltiples partes del sistema, en lugar de centrarse únicamente en una sola área.

