Los operadores son símbolos especiales que le indican al compilador que realice operaciones específicas (matemáticas, lógicas, de bits, etc.) sobre uno, dos o tres operandos. El resultado de una operación suele ser un valor.

#### Expresiones Booleanas y el Tipo `bool`

C++ introduce el tipo de dato `bool`, que puede almacenar dos únicos valores literales: `true` (verdadero) y `false` (falso). Una **expresión booleana** (o lógica) es una combinación de operandos y operadores que, al evaluarse, produce un resultado `true` o `false`.

Es importante destacar una diferencia con C:

- **C++**: Utiliza `bool` para valores de verdad.
- **C**: No posee un tipo booleano nativo. En su lugar, utiliza el tipo `int`. El valor `0` se interpreta como falso, y cualquier otro valor entero distinto de cero se interpreta como verdadero.

#### Precedencia y Asociatividad de Operadores

Cuando una expresión contiene múltiples operadores, C++ sigue reglas específicas para determinar el orden en que se evalúan:

1. **Precedencia (Nivel de precedencia):**
    
    - Los operadores con mayor precedencia se evalúan antes que los operadores con menor precedencia.
    - Por ejemplo, en la expresión `a + b * c`, la multiplicación (`*`) generalmente tiene mayor precedencia que la adición (`+`), por lo que `b * c` se calcularía primero.
2. **Asociatividad (Agrupamiento):**
    
    - Cuando en una expresión hay varios operadores con el _mismo nivel de precedencia_, la asociatividad determina el orden de evaluación.
    - Puede ser:
        - **De izquierda a derecha:** Los operadores se evalúan desde el que aparece más a la izquierda hacia la derecha. (Ej: `a - b - c` se evalúa como `(a - b) - c`).
        - **De derecha a izquierda:** Los operadores se evalúan desde el que aparece más a la derecha hacia la izquierda. (Ej: los operadores de asignación como `a = b = c` se evalúan como `a = (b = c)`).
3. **Uso de Paréntesis `()`:**
    
    - Puedes alterar el orden de evaluación predeterminado usando paréntesis. Las expresiones dentro de los paréntesis se evalúan primero. Si hay paréntesis anidados, los más internos se evalúan primero.
    - Esto es muy útil para clarificar expresiones complejas o para forzar un orden específico que difiere de la precedencia y asociatividad naturales.

#### Lista de Operadores por Precedencia (de Mayor a Menor)

|           |                                                                               |                                                                                                                                       |                     |
| --------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ------------------- |
| **Nivel** | **Descripción**                                                               | **Operadores**                                                                                                                        | **Asociatividad**   |
| 1         | Ámbito                                                                        | `::`                                                                                                                                  | Izquierda a derecha |
| 2         | Posfijo, Acceso, Conversión explícita, `typeid`                               | `()` `[]` `.` `->` `++` `--` (posfijos)&lt;br>`dynamic_cast` `static_cast`&lt;br>`reinterpret_cast` `const_cast` `typeid`             | Izquierda a derecha |
| 3         | Unarios (prefijo), Indirección y Referencia, `sizeof`, `new`, `delete`, Signo | `++` `--` (prefijos)&lt;br>`~` `!` `sizeof` `new` `delete`&lt;br>`*` (indirección) `&` (dirección/referencia)&lt;br>`+` `-` (unarios) | Derecha a izquierda |
| 4         | Conversión de tipo (estilo C)                                                 | `(type)`                                                                                                                              | Derecha a izquierda |
| 5         | Acceso a miembro (punteros)                                                   | `.*` `->*`                                                                                                                            | Izquierda a derecha |
| 6         | Multiplicativos                                                               | `*` `/` `%`                                                                                                                           | Izquierda a derecha |
| 7         | Aditivos                                                                      | `+` `-`                                                                                                                               | Izquierda a derecha |
| 8         | Desplazamiento de bits                                                        | `<<` `>>`                                                                                                                             | Izquierda a derecha |
| 9         | Relacionales                                                                  | `<` `>` `<=` `>=`                                                                                                                     | Izquierda a derecha |
| 10        | Igualdad                                                                      | `==` `!=`                                                                                                                             | Izquierda a derecha |
| 11        | AND a nivel de bits                                                           | `&`                                                                                                                                   | Izquierda a derecha |
| 12        | XOR a nivel de bits                                                           | `^`                                                                                                                                   | Izquierda a derecha |
| 13        | OR a nivel de bits                                                            | `                                                                                                                                     | `                   |
| 14        | AND lógico                                                                    | `&&`                                                                                                                                  | Izquierda a derecha |
| 15        | OR lógico                                                                     | `                                                                                                                                     | `                   |
| 16        | Condicional (ternario)                                                        | `?:`                                                                                                                                  | Derecha a izquierda |
| 17        | Asignación                                                                    | `=` `*=` `/=` `%=` `+=` `-=` `>>=` `<<=` `&=` `^=` `                                                                                  | =`                  |
| 18        | Coma                                                                          | `,`                                                                                                                                   | Izquierda a derecha |

**Notas importantes sobre algunos operadores:**

- **Operadores Unarios vs. Binarios:** Algunos símbolos como `*`, `&`, `+`, `-` pueden ser unarios (operan sobre un solo operando, ej: `-5`, `*ptr`) o binarios (operan sobre dos operandos, ej: `a * b`, `a + b`). Su significado y precedencia pueden cambiar según el contexto. La tabla distingue esto (ej. nivel 3 para unarios, nivel 6 y 7 para binarios).
- **`++` y `--` (Incremento y Decremento):**
    - **Posfijo (`variable++`):** Devuelve el valor original de la variable y _luego_ la incrementa/decrementa.
    - **Prefijo (`++variable`):** Incrementa/decrementa la variable _primero_ y luego devuelve el nuevo valor.
- **Operadores de Bits vs. Lógicos:**
    - **De Bits (`&`, `|`, `^`, `~`, `<<`, `>>`):** Realizan operaciones directamente sobre la representación binaria de los números.
    - **Lógicos (`&&`, `||`, `!`):** Operan sobre valores booleanos (o valores que se pueden convertir a booleanos). `&&` y `||` realizan evaluación de "cortocircuito" (si el primer operando es suficiente para determinar el resultado, el segundo no se evalúa).
- **Operador Condicional `?:` (Ternario):** Es una forma concisa de escribir una sentencia `if-else`. Su forma es `condicion ? expresion_si_verdadero : expresion_si_falso`.
- **Operador Coma `,`:** Evalúa la primera expresión, descarta su resultado, luego evalúa la segunda expresión y su resultado es el de esta última. Se usa con poca frecuencia, principalmente en bucles `for` para múltiples inicializaciones o incrementos.

Entender la precedencia y asociatividad es crucial para escribir código C++ correcto y predecible, y para leer y entender el código escrito por otros. Cuando tengas dudas, ¡usa paréntesis para asegurar el orden de evaluación deseado!

