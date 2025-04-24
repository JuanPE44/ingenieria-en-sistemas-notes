La **Arquitectura Harvard** es un diseño de arquitectura de computadoras que se distingue por utilizar **espacios de memoria físicamente separados** para las **instrucciones** y para los **datos**.

*   **Memorias Separadas:** Una memoria almacena el código del programa (instrucciones) y otra almacena los datos que manipula el programa.
*   **Buses Separados (Generalmente):** Cada memoria suele tener su propio bus (de datos y direcciones), permitiendo la comunicación independiente y simultánea con el procesador.
*   **Contraste con Von Neumann:** La Arquitectura Von Neumann usa una *única* memoria y bus para instrucciones y datos, forzando accesos secuenciales.

**Ventaja Principal:** Permite al procesador buscar la siguiente instrucción en la memoria de instrucciones *al mismo tiempo* que accede (lee/escribe) a la memoria de datos para la instrucción actual. Esto mejora el **paralelismo** y el **rendimiento**, especialmente en pipelines.

## ¿Por qué MIPS utiliza la Arquitectura Harvard?

MIPS fue diseñado buscando **alto rendimiento** mediante un **pipelining eficiente**. La Arquitectura Harvard es clave para esto:

1.  **Facilita el Pipelining:**
    *   El pipeline de MIPS tiene etapas como Búsqueda de Instrucción (IF) y Acceso a Memoria (MEM).
    *   Harvard permite que la etapa **IF** (acceso a memoria de instrucciones) y la etapa **MEM** (acceso a memoria de datos para `lw`/`sw`) ocurran **simultáneamente** sin competir por el mismo bus.
    *   Esto evita detenciones (stalls) en el pipeline, manteniendo un flujo constante y rápido.

2.  **Maximiza el Ancho de Banda de Memoria:**
    *   Tener buses separados duplica el ancho de banda efectivo entre el procesador y las memorias.

3.  **Alineación con la Filosofía RISC:**
    *   La simplicidad de RISC se complementa con la separación de memorias, que simplifica el control del pipeline y optimiza los accesos para una ejecución rápida.
