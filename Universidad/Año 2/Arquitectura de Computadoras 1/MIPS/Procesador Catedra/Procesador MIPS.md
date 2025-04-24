
MIPS (Microprocessor without Interlocked Pipeline Stages) es una arquitectura de conjunto de instrucciones reducido ([[RISC (Reduced Instruction Set Computer)]]) ampliamente utilizada en la enseñanza y en sistemas embebidos. Sus características clave son:

## Arquitectura Harvard 

[[Artectura Harvard]]

## Conjunto de Instrucciones (ISA)

[[Conjunto de instrucciones ISA (Instruction Set Architecture)]]

## Modos de direccionamiento

[[Modo de direccionamiento en MIPS]]

## Diseño de un Microprocesador MIPS Monociclo (Un Ciclo)

Este diseño representa una implementación básica de la arquitectura MIPS de 32 bits donde **cada instrucción se completa en un único ciclo de reloj**. Por eso también se le llama "uniciclo combinacional". Aunque simple, sirve como base para entender diseños más complejos.

![image.png](media/circuito-alto.png)

## Instrucciones Soportadas

El diseño se centrará en implementar un subconjunto representativo de instrucciones MIPS:

1.  **Referencia a Memoria:**
    *   `lw` (load word): Carga una palabra desde la memoria a un registro.
    *   `sw` (store word): Almacena una palabra desde un registro a la memoria.
2.  **Aritmético-Lógicas (Tipo R):**
    *   `add`, `sub`, `and`, `or`, `slt` (set on less than), etc. Operan sobre registros.
3.  **Saltos:**
    *   `beq` (branch on equal): Salta a una dirección si dos registros son iguales.
    *   `j` (jump): Salta incondicionalmente a una dirección.

## Componentes Principales del Datapath

Basado en el diagrama y las notas, los bloques funcionales clave son:

1.  **[[PC (Program Counter)]]**
2.  **[[Instruction Memory (Memoria de Instrucciones)]]**
3.  **[[Registers (Banco de Registros)]]**
4.  **[[ALU (Arithmetic Logic Unit)]]**
5.  **[[Data Memory (Memoria de Datos)]]**
6.  **Adders (Sumadores):**
    *   **Adder 1 (PC+4):** Calcula la dirección de la siguiente instrucción secuencial sumando 4 al PC actual.
    *   **Adder 2 (Branch Target):** Calcula la dirección de destino para la instrucción `beq`. Suma la salida del Adder 1 (PC+4) con el desplazamiento (`offset` de la instrucción, extendido con signo y desplazado 2 bits a la izquierda).

7.  **Multiplexores (Mux):**
    *   Componentes clave para seleccionar qué dato usar en diferentes puntos del datapath, dependiendo de la instrucción que se esté ejecutando. Son controlados por señales derivadas del `opcode`.
    *   **Ejemplos de uso:**
        *   Seleccionar el segundo operando de la ALU (puede ser un registro `rt` o el inmediato extendido).
        *   Seleccionar qué valor escribir de vuelta en el banco de registros (el resultado de la ALU o el dato leído de memoria).
        *   Seleccionar la próxima dirección para el PC (PC+4, la dirección de destino de `beq`, o la dirección de destino de `j`).

## Flujo de Ejecución General (RTL Simplificado)

[[Flujo de Ejercucion (RTL Simplificado) en Monociclo]]

## Consideraciones del Diseño Monociclo

*   **Ventaja:** Simple de diseñar y entender. La unidad de control es combinacional.
*   **Desventaja:** El rendimiento está limitado por la instrucción más lenta (normalmente `lw`, que accede a memoria de instrucciones, registros, ALU y memoria de datos). Todas las instrucciones tardan lo mismo, incluso las más rápidas, lo que lo hace ineficiente. Diseños más avanzados (multiciclo, pipeline) abordan esta limitación.


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


En MIPS, la dirección de memoria es de 32 bits. Los 4 bits más significativos (los primeros de izquierda a derecha) determinan en qué segmento de memoria estamos ubicados. Los 28 bits restantes indican el desplazamiento o la dirección dentro de ese segmento, lo que permite acceder a un rango de hasta 2^28 bytes (256 MB) dentro de cada segmento.

Por ejemplo, si la dirección del *program counter* (PC) es: 1010 0101010000101010101010101010

Los 4 bits más significativos son `1010`, lo que indica que estamos en el segmento `0xA`. El resto, `0101010000101010101010101010`, representa la posición dentro de ese segmento.
