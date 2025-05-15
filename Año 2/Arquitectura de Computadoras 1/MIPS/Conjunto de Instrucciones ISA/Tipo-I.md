### Formato de Instrucción Tipo-I (Immediate)

Las instrucciones de Tipo-I se utilizan para operaciones que involucran un **valor inmediato** (una constante codificada directamente en la instrucción). Son fundamentales para cargar constantes, realizar operaciones aritméticas con constantes, acceder a memoria (loads/stores) y para saltos condicionales.

**Estructura (32 bits):**

![image.png](tipo-i.png)

**Descripción de los Campos:**

*   **`opcode` (Código de Operación):** A diferencia del Tipo-R, aquí el `opcode` **sí especifica la operación principal** (por ejemplo, `addi`, `andi`, `lw`, `sw`, `beq`, `bne`). Este código distingue la instrucción de las de Tipo-R y Tipo-J.
*   **`rs` (Registro Fuente 1):** Generalmente especifica el número (0-31) del **primer registro operando**. Para instrucciones `load` y `store`, este registro contiene la **dirección base** de memoria. Para saltos condicionales (`beq`, `bne`), es uno de los registros a comparar.
*   **`rt` (Registro Fuente 2 / Registro Destino):** Este campo tiene un **doble propósito** dependiendo de la instrucción:
    *   Para operaciones **aritmético-lógicas inmediatas** (como `addi`, `andi`) y para **loads** (`lw`, `lb`), `rt` es el **registro destino** donde se guardará el resultado.
    *   Para **stores** (`sw`, `sb`), `rt` es el **registro fuente** cuyo valor se escribirá en memoria.
    *   Para **saltos condicionales** (`beq`, `bne`), `rt` es el **segundo registro** a comparar con `rs`.
*   **`immediate` (Valor Inmediato):** Es un valor constante de **16 bits**. Su interpretación depende de la instrucción:
    *   Para **operaciones aritméticas** (`addi`) y **loads/stores** (`lw`, `sw`), se suele **extender el signo** a 32 bits antes de usarlo (para permitir constantes negativas). Se usa como operando directo o como *offset* que se suma a la dirección base (`rs`) para calcular la dirección de memoria efectiva.
    *   Para **operaciones lógicas** (`andi`, `ori`), se suele **extender con ceros** (zero-extension) a 32 bits.
    *   Para **saltos condicionales** (`beq`, `bne`), representa un *offset* (desplazamiento) relativo al PC (Contador de Programa). La dirección de salto se calcula sumando este offset (multiplicado por 4, ya que las instrucciones están alineadas a palabras) a la dirección de la instrucción siguiente al salto.

**Usos Comunes:**

*   Operaciones aritméticas/lógicas con una constante: `addi $t0, $s1, 100` ( $t0 = $s1 + 100 )
*   Carga de datos desde memoria: `lw $t0, 32($s3)` ( Carga en $t0 la palabra ubicada en la dirección $s3 + 32 )
*   Almacenamiento de datos en memoria: `sw $t1, -4($sp)` ( Guarda el valor de $t1 en la dirección $sp - 4 )
*   Saltos condicionales: `beq $s0, $s1, L1` ( Si $s0 == $s1, salta a la etiqueta L1 )

**En Resumen:** Las instrucciones Tipo-I combinan un registro fuente (`rs`) con un valor inmediato de 16 bits para realizar operaciones, accesos a memoria (usando `rs` + inmediato como dirección) o saltos condicionales (comparando `rs` y `rt`, y usando el inmediato como offset de salto). El registro `rt` actúa como destino o como segunda fuente según la instrucción.

