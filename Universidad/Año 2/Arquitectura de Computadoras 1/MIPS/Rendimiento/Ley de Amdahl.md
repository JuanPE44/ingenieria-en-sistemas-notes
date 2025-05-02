La **Ley de Amdahl**, propuesta por Gene Amdahl en 1967, es una fórmula fundamental utilizada para estimar la **máxima mejora teórica en el rendimiento (aceleración o *speedup*)** de un sistema completo cuando solo una parte de ese sistema es mejorada.

El principio clave, citado a menudo, es:

> "La mejora obtenida en el rendimiento al utilizar algún modo de ejecución más rápido está limitada por la fracción de tiempo que se pueda utilizar en ese modo más rápido."

En esencia, la ley nos dice que, aunque mejoremos drásticamente una porción de una tarea, la aceleración total que podemos lograr está **limitada por la porción de la tarea que *no* se mejora**. Esta parte no mejorada actúa como un cuello de botella.

### Componentes de la Fórmula

Para aplicar la Ley de Amdahl, necesitamos definir dos factores clave:

1.  **$F_m$ (Fracción Mejorada):** Es la fracción del tiempo de ejecución *original* que corresponde a la parte del sistema o tarea que *puede ser* y *será* mejorada. Este valor está entre 0 y 1.
    *   Si $F_m = 0.6$, significa que el 60% del tiempo original se gasta en la parte que vamos a acelerar.
2.  **$Acc_m$ (Aceleración de la Mejora):** Es el factor por el cual se acelera *esa parte específica* ($F_m$) de la tarea.
    *   Si la parte mejorada ahora corre 2 veces más rápido, $Acc_m = 2$.
    *   Si la parte mejorada ahora corre 10 veces más rápido, $Acc_m = 10$.

### Cálculo del Tiempo Mejorado

El tiempo total de ejecución después de aplicar la mejora ($T_{mejorado}$) se calcula sumando el tiempo de la parte no mejorada y el nuevo tiempo (reducido) de la parte mejorada:

*   Tiempo de la parte no mejorada: $T_{original} \times (1 - F_m)$
*   Tiempo de la parte mejorada (acelerada): $\frac{T_{original} \times F_m}{Acc_m}$

Combinando ambos:
$$
T_{mejorado} = T_{original} \times \left( (1 - F_m) + \frac{F_m}{Acc_m} \right)
$$

### Cálculo de la Aceleración Global ($Acc_G$)

La aceleración global ($Acc_G$) o *speedup* total del sistema es la relación entre el tiempo de ejecución original y el tiempo de ejecución mejorado:
$$
Acc_G = \frac{T_{original}}{T_{mejorado}}
$$
Sustituyendo la expresión para $T_{mejorado}$ y simplificando (el término $T_{original}$ se cancela), obtenemos la forma más común de la Ley de Amdahl:
$$
Acc_G = \frac{1}{(1 - F_m) + \frac{F_m}{Acc_m}}
$$

### Implicaciones Clave

*   **Límite Teórico:** La ley muestra que existe un límite superior a la aceleración posible. Incluso si la mejora de la parte optimizada es infinita ($Acc_m \to \infty$), la aceleración global máxima está limitada a $Acc_G = \frac{1}{1 - F_m}$. Esto significa que si solo puedes mejorar el 90% de la tarea ($F_m = 0.9$), la máxima aceleración posible es $1 / (1 - 0.9) = 1 / 0.1 = 10$ veces, sin importar cuánto aceleres esa porción.
*   **Importancia de $F_m$:** La fracción del programa que puede ser mejorada ($F_m$) es crucial. Si $F_m$ es pequeña, la aceleración global será limitada, incluso con grandes valores de $Acc_m$. Esto resalta la importancia de aplicar la "Aceleración del Caso Común": enfocar los esfuerzos de optimización en las partes que consumen la mayor parte del tiempo.
*   **Rendimientos Decrecientes:** A medida que $Acc_m$ aumenta, las ganancias adicionales en $Acc_G$ se vuelven cada vez menores, especialmente si $F_m$ no es cercano a 1.


## Ley de Amdahl: Caso General con *n* Mejoras

La Ley de Amdahl, en su forma más general, se extiende para considerar la situación en la que se aplican *múltiples* mejoras a diferentes partes de un sistema o tarea. En lugar de mejorar solo una fracción del trabajo, ahora tenemos *n* fracciones diferentes, cada una con su propia aceleración.

### Componentes

Para este caso general, necesitamos definir lo siguiente:

*   $F_{i}$: La fracción del tiempo de ejecución original que corresponde a la parte *i* del sistema que se puede mejorar, donde $i$ va desde 1 hasta *n*. Es importante notar que la suma de todas las fracciones mejorables *no* necesariamente tiene que ser 1 (puede haber partes del sistema que no se mejoran en absoluto).
*   $Acc_{i}$: La aceleración (speedup) obtenida al mejorar la parte *i* del sistema.

### Tiempo de Ejecución Mejorado

El tiempo de ejecución total después de aplicar las *n* mejoras ($T_{mejorado}$) se calcula de la siguiente manera:

1.  **Tiempo de la parte no mejorada:** Esta es la fracción del tiempo original que no se ve afectada por ninguna de las mejoras. Se calcula como $T_{original} \times (1 - \sum_{i=1}^{n} F_i)$.  Es decir, restamos del tiempo original la suma de todas las fracciones que sí se mejoran.
2.  **Tiempo de cada parte mejorada:** Para cada parte *i* que se mejora, el nuevo tiempo de ejecución es $\frac{T_{original} \times F_i}{Acc_i}$.

Sumando todo, obtenemos:

$$
T_{mejorado} = T_{original} \times \left( (1 - \sum_{i=1}^{n} F_i) + \sum_{i=1}^{n} \frac{F_i}{Acc_i} \right)
$$

### Aceleración Global

La aceleración global ($Acc_G$) se calcula como la relación entre el tiempo de ejecución original y el tiempo de ejecución mejorado:

$$
Acc_G = \frac{T_{original}}{T_{mejorado}}
$$

Sustituyendo la expresión para $T_{mejorado}$ y simplificando (cancelando $T_{original}$), obtenemos:

$$
Acc_G = \frac{1}{(1 - \sum_{i=1}^{n} F_i) + \sum_{i=1}^{n} \frac{F_i}{Acc_i}}
$$

### Interpretación

*   **Múltiples Cuellos de Botella:** Esta forma general de la Ley de Amdahl nos permite analizar sistemas con múltiples cuellos de botella. Cada parte que no se mejora significativamente ($F_i$ pequeño o $Acc_i$ cercano a 1) contribuye a limitar la aceleración global.
*   **Priorización de Mejoras:** La fórmula ayuda a priorizar los esfuerzos de optimización. Es más beneficioso enfocarse en las partes que tienen una fracción de tiempo de ejecución original grande ($F_i$ grande) y que se pueden acelerar significativamente ($Acc_i$ grande).
*   **Límite Superior:** Incluso con múltiples mejoras, la aceleración global sigue estando limitada. Si la suma de todas las fracciones mejoradas es menor que 1, siempre habrá una parte del sistema que no se puede acelerar, lo que impone un límite superior a la aceleración global.

### Ejemplo

Imaginemos que tenemos una tarea que se divide en tres partes:

*   Parte A: $F_1 = 0.4$, $Acc_1 = 2$ (se acelera 2 veces)
*   Parte B: $F_2 = 0.3$, $Acc_2 = 4$ (se acelera 4 veces)
*   Parte C: $F_3 = 0.1$, $Acc_3 = 1.5$ (se acelera 1.5 veces)

La fracción del trabajo que no se mejora es $1 - (0.4 + 0.3 + 0.1) = 0.2$.

La aceleración global sería:

$$
Acc_G = \frac{1}{(1 - (0.4 + 0.3 + 0.1)) + (\frac{0.4}{2} + \frac{0.3}{4} + \frac{0.1}{1.5})} = \frac{1}{0.2 + 0.2 + 0.075 + 0.0667} \approx \frac{1}{0.5417} \approx 1.846
$$

En este caso, la aceleración global es de aproximadamente 1.846 veces.


## Ejemplo de Aplicación: Ley de Amdahl

## Problema

Se tiene un circuito que realiza una operación de multiplicación en un tiempo total de **2.3 microsegundos** ($T_{original}$). Dentro de este tiempo, **0.5 microsegundos** ($T_{original-rebalse}$) se dedican específicamente al cálculo de rebalse (overflow) del resultado.

Se diseña una versión optimizada de este circuito donde el tiempo necesario para el cálculo de rebalse se **reduce a la mitad**.

Se pide:

1.  Hallar la **fracción mejorada** ($F_m$).
2.  Hallar la **aceleración de la parte mejorada** ($Acc_m$).
3.  Calcular la **aceleración global** ($Acc_G$) del nuevo circuito respecto al original.

## Solución

### Datos Iniciales

*   Tiempo total original: $T_{original} = 2.3$ μs
*   Tiempo original de la parte a mejorar (cálculo de rebalse): $T_{original-rebalse} = 0.5$ μs
*   Mejora: El tiempo de rebalse se reduce a la mitad.

### 1. Hallar la Fracción Mejorada ($F_m$)

La fracción mejorada ($F_m$) representa qué porción del tiempo *original* total se dedicaba a la parte que ahora estamos optimizando (el cálculo de rebalse).

$$
F_m = \frac{\text{Tiempo original de la parte mejorada}}{\text{Tiempo total original}} = \frac{T_{original-rebalse}}{T_{original}}
$$

$$
F_m = \frac{0.5 \text{ μs}}{2.3 \text{ μs}} \approx 0.2174
$$

Esto significa que aproximadamente el 21.74% del tiempo original se dedicaba al cálculo de rebalse.

### 2. Hallar la Aceleración Mejorada ($Acc_m$)

La aceleración mejorada ($Acc_m$) indica cuántas veces más rápida es *específicamente la parte optimizada* (el cálculo de rebalse) en la nueva versión.

Primero, calculamos el nuevo tiempo para el cálculo de rebalse ($T_{nuevo-rebalse}$):
$$
T_{nuevo-rebalse} = \frac{T_{original-rebalse}}{2} = \frac{0.5 \text{ μs}}{2} = 0.25 \text{ μs}
$$

Ahora, calculamos la aceleración de esta parte:
$$
Acc_m = \frac{\text{Tiempo original de la parte mejorada}}{\text{Tiempo nuevo de la parte mejorada}} = \frac{T_{original-rebalse}}{T_{nuevo-rebalse}}
$$

$$
Acc_m = \frac{0.5 \text{ μs}}{0.25 \text{ μs}} = 2
$$

La parte del cálculo de rebalse es ahora 2 veces más rápida.

### 3. Hallar la Aceleración Global ($Acc_G$)

Podemos calcular la aceleración global de dos maneras:

**Método A: Cálculo Directo (Solución "Convencional")**

Calculamos el nuevo tiempo total de ejecución ($T_{mejorado}$) sumando el tiempo de la parte *no* mejorada y el *nuevo* tiempo de la parte mejorada:

*   Tiempo de la parte no mejorada: $T_{original} - T_{original-rebalse} = 2.3 \text{ μs} - 0.5 \text{ μs} = 1.8 \text{ μs}$
*   Nuevo tiempo de la parte mejorada: $T_{nuevo-rebalse} = 0.25 \text{ μs}$

$$
T_{mejorado} = (T_{original} - T_{original-rebalse}) + T_{nuevo-rebalse} = 1.8 \text{ μs} + 0.25 \text{ μs} = 2.05 \text{ μs}
$$

Ahora, la aceleración global es la relación entre el tiempo original y el tiempo mejorado:
$$
Acc_G = \frac{T_{original}}{T_{mejorado}} = \frac{2.3 \text{ μs}}{2.05 \text{ μs}} \approx 1.122
$$

**Método B: Usando la Fórmula de la Ley de Amdahl**

Utilizamos los valores calculados de $F_m$ y $Acc_m$ en la fórmula de Amdahl:
$$
Acc_G = \frac{1}{(1 - F_m) + \frac{F_m}{Acc_m}}
$$

$$
Acc_G = \frac{1}{(1 - 0.2174) + \frac{0.2174}{2}} = \frac{1}{0.7826 + 0.1087} = \frac{1}{0.8913} \approx 1.122
$$

## Conclusión

*   La fracción del tiempo original dedicada a la parte mejorable (rebalse) es $F_m \approx 0.2174$.
*   La parte mejorada (rebalse) se acelera por un factor de $Acc_m = 2$.
*   La **aceleración global** del circuito, gracias a esta optimización, es $Acc_G \approx 1.122$. Esto significa que el circuito completo es aproximadamente un 12.2% más rápido que el original.


## Problema 2: Ley de Amdahl con Múltiples Mejoras y Recálculo de Fracciones

## Planteamiento del Problema

*   **Procesador A:** Realiza una operación en un tiempo base de *N* segundos.
*   **Procesador B:** Optimiza el procesador A mejorando 2/3 de la operación en un factor de 2.5.
*   **Procesador C:** Se basa en el procesador B y optimiza *aún más* la operación, duplicando la velocidad de una parte. Tenemos dos escenarios para C:
    *   **C1:** Mejora la fracción que *ya había mejorado* B (los 2/3 originales).
    *   **C2:** Mejora la fracción que *no había mejorado* B (el 1/3 original).

Se pide calcular la aceleración global de C con respecto a A ($Acc_{C1-A}$ y $Acc_{C2-A}$) en ambos escenarios. Además, se analiza cómo calcular la aceleración de C con respecto a B ($Acc_{C1-B}$ y $Acc_{C2-B}$).

## Solución

### Análisis Inicial: Procesador B vs. Procesador A

*   $F_m = 2/3$ (fracción mejorada por B)
*   $Acc_m = 2.5$ (aceleración de la fracción mejorada por B)
*   $F_{nm} = 1/3$ (fracción *no* mejorada por B)

Usando la Ley de Amdahl, la aceleración de B con respecto a A es:

$$
Acc_{B-A} = \frac{1}{(1 - F_m) + \frac{F_m}{Acc_m}} = \frac{1}{(1 - \frac{2}{3}) + \frac{\frac{2}{3}}{2.5}} = \frac{1}{\frac{1}{3} + \frac{2}{7.5}} = \frac{1}{\frac{1}{3} + \frac{4}{15}} = \frac{1}{\frac{5+4}{15}} = \frac{1}{\frac{9}{15}} = \frac{15}{9} = \frac{5}{3} \approx 1.667
$$

### Escenario C1: C mejora la fracción que ya mejoró B

En este caso, C duplica la velocidad de la fracción que B ya había mejorado. Esto significa que la aceleración total de esa fracción (con respecto a A) es ahora $2.5 \times 2 = 5$.

*   $F_m = 2/3$
*   $Acc_m = 5$

La aceleración de C1 con respecto a A es:

$$
Acc_{C1-A} = \frac{1}{(1 - F_m) + \frac{F_m}{Acc_m}} = \frac{1}{(1 - \frac{2}{3}) + \frac{\frac{2}{3}}{5}} = \frac{1}{\frac{1}{3} + \frac{2}{15}} = \frac{1}{\frac{5+2}{15}} = \frac{1}{\frac{7}{15}} = \frac{15}{7} \approx 2.143
$$

### Escenario C2: C mejora la fracción que *no* mejoró B

Aquí, C duplica la velocidad de la fracción que B *no* había mejorado. Esto significa que la fracción no mejorada por B ahora tiene una aceleración de 2 (con respecto a A).

*   $F_m = 2/3$ (fracción mejorada por B, sigue con aceleración 2.5)
*   La fracción *no* mejorada por B (1/3) ahora se mejora con un factor de 2.

La aceleración de C2 con respecto a A es:

$$
Acc_{C2-A} = \frac{1}{(1 - \frac{2}{3}) + \frac{\frac{2}{3}}{2.5} +  \frac{\frac{1}{3}}{2}} = \frac{1}{\frac{1}{3} + \frac{4}{15} + \frac{1}{6}} = \frac{1}{\frac{10+8+5}{30}} = \frac{1}{\frac{23}{30}} = \frac{30}{23} \approx 1.304
$$

### Aceleración de C con respecto a B (Recálculo de Fracciones)

Aquí es donde se pone interesante. No podemos simplemente usar las fracciones originales (1/3 y 2/3) porque ahora estamos comparando C con B, *no* con A. Necesitamos recalcular las fracciones con respecto al tiempo de ejecución de B.

1.  **Tiempo de ejecución de B:** Ya sabemos que $Acc_{B-A} = \frac{5}{3}$.  Por lo tanto, si el tiempo de ejecución de A es *N*, el tiempo de ejecución de B es $\frac{3}{5}N$.

2.  **Recálculo de fracciones:**
    *   **Fracción no mejorada por B:** Originalmente era 1/3 del tiempo de A.  Después de la mejora de B, esta fracción representa $\frac{\frac{1}{3}N}{\frac{3}{5}N} = \frac{5}{9}$ del tiempo de B.
    *   **Fracción mejorada por B:** Originalmente era 2/3 del tiempo de A. Después de la mejora de B, esta fracción representa $\frac{\frac{2}{3}N / 2.5}{\frac{3}{5}N} = \frac{\frac{4}{15}N}{\frac{9}{15}N} = \frac{4}{9}$ del tiempo de B.

Ahora tenemos las nuevas fracciones con respecto al tiempo de ejecución de B:

*   $F_{nm} = 5/9$ (fracción *no* mejorada por B)
*   $F_m = 4/9$ (fracción mejorada por B)

#### Aceleración de C1 con respecto a B

C1 duplica la velocidad de la fracción que B ya había mejorado (los 4/9).

$$
Acc_{C1-B} = \frac{1}{(1 - \frac{4}{9}) + \frac{\frac{4}{9}}{2}} = \frac{1}{\frac{5}{9} + \frac{2}{9}} = \frac{1}{\frac{7}{9}} = \frac{9}{7} \approx 1.286
$$

#### Aceleración de C2 con respecto a B

C2 duplica la velocidad de la fracción que B *no* había mejorado (los 5/9).

$$
Acc_{C2-B} = \frac{1}{(1 - \frac{5}{9}) + \frac{\frac{5}{9}}{2}} = \frac{1}{\frac{4}{9} + \frac{5}{18}} = \frac{1}{\frac{8+5}{18}} = \frac{1}{\frac{13}{18}} = \frac{18}{13} \approx 1.385
$$

### Verificación

Es importante verificar que la aceleración total sea consistente:

*   $Acc_{C1-A} = Acc_{C1-B} \times Acc_{B-A} \Rightarrow \frac{15}{7} = \frac{9}{7} \times \frac{5}{3} \Rightarrow \frac{15}{7} = \frac{45}{21} = \frac{15}{7}$ (Correcto)
*   $Acc_{C2-A} = Acc_{C2-B} \times Acc_{B-A} \Rightarrow \frac{30}{23} = \frac{18}{13} \times \frac{5}{3} \Rightarrow \frac{30}{23} = \frac{90}{39} = \frac{30}{13}$ (Incorrecto)

Hay un error en el cálculo de AccC2-A. Vamos a corregirlo:

AccC2-A = 1 / ((1/3)/2 + (2/3)/2.5) = 1 / (1/6 + 4/15) = 1 / (5/30 + 8/30) = 1 / (13/30) = 30/13

Ahora verificamos de nuevo:
*   $Acc_{C2-A} = Acc_{C2-B} \times Acc_{B-A} \Rightarrow \frac{30}{13} = \frac{18}{13} \times \frac{5}{3} \Rightarrow \frac{30}{13} = \frac{90}{39} = \frac{30}{13}$ (Correcto)

## Resumen de Resultados

*   $Acc_{B-A} = \frac{5}{3} \approx 1.667$
*   $Acc_{C1-A} = \frac{15}{7} \approx 2.143$
*   $Acc_{C2-A} = \frac{30}{13} \approx 2.308$
*   $Acc_{C1-B} = \frac{9}{7} \approx 1.286$
*   $Acc_{C2-B} = \frac{18}{13} \approx 1.385$

## Conclusiones

*   Este problema ilustra cómo la Ley de Amdahl se puede aplicar en escenarios con múltiples mejoras.
*   Es crucial recalcular las fracciones cuando se comparan las aceleraciones con respecto a un punto intermedio (como C con respecto a B).
*   La verificación de los resultados es esencial para asegurar la precisión de los cálculos.