El **Pipelining** es una técnica de implementación utilizada en los procesadores para **aumentar el rendimiento** (throughput) al permitir que **múltiples instrucciones se ejecuten de forma solapada**. En lugar de esperar a que una instrucción complete todas sus fases antes de comenzar la siguiente, el pipeline divide la ejecución de una instrucción en varias **etapas** o **fases** independientes.

Piensa en una **línea de ensamblaje**:
*   **Sin pipeline:** Se construye un coche completo antes de empezar el siguiente.
*   **Con pipeline:** Hay varias estaciones (etapas). Mientras un coche está en la estación de pintura (una etapa), otro coche puede estar en la estación de montaje del motor (otra etapa), y un tercero puede estar empezando en la estación de chasis (etapa inicial). Varios coches están en proceso simultáneamente.

De manera similar, en un procesador con pipeline, diferentes instrucciones pueden estar en diferentes etapas de su ejecución al mismo tiempo.

## Etapas Típicas del Pipeline MIPS (5 Etapas Clásico)

El pipeline MIPS clásico se divide comúnmente en 5 etapas:

1.  **IF (Instruction Fetch - Búsqueda de Instrucción):**
    *   Se lee la siguiente instrucción de la memoria de instrucciones, utilizando la dirección almacenada en el Contador de Programa (PC).
    *   Se incrementa el PC para apuntar a la siguiente instrucción (provisionalmente).

2.  **ID (Instruction Decode & Register Fetch - Decodificación y Búsqueda en Registros):**
    *   Se decodifica la instrucción leída en IF para determinar qué operación realizar.
    *   Se leen los valores de los registros fuente necesarios desde el banco de registros.
    *   Se podría empezar a calcular la dirección de salto para branches/jumps.

3.  **EX (Execute - Ejecución):**
    *   Se realiza la operación principal de la instrucción.
    *   Si es una instrucción aritmético-lógica (como `add`, `sub`, `and`), la ALU (Unidad Aritmético-Lógica) realiza el cálculo.
    *   Si es una instrucción de carga/almacenamiento (`lw`, `sw`), la ALU calcula la dirección efectiva de memoria (base + desplazamiento).
    *   Si es una instrucción de salto (branch), se evalúa la condición y se calcula la dirección de destino si el salto se toma.

4.  **MEM (Memory Access - Acceso a Memoria):**
    *   Esta etapa interactúa con la memoria de datos.
    *   Si es una instrucción `lw` (load word), se lee el dato desde la dirección calculada en EX.
    *   Si es una instrucción `sw` (store word), se escribe el dato (leído del registro en ID) en la dirección calculada en EX.
    *   Las instrucciones aritmético-lógicas o de salto generalmente no hacen nada significativo en esta etapa.

5.  **WB (Write Back - Escritura en Registro):**
    *   El resultado de la instrucción se escribe de nuevo en el banco de registros.
    *   Para instrucciones aritmético-lógicas, es el resultado de la ALU (de la etapa EX).
    *   Para instrucciones `lw`, es el dato leído de la memoria (en la etapa MEM).

## Funcionamiento y Beneficios

En un ciclo de reloj ideal, cada etapa del pipeline está trabajando en una instrucción diferente:

| Ciclo Reloj | 1    | 2    | 3    | 4    | 5    | 6    | 7    |
| :---------- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Instr 1     | IF   | ID   | EX   | MEM  | WB   |      |      |
| Instr 2     |      | IF   | ID   | EX   | MEM  | WB   |      |
| Instr 3     |      |      | IF   | ID   | EX   | MEM  | WB   |
| Instr 4     |      |      |      | IF   | ID   | EX   | MEM  |
| Instr 5     |      |      |      |      | IF   | ID   | EX   |

*   **Mayor Throughput:** Aunque una instrucción individual sigue tardando 5 ciclos en completarse (latencia), en el estado ideal, una nueva instrucción *termina* en cada ciclo de reloj. Esto aumenta significativamente la cantidad de instrucciones completadas por unidad de tiempo.
*   **Mejor Utilización del Hardware:** Las diferentes unidades funcionales del procesador (unidad de búsqueda, ALU, unidad de memoria) están ocupadas trabajando en diferentes instrucciones simultáneamente.

## Desafíos del Pipelining: Hazards (Riesgos)

El funcionamiento ideal se ve interrumpido por **hazards**: situaciones que impiden que la siguiente instrucción se ejecute en el siguiente ciclo de reloj. Los principales tipos son:

1.  **Structural Hazards (Riesgos Estructurales):** El hardware no puede soportar la combinación de instrucciones que se quieren ejecutar en el mismo ciclo (ej., si solo hubiera una memoria para datos e instrucciones - Arquitectura Von Neumann - habría conflicto entre IF y MEM). La Arquitectura Harvard de MIPS ayuda a evitar muchos de estos.
2.  **Data Hazards (Riesgos de Datos):** Una instrucción necesita el resultado de una instrucción anterior que aún no ha completado la etapa WB.
    *   Ejemplo: `add $t0, $s0, $s1` seguido de `sub $t1, $t0, $s2`. La `sub` necesita el valor de `$t0` antes de que `add` lo escriba en WB.
    *   Soluciones: **Stalling** (detener el pipeline) o **Forwarding/Bypassing** (enviar el resultado directamente desde donde se produce - ej., salida de la ALU en EX - a donde se necesita - ej., entrada de la ALU en EX para la siguiente instrucción).
3.  **Control Hazards (Riesgos de Control):** Ocurren con instrucciones de salto (branches, jumps). El procesador no sabe qué instrucción buscar (la siguiente secuencial o la del destino del salto) hasta que la instrucción de salto se resuelve (a menudo en ID o EX). Mientras tanto, ya ha empezado a buscar instrucciones secuenciales que podrían ser incorrectas.
    *   Soluciones: **Stalling**, **Branch Prediction** (adivinar si el salto se tomará o no), **Delayed Branch** (ejecutar la instrucción que *sigue inmediatamente* al salto, independientemente de si se toma o no; MIPS utiliza esto, el compilador debe llenar ese "slot" con algo útil o un NOP).

En resumen, el pipelining es una técnica fundamental para el alto rendimiento de MIPS, permitiendo la ejecución solapada de instrucciones dividiéndolas en etapas, aunque requiere manejar cuidadosamente los hazards para mantener la eficiencia.