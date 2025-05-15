El rendimiento de un procesador se refiere a su capacidad para ejecutar tareas. Se puede medir de diferentes maneras, principalmente enfocándose en el tiempo que tarda en completar una tarea o en la cantidad de trabajo que puede realizar en un tiempo determinado.

## Métricas de Rendimiento

Existen dos métricas principales para evaluar el rendimiento:

### 1. Tiempo de Respuesta / Tiempo de Ejecución / Latencia

*   **Definición:** Es el tiempo total transcurrido desde que una tarea comienza hasta que finaliza.
*   **Interpretación:** Una computadora se considera más rápida si puede ejecutar un programa específico en menos tiempo. Menor tiempo de respuesta implica mayor rendimiento para esa tarea específica.
*   **Ejemplo:** Si el procesador A tarda 10 segundos en ejecutar un programa y el procesador B tarda 15 segundos, el procesador A tiene mejor tiempo de respuesta para ese programa.

### 2. Incremento de Productividad / Throughput / Ancho de Banda

*   **Definición:** Es la cantidad total de trabajo (o número de tareas) que se puede realizar en un período de tiempo determinado.
*   **Interpretación:** Un mayor throughput significa que el sistema puede manejar más tareas simultáneamente o completar más trabajo en el mismo lapso.
*   **Ejemplo:** Si el sistema A puede procesar 100 transacciones por segundo y el sistema B puede procesar 80, el sistema A tiene mayor throughput.

## Comparación de Rendimiento Relativo

Cuando se comparan dos máquinas, A y B, generalmente se analiza su velocidad relativa para una tarea específica.

*   Si decimos que **"A es más rápida que B"**, significa que el **tiempo de ejecución de A es menor que el tiempo de ejecución de B** para esa tarea.

La mejora relativa del rendimiento de A sobre B se puede expresar como la relación de sus tiempos de ejecución:

$$
\frac{\text{Tiempo de ejecución de B}}{\text{Tiempo de ejecución de A}}
$$

Si A es un $n\%$ más rápida que B, la relación se puede escribir como:

$$
\frac{\text{Tiempo de ejecución de B}}{\text{Tiempo de ejecución de A}} = 1 + \frac{n}{100}
$$

## Relación entre Tiempo de Ejecución y Rendimiento

Se asume que el rendimiento es inversamente proporcional al tiempo de ejecución:

$$ \text{Tiempo de ejecución} = \frac{1}{\text{Rendimiento}} $$

Por lo tanto, la comparación de rendimiento también se puede expresar en términos de rendimiento. Sustituyendo la relación inversa en la comparación de tiempos de ejecución:

$$
\frac{\text{Tiempo de ejecución de B}}{\text{Tiempo de ejecución de A}} = \frac{\frac{1}{\text{Rendimiento de B}}}{\frac{1}{\text{Rendimiento de A}}} = \frac{\text{Rendimiento de A}}{\text{Rendimiento de B}}
$$

Combinando esto con la fórmula del porcentaje de mejora:

$$
\frac{\text{Rendimiento de A}}{\text{Rendimiento de B}} = 1 + \frac{n}{100}
$$

Esto significa que si A es un $n\%$ más rápida que B, su rendimiento es $(1 + n/100)$ veces el rendimiento de B.