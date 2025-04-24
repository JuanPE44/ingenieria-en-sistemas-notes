La Memoria de Instrucciones es un componente esencial del procesador, actuando como el repositorio donde reside el programa que se va a ejecutar. Su función es simple pero vital: **suministrar la instrucción correcta al resto del procesador en cada ciclo de reloj**.
[[PC (Program Counter)]]
Vamos a desglosar sus características clave:

1.  **Almacena las instrucciones del programa:**
    *   **Contenido:** Guarda la secuencia de instrucciones de máquina (código binario de 32 bits por instrucción) que componen el programa compilado. Cada instrucción MIPS ocupa exactamente 32 bits (4 bytes).
    *   **Origen:** Estas instrucciones son el resultado de compilar un programa escrito en un lenguaje de alto nivel (como C) o en ensamblador MIPS. Antes de que el procesador pueda ejecutar el programa, este código máquina debe cargarse en esta memoria.
    *   **Organización:** Se puede pensar en ella como un gran array o una lista numerada. Cada "casilla" o posición tiene una dirección única, y cada una almacena una instrucción de 32 bits.

2.  **Recibe la dirección del PC y devuelve la instrucción de 32 bits ubicada en esa dirección:**
    *   **Entrada (Input):** Su única entrada principal es la **dirección** proporcionada por el **Program Counter (PC)**. El valor actual del PC le dice a la Memoria de Instrucciones *cuál* instrucción debe buscar. Esta dirección es de 32 bits.
    *   **Operación:** Internamente, la memoria utiliza la dirección recibida para localizar la instrucción correspondiente. Dado que la memoria es direccionable por bytes pero las instrucciones son de 4 bytes (32 bits), la dirección del PC siempre estará alineada a 4 bytes (los dos bits menos significativos serán '00'). La memoria lee los 4 bytes (la palabra completa de 32 bits) a partir de esa dirección.
    *   **Salida (Output):** Su única salida es la **instrucción de 32 bits** leída de la dirección especificada por el PC. Esta instrucción es luego enviada a otras partes del procesador (como la unidad de control y el banco de registros) para ser decodificada y ejecutada.

3.  **Es una memoria de solo lectura (Read-Only) en este modelo simple:**
    *   **¿Por qué Read-Only?** Para simplificar el diseño básico del procesador monociclo, asumimos que el programa se carga en la memoria *antes* de empezar la ejecución y *no cambia* mientras el procesador está funcionando. El procesador solo necesita *leer* las instrucciones, no modificarlas.
    *   **Implicaciones en el Diseño:** Esto significa que no necesitamos incluir lógica ni puertos para escribir en la Memoria de Instrucciones (como sí necesitamos para la Memoria de Datos con la instrucción `sw`). No hay señales de control como `MemWrite` para esta memoria.
    *   **Diferencia con la Memoria de Datos:** Es crucial distinguirla de la `Data Memory`. La `Data Memory` almacena los datos con los que trabaja el programa (variables, arrays, etc.) y *sí* necesita ser de lectura y escritura (para soportar `lw` y `sw`). La `Instruction Memory` solo guarda el código.
    *   **En Sistemas Reales:** Aunque en sistemas reales la memoria de instrucciones suele estar en la RAM principal (que es de lectura/escritura), para el propósito de entender el flujo de datos y control de un procesador simple, tratarla como ROM (Read-Only Memory) es una abstracción válida y útil.

**En Resumen:**

La Memoria de Instrucciones actúa como un "libro de recetas" para el procesador. El PC le dice qué página (dirección) leer, y la memoria le entrega la receta completa (la instrucción de 32 bits) de esa página. En el modelo monociclo, este libro no se reescribe durante la ejecución. Su salida es el punto de partida para que el resto del hardware sepa qué hacer en el ciclo actual.