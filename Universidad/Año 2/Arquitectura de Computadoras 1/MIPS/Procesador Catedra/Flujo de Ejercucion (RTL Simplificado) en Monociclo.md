Este flujo describe las acciones que ocurren concurrentemente durante un ciclo de reloj para ejecutar una instrucción MIPS. Recuerda que en el diseño monociclo, todas estas etapas suceden dentro del mismo ciclo de reloj, que debe ser lo suficientemente largo para la instrucción más lenta.

**1. Fetch (Búsqueda de Instrucción):**

*   **Acción:** Se lee la instrucción de la memoria en la dirección indicada por el PC actual.
*   **Componentes:** PC, Memoria de Instrucciones.
*   **RTL:**
    ```
    Instrucción = MemoriaInstrucciones[PC];
    ```
*   **Descripción:** El valor actual del PC se usa como dirección para la Memoria de Instrucciones, la cual devuelve la instrucción binaria de 32 bits correspondiente.

**2. Cálculo de la Siguiente Dirección Secuencial (PC+4):**

*   **Acción:** Se calcula la dirección de la instrucción que seguiría si no hubiera saltos.
*   **Componentes:** PC, Sumador (Adder 1).
*   **RTL:**
    ```
    PC_Siguiente = PC + 4;
    ```
*   **Descripción:** En paralelo con la búsqueda, un sumador calcula `PC + 4`. Este valor será el próximo PC *a menos que* la instrucción actual sea un salto exitoso.

**3. Decode y Lectura de Registros:**

*   **Acción:** Se decodifica la instrucción para determinar qué operación realizar y qué registros usar. Se leen los valores de los registros fuente del Banco de Registros.
*   **Componentes:** Instrucción (salida de Memoria Instr.), Unidad de Control, Banco de Registros.
*   **RTL:**
    ```
    // Decodificación (conceptual, genera señales de control)
    (RegWrite, MemRead, MemWrite, Branch, ALUSrc, RegDst, MemToReg, Jump, ALUOp) = UnidadControl(Instrucción[31:26]); // Basado en Opcode

    // Lectura de Registros
    RegData1 = BancoRegistros[Instrucción[25:21]]; // Lee registro rs
    RegData2 = BancoRegistros[Instrucción[20:16]]; // Lee registro rt
    ```
*   **Descripción:** Los bits de la instrucción (especialmente el `opcode` [31:26]) van a la Unidad de Control, que genera todas las señales de control necesarias para el resto del datapath. Simultáneamente, los campos `rs` y `rt` de la instrucción se usan como direcciones para leer los valores correspondientes del Banco de Registros.

**4. Ejecución (Operación de la ALU):**

*   **Acción:** La ALU realiza la operación requerida por la instrucción.
*   **Componentes:** RegData1, RegData2, Campo Inmediato (extendido), Mux (ALUSrc), ALU, ALU Control Unit.
*   **RTL:**
    ```
    // Selección del segundo operando de la ALU
    InmediatoExtendido = SignExtend(Instrucción[15:0]);
    OperandoB_ALU = (ALUSrc == 1) ? InmediatoExtendido : RegData2; // Selecciona entre rt o inmediato

    // Generación de la señal específica para la ALU
    ControlALU = UnidadControlALU(ALUOp, Instrucción[5:0]); // Usa ALUOp y Funct si es R-Type

    // Operación de la ALU
    ResultadoALU = ALU(RegData1, OperandoB_ALU, ControlALU);
    FlagZero = ALU.ZeroOutput; // El flag Zero se genera basado en ResultadoALU
    ```
*   **Descripción:** La ALU recibe sus operandos (uno siempre de `RegData1`, el otro puede ser `RegData2` o el inmediato extendido) y la señal `ControlALU` (derivada del `opcode` y/o `funct`). Realiza la operación (suma, resta, AND, OR, SLT) y genera el resultado (`ResultadoALU`) y el flag `Zero`.

**5. Acceso a Memoria de Datos (si es necesario):**

*   **Acción:** Si la instrucción es `lw` o `sw`, se accede a la Memoria de Datos para leer o escribir.
*   **Componentes:** ResultadoALU (dirección), RegData2 (dato a escribir para `sw`), Memoria de Datos, señales MemRead, MemWrite.
*   **RTL:**
    ```
    // Lectura de memoria (si MemRead = 1)
    DatoLeidoMemoria = MemoriaDatos[ResultadoALU];

    // Escritura en memoria (si MemWrite = 1)
    MemoriaDatos[ResultadoALU] = RegData2;
    ```
*   **Descripción:** Si `MemRead` está activo (`lw`), la `MemoriaDatos` usa `ResultadoALU` como dirección y pone el dato leído en `DatoLeidoMemoria`. Si `MemWrite` está activo (`sw`), la `MemoriaDatos` usa `ResultadoALU` como dirección y almacena el valor de `RegData2` en esa ubicación. Si ninguna señal está activa, la memoria no hace nada relevante para el flujo.

**6. Escritura en Registro (Write-Back, si es necesario):**

*   **Acción:** Si la instrucción escribe un resultado en un registro (Tipo R, `lw`, `addi`), este se escribe en el Banco de Registros.
*   **Componentes:** ResultadoALU, DatoLeidoMemoria, Mux (MemToReg), Mux (RegDst), Banco de Registros, señal RegWrite.
*   **RTL:**
    ```
    // Selección del registro destino (rd o rt)
    RegistroDestino = (RegDst == 1) ? Instrucción[15:11] : Instrucción[20:16];

    // Selección del dato a escribir (resultado ALU o dato de memoria)
    DatoAEscribir = (MemToReg == 1) ? DatoLeidoMemoria : ResultadoALU;

    // Escritura en el banco de registros (si RegWrite = 1)
    if (RegWrite == 1) {
        BancoRegistros[RegistroDestino] = DatoAEscribir;
    }
    ```
*   **Descripción:** Si `RegWrite` está activo, se selecciona el registro destino correcto (`rd` para Tipo R, `rt` para `lw`/`addi`) y el dato correcto a escribir (`ResultadoALU` para Tipo R/`addi`, `DatoLeidoMemoria` para `lw`). Este dato se escribe en el registro seleccionado en el flanco de reloj. (Nota: Usé un `if` en RTL para mayor claridad, aunque en hardware es una habilitación).

**7. Actualización del PC:**

*   **Acción:** Se determina y se carga la dirección de la *próxima* instrucción en el PC.
*   **Componentes:** PC_Siguiente (PC+4), FlagZero, Campo Inmediato (offset), Campo Address (jump), Sumador (Adder 2 para branch), Muxes, PC.
*   **RTL:**
    ```
    // Cálculo de la dirección de salto para BEQ
    DireccionSaltoBEQ = PC_Siguiente + (InmediatoExtendido << 2); // Suma PC+4 y offset*4

    // Cálculo de la dirección de salto para J
    DireccionSaltoJ = { PC_Siguiente[31:28], Instrucción[25:0], 2'b00 }; // Pseudo-directo

    // Selección de la próxima dirección del PC
    TomarSaltoBEQ = Branch && FlagZero; // Condición para tomar el salto BEQ
    PC_EntradaMux1 = (TomarSaltoBEQ == 1) ? DireccionSaltoBEQ : PC_Siguiente; // Elige entre salto BEQ o PC+4
    PC_EntradaFinal = (Jump == 1) ? DireccionSaltoJ : PC_EntradaMux1; // Elige entre salto J o el resultado anterior

    // Carga del nuevo valor en el PC (ocurre en el flanco de reloj)
    PC = PC_EntradaFinal;
    ```
*   **Descripción:** Se calculan las posibles direcciones de destino para `beq` y `j`. Basándose en las señales de control (`Branch`, `Jump`) y el resultado de la comparación (`FlagZero`), un conjunto de multiplexores selecciona la dirección correcta para la siguiente instrucción: `PC+4` (secuencial), `DireccionSaltoBEQ` (si `beq` es exitoso), o `DireccionSaltoJ` (si es `j`). Este valor final se carga en el PC en el mismo flanco de reloj en que se actualiza el Banco de Registros, preparándolo para el *siguiente* ciclo.
