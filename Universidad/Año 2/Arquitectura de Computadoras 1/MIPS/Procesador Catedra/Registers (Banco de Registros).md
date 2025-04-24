El Banco de Registros es una pieza central del datapath de MIPS. Es una memoria pequeña y muy rápida que contiene los **registros de propósito general (GPRs)** del procesador. Estos registros son el lugar principal donde las instrucciones aritmético-lógicas encuentran sus operandos y donde almacenan sus resultados. El acceso a los registros es mucho más rápido que el acceso a la memoria principal (Data Memory), por lo que la filosofía RISC (y MIPS en particular) fomenta mantener los datos activos en los registros tanto como sea posible.

Desglosemos sus características:

1.  **Contiene los 32 registros de propósito general de MIPS:**
    *   **Identificación:** MIPS define 32 registros, cada uno de 32 bits de ancho. Se identifican por números del 0 al 31, pero en ensamblador se usan nombres nemotécnicos como `$zero` (`$0`), `$at` (`$1`), `$v0`-`$v1` (valores de retorno), `$a0`-`$a3` (argumentos), `$t0`-`$t9` (temporales), `$s0`-`$s7` (guardados), `$k0`-`$k1` (kernel), `$gp` (puntero global), `$sp` (puntero de pila), `$fp` (puntero de marco) y `$ra` (dirección de retorno).
    *   **Función:** Aunque llamados "de propósito general", algunos tienen convenciones de uso específicas (como `$sp` o `$ra`). Sin embargo, la mayoría (`$t`, `$s`) pueden ser usados por el programador/compilador para almacenar valores intermedios durante los cálculos. El registro `$zero` (`$0`) es especial: siempre contiene el valor 0 y no se puede escribir en él.
    *   **Almacenamiento:** Físicamente, se implementa como un conjunto de flip-flops o celdas SRAM, optimizado para lecturas y escrituras rápidas.

2.  **Tiene puertos para leer simultáneamente el contenido de dos registros:**
    *   **Necesidad:** Muchas instrucciones MIPS (especialmente las de tipo R como `add $t0, $t1, $t2` y tipo I como `beq $t1, $t2, label` o `sw $t1, 0($t2)`) necesitan leer los valores de *dos* registros fuente al mismo tiempo. Por ejemplo, `add` necesita los valores de `$t1` y `$t2` para sumarlos. `sw` necesita el valor de `$t1` para almacenarlo y el valor de `$t2` como dirección base.
    *   **Puertos de Lectura (Read Ports):** Para permitir esto en un solo ciclo, el banco de registros tiene dos puertos de lectura independientes.
    *   **Direccionamiento de Lectura:** Cada puerto de lectura tiene una entrada de dirección de 5 bits (ya que $2^5 = 32$, suficiente para seleccionar uno de los 32 registros). Estas direcciones provienen directamente de los campos `rs` (para el primer operando leído, conectado a la salida "Read data 1") y `rt` (para el segundo operando leído, conectado a la salida "Read data 2") de la instrucción MIPS que se está decodificando.
        *   `Read register 1` (dirección) ← `Instrucción[25:21]` (campo `rs`)
        *   `Read register 2` (dirección) ← `Instrucción[20:16]` (campo `rt`)
    *   **Salidas de Datos:** Las salidas de estos puertos (`Read data 1` y `Read data 2`) proporcionan los valores de 32 bits leídos de los registros seleccionados. Estos valores se envían típicamente a la ALU o a la Memoria de Datos.
    *   **Operación Combinacional:** La lectura suele ser una operación combinacional: tan pronto como las direcciones de lectura (`rs`, `rt`) están estables en las entradas, los datos correspondientes aparecen en las salidas (`Read data 1`, `Read data 2`) tras un pequeño retardo de propagación, sin necesidad de una señal de reloj.

3.  **Tiene un puerto para escribir datos en un registro:**
    *   **Necesidad:** Instrucciones como `add`, `sub`, `lw`, etc., necesitan escribir su resultado de vuelta en uno de los registros.
    *   **Puerto de Escritura (Write Port):** El banco de registros tiene un único puerto de escritura. Esto se debe a que en MIPS (y en la mayoría de las arquitecturas) una instrucción escribe como máximo en un solo registro de propósito general por ciclo.
    *   **Direccionamiento de Escritura (`Write register`):** También requiere una dirección de 5 bits para seleccionar a cuál de los 32 registros se va a escribir. Aquí hay una sutileza:
        *   Para instrucciones de **Tipo R** (`add`, `sub`, ...), el registro destino está especificado en el campo `rd` (`Instrucción[15:11]`).
        *   Para instrucciones de **Tipo I** que escriben en un registro (como `lw` o `addi`), el registro destino es `rt` (`Instrucción[20:16]`).
        *   Se necesita un **Multiplexor (Mux)** (a menudo controlado por la señal `RegDst` de la unidad de control) para seleccionar si la dirección de escritura proviene del campo `rt` o `rd` de la instrucción. La salida de este Mux se conecta a la entrada `Write register`.
    *   **Datos de Escritura (`Write data`):** La entrada de datos de 32 bits que se escribirán en el registro seleccionado. De nuevo, se necesita otro **Multiplexor** (controlado por la señal `MemToReg`) para elegir de dónde provienen estos datos:
        *   Del resultado de la **ALU** (para instrucciones Tipo R o `addi`).
        *   Del dato leído de la **Data Memory** (para la instrucción `lw`).
        *   La salida de este Mux se conecta a la entrada `Write data`.
    *   **Señal de Habilitación (`RegWrite`):** La escritura no ocurre siempre. Solo las instrucciones que modifican un registro deben habilitar la escritura. La unidad de control genera la señal `RegWrite`. Si `RegWrite` está activa (ej. en '1'), la escritura se realiza; si está inactiva (ej. en '0', como para `sw` o `beq`), no se modifica ningún registro.
    *   **Operación Síncrona:** La escritura en el registro es una operación **síncrona**. Los datos y la dirección deben estar estables, y la señal `RegWrite` debe estar activa *antes* del flanco activo del reloj del sistema. La escritura real ocurre *en* el flanco del reloj. Esto asegura que los valores de los registros solo cambien en momentos precisos y controlados del ciclo.

**En Resumen:**

El Banco de Registros es como una "pizarra" muy rápida y organizada para el procesador. Tiene dos "ojos" (puertos de lectura) que pueden leer dos números de la pizarra simultáneamente y una "mano" (puerto de escritura) que puede escribir un nuevo número en un lugar específico de la pizarra, pero solo cuando se le da la orden (`RegWrite`) y en el momento exacto del ciclo de reloj. La selección de qué leer y dónde escribir viene dictada por los campos de la instrucción actual.