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