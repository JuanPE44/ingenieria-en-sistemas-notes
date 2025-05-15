### Formato de Instrucción Tipo-J (Jump)

Las instrucciones de Tipo-J se utilizan exclusivamente para **saltos incondicionales** (`j` y `jal`). Permiten transferir el flujo de ejecución a una dirección de instrucción lejana dentro del programa.

**Estructura (32 bits):**

![image.png](tipo-j.png)


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