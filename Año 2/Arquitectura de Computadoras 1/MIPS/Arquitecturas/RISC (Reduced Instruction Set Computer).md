RISC es un tipo de diseño de microprocesadores que se enfoca en tener un conjunto de instrucciones **simple y reducido**. La filosofía detrás de RISC es que al simplificar las instrucciones que el procesador puede ejecutar directamente en hardware, se puede lograr un rendimiento más alto, menor consumo de energía y un diseño de chip más sencillo.

## Características Principales

*   **Conjunto de Instrucciones Reducido:**
    *   Contiene un número relativamente pequeño de instrucciones.
    *   Las instrucciones son de formato fijo y simples en su operación.
*   **Ejecución en un Ciclo de Reloj (Ideal):**
    *   La mayoría de las instrucciones están diseñadas para completarse en un solo ciclo de reloj, lo que facilita el [[Pipelining (Segmentación de Cauce)]].
*   **Arquitectura Carga/Almacenamiento (Load/Store):**
    *   Las únicas instrucciones que acceden a la memoria son las de carga (`LOAD`) y almacenamiento (`STORE`).
    *   Las operaciones aritméticas y lógicas solo operan sobre registros internos del procesador.
*   **Gran Número de Registros:**
    *   Disponen de una cantidad significativa de registros de propósito general para minimizar las interacciones con la memoria principal, que es más lenta.
*   **Pipelining:**
    *   El diseño simple de las instrucciones facilita la implementación de técnicas de , [[Pipelining (Segmentación de Cauce)]] donde múltiples instrucciones se ejecutan de forma solapada en diferentes etapas.
*   **Énfasis en el Compilador:**
    *   Se depende más del compilador para optimizar el código y traducir operaciones complejas en secuencias de instrucciones simples RISC.

## Ventajas

*   **Mayor Rendimiento:** La simplicidad permite velocidades de reloj más altas y un pipelining más eficiente.
*   **Menor Consumo de Energía:** Menos complejidad en el hardware se traduce generalmente en menor consumo.
*   **Diseño más Sencillo:** Facilita el diseño, la verificación y la fabricación de los chips.

## Desventajas

*   **Mayor Densidad de Código:** Se pueden necesitar más instrucciones simples para realizar la misma tarea que una sola instrucción compleja en [[CISC (Complex Instruction Set Computer)]].
*   **Dependencia del Compilador:** La eficiencia del código generado depende en gran medida de la calidad del compilador.

## Ejemplos

Arquitecturas comunes basadas en RISC incluyen ARM (ampliamente usada en dispositivos móviles), MIPS, RISC-V (código abierto) y PowerPC.