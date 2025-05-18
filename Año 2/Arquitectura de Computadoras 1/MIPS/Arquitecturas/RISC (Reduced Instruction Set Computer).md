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

Claro, aquí tienes algunos ejemplos de instrucciones en MIPS RISC, categorizadas por tipo:

**Aritméticas:**

*   `add $t0, $t1, $t2`: Suma el valor de los registros `$t1` y `$t2`, y guarda el resultado en `$t0`.
*   `sub $t0, $t1, $t2`: Resta el valor de `$t2` de `$t1`, y guarda el resultado en `$t0`.
*   `addi $t0, $t1, 10`: Suma el valor inmediato 10 al registro `$t1`, y guarda el resultado en `$t0`.
*   `mul $t0, $t1, $t2`: Multiplica el valor de los registros `$t1` y `$t2`, y guarda el resultado en `$t0`.
*   `div $t0, $t1, $t2`: Divide el valor de `$t1` entre `$t2`, y guarda el cociente en `$t0`.

**Lógicas:**

*   `and $t0, $t1, $t2`: Realiza una operación AND bit a bit entre `$t1` y `$t2`, y guarda el resultado en `$t0`.
*   `or $t0, $t1, $t2`: Realiza una operación OR bit a bit entre `$t1` y `$t2`, y guarda el resultado en `$t0`.
*   `nor $t0, $t1, $t2`: Realiza una operación NOR bit a bit entre `$t1` y `$t2`, y guarda el resultado en `$t0`.
*   `xor $t0, $t1, $t2`: Realiza una operación XOR bit a bit entre `$t1` y `$t2`, y guarda el resultado en `$t0`.
*   `andi $t0, $t1, 0xFF`: Realiza una operación AND bit a bit entre `$t1` y el valor inmediato 0xFF, y guarda el resultado en `$t0`.

**Transferencia de datos:**

*   `lw $t0, 0($t1)`: Carga una palabra (4 bytes) desde la dirección de memoria contenida en `$t1` + 0, y la guarda en `$t0`.
*   `sw $t0, 0($t1)`: Guarda el valor de `$t0` en la dirección de memoria contenida en `$t1` + 0.
*   `lb $t0, 0($t1)`: Carga un byte desde la dirección de memoria contenida en `$t1` + 0, y lo guarda en `$t0`.
*   `sb $t0, 0($t1)`: Guarda el byte menos significativo de `$t0` en la dirección de memoria contenida en `$t1` + 0.
*   `lui $t0, 0x1234`: Carga el valor inmediato 0x1234 en los 16 bits más significativos de `$t0`, y pone los 16 bits menos significativos a cero.
*   `move $t0, $t1`: Copia el valor de `$t1` a `$t0`. (En realidad, esto es un pseudoinstrucción que se traduce a `add $t0, $t1, $zero`).

**Control de flujo:**

*   `beq $t0, $t1, label`: Bifurca a la etiqueta `label` si el valor de `$t0` es igual al valor de `$t1`.
*   `bne $t0, $t1, label`: Bifurca a la etiqueta `label` si el valor de `$t0` no es igual al valor de `$t1`.
*   `blt $t0, $t1, label`: Bifurca a la etiqueta `label` si el valor de `$t0` es menor que el valor de `$t1` (con signo).
*   `bgt $t0, $t1, label`: Bifurca a la etiqueta `label` si el valor de `$t0` es mayor que el valor de `$t1` (con signo).
*   `ble $t0, $t1, label`: Bifurca a la etiqueta `label` si el valor de `$t0` es menor o igual que el valor de `$t1` (con signo).
*   `bge $t0, $t1, label`: Bifurca a la etiqueta `label` si el valor de `$t0` es mayor o igual que el valor de `$t1` (con signo).
*   `j label`: Salta incondicionalmente a la etiqueta `label`.
*   `jal label`: Salta a la etiqueta `label` y guarda la dirección de retorno en el registro `$ra` (para llamadas a funciones).
*   `jr $ra`: Salta a la dirección contenida en el registro `$ra` (para retornar de una función).

**Otras:**

*   `syscall`: Realiza una llamada al sistema operativo. El servicio solicitado se especifica en el registro `$v0`.
*   `nop`: No hace nada. (Se utiliza para relleno o para evitar riesgos de hardware).

**Ejemplo de un pequeño programa:**

```assembly
# Suma dos números y guarda el resultado

.data
    num1: .word 5
    num2: .word 10
    result: .word 0

.text
.globl main

main:
    # Cargar los números en registros
    lw $t0, num1
    lw $t1, num2

    # Sumar los números
    add $t2, $t0, $t1

    # Guardar el resultado en memoria
    sw $t2, result

    # Terminar el programa (syscall para exit)
    li $v0, 10  # Código para exit
    syscall
```

Este es un ejemplo básico.  MIPS tiene muchas más instrucciones y opciones.  Si tienes alguna pregunta específica sobre alguna instrucción o cómo realizar una tarea en MIPS, no dudes en preguntar.
