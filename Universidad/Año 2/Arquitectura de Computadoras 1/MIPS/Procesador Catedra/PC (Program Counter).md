El Program Counter (PC) es un registro **fundamental y crítico** dentro de cualquier procesador, incluido nuestro diseño MIPS monociclo. Su función principal es **mantener la dirección de memoria de la próxima instrucción que el procesador debe buscar (fetch) y ejecutar**. Piensa en él como el "dedo" que apunta a la línea actual del programa que se está leyendo.

Aquí desglosamos los puntos clave con más detalle:

1.  **Registro de 32 bits que almacena la dirección de la próxima instrucción:**
    *   **¿Por qué 32 bits?** La arquitectura MIPS que estamos considerando es de 32 bits. Esto significa que las direcciones de memoria que utiliza para acceder tanto a instrucciones como a datos son de 32 bits. Por lo tanto, el PC *debe* ser capaz de almacenar una dirección completa de 32 bits para poder apuntar a cualquier ubicación válida dentro del espacio de direcciones de la memoria de instrucciones.
    *   **"Próxima" Instrucción:** Es crucial entender que el PC *siempre* apunta a la instrucción que está *a punto de ser buscada* o que *está siendo buscada* en el ciclo actual. Una vez que esa instrucción se ha buscado, el procesador necesita saber cuál será la siguiente, y para eso se actualiza el PC.

2.  **Normalmente se incrementa en 4 en cada ciclo:**
    *   **¿Por qué 4?** Las instrucciones MIPS tienen una longitud fija de 32 bits, lo que equivale a 4 bytes. La memoria se direcciona a nivel de byte (cada dirección de memoria apunta a un byte individual). Por lo tanto, para pasar de la dirección de una instrucción a la dirección de la *siguiente instrucción consecutiva* en la memoria, necesitamos sumar 4 a la dirección actual.
    *   **Hardware Implicado:** En el diagrama del datapath, verás un **Sumador (Adder)** dedicado específicamente a esta tarea. Una de sus entradas es el valor actual del PC, y la otra entrada es la constante '4'. La salida de este sumador (`PC + 4`) representa la dirección de la siguiente instrucción si el programa sigue su flujo secuencial normal. Esta dirección calculada (`PC + 4`) es una de las *posibles* entradas al multiplexor que decide qué valor se cargará en el PC al final del ciclo.

3.  **En caso de un salto (`beq` exitoso o `j`), se carga con la dirección de destino del salto:**
    *   **Flujo No Secuencial:** Los programas no siempre ejecutan una instrucción tras otra. Las estructuras de control como condicionales (`if`/`else`, implementados con `beq`, `bne`), bucles (`while`, `for`) y llamadas a funciones requieren cambiar el flujo de ejecución a una ubicación diferente en el código.
    *   **Instrucciones de Salto/Bifurcación:**
        *   **`beq` (Branch on Equal):** Compara dos registros. Si son iguales, el flujo debe saltar a una dirección diferente (la "etiqueta" o *branch target address*). Esta dirección se calcula de forma *relativa al PC*: se toma el `offset` de 16 bits de la instrucción, se extiende en signo, se multiplica por 4 (desplazamiento a la izquierda de 2 bits) y se suma al valor de `PC + 4` (calculado por el Adder 1). El resultado es la dirección de destino del salto condicional.
        *   **`j` (Jump):** Realiza un salto incondicional a una dirección especificada en la instrucción. La dirección de destino se calcula usando el modo de direccionamiento *pseudo-directo*.
    *   **Hardware Implicado:**
        *   Se calcula la dirección de destino del salto (ya sea para `beq` o `j`) utilizando lógica adicional (otro sumador para `beq`, lógica de concatenación para `j`).
        *   Un **Multiplexor (Mux)** se coloca justo antes de la entrada del registro PC. Este Mux es crucial. Tiene varias entradas:
            *   La salida del sumador `PC + 4` (flujo secuencial).
            *   La dirección de destino calculada para `beq` (si la condición es verdadera).
            *   La dirección de destino calculada para `j`.
        *   Las **señales de control** (generadas a partir del `opcode` de la instrucción actual y, en el caso de `beq`, del resultado de la comparación de la ALU) determinan cuál de estas entradas se selecciona.
        *   La salida seleccionada por el Mux es el valor que se **cargará** en el registro PC al final del ciclo de reloj actual.

**En Resumen en el Monociclo:**

*   Al **inicio** de un ciclo de reloj, el valor del PC se envía a la Memoria de Instrucciones para buscar la instrucción actual.
*   **Durante** el ciclo, se calcula `PC + 4` y, si la instrucción es un salto, también se calcula la dirección de destino del salto.
*   La unidad de control determina si se debe seguir secuencialmente (`PC + 4`) o si se debe tomar un salto (usando la dirección de destino calculada).
*   **Al final** del ciclo de reloj (en el flanco de subida, por ejemplo), el valor seleccionado por el Mux se escribe en el registro PC.
*   Este **nuevo valor** en el PC será la dirección utilizada para buscar la instrucción en el **siguiente** ciclo de reloj.

El PC es, por tanto, el motor que impulsa la ejecución del programa, paso a paso, instrucción tras instrucción, ya sea secuencialmente o saltando a través del código según sea necesario.