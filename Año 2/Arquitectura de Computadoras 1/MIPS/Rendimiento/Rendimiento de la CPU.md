El rendimiento de la CPU es una medida de la rapidez con la que un procesador puede ejecutar un programa o una tarea. Una forma común de cuantificar el rendimiento es a través del **tiempo de CPU**, que representa el tiempo que la CPU dedica exclusivamente a ejecutar las instrucciones de un programa.

El tiempo de CPU no incluye el tiempo que el programa pasa esperando por operaciones de entrada/salida (E/S) u otros recursos del sistema. Se centra únicamente en el tiempo de procesamiento real.

### Factores que Afectan el Tiempo de CPU

El tiempo de CPU está influenciado por varios factores, incluyendo:

1.  **Recuento de Instrucciones (RI):** Es el número total de instrucciones que un programa ejecuta. Este número depende del programa en sí, del conjunto de instrucciones de la arquitectura (ISA), y del compilador utilizado.
2.  **Ciclos de Reloj de CPU por Programa:** Es el número de ciclos de reloj que la CPU necesita para ejecutar todas las instrucciones de un programa.
3.  **Ciclos Por Instrucción (CPI):** Es el número promedio de ciclos de reloj que se requieren para ejecutar una instrucción. Este valor depende de la arquitectura de la CPU y de la naturaleza de las instrucciones que se están ejecutando.
4.  **Frecuencia de Reloj:** Es la velocidad a la que la CPU ejecuta los ciclos de reloj, medida en Hertz (Hz).

### Relación entre RI, CPI, Frecuencia de Reloj y Tiempo de CPU

En lugar de simplemente contar los ciclos de reloj totales, podemos descomponer el tiempo de CPU en términos del recuento de instrucciones (RI) y el número medio de ciclos por instrucción (CPI).

**Fórmula para CPI:**

$$
\text{CPI} = \frac{\text{Ciclos de reloj de CPU por programa}}{\text{Recuento de instrucciones}}
$$

El CPI nos da una idea de la eficiencia con la que la CPU está ejecutando las instrucciones. Un CPI más bajo significa que, en promedio, cada instrucción tarda menos ciclos de reloj en completarse.

**Fórmula para el Tiempo de CPU (con RI y CPI):**

$$
\text{Tiempo de CPU} = \text{RI} \times \text{CPI} \times \text{Tiempo por ciclo de reloj}
$$

Como la frecuencia de reloj es el inverso del tiempo por ciclo de reloj, podemos reescribir la fórmula como:

$$
\text{Tiempo de CPU} = \frac{\text{RI} \times \text{CPI}}{\text{Frecuencia de reloj}}
$$

Esta fórmula es fundamental porque relaciona el tiempo de CPU con factores que dependen del programa (RI), de la arquitectura de la CPU (CPI), y de la tecnología del hardware (frecuencia de reloj).

**Unidades:**

$$
\frac{\text{segundos}}{\text{programa}} = \frac{\text{instrucciones}}{\text{programa}} \times \frac{\text{ciclos de reloj}}{\text{instrucciones}} \times \frac{\text{segundos}}{\text{ciclo de reloj}}
$$

### Factores que Influyen en RI y CPI

*   **Arquitectura a Nivel de Lenguaje de Máquina (ISA):** El conjunto de instrucciones de la arquitectura (ISA) afecta tanto al RI como al CPI. Una ISA más eficiente puede permitir que un programa se ejecute con menos instrucciones (menor RI) y/o que cada instrucción tarde menos ciclos en promedio (menor CPI).
*   **Tecnología de Compiladores:** Un buen compilador puede generar código más eficiente, lo que puede reducir el RI y/o el CPI.
*   **Organización de la CPU:** La forma en que la CPU está organizada internamente (por ejemplo, el uso de pipelines, caches, etc.) afecta al CPI.

### Resumen de Influencias

*   **Tecnología de Hardware (Frecuencia de Reloj):** Afecta directamente la velocidad a la que se ejecutan los ciclos de reloj.
*   **Organización de la CPU (CPI):** Afecta el número de ciclos necesarios por instrucción.
*   **Arquitectura a Nivel de Lenguaje de Máquina (ISA) (RI y CPI):** Afecta tanto el número de instrucciones necesarias como la eficiencia con la que se ejecutan.
*   **Tecnología de Compiladores (RI y CPI):** Afecta la eficiencia del código generado, influyendo en el número de instrucciones y en el CPI.


## Problema 3: Ley de Amdahl y Rendimiento de la CPU

## Planteamiento del Problema

Se tiene un procesador con un conjunto de instrucciones cuyas características se describen en la siguiente tabla:

| Tipo de Instrucción | Promedio de Uso | CPI (ALU) | CPI (MEM) |
| ------------------- | --------------- | --------- | --------- |
| Enteros             | 45%             | 1         | 3         |
| Punto Flotante      | 25%             | 6         | 3         |
| Load                | 15%             | 1         | 6         |
| Store               | 15%             | 1         | 6         |

Donde:

*   **Promedio de Uso:** El porcentaje de veces que se utiliza cada tipo de instrucción en un programa típico.
*   **CPI (ALU):** El número de ciclos de reloj promedio que tarda cada tipo de instrucción en la unidad aritmético-lógica (ALU).
*   **CPI (MEM):** El número de ciclos de reloj promedio que tarda cada tipo de instrucción en acceder a la memoria.

Se duplica la frecuencia del reloj del sistema, pero el tiempo de acceso a la memoria no cambia. Se pide calcular la mejora en el rendimiento utilizando la Ley de Amdahl.

## Solución

### 1. Calcular el CPI Promedio Original

Primero, necesitamos calcular el CPI promedio original del procesador. Para ello, ponderamos el CPI de cada tipo de instrucción por su promedio de uso:

$$
\text{CPI}_{original} = \sum (\text{Promedio de Uso} \times \text{CPI})
$$

Como cada instrucción tiene un componente ALU y un componente de acceso a memoria, calculamos el CPI total para cada tipo de instrucción sumando CPI(ALU) y CPI(MEM):

*   Enteros: CPI = 1 + 3 = 4
*   Punto Flotante: CPI = 6 + 3 = 9
*   Load: CPI = 1 + 6 = 7
*   Store: CPI = 1 + 6 = 7

Ahora, calculamos el CPI promedio original:

$$
\text{CPI}_{original} = (0.45 \times 4) + (0.25 \times 9) + (0.15 \times 7) + (0.15 \times 7) = 1.8 + 2.25 + 1.05 + 1.05 = 6.15
$$

### 2. Identificar la Fracción No Mejorada

El problema indica que el tiempo de acceso a la memoria *no* varía. Esto significa que la parte del tiempo de CPU que se dedica al acceso a la memoria *no* se beneficia del aumento en la frecuencia del reloj. Necesitamos calcular qué fracción del CPI original corresponde al acceso a la memoria.

Calculamos el CPI promedio para el acceso a la memoria:

$$
\text{CPI}_{MEM} = (0.45 \times 3) + (0.25 \times 3) + (0.15 \times 6) + (0.15 \times 6) = 1.35 + 0.75 + 0.9 + 0.9 = 3.9
$$

La fracción del tiempo original que *no* se mejora (debido al acceso a la memoria) es:

$$
F_{no\_mejorada} = \frac{\text{CPI}_{MEM}}{\text{CPI}_{original}} = \frac{3.9}{6.15} \approx 0.6341
$$

### 3. Aplicar la Ley de Amdahl

La Ley de Amdahl nos dice que la aceleración global está limitada por la fracción del trabajo que no se puede mejorar. En este caso, la parte que *sí* se mejora es la que corresponde a las operaciones de la ALU, que ahora se ejecutan al doble de velocidad.

*   $F_{no\_mejorada} \approx 0.6341$ (fracción no mejorada, acceso a memoria)
*   $F_{mejorada} = 1 - F_{no\_mejorada} = 1 - 0.6341 = 0.3659$ (fracción mejorada, operaciones ALU)
*   $Acc_{mejorada} = 2$ (la frecuencia del reloj se duplica, por lo que las operaciones ALU son 2 veces más rápidas)

La aceleración global ($Acc_G$) es:

$$
Acc_G = \frac{1}{(1 - F_{mejorada}) + \frac{F_{mejorada}}{Acc_{mejorada}}} = \frac{1}{F_{no\_mejorada} + \frac{F_{mejorada}}{Acc_{mejorada}}}
$$

$$
Acc_G = \frac{1}{0.6341 + \frac{0.3659}{2}} = \frac{1}{0.6341 + 0.18295} = \frac{1}{0.81705} \approx 1.224
$$

### 4. Calcular el Porcentaje de Mejora

El porcentaje de mejora se calcula como:

$$
\text{Porcentaje de Mejora} = (Acc_G - 1) \times 100\%
$$

$$
\text{Porcentaje de Mejora} = (1.224 - 1) \times 100\% = 0.224 \times 100\% = 22.4\%
$$

## Respuesta

El porcentaje de mejora en el rendimiento al duplicar la frecuencia del reloj, considerando que el tiempo de acceso a la memoria no varía, es aproximadamente del **22.4%**.