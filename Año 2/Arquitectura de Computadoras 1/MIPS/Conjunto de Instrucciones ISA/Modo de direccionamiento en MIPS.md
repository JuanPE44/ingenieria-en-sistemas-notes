Los modos de direccionamiento definen cómo las instrucciones MIPS especifican la ubicación de sus operandos (datos sobre los que operan o direcciones a las que saltan). MIPS, siendo una arquitectura RISC, tiene un conjunto relativamente simple y limitado de modos de direccionamiento.

## 1. Direccionamiento por Registro (Register Addressing)

*   **Descripción:** Los operandos se encuentran directamente en los registros especificados en la instrucción.
*   **Uso Típico:** Instrucciones aritmético-lógicas de tipo R (Register-type), como `add`, `sub`, `and`, `or`, `slt`.
*   **Formato (Tipo R):** `opcode | rs | rt | rd | shamt | funct`
    *   `rs` (source register), `rt` (source register), `rd` (destination register) especifican los registros que contienen los operandos o donde se guardará el resultado.
*   **Ejemplo:** `add $t0, $t1, $t2`
    *   Lee los valores de los registros `$t1` y `$t2`.
    *   Suma los valores.
    *   Escribe el resultado en el registro `$t0`.

## 2. Direccionamiento Inmediato (Immediate Addressing)

*   **Descripción:** Uno de los operandos es un valor constante (inmediato) que está codificado directamente dentro de la propia instrucción.
*   **Uso Típico:** Instrucciones aritmético-lógicas de tipo I (Immediate-type), como `addi`, `andi`, `ori`, `lui`. También se usa en cargas/almacenamientos y saltos condicionales.
*   **Formato (Tipo I - Aritmético):** `opcode | rs | rt | immediate`
    *   `rs` especifica un registro fuente.
    *   `rt` especifica el registro destino.
    *   `immediate` es el valor constante de 16 bits (con signo extendido para operaciones aritméticas).
*   **Ejemplo:** `addi $t0, $t1, 100`
    *   Lee el valor del registro `$t1`.
    *   Suma el valor inmediato `100` (extendido a 32 bits).
    *   Escribe el resultado en el registro `$t0`.

## 3. Direccionamiento Base o por Desplazamiento (Base Addressing / Displacement Addressing)

*   **Descripción:** Se utiliza para acceder a la memoria. La dirección de memoria efectiva se calcula sumando un valor constante (desplazamiento o *offset*) codificado en la instrucción al contenido de un registro base especificado en la instrucción.
*   **Uso Típico:** Instrucciones de carga (`lw`, `lb`, `lh`) y almacenamiento (`sw`, `sb`, `sh`).
*   **Formato (Tipo I - Load/Store):** `opcode | rs (base) | rt (dest/src) | offset`
    *   `rs` es el registro que contiene la dirección base.
    *   `rt` es el registro destino (para cargas) o fuente (para almacenamientos).
    *   `offset` es el valor inmediato de 16 bits (con signo) que se suma a la dirección base.
*   **Cálculo de Dirección:** `Dirección Efectiva = Contenido(Registro Base) + Offset`
*   **Ejemplo:** `lw $t0, 32($sp)`
    *   Calcula la dirección de memoria sumando `32` al contenido del registro `$sp` (stack pointer).
    *   Lee la palabra (32 bits) de esa dirección de memoria.
    *   Escribe el valor leído en el registro `$t0`.

## 4. Direccionamiento Relativo al PC (PC-Relative Addressing)

*   **Descripción:** La dirección destino de un salto condicional se calcula sumando un desplazamiento (codificado en la instrucción y multiplicado por 4) al valor actual del Contador de Programa (PC). El PC, en este contexto, apunta a la instrucción *siguiente* a la instrucción de salto.
*   **Uso Típico:** Instrucciones de salto condicional (`beq`, `bne`).
*   **Formato (Tipo I - Branch):** `opcode | rs | rt | offset`
    *   `rs` y `rt` son los registros a comparar.
    *   `offset` es el desplazamiento de 16 bits (con signo).
*   **Cálculo de Dirección Destino:** `Dirección Destino = PC_siguiente + (Offset << 2)`
    *   El `Offset` se multiplica por 4 (desplazamiento a la izquierda de 2 bits) porque las instrucciones MIPS están alineadas a palabras (4 bytes) y el offset cuenta palabras.
*   **Ejemplo:** `beq $t0, $t1, etiqueta`
    *   Compara los valores de `$t0` y `$t1`.
    *   Si son iguales, calcula la dirección de `etiqueta` relativa al PC y salta allí. El ensamblador calcula el `offset` necesario.

## 5. Direccionamiento Pseudo-Directo (Pseudo-direct Addressing)

*   **Descripción:** Se utiliza para saltos incondicionales (`j`, `jal`). La dirección destino se forma concatenando los 4 bits más significativos del PC actual con los 26 bits de la dirección objetivo codificados en la instrucción (multiplicados por 4).
*   **Uso Típico:** Instrucciones de salto incondicional (`j`, `jal`).
*   **Formato (Tipo J - Jump):** `opcode | address`
    *   `address` son 26 bits de la dirección destino.
*   **Cálculo de Dirección Destino:** `Dirección Destino = { PC_siguiente[31:28], address[25:0], 2'b00 }`
    *   Se toman los 4 bits superiores del PC de la siguiente instrucción.
    *   Se toman los 26 bits de la instrucción `j` o `jal`.
    *   Se añaden dos ceros al final (multiplicación por 4) para obtener la dirección de palabra.
*   **Ejemplo:** `j etiqueta`
    *   Calcula la dirección absoluta de `etiqueta` usando el modo pseudo-directo y salta incondicionalmente allí.

Estos son los modos de direccionamiento fundamentales en la arquitectura MIPS estándar. Permiten un diseño simple y eficiente, característico de RISC.