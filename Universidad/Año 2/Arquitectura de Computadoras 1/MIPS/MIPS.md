
# Introduccion a MIPS

MIPS (Microprocessor without Interlocked Pipeline Stages) es una arquitectura de conjunto de instrucciones reducido (RISC) ampliamente utilizada en la enseñanza y en sistemas embebidos. Sus características clave son:

## 1. Registros

*   Posee **32 registros de propósito general** (numerados de `$0` a `$31`).
*   Cada registro tiene un tamaño de **32 bits**.
*   Se utilizan para almacenar datos temporales, operandos y direcciones.

## 2. Arquitectura

*   Utiliza una **Arquitectura Harvard**, lo que implica:
    *   **Memorias separadas** para instrucciones y para datos.
    *   Esto permite buscar la siguiente instrucción al mismo tiempo que se accede a los datos para la instrucción actual, mejorando el paralelismo y rendimiento.

## 3. Memoria

*   **Direccionamiento:** Es **byte-addressable**, es decir, cada byte individual en la memoria tiene una dirección única.
*   **Tamaño del Espacio de Direcciones:** Puede direccionar hasta $2^{30}$ palabras (word), donde cada palabra es de 32 bits. Esto equivale a un espacio total de $2^{32}$ bytes (4 Gigabytes).
*   **Acceso (Arquitectura Load/Store):** El acceso a la memoria de datos se realiza *exclusivamente* mediante instrucciones específicas:
    *   `load` (ej. `lw`, `lb`): Carga datos *desde* la memoria *hacia* un registro.
    *   `store` (ej. `sw`, `sb`): Guarda datos *desde* un registro *hacia* la memoria.
    *   Las operaciones aritmético-lógicas (suma, resta, etc.) operan únicamente sobre los valores contenidos en los registros.

## 4. Conjunto de Instrucciones (ISA)

*   Todas las instrucciones MIPS tienen un tamaño fijo de **32 bits**.
*   Existen principalmente tres formatos de instrucción (Tipo R, Tipo I, Tipo J) que definen cómo se interpretan esos 32 bits (qué campos representan códigos de operación, registros, inmediatos, direcciones, etc.).

![conjunto-instruccones.png](conjunto-instruccones.png)


### Formato de Instrucción Tipo-R (Register)

Las instrucciones de Tipo-R se utilizan principalmente para operaciones **aritmético-lógicas** que operan **directamente entre registros**. No acceden a la memoria ni utilizan valores inmediatos (excepto por el campo `shamt`).

**Estructura (32 bits):**

![image.png](media/tipo-r.png)


**Descripción de los Campos:**

*   **`opcode` (Código de Operación):** Para *todas* las instrucciones de Tipo-R, este campo siempre tiene el valor **0**. Indica que la instrucción pertenece a este formato.
*   **`rs` (Registro Fuente 1):** Especifica el número (0-31) del **primer registro operando**.
*   **`rt` (Registro Fuente 2):** Especifica el número (0-31) del **segundo registro operando**.
*   **`rd` (Registro Destino):** Especifica el número (0-31) del registro donde se **guardará el resultado** de la operación.
*   **`shamt` (Shift Amount / Cantidad de Desplazamiento):** Se utiliza **únicamente** en las instrucciones de desplazamiento (como `sll`, `srl`). Indica cuántos bits se debe desplazar el valor del registro `rt`. Para otras instrucciones Tipo-R (como `add`, `sub`, `and`), este campo es **0**.
*   **`funct` (Código de Función):** Como el `opcode` es siempre 0 para las Tipo-R, este campo es **esencial**. Especifica la **operación concreta** que se debe realizar (por ejemplo, suma, resta, AND lógico, OR lógico, set-on-less-than). La unidad de control utiliza este campo junto con el `opcode` (que es 0) para determinar la acción exacta de la ALU.

**Ejemplo Conceptual:**

Una instrucción como `add $t0, $s1, $s2` (que suma el contenido de `$s1` y `$s2` y guarda el resultado en `$t0`) se codificaría en formato Tipo-R:

*   `opcode` sería 0.
*   `rs` codificaría el número del registro `$s1`.
*   `rt` codificaría el número del registro `$s2`.
*   `rd` codificaría el número del registro `$t0`.
*   `shamt` sería 0 (porque no es un desplazamiento).
*   `funct` tendría un valor específico que representa la operación de suma (`add`).

**En Resumen:** Las instrucciones Tipo-R realizan operaciones entre registros, definidas por el campo `funct`, y almacenan el resultado en un registro destino `rd`.


### Formato de Instrucción Tipo-I (Immediate)

Las instrucciones de Tipo-I se utilizan para operaciones que involucran un **valor inmediato** (una constante codificada directamente en la instrucción). Son fundamentales para cargar constantes, realizar operaciones aritméticas con constantes, acceder a memoria (loads/stores) y para saltos condicionales.

**Estructura (32 bits):**

![image.png](media/tipo-i.png)

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


### Formato de Instrucción Tipo-J (Jump)

Las instrucciones de Tipo-J se utilizan exclusivamente para **saltos incondicionales** (`j` y `jal`). Permiten transferir el flujo de ejecución a una dirección de instrucción lejana dentro del programa.

**Estructura (32 bits):**

![image.png](media/tipo-j.png)


**Descripción de los Campos:**

*   **`opcode` (Código de Operación):** Identifica la instrucción como un salto incondicional. Hay dos opcodes principales para este formato:
    *   `j` (Jump): Salta a la dirección calculada.
    *   `jal` (Jump and Link): Salta a la dirección calculada y, además, **guarda la dirección de la instrucción siguiente al salto** (PC + 4) en el registro `$ra` (`$31`). Esto es fundamental para implementar llamadas a subrutinas/funciones, ya que `$ra` contendrá la dirección a la que se debe retornar.
*   **`address` (Dirección / Pseudo-dirección):** Son **26 bits** que representan una parte de la dirección de destino del salto. **No es la dirección completa**.

**Cálculo de la Dirección de Salto:**

La dirección de destino real (de 32 bits) se calcula de la siguiente manera:

1.  Se toman los **4 bits más significativos** de la dirección de la instrucción *siguiente* al salto (PC + 4).
2.  Se toman los **26 bits** del campo `address` de la instrucción Tipo-J.
3.  Se añaden **dos ceros** (`00`) al final de los 26 bits del campo `address`. Esto se debe a que las instrucciones MIPS están alineadas a palabras (4 bytes), por lo que las direcciones de instrucción siempre terminan en `00` en binario.
4.  Se **concatenan** los 4 bits del PC+4 con los 28 bits resultantes (26 bits de `address` + `00`).

**Fórmula:**
`Dirección_Salto [31:0] = (PC + 4) [31:28]  ||  address [25:0]  ||  00`

Esto permite saltar a cualquier instrucción dentro del mismo **segmento de 256 MB** ( $2^{28}$ bytes) en el que se encuentra la instrucción de salto.

**Ejemplo Conceptual:**

Una instrucción como `j TargetLabel` se codificaría en formato Tipo-J:

*   `opcode` sería el código para `j`.
*   `address` contendría los 26 bits intermedios de la dirección de la etiqueta `TargetLabel`.

**En Resumen:** Las instrucciones Tipo-J realizan saltos incondicionales utilizando un campo de dirección de 26 bits. La dirección de destino completa se construye combinando estos 26 bits con los 4 bits superiores del PC actual (más 4) y añadiendo dos ceros al final. La instrucción `jal` es idéntica pero además guarda la dirección de retorno en `$ra`.

## 5. Naturaleza del Circuito (Combinacional vs. Secuencial)

Es crucial diferenciar entre el circuito completo y la lógica de ejecución dentro de un ciclo:

### Circuito Completo del Procesador (Secuencial)

*   El diseño **completo** del procesador MIPS incluye **elementos de memoria (secuenciales)** que almacenan estado entre ciclos de reloj. Estos son:
    *   El **Contador de Programa (`PC`)**: Guarda la dirección de la siguiente instrucción.
    *   El **Banco de Registros**: Almacena los valores de los 32 registros generales.
    *   La **Memoria de Instrucciones** y la **Memoria de Datos**.
*   Estos elementos **actualizan su estado únicamente en los flancos de reloj**, lo que hace que el circuito general sea **secuencial**.

### Ejecución Dentro de un Ciclo de Reloj (Combinacional)

*   Durante **un único ciclo de reloj**, los datos y las señales de control fluyen a través de varios bloques lógicos para realizar parte (o toda, en un diseño monociclo) de la ejecución de una instrucción. Estos bloques incluyen:
    *   Multiplexores (MUX).
    *   La Unidad Aritmético-Lógica (ALU).
    *   La Unidad de Control.
    *   Sumadores, extensores de signo, etc.
*   Las salidas de estos bloques **dependen únicamente de las entradas presentes en ese instante** (dentro de ese ciclo). No hay almacenamiento de estado *intermedio* dentro de esta lógica que dependa del reloj.
*   Por lo tanto, el **camino lógico que procesa los datos *dentro* de un ciclo de reloj** se comporta como un **circuito combinacional**.




```wasm
j L    # goto L
```

```wasm
// Saltos condicionales

j 334    # PC = (PC+4)[31..28] & 334*4

jal 189    # PC = (PC+4)[31..28] & 189*4 $31=PC+4
```

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%208.png)

En MIPS, la dirección de memoria es de 32 bits. Los 4 bits más significativos (los primeros de izquierda a derecha) determinan en qué segmento de memoria estamos ubicados. Los 28 bits restantes indican el desplazamiento o la dirección dentro de ese segmento, lo que permite acceder a un rango de hasta 2^28 bytes (256 MB) dentro de cada segmento.

Por ejemplo, si la dirección del *program counter* (PC) es: 1010 0101010000101010101010101010

Los 4 bits más significativos son `1010`, lo que indica que estamos en el segmento `0xA`. El resto, `0101010000101010101010101010`, representa la posición dentro de ese segmento.

## Modos de direccionamiento

### Mediante registros

- Tipo-R. ej: add, sub, and…

### Inmediato

- Tipo-I ej: addi, subi, andi…

### Mediante registro base

- Tipo-I. ej: lw y sw

### Relativo a PC

- Tipo-I. ej: beq, bne

### Pseudo directo

- Tipo-J. ej: j, jal

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%209.png)

## Diseño del microprocesador MIPS

- microprocesador de 32 bits de un ciclo
    - Tambien llamado uniciclo combinacional
    - Cada intruccion se ejecuta en un ciclo de relog
- Se diseñara para las siguiente instrucciones
    - Referencia a memoria: lw y sw
    - Aritmeticas-logicas de tipo-R: add, sub, and, sit, …
    - Saltos: beq y

### Ejecucion RTL (Register Transfer Level) de una instruccion

Nos sirve para ver que hace el procesador cuando interpreta una intruccion, para ver que es lo que tenemos que modelar

- fetching
- PC + 4
- es lo que hay en la memoria

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2010.png)

- Para todas las intrucciones los dos primeros pasos son los mismos
    - Obtener la instruccion desde la memoria y actualizar el PC
    - Leer uno o dos registros
- El resto de los pasos depende de la instruccion a ejecutar
- Todas usan de alguna manera la ALU
    - Referencia a memoria: calculo de direccion de acceso
    - Aritmeticas-logicas: segun campo funct de la instruccion
    - Saltos: para determinar condicion

## Vista a muy alto nivel

- Arquitectura harvard

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2011.png)

### **PC (Program Counter)**

- Guarda la dirección de la **próxima instrucción** a ejecutar.
- En cada ciclo, normalmente se incrementa en 4 (porque las instrucciones MIPS ocupan 4 bytes).
- Si hay un salto o rama, se actualiza con otra dirección.

### **Instruction Memory**

- Es la **memoria de instrucciones de 32 bits**.
- A partir de la dirección del PC, recupera la instrucción que se va a ejecutar.

### **Registers**

- Es el **banco de registros**, donde están los 32 registros (`$t0`, `$s0`, etc.).
- A partir de la instrucción, se determinan:
    - Dos registros a **leer**
    - Uno a **escribir** (si la instrucción lo requiere)

### **ALU (Unidad Aritmético Lógica)**

- Ejecuta operaciones como suma, resta, comparación, etc.
- Se usa para:
    - Realizar cálculos aritméticos
    - Calcular direcciones (por ejemplo, para `lw`, `sw`)
    - Comparar en saltos condicionales (`beq`, `bne`)

### **Data Memory**

- Se accede en instrucciones de acceso a memoria:
    - `lw` (load word): lee datos de memoria
    - `sw` (store word): escribe datos en memoria

### **Adders (Sumadores)**

- Hay dos bloques `Add` en el diagrama:
    - Uno suma 4 al PC → calcula la siguiente instrucción secuencial.
    - Otro calcula direcciones de salto (por ejemplo, para `beq` o `j`).

### **Multiplexores (Mux)**

- Son los “selectores” que eligen entre dos posibles entradas.
- Según la instrucción, eligen:
    - Qué valor entra a la ALU
    - Qué dirección de PC tomar (siguiente secuencial o salto)
    - Qué dato escribir en los registros

### ¿Cómo fluye todo esto?

1. **PC** dice qué instrucción buscar → se va a **Instruction Memory**
2. Se decodifica la instrucción → se accede al **banco de registros**
3. La **ALU** realiza una operación (suma, comparación, etc.)
4. Si es una instrucción de memoria, se usa **Data Memory**
5. Si corresponde, se escribe el resultado de vuelta en un **registro**
6. Se actualiza el **PC** para ir a la siguiente instrucción

## Fetch de la instruccion

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2012.png)

### ¿Qué es el *fetch*?

El *fetch* (en español, **búsqueda o captura**) es la **primera etapa del ciclo de ejecución** de cualquier instrucción. Su función es **obtener la instrucción que está en la dirección indicada por el PC (Program Counter)**.

### ¿Cómo funciona?

Mirando el área sombreada en azul y el texto:

1. `Instruction ← Mem[PC]`
    - El valor del **PC** (Program Counter) se usa como **dirección de lectura** en la **Instruction Memory**.
    - Se obtiene la instrucción almacenada en esa dirección (recordá que cada instrucción ocupa 4 bytes).
    - Esa instrucción se envía al resto del procesador para que se ejecute en los próximos ciclos.
2. `PC ← PC + 4`
    - El valor del PC se incrementa en 4, apuntando a la **siguiente instrucción**.
    - Esto se hace automáticamente en instrucciones que **no saltan** (como `add`, `sub`, etc.).

### Ejemplo real:

Supongamos que el PC contiene `0x00400000`.

- Se hace: `Instruction ← Mem[0x00400000]` → se busca la instrucción en esa dirección.
- Luego: `PC ← 0x00400000 + 4` → se actualiza el PC para que apunte a la próxima instrucción (`0x00400004`).

## Referencia a memoria

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2013.png)

### ¿Qué significa "referencia a memoria"?

Se refiere a cualquier instrucción que **lee o escribe datos desde/hacia memoria**. En MIPS, esto ocurre en instrucciones como:

- `lw rt, offset(rs)` → **Carga** en el registro `rt` el dato que está en la dirección `rs + offset`.
- `sw rt, offset(rs)` → **Guarda** el contenido del registro `rt` en la dirección `rs + offset`.

### ¿Cómo funciona esta etapa?

1. **Lectura de registros**
    - Se leen los registros involucrados: `rs` (base) y `rt` (dato o destino).
    - Esto ya ocurrió en la etapa anterior (decode), y ahora tenemos los valores necesarios.
2. **Cálculo de dirección**
    - La **ALU** suma el valor de `rs` con el **inmediato (offset)** de la instrucción.
    - Resultado: la **dirección efectiva** a la que se accede en la memoria.
3. **Acceso a la memoria de datos**
    - Si es `lw`, se **lee** desde esa dirección y el dato se guarda en `rt`.
    - Si es `sw`, se **escribe** en esa dirección el valor de `rt`.

Esta etapa es esencial para todas las instrucciones que **interactúan con memoria de datos**, que en MIPS se hace **solo de forma explícita** con `lw` y `sw`. Gracias a este diseño, el acceso a memoria es **claro y controlado** en MIPS.

## Aritmeticas-logicas

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2014.png)

### ¿Qué son las instrucciones aritmético-lógicas?

Son instrucciones que **realizan operaciones matemáticas o lógicas** entre registros.

Por ejemplo:

- `add $t0, $t1, $t2` ⇒ `$t0 ← $t1 + $t2`
- `sub $s1, $s2, $s3` ⇒ `$s1 ← $s2 - $s3`
- `and $a0, $a1, $a2` ⇒ `$a0 ← $a1 AND $a2`

### ¿Cómo funciona esta etapa?

1. **Lectura de registros**
    - Se extraen los valores de los registros fuente `rs` y `rt` desde el bloque de **Registers**.
2. **Operación en la ALU**
    - La **ALU** toma esos dos valores y realiza la operación indicada por la instrucción (`+`, , `AND`, `OR`, etc.).
3. **Resultado**
    - El valor resultante queda listo para ser almacenado en el registro destino (`rd`) en la próxima etapa (**write-back**).

## Intruccion beq

### **¿Qué hace la instrucción `beq`?**

`beq rs, rt, inm`

Significa:

> Si el contenido de rs es igual al de rt, entonces salta (branch) a la dirección actual del PC + 4 + (inmediato × 4).
> 

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2015.png)

En este primer paso:

- Se cargan los registros `rs` y `rt`.
- La **ALU** realiza la operación `rs - rt`.
- El resultado **no se guarda** como tal, pero sí se utiliza para **determinar si el resultado es cero** (lo que significa que los registros son iguales).
- Esa condición se almacena en una especie de **"flag" interno** que se usará para decidir si se hace o no el salto.

🧠 **Idea clave:** Este paso evalúa si `rs == rt` (si la diferencia es 0).

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2016.png)

Ahora entra en juego la segunda parte:

- Si la **ALU** detecta que `rs == rt` (la resta dio cero), entonces se **actualiza el PC** (program counter) con una nueva dirección.
- Esa dirección es:
    
    `PC ← PC + 4 + (inmediato × 4)`
    
- El inmediato se multiplica por 4 porque las instrucciones en MIPS están alineadas en palabras de 4 bytes.

Este camino está resaltado en azul en el diagrama: incluye la unidad de suma adicional que calcula la nueva dirección de salto, y el multiplexor que elige entre `PC+4` (la siguiente instrucción normal) o `PC+4+inm*4` (el salto).

## Parte del circuito para instruccion aritmetico logicas (Tipo-R)

- extraccion de operandos
- ejecucion
- almacenamiento de resultado

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2017.png)

## Parte del circuito para salto condicional (beq)

- ALU para evaluar la condicion de salto
- Sumador para determinar la direccion de salto

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2018.png)

## Parte del circuito para instrucciones lw y sw

- ALU determina la direccion de acceso a memoria

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2019.png)

## Combinacion de todos los circuitos

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2020.png)

## Control de la ALU

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2021.png)

## Diseño completo con unidad de control

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2022.png)

## Señales de control para instrucciones de Tipo-R

ALUOP?? son 2 bits que dice que va a usar de la instruccion tipo r

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2023.png)

| Señal | Valor | ¿Qué hace? |
| --- | --- | --- |
| **RegDst** | `1` | Selecciona el registro `rd` como destino (campo [15:11] de la instrucción). Esto es típico de instrucciones tipo R. |
| **ALUSrc** | `0` | La ALU toma como segundo operando el contenido del registro `rt`, no un inmediato. |
| **MemtoReg** | `0` | El valor que se va a escribir en el registro proviene de la ALU (no de memoria). |
| **RegWrite** | `1` | Habilita la escritura en el registro destino (va a escribir el resultado de la ALU en `rd`). |
| **MemRead** | `0` | No se lee de memoria (no es una instrucción `lw`). |
| **MemWrite** | `0` | No se escribe en memoria (no es una instrucción `sw`). |
| **Branch** | `0` | No es una instrucción de salto condicional (`beq`). Así que el PC no se altera con lógica de branch. |
| **ALUOp1** | `1` | Parte del código que define la operación a realizar por la ALU. En este caso, indica una operación tipo R. |
| **ALUOp0** | `0` | En combinación con `ALUOp1`, define que la operación será decodificada por el campo `funct`. |

### ¿Qué pasa paso a paso con estas señales?

1. **PC** accede a la memoria de instrucciones y trae la instrucción tipo R (ej: `add $t0, $t1, $t2`).
2. **Instruction Memory** divide la instrucción:
    - `rs = $t1` (registro fuente 1)
    - `rt = $t2` (registro fuente 2)
    - `rd = $t0` (registro destino)
    - `funct = 100000` (ADD)
3. **Registers**:
    - Lee los valores de `$t1` y `$t2`.
    - Como `RegDst = 1`, selecciona `rd` como destino del resultado.
4. **ALU**:
    - `ALUSrc = 0`: elige como segundo operando el valor del registro `rt`, no un inmediato.
    - `ALUOp = 10` (`ALUOp1=1`, `ALUOp0=0`): esto le indica al bloque de **ALU Control** que mire el campo `funct` para saber qué operación hacer (en este caso, suma).
5. **ALU Result** se guarda y va hacia:
    - `MemtoReg = 0`: se selecciona el resultado de la ALU para ir a los registros.
    - `RegWrite = 1`: se escribe el resultado en el registro `rd`.

## Señales de control para instrucciones lw

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2024.png)

| Señal | Valor | ¿Qué hace? |
| --- | --- | --- |
| **RegDst** | `0` | El registro destino es `rt` (campo [20:16]), porque `lw` escribe en ese registro. |
| **ALUSrc** | `1` | La ALU va a sumar el registro base (`rs`) con un **inmediato** (desplazamiento), no con otro registro. |
| **MemtoReg** | `1` | El dato que se escribe en el registro viene de **memoria**. |
| **RegWrite** | `1` | Se activa la escritura al registro destino (`rt`). |
| **MemRead** | `1` | Se activa la lectura desde memoria. |
| **MemWrite** | `0` | No se escribe en memoria (no es `sw`). |
| **Branch** | `0` | No es una instrucción de salto. |
| **ALUOp1** | `0` |  |
| **ALUOp0** | `0` | Ambos en 0 indican que la ALU va a hacer una **suma**, sin necesidad de mirar el campo `funct`. |

### ¿Qué ocurre paso a paso?

1. **PC** trae la instrucción `lw`.
2. Se separan los campos:
    - `rs = $t1` → base
    - `rt = $t0` → destino
    - offset inmediato = `4`
3. **RegDst = 0** → el dato se va a guardar en `rt` (`$t0`).
4. **ALUSrc = 1** → el segundo operando de la ALU viene del inmediato (offset), no de un registro.
5. **ALU** realiza la suma `rs + inmediato` → calcula la **dirección de memoria** donde buscar.
6. **MemRead = 1** → se activa la lectura desde la **Data memory** usando esa dirección.
7. **MemtoReg = 1** → el dato leído se envía al multiplexor que selecciona qué guardar en el registro.
8. **RegWrite = 1** → el dato se guarda en `rt` (`$t0`).

## Señales de control para instrucciones sw

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2025.png)

| Señal | Valor | ¿Qué hace? |
| --- | --- | --- |
| **RegDst** | `X` | No importa ("don’t care") porque **no se escribe** en ningún registro. |
| **ALUSrc** | `1` | La ALU necesita sumar un registro con un **inmediato** (offset). |
| **MemtoReg** | `X` | Tampoco importa, ya que no hay escritura en registros. |
| **RegWrite** | `0` | No se escribe en registros. |
| **MemRead** | `0` | No se lee desde memoria. |
| **MemWrite** | `1` | Se activa la escritura en memoria. |
| **Branch** | `0` | No es una instrucción de salto. |
| **ALUOp1** | `0` |  |
| **ALUOp0** | `0` | Ambos en 0 indican que la ALU debe realizar una **suma** (para calcular la dirección) |

### Paso a paso para `sw`

1. El **PC** busca la instrucción `sw`.
2. Se decodifican:
    - `rs = $t1` → base
    - `rt = $t0` → valor a guardar
    - offset = 4
3. **ALUSrc = 1** → la ALU suma `rs + inmediato`.
4. El resultado es la **dirección de memoria**.
5. **MemWrite = 1** → el valor en `rt` (que es `$t0`) se escribe en esa dirección de memoria.
6. **RegWrite = 0** → no se escribe nada en registros.

## Señales de control para instrucciones beq

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2026.png)

| Señal | Valor | ¿Qué hace? |
| --- | --- | --- |
| **RegDst** | `X` | No se escribe en registros → no importa |
| **ALUSrc** | `0` | Se comparan dos registros (`rs` y `rt`), no un inmediato |
| **MemtoReg** | `X` | Tampoco importa porque no se escribe en registros |
| **RegWrite** | `0` | No se escribe en registros |
| **MemRead** | `0` | No se accede a memoria |
| **MemWrite** | `0` | Tampoco se escribe en memoria |
| **Branch** | `1` | Activa el control de salto condicional |
| **ALUOp1** | `0` |  |
| **ALUOp0** | `1` | Combinados (`01`) → la ALU debe hacer una **resta** para comparar igualdad |

### Paso a paso para `beq`

1. Se leen los registros `$t0` y `$t1`.
2. **ALUOp = 01** y **ALUSrc = 0** → la ALU hace la resta `$t0 - $t1`.
3. Si el resultado da cero (**Zero = 1**), el resultado de `Shift left 2` + PC+4 se usa como **nueva dirección de salto**.
4. Si no son iguales, el `PC` sigue como siempre.

## Las señales generadas por la Unidad de Control actuan sobre:

- multiplexores
- habilitacion de escritura en banco de registro y memoria
- operaciones de la ALU

## Señales de instruccion para la instruccion j

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2027.png)

| Señal | Valor | ¿Por qué? |
| --- | --- | --- |
| **RegDst** | `X` | No se escribe en registros |
| **ALUSrc** | `X` | No se usa la ALU |
| **MemtoReg** | `X` | No se lee memoria ni se escribe en registros |
| **RegWrite** | `0` | No se escribe en registros |
| **MemRead** | `0` | No se accede a memoria |
| **MemWrite** | `0` | No se escribe en memoria |
| **Branch** | `0` | No es un salto condicional |
| **ALUOp1** | `X` | No importa, la ALU no se usa |
| **ALUOp0** | `X` | - |
| **Jump** | `1` | Señal que activa el salto incondicional |

### Explicación gráfica

En el diagrama:

- Se toma el campo de 26 bits de la instrucción (`[25:0]`),
- se lo **shiftea 2** para convertirlo en dirección de palabra,
- se **concatenan los 4 bits superiores** del `PC + 4`,
- y esa dirección se asigna directamente al **nuevo PC**.

## Mircroprocesador uniciclo

Análisis simplificado de tiempo desde que se extrae la
instrucción (fetch) hasta que se deposita resultado o
determina salto

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2028.png)

![image.png](MIPS%201ce3df73dd3780a8bf6aefb674e11faf/image%2029.png)

Posibles inconvenientes:

- Se debe respetar la instrucción que más tarda para
determinar el tiempo de ciclo de reloj
- Todas las instrucciones utilizan la misma cantidad de tiempo
que la instrucción más lenta
- Mucho tiempo de cómputo para programas con muchas
instrucciones
- Duplicación de componentes de similar funcionalidad
- Imposibilidad de reutilizar componentes inactivos durante la
ejecución de una instrucción

El circuito no es combinacional, pero la ejecucion de una instruccion es conbinacional

memoria interna ⇒ lectura depende del clock

el flag de zero se usa para el beq

jump se desplaza concatenando. Agregar regDst

hay registros particulares que no se modifican