La **ISA (Instruction Set Architecture)** es la interfaz entre el software y el hardware, definiendo el lenguaje que entiende el procesador. En **MIPS (Microprocessor without Interlocked Pipeline Stages)**, la ISA define:

1.  **Conjunto de Instrucciones:**
    *   Operaciones básicas (aritméticas, lógicas, transferencia de datos, control de flujo).
    *   MIPS es **RISC (Reduced Instruction Set Computer)**: conjunto de instrucciones pequeño, simple y de longitud fija (32 bits).

2.  **Formatos de Instrucción:**
    *   Codificación binaria de las instrucciones.
    *   Tamaño fijo de **32 bits**.
    *   Formatos principales: **Tipo R, Tipo I, Tipo J**. Simplifican la decodificación.

3.  **Registros:**
    *   Registros accesibles por las instrucciones.
    *   **32 registros de propósito general** (`$0` - `$31`).
    *   Registros especiales como el **Contador de Programa (PC)**.

4.  **Modos de Direccionamiento:**
    *   Cómo las instrucciones especifican la ubicación de los operandos.
    *   Arquitectura **load/store**: operaciones aritmético-lógicas solo sobre registros.
    *   Acceso a memoria con `lw`, `sw` usando direccionamiento **base + desplazamiento**.

5.  **Tipos de Datos:**
    *   Tamaños y formatos de datos manipulables (ej., enteros de 32 bits).

6.  **Manejo de Memoria:**
    *   Organización y acceso al espacio de memoria.

![conjunto-instruccones.png](conjunto-instruccones.png)

## Tipo-R

[[Tipo-R]]

## Tipo-J

[[Tipo-J]]
## Tipo-I

[[Tipo-I]]

## Registros

**Registros Preservados por el Llamador (Caller-Saved)**
*(El llamador debe guardar estos registros si necesita su valor después de la llamada)*

| Nombre  | Número  | Uso                                | Se preserva |
| :------ | :------ | :--------------------------------- | :---------- |
| $at     | $1      | Reservado ensamblador              | No          |
| $v0–$v1 | $2–$3   | Valores de retorno y expresiones   | No          |
| $a0–$a3 | $4–$7   | Argumentos de funciones            | No          |
| $t0–$t7 | $8–$15  | Temporales                         | No          |
| $t8–$t9 | $24–$25 | Temporales                         | No          |
| $k0–$k1 | $26–$27 | Reservados para el Núcleo del S.O. | No          |
| $ra     | $31     | Dirección de Retorno               | No          |

**Registros Preservados por el Llamado (Callee-Saved)**
*(El llamado (la función) debe guardar y restaurar estos registros si los modifica)*

| Nombre | Número | Uso                               | Se preserva |
| :----- | :----- | :-------------------------------- | :---------- |
| $zero  | $0     | Constante 0                       | Sí          |
| $s0–$s7 | $16–$23| Temporales preservados            | Sí          |
| $gp    | $28    | Puntero Global                    | Sí          |
| $fp    | $29    | Puntero Base Reg. Act.            | Sí          |
| $sp    | $30    | Puntero de Pila                   | Sí          |


## Carga y Almacenaje en Memoria

| Nombre                 | Sintaxis     | Formato | Código | Semántica                     |
| :--------------------- | :----------- | :------ | :----- | :---------------------------- |
| Load Byte              | LB $t,I($s)  | I       | 0x20   | $t = M( $s+I ) (signed)       |
| Load HalfWord          | LH $t,I($s)  | I       | 0x21   | $t = M( $s+I ) (signed)       |
| Load Word Left         | LWL $t,I($s) | I       | 0x22   | $t = M( $s+I ) (left part)    |
| Load Word              | LW $t,I($s)  | I       | 0x23   | $t = M( $s+I )                |
| Load Byte Unsigned     | LBU $t,I($s) | I       | 0x24   | $t = M( $s+I ) (unsigned)     |
| Load HalfWord Unsigned | LHU $t,I($s) | I       | 0x25   | $t = M( $s+I ) (unsigned)     |
| Load Word Right        | LWR $t,I($s) | I       | 0x26   | $t = M( $s+I ) (right part)   |
| Store Byte             | SB $t,I($s)  | I       | 0x28   | M( $s + I ) = $t              |
| Store HalfWord         | SH $t,I($s)  | I       | 0x29   | M( $s + I ) = $t              |
| Store Word Left        | SWL $t,I($s) | I       | 0x2A   | M( $s + I ) = $t (left part)  |
| Store Word             | SW $t,I($s)  | I       | 0x2B   | M( $s + I ) = $t              |
| Store Word Right       | SWR $t,I($s) | I       | 0x2E   | M( $s + I ) = $t (right part) |

## Acceso a la ALU

| Nombre                           | Sintaxis      | Código | Función | Semántica                             |
| :------------------------------- | :------------ | :----- | :------ | :------------------------------------ |
| Add                              | add $d,$s,$t  | 0      | 0x20    | $d = $s+$t                            |
| Add Unsigned                     | addu $d,$s,$t | 0      | 0x21    | $d = $s+$t                            |
| Substract                        | sub $d,$s,$t  | 0      | 0x22    | $d = $s-$t                            |
| Substract Unsigned               | subu $d,$s,$t | 0      | 0x23    | $d = $s-$t                            |
| Add Immediate                    | addi $t,$s,I  | 0x8    | —       | $t = $s+I$ (signed)                   |
| Add Immediate Unsigned           | addiu $t,$s,I | 0x9    | —       | $t = $s+I$ (unsigned)                 |
| And                              | and $d,$s,$t  | 0      | 0x24    | $d = $s \text{ and } $t$              |
| And Immediate                    | andi $t,$s,I  | 0xC    | —       | $t = $s \text{ and } I$ (unsigned)    |
| Or                               | or $d,$s,$t   | 0      | 0x25    | $d = $s \text{ or } $t$               |
| Or Immediate                     | ori $t,$s,I   | 0xD    | —       | $t = $s \text{ or } I$ (unsigned)     |
| Xor                              | xor $d,$s,$t  | 0      | 0x26    | $d = $s \text{ xor } $t$              |
| Xor Immediate                    | xori $t,$s,I  | 0xE    | —       | $t = $s \text{ xor } I$ (unsigned)    |
| Nor                              | nor $d,$s,$t  | 0      | 0x27    | $d = \text{not}( $s \text{ or } $t )$ |
| Set on Less Than                 | slt $d,$s,$t  | 0      | 0x2A    | $d = ($s < $t) ? 1 : 0$               |
| Set on Less Than Unsigned        | sltu $d,$s,$t | 0      | 0x2B    | $d = ($s < $t) ? 1 : 0$ (unsigned)    |
| Set on Less Than Immediate       | slti $t,$s,I  | 0xA    | —       | $t = ($s < I) ? 1 : 0$                |
| Set on Less Than Immediate Unsig | sltiu $t,$s,I | 0xB    | —       | $t = ($s < I) ? 1 : 0$ (unsigned)     |
| Load Upper Immediate             | lui $t,I      | 0xF    | —       | $t = I << 16$                         |

## Desplazamientos

| Nombre                        | Sintaxis       | Código | Función | Semántica               |
| :---------------------------- | :------------- | :----- | :------ | :---------------------- |
| Shift Left Logic              | sll $d,$t,S    | 0      | 0x00    | $d = $t << S$           |
| Shift Right Logic             | srl $d,$t,S    | 0      | 0x02    | $d = $t >> S$           |
| Shift Right Arithmetic        | sra $d,$t,S    | 0      | 0x03    | $d = $t >> S$ (signed)  |
| Shift Left Logic Variable     | sllv $d,$t,$s  | 0      | 0x04    | $d = $t << $s$          |
| Shift Right Logic Variable    | srlv $d,$t,$s  | 0      | 0x06    | $d = $t >> $s$          |
| Shift Right Arithmetic Var. | srav $d,$t,$s  | 0      | 0x07    | $d = $t >> $s$ (signed) |

##  Multiplicaciones y Divisiones

| Nombre           | Sintaxis     | Código | Función | Semántica                                  |
| :--------------- | :----------- | :----- | :------ | :----------------------------------------- |
| Multiply         | mult $s,$t   | 0      | 0x18    | $( HI , LO ) = $s * $t$                     |
| Multiply Unsigned| multu $s,$t  | 0      | 0x19    | $( HI , LO ) = $s * $t$ (unsigned)          |
| Divide           | div $s,$t    | 0      | 0x1A    | $HI= $s \% $t, LO = $s / $t$                |
| Divide Unsigned  | divu $s,$t   | 0      | 0x1B    | $HI= $s \% $t, LO = $s / $t$ (unsigned)     |
| Move from HI     | mfhi $d      | 0      | 0x10    | $d = HI$                                   |
| Move to HI       | mthi $s      | 0      | 0x11    | $HI = $s$                                  |
| Move from LO     | mflo $d      | 0      | 0x12    | $d = LO$                                   |
| Move to LO       | mtlo $s      | 0      | 0x13    | $LO = $s$                                  |
*(Nota: Se corrigió la sintaxis de la última instrucción a `mtlo $s` para que coincida con el código de función 0x13. También se eliminó la nota sobre ciclos de espera, ya que eso depende de la implementación específica del pipeline y los hazards)*

## Saltos

| Nombre                 | Sintaxis       | Código | Función | Semántica                             |
| :--------------------- | :------------- | :----- | :------ | :------------------------------------ |
| Branch on Equal        | beq $s,$t,I    | 0x4    | –       | if($s == $t$) PC = PC + 4 + 4*I$      |
| Branch on Not Equal    | bne $s,$t,I    | 0x5    | –       | if($s != $t$) PC = PC + 4 + 4*I$      |
| Jump                   | j A            | 0x2    | –       | PC = (PC & 0xF0000000) \| (A << 2)$ |
| Jump Register          | jr $s          | 0      | 0x8     | PC = $s$                              |
| Jump and Link          | jal A          | 0x3    | –       | $ra = PC + 8$; PC = (PC & 0xF0000000) \| (A << 2)$ |
| Jump and Link Register | jalr $d,$s     | 0      | 0x9     | $d = PC + 8$; PC = $s$                |
*(Nota: Se ajustó la semántica de los saltos `j` y `jal` para reflejar cómo se construye la dirección de destino usando los bits superiores del PC actual y la dirección A desplazada. Se ajustó la semántica de `beq`/`bne` para incluir el PC+4 estándar. Se ajustó `jalr` para incluir el registro destino opcional `$d`, que por defecto es `$ra` ($31$). Se ajustó el valor guardado en `$ra` para `jal`/`jalr` para apuntar a la instrucción *después* del delay slot)*