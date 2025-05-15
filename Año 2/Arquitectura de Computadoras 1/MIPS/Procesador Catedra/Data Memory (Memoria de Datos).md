La Memoria de Datos es el componente del sistema donde el programa almacena y recupera los datos con los que opera durante su ejecución. A diferencia de la Memoria de Instrucciones (que contiene el código y es de solo lectura en nuestro modelo), la Memoria de Datos es de **lectura y escritura**, ya que los valores de las variables cambian constantemente.

Aquí explicamos sus características en detalle:

1.  **Almacena los datos del programa:**
    *   **Contenido:** Guarda los valores de las variables, los elementos de los arrays, las estructuras de datos, y también es donde se suele ubicar la pila (stack) del programa (utilizada para variables locales, parámetros de funciones y guardar registros temporalmente).
    *   **Organización:** Al igual que la memoria de instrucciones, se puede ver como un gran array de bytes. En MIPS de 32 bits, cada byte tiene una dirección única. Sin embargo, las instrucciones `lw` y `sw` operan sobre **palabras** (words) de 32 bits (4 bytes).
    *   **Capacidad:** Teóricamente, en un sistema de 32 bits, podría direccionar hasta 2^32 bytes (4 Gigabytes) de datos, aunque la cantidad física real puede ser menor.

2.  **Se accede mediante las instrucciones `lw` (load word) y `sw` (store word):**
    *   **Arquitectura Load/Store:** MIPS es una arquitectura "Load/Store". Esto significa que las operaciones aritmético-lógicas (como `add`, `sub`) *solo* pueden operar con datos que están en los registros. No pueden acceder directamente a la memoria.
    *   **Puente entre Registros y Memoria:** Las instrucciones `lw` y `sw` son el puente necesario.
        *   `lw`: Carga (lee) una palabra de 32 bits desde una dirección específica en la Memoria de Datos y la coloca en un registro destino (`rt`).
        *   `sw`: Almacena (escribe) una palabra de 32 bits desde un registro fuente (`rt`) a una dirección específica en la Memoria de Datos.
    *   **Otras (no siempre en el diseño básico):** Existen variantes como `lb` (load byte), `lh` (load halfword), `sb` (store byte), `sh` (store halfword) que manejan unidades de datos más pequeñas, pero `lw` y `sw` son las fundamentales para palabras completas.

3.  **Recibe entradas clave para operar:**
    *   **Address (Dirección):**
        *   **Origen:** Esta entrada de 32 bits proviene directamente del **resultado de la ALU (`ALUResult`)**.
        *   **Cálculo:** Para `lw` y `sw`, la ALU calcula esta dirección sumando el contenido del registro base (especificado por `rs`) y el valor inmediato de 16 bits (offset) de la instrucción, después de haber sido extendido en signo a 32 bits. `Dirección = Registros[rs] + SignExtend(offset)`.
        *   **Alineación:** Para `lw` y `sw`, esta dirección *debe* estar alineada a palabra, lo que significa que debe ser un múltiplo de 4 (los dos bits menos significativos deben ser 00). Si no lo está, se produciría un error de alineación en un sistema real (aunque en simuladores simples a veces se ignora).
    *   **Write Data (Dato a Escribir):**
        *   **Origen:** Esta entrada de 32 bits proviene de la salida `Read data 2` del **Banco de Registros**. Corresponde al valor del registro especificado por el campo `rt` de la instrucción `sw`.
        *   **Uso:** Solo se utiliza durante una instrucción `sw`. La memoria tomará este valor y lo almacenará en la `Address` especificada. Para una instrucción `lw`, este puerto de entrada es ignorado por la memoria.
    *   **Señales de Control:**
        *   **`MemRead`:** Una señal de 1 bit generada por la Unidad de Control principal. Se activa (pone a '1') **solo** cuando la instrucción es `lw`. Indica a la memoria que debe realizar una operación de lectura en la `Address` dada y poner el resultado en su salida `Read Data`.
        *   **`MemWrite`:** Una señal de 1 bit generada por la Unidad de Control principal. Se activa (pone a '1') **solo** cuando la instrucción es `sw`. Indica a la memoria que debe tomar el valor presente en la entrada `Write Data` y almacenarlo en la `Address` dada.
        *   **Exclusión Mutua:** En cualquier ciclo dado, solo una de estas señales (`MemRead` o `MemWrite`) puede estar activa, o ninguna de las dos (si la instrucción no accede a la memoria de datos, como `add` o `beq`).

4.  **Genera una salida (si se lee):**
    *   **Read Data (Dato Leído):**
        *   **Función:** Es la salida de 32 bits de la Memoria de Datos.
        *   **Validez:** Solo contiene un valor válido cuando se está ejecutando una instrucción `lw` (es decir, cuando `MemRead` está activo). En ese caso, contiene la palabra de 32 bits leída de la `Address` especificada.
        *   **Destino:** Esta salida se conecta a uno de los Mux que selecciona qué dato se escribirá de vuelta en el Banco de Registros (el Mux controlado por `MemToReg`). Para `lw`, este dato leído es el que finalmente se escribe en el registro `rt`.
        *   **Irrelevante en otros casos:** Si `MemRead` está inactivo (durante `sw`, `add`, `beq`, etc.), el valor en esta salida no importa y no se utiliza.

**En Resumen:**

La Memoria de Datos es el almacén principal para los datos variables del programa. Actúa bajo las órdenes de las instrucciones `lw` (leer) y `sw` (escribir). Recibe la dirección calculada por la ALU y, dependiendo de las señales `MemRead` y `MemWrite` de la Unidad de Control, lee un dato y lo envía hacia el Banco de Registros (`lw`) o toma un dato del Banco de Registros y lo escribe en la ubicación especificada (`sw`). Es una etapa crucial en el datapath, y su tiempo de acceso suele ser uno de los factores limitantes en el rendimiento del procesador, especialmente en diseños simples como el monociclo.