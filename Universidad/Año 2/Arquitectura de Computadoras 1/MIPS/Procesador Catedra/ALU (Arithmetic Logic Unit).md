La ALU es el corazón computacional del procesador. Es un circuito combinacional complejo diseñado para realizar una variedad de operaciones aritméticas y lógicas sobre datos. Piensa en ella como la calculadora avanzada del microprocesador, capaz de ejecutar las operaciones fundamentales que requieren las instrucciones.
Desglosemos sus características y funcionamiento:

1.  **Realiza operaciones aritméticas y lógicas sobre dos operandos de entrada de 32 bits:**
    *   **Entradas de Datos:** La ALU típicamente tiene dos entradas principales para los operandos sobre los que va a trabajar, ambas de 32 bits en nuestro caso MIPS.
        *   **Entrada A:** Generalmente conectada a la salida `Read data 1` del Banco de Registros (el valor del registro `rs`).
        *   **Entrada B:** Esta entrada es más versátil. Necesita poder recibir datos de dos fuentes diferentes, por lo que hay un **Multiplexor (Mux)** justo antes de esta entrada (controlado por la señal `ALUSrc`):
            *   Fuente 1: La salida `Read data 2` del Banco de Registros (el valor del registro `rt`). Usado por instrucciones Tipo R y `beq`.
            *   Fuente 2: El valor inmediato de 16 bits de la instrucción, extendido a 32 bits (normalmente con extensión de signo). Usado por instrucciones como `lw`, `sw`, `addi`.
    *   **Operaciones Soportadas:** Debe ser capaz de realizar, como mínimo:
        *   **Aritméticas:** Suma (para `add`, `addi`, cálculo de dirección en `lw`/`sw`), Resta (para `sub`, `beq`).
        *   **Lógicas:** AND (para `and`, `andi`), OR (para `or`, `ori`).
        *   **Comparación:** Set on Less Than (`slt`, `slti`). A menudo, la resta se usa internamente para verificar igualdad (`beq`).

2.  **La operación específica es seleccionada por una señal de control (ALUControl):**
    *   **Entrada de Control:** La ALU no decide por sí misma qué operación hacer. Recibe una señal de control de varios bits (llamada `ALUControl` o similar) que le indica cuál de sus funciones ejecutar (ej. '0010' para suma, '0110' para resta, '0000' para AND, '0001' para OR, '0111' para SLT, etc.).
    *   **Origen de ALUControl:** Esta señal *no* es directamente el `opcode` o el `funct` de la instrucción. Se genera mediante una pequeña unidad lógica separada, a menudo llamada **ALU Control Unit**.
        *   La ALU Control Unit recibe como entrada principal el `opcode` de la instrucción.
        *   Para algunas instrucciones (como `lw`, `sw`, `beq`), el `opcode` es suficiente para determinar la operación de la ALU (suma para `lw`/`sw`, resta para `beq`).
        *   Para las instrucciones de Tipo R (que suelen tener un `opcode` de `000000`), la ALU Control Unit también necesita mirar el campo `funct` de la instrucción para determinar la operación específica (`add`, `sub`, `and`, `or`, `slt`, etc.).
        *   Basándose en estas entradas (`opcode` y a veces `funct`), la ALU Control Unit genera el código `ALUControl` correcto que se envía a la ALU principal.

3.  **Genera flags, como el flag 'Zero':**
    *   **Salida de Resultado:** La salida principal de la ALU es el resultado de 32 bits de la operación realizada (`ALUResult`).
    *   **Salidas de Estado (Flags):** Además del resultado, la ALU genera señales de estado que proporcionan información adicional sobre el resultado. La más importante para nuestro conjunto de instrucciones básico es:
        *   **Flag `Zero`:** Es una señal de 1 bit. Se activa (se pone a '1') si y solo si el `ALUResult` de 32 bits es exactamente cero. Si el resultado es cualquier otro valor, el flag `Zero` se desactiva ('0').
        *   **Importancia para `beq`:** La instrucción `beq rs, rt, label` (Branch on Equal) utiliza este flag directamente. La ALU realiza la operación `rs - rt`. Si los registros son iguales, el resultado de la resta será cero, el flag `Zero` se activará, y la lógica de control sabrá que debe tomar el salto (actualizar el PC con la dirección de destino del branch). Si los registros son diferentes, el resultado no será cero, el flag `Zero` estará en '0', y el salto no se tomará (el PC se actualizará a `PC + 4`).
    *   **Otros Flags (Posibles):** ALUs más complejas pueden generar otros flags como Carry (acarreo), Overflow (desbordamiento aritmético), Negative (signo), etc., pero para este conjunto básico, `Zero` es el crucial.

4.  **Usos Clave (Ejemplos concretos):**
    *   **Instrucciones Tipo R (`add`, `sub`, `and`, `or`, `slt`):**
        *   Operandos: `Registros[rs]` y `Registros[rt]`.
        *   `ALUControl`: Determinado por el campo `funct`.
        *   `ALUResult`: Es el resultado final de la operación, que se escribirá de vuelta en `Registros[rd]`.
    *   **Instrucciones `lw` y `sw` (Load/Store):**
        *   Propósito: Calcular la dirección de memoria efectiva.
        *   Operandos: `Registros[rs]` (dirección base) y `sign_extend(immediate)` (offset).
        *   `ALUControl`: Se configura para realizar una **suma**.
        *   `ALUResult`: Contiene la dirección de memoria calculada, que se enviará a la `Data Memory`.
    *   **Instrucción `beq` (Branch on Equal):**
        *   Propósito: Comparar si dos registros son iguales.
        *   Operandos: `Registros[rs]` y `Registros[rt]`.
        *   `ALUControl`: Se configura para realizar una **resta**.
        *   Salida Clave: El **flag `Zero`**. El `ALUResult` (la diferencia) no se usa directamente, pero su valor determina el estado del flag `Zero`, que a su vez controla si el salto se toma o no.

**En Resumen:**

La ALU es el componente ejecutor central para una amplia gama de instrucciones. Actúa como un "trabajador" versátil que toma dos números y una orden (`ALUControl`), realiza la operación solicitada, produce un resultado y, crucialmente para el control de flujo, informa si ese resultado fue cero. Su flexibilidad para realizar diferentes operaciones (suma, resta, lógica, comparación) según las señales de control la hace indispensable en el datapath.