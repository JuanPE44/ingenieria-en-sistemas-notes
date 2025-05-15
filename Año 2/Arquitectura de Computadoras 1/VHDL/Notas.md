c) Analice la latencia involucrada en la ejecución de los dos programas.
cantidad ciclos desde que reset = 0: 29

Program1 latencia => 29 Ciclos x TiempoCiclo
Program2 latencia => 29 Ciclos x TiempoCiclo




## Cálculo de Latencia en un Procesador MIPS Uniciclo

## ¿Qué es la Latencia?

En el contexto de la ejecución de un programa en un procesador, la **latencia** se refiere al tiempo total que tarda el programa en completarse, desde que comienza la primera instrucción hasta que finaliza la última.

## Procesador Uniciclo

La característica clave de un procesador **uniciclo** es que cada instrucción, sin importar su complejidad (sea `add`, `lw`, `sw`, `beq`, etc.), tarda exactamente **un ciclo de reloj** en ejecutarse por completo.

## Cálculo de la Latencia

Dado que cada instrucción toma un ciclo de reloj, el cálculo de la latencia total es relativamente sencillo:

1.  **Determina el Número Total de Instrucciones Ejecutadas:**
    *   Necesitas saber cuántas instrucciones ejecuta tu programa en total. Esto no es necesariamente el número de líneas de código, ya que los bucles y saltos pueden hacer que algunas instrucciones se ejecuten múltiples veces y otras ninguna.
    *   La forma más fiable de obtener este número es a través de la propia simulación en EDA Playground. A menudo, las herramientas de simulación o los testbenches pueden configurarse para contar el número de instrucciones ejecutadas. Si no, podrías necesitar analizar el flujo de ejecución de tu código MIPS.

2.  **Determina el Periodo del Ciclo de Reloj (Clock Cycle Time):**
    *   Este es el tiempo que dura un único ciclo de reloj. Se mide en unidades de tiempo (por ejemplo, nanosegundos - ns, picosegundos - ps).
    *   Este valor lo defines tú o está definido en la configuración de tu simulación o en el testbench dentro de EDA Playground. Busca la definición de la señal de reloj (`clk`) y su periodo. Por ejemplo, si el reloj tiene una frecuencia de 100 MHz, el periodo es 1 / (100 * 10^6 Hz) = 10 ns.

3.  **Calcula la Latencia Total:**
    *   La fórmula es:
        ```
        Latencia = (Número Total de Instrucciones Ejecutadas) * (Periodo del Ciclo de Reloj)
        ```

## Ejemplo

Supongamos que:

*   Tu Programa 1 ejecuta un total de **150 instrucciones**.
*   Tu Programa 2 ejecuta un total de **220 instrucciones**.
*   El periodo del ciclo de reloj de tu procesador simulado es de **10 nanosegundos (ns)**.

Entonces:

*   **Latencia Programa 1** = 150 instrucciones * 10 ns/instrucción = 1500 ns
*   **Latencia Programa 2** = 220 instrucciones * 10 ns/instrucción = 2200 ns

## Análisis

Para analizar la latencia involucrada en la ejecución de los dos programas, simplemente sigue estos pasos para cada uno de ellos y compara los resultados. El programa con la latencia más alta es el que tarda más tiempo en ejecutarse en el procesador uniciclo simulado.

**En resumen:** Para un procesador uniciclo, la latencia depende directamente de cuántas instrucciones se ejecutan y de la velocidad (periodo) del reloj del sistema.

banco refistro flanco descendente
ascendente memoria datos