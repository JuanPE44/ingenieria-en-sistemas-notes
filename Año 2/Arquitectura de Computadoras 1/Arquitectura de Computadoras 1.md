## **Tareas pendientes**
- [ ] TP Riesgos
- [ ] (3) VHDL
- [ ] Resumenes

# **Parcial:** 10/06/2025

# **Recuperatorio:** 24/06/2025

## ¿Para qué le sirve a un programador saber Arquitectura de Computadoras?

Se puede responder fácilmente con otra pregunta: los programadores programan computadoras, ¿verdad? ¿Cómo trabajar sobre algo cuyas bases se desconocen? Los programadores de los años 60' sabían fundamentalmente que disponían de escasa memoria y desarrollaban sus programas en consecuencia. Ahora, para desarrollar programas y sistemas _competitivos_ hay que saber fundamentos de organización de computadoras, específicamente jerarquía de memoria y procesamiento paralelo.

---
[[MIPS]]

## 1. UNIDAD ARITMÉTICO-LÓGICA

- ##### Sumador binario sin y con signo
	- Generación y propagación del acarreo. Sumador Ripple-carry
	- Sumador carry look-ahead

- ##### Multiplicación binaria sin y con signo
	- Multiplicadores celulares
	    - Algoritmo y celda básica ripple-carry
	    - Algoritmo y celda básica carry-save
	- Multiplicador secuencial shift and add.

- ##### División binaria sin y con signo
	- División con restauración.
	- División sin restauración.

---

## 2. ARQUITECTURA DE ORDENADORES. EL PAPEL DEL RENDIMIENTO

- ##### [Introducción](https://moodle.exa.unicen.edu.ar/mod/page/view.php?id=83361 "Introducción").

- ##### Arquitectura (clásica) de un ordenador
	- Arquitecturas Von-Neumann y Harvard
	- Arquitecturas CISC y RISC

- ##### El rendimiento del sistema
	- Unidades de medida
	- Comparativa de rendimientos
	- Mejorar el rendimiento. La ley de Amdahl

- ##### Ejemplo de la evolución en el rendimiento de los microprocesadores

---

## 3. SEGMENTACIÓN EN LA EJECUCIÓN DE INSTRUCCIONES

- ##### Fundamentos de diseño de un procesador
	- El repertorio de instrucciones
	- Ciclo único y multiciclo
	- Ruta de datos y control

- ##### La técnica de la segmentación
	- Funcionamiento ideal
	- Conceptos asociados: Latencia y Rendimiento (Throughput)

- ##### Diseño de un procesador con segmentado (Pipeline)

- ##### Limitaciones del cauce de instrucciones segmentado
	- Causas que producen perdidas de rendimiento por detención del pipeline.
	    - Conflictos por limitaciones estructurales
	    - Conflictos por riesgos de control
	    - Conflictos por dependencia de datos
	- Técnicas para evitar detenciones
	     - Adelantamiento de datos
	    - Predicción de saltos

---

## 4. ORGANIZACIÓN Y ESTRUCTURA DE LA MEMORIA: CACHÉS Y MEMORIA VIRTUAL

### 4.1. Jerarquía de memoria

- ##### Principios básicos de la memoria caché
	- Caché de varios niveles 
	- Organizaciones: Completamente asociativa, Correspondencia directa y Asociativa por vías
	- Esquemas de funcionamiento. Escritura directa (Write Through) con asignación en escritura (Fetch on-write) y sin asignación en escritura. Post-escritura o escritura diferida
	- Algoritmos de sustitución
	- Coherencia caché
	- Ejemplos de cachés

- ##### La Memoria virtual
	- Funcionamiento de la memoria virtual: paginación, segmentación, segmentos paginados
	- Traducción de direcciones virtuales a direcciones físicas o reales
	- Unidad de gestión de la memoria (MMU)
	- Buffer de traducción anticipada (TLB)

- ##### Integración del sistema de memoria: el TLB y la caché
	-  Sistema con caché virtual o caché real

---

## 5. SISTEMAS DE ENTRADA SALIDA E INTERCONEXIÓN
-  Medidas de [rendimiento de sistemas](https://moodle.exa.unicen.edu.ar/mod/resource/view.php?id=85936 "Rendimiento de Sistemas") de entrada salida
-  Buses
- Diseño de sistemas de E/S
- Casos Reales


# Notas

### Segmentación (Pipelining) en Arquitectura de Computadoras (MIPS)

La **segmentación** o **pipeline** es una técnica de implementación de procesadores que permite la ejecución simultánea de múltiples instrucciones, mejorando el rendimiento. En un procesador MIPS estándar, el pipeline se divide comúnmente en **5 etapas**. Esto significa que, idealmente, hay 5 instrucciones ejecutándose al mismo tiempo, cada una en una etapa diferente del proceso.

Imagina el flujo de instrucciones como una "tubería":
*   Mientras una instrucción `i` está en la etapa de **Búsqueda de Instrucción (IF)**,
*   la instrucción anterior `i-1` está avanzando a la etapa de **Decodificación y Lectura de Registros (ID)**,
*   la instrucción `i-2` está en la etapa de **Ejecución (EX)** en la ALU,
*   la instrucción `i-3` está en la etapa de **Acceso a Memoria (MEM)**,
*   y la instrucción `i-4` está en la etapa de **Escritura en Banco de Registros (WB)**.

Cada etapa realiza una parte específica del procesamiento de una instrucción.

#### Sincronización y "Wave Pipelining"

Implementar un pipeline no es sencillo debido a la necesidad de una **sincronización precisa**. Si está mal implementado, las instrucciones pueden desfasarse. El concepto de "**wave pipelining**" describe cómo las instrucciones avanzan como "olas" a través de las etapas, lo que requiere que todo esté perfectamente sincronizado y balanceado.

Para lograr esta sincronización, se utilizan **registros de segmentación** (o registros de pipeline) entre cada etapa. La salida de una etapa se almacena en un registro de segmentación, y la etapa siguiente toma sus entradas de este registro.
*   El **clock** del procesador determina la velocidad del pipeline.
*   Cada etapa idealmente debe tardar un ciclo de clock.
*   El **tiempo del ciclo de clock (Tclock)** del pipeline está determinado por la duración de la **etapa más lenta**.
*   Con cada flanco del clock, todos los registros de segmentación se actualizan simultáneamente.

#### Comparación: Uniciclo vs. Segmentado

| Característica | Uniciclo                                  | Segmentado (Ideal)                        |
| :------------- | :---------------------------------------- | :---------------------------------------- |
| CPI            | 1 (cada instrucción toma 1 ciclo largo) | 1 (una instrucción finaliza por ciclo corto) |
| Tclock         | Suma de los tiempos de todas las etapas   | Tiempo de la etapa más larga              |

La ventaja principal es que **$T_{clk\_pipe} < T_{clk\_uniciclo}$**, lo que lleva a una mayor tasa de finalización de instrucciones (throughput).

#### Etapas del Pipeline MIPS

1.  **IF (Instruction Fetch):** Busca la instrucción en memoria.
2.  **ID (Instruction Decode):** Decodifica la instrucción, lee operandos del banco de registros. La unidad de control genera las señales.
3.  **EX (Execute):** La ALU realiza la operación aritmética/lógica o calcula la dirección de salto.
4.  **MEM (Memory Access):** Lee o escribe datos en la memoria de datos.
5.  **WB (Write Back):** Escribe el resultado de la operación (de la ALU o de memoria) en el banco de registros.

#### Registros de Segmentación

Estos registros almacenan la información necesaria para la siguiente etapa:
*   **IF/ID:** Almacena la instrucción leída y PC+4. (Tus notas mencionan 2 registros, probablemente para estos dos valores).
*   **ID/EX:** Almacena PC+4, valores leídos de los registros fuente, el inmediato extendido, los números de los registros destino (Rt, Rd), y las señales de control generadas en ID. (Tus notas mencionan 4 registros, lo que podría corresponder a los datos principales como operandos, inmediato y señales de control empaquetadas).
*   **EX/MEM:** Almacena el resultado de la ALU, el valor a escribir en memoria (si es un `sw`), la señal Zero (para saltos), la dirección de salto calculada (si es un salto), y el número del registro destino (Rd) junto con las señales de control para MEM y WB.
*   **MEM/WB:** Almacena el dato leído de memoria (si es un `lw`), el resultado de la ALU (si no hubo acceso a memoria o para pasarlo), y el número del registro destino (Rd) junto con la señal de control para WB.

#### Problemas y Conflictos (Riesgos)

La segmentación introduce complejidades, principalmente debido a las dependencias entre instrucciones. Estos se conocen como **riesgos**.

1.  **Riesgos de Control (Ejemplo con `beq`):**
    ```assembly
    beq $1, $2, L  // Etapa ID/EX: Se evalúa la condición y se calcula la dirección de L
    add $2, $3, $4 // Etapa IF: Ya se buscó, aunque el beq aún no decidió si saltar
    sub $10, $5, $2
    ...
    L: ...
    ```
    La instrucción `add` (y `sub`) entra al pipeline antes de que se sepa si el salto `beq` se tomará o no. Si se toma el salto, las instrucciones que ya ingresaron deben ser descartadas.

2.  **Riesgos de Datos (Ejemplo con `lw` y `add`):**
    Considera la secuencia:
    ```assembly
    lw  $2, 32($5)   // Carga un valor de memoria en $2
    add $12, $2, $3  // Usa el valor de $2
    ```
    *   La instrucción `lw` estará en la etapa MEM/WB cuando el valor leído de memoria esté disponible para escribir en `$2`.
    *   La instrucción `add` estará en la etapa ID/EX, necesitando el valor de `$2` que aún no ha sido actualizado por `lw`.

    **Solución (parcialmente indicada en tus notas):** Para asegurar que la instrucción correcta (`add`) escriba en el registro correcto (`$12`) y no haya confusión con el registro destino de `lw` (`$2`), el **número del registro de escritura (Rd o Rt)** se propaga a través de los registros del pipeline junto con los datos y señales de control. Esto permite que la etapa WB sepa a qué registro escribir. Para resolver la dependencia de datos en sí (que `add` use el valor correcto de `lw`), se requieren técnicas como el **adelantamiento de datos (forwarding/bypassing)** o la inserción de paradas (stalls).

#### Señales de Control en el Pipeline

*   Las señales de control para una instrucción se **determinan en la etapa de decodificación (ID)**.
*   Estos valores de señales de control son los mismos que se calcularían en un procesador uniciclo.
*   Para asegurar que cada instrucción utilice sus propias señales de control en la etapa correcta, estas señales **se propagan a través de los registros de segmentación** junto con los datos de la instrucción. Por ejemplo, las señales para la ALU (generadas en ID) se usan en EX, las señales para el acceso a memoria se usan en MEM, y las señales para la escritura en registros se usan en WB.

