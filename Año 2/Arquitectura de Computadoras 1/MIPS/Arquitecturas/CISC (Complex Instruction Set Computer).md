CISC es un tipo de diseño de microprocesadores que se caracteriza por tener un conjunto de instrucciones **amplio y complejo**. La filosofía detrás de CISC es proporcionar instrucciones que puedan realizar tareas complejas en un solo paso, intentando acercar el lenguaje máquina al lenguaje de alto nivel y simplificar la tarea del programador (o del compilador en tiempos más modernos).

## Características Principales

*   **Conjunto de Instrucciones Complejo:**
    *   Contiene un gran número de instrucciones.
    *   Las instrucciones pueden tener formatos de longitud variable y realizar operaciones complejas (ej. una sola instrucción puede leer de memoria, realizar una operación aritmética y escribir el resultado en memoria).
*   **Acceso Directo a Memoria:**
    *   Muchas instrucciones pueden operar directamente sobre operandos en la memoria principal, no solo en registros.
*   **Número Reducido de Registros (Históricamente):**
    *   Tradicionalmente, las arquitecturas CISC tenían menos registros de propósito general en comparación con RISC, ya que muchas operaciones podían realizarse directamente en memoria.
*   **Microcódigo:**
    *   Las instrucciones complejas a menudo se decodifican internamente en una secuencia de operaciones más simples llamadas microinstrucciones o microcódigo, que son ejecutadas por el hardware subyacente.
*   **Énfasis en el Hardware:**
    *   Se busca que el hardware maneje directamente la mayor cantidad de complejidad posible.

## Ventajas

*   **Menor Densidad de Código (Potencialmente):** Una tarea compleja puede requerir menos líneas de código máquina, lo que históricamente era importante cuando la memoria era cara y limitada.
*   **Compiladores más Sencillos (Históricamente):** Era más fácil para los primeros compiladores mapear construcciones de lenguaje de alto nivel a instrucciones CISC complejas.

## Desventajas

*   **Diseño de Hardware Complejo:** La gran cantidad y complejidad de las instrucciones dificulta el diseño, la implementación y la verificación del procesador.
*   **Ejecución Lenta y Variable:** Las instrucciones complejas requieren múltiples ciclos de reloj para ejecutarse, y el tiempo varía según la instrucción, lo que complica el [[Pipelining (Segmentación de Cauce)]].
*   **Mayor Consumo de Energía:** La complejidad del hardware generalmente implica un mayor consumo.
*   **Pipelining Menos Eficiente:** La variabilidad en la duración y formato de las instrucciones dificulta la implementación eficiente de pipelines profundos.

## Ejemplos

La arquitectura más conocida y dominante basada en CISC es la **x86** (utilizada por Intel y AMD en la mayoría de los ordenadores personales y servidores). Otros ejemplos históricos incluyen el VAX y el Motorola 68k.

## Nota Importante

Es relevante mencionar que las arquitecturas modernas, incluso las CISC como x86, han adoptado muchas técnicas originalmente asociadas con RISC internamente (como el uso de micro-operaciones similares a RISC y pipelining avanzado) para mejorar el rendimiento. Por lo tanto, la distinción entre RISC y CISC es menos marcada a nivel de implementación interna en los procesadores de alto rendimiento actuales, aunque sigue siendo válida a nivel de conjunto de instrucciones visible para el programador/compilador.