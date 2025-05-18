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


**Instrucciones Complejas de Transferencia de Datos:**

*   `mov string1, string2, length`:  Mueve un bloque de memoria de `string2` a `string1` con una longitud especificada en `length`.  Esto podría implicar la carga de múltiples bytes, el incremento de punteros y la verificación de límites, todo en una sola instrucción.
*   `load_effective_address dest, [base + index * scale + displacement]`: Calcula una dirección de memoria compleja (usando un registro base, un registro índice multiplicado por un factor de escala y un desplazamiento) y guarda la dirección resultante en `dest`.  Esto es útil para acceder a elementos dentro de arreglos o estructuras de datos complejas.

**Instrucciones Aritméticas y Lógicas Complejas:**

*   `add mem_location, value`: Suma un valor a una ubicación de memoria directamente.  En lugar de cargar el valor de la memoria en un registro, sumarle algo y luego guardarlo de vuelta, esta instrucción lo hace todo en un solo paso.
*   `multiply_accumulate dest, src1, src2`: Multiplica `src1` y `src2`, y luego suma el resultado al valor actual de `dest`.  Esto es común en procesamiento de señales digitales y otras aplicaciones donde se realizan muchas multiplicaciones y acumulaciones.
*   `complex_divide dest, src`: Realiza una división compleja (números complejos) de `dest` entre `src`.  Esto implicaría múltiples operaciones aritméticas (multiplicaciones, sumas, restas) para manejar las partes real e imaginaria de los números complejos.

**Instrucciones de Control de Flujo Complejas:**

*   `loop label, count`: Decrementa un contador (`count`) y salta a la etiqueta `label` si el contador no es cero.  Esto simplifica la creación de bucles.
*   `call function_address`: Llama a una función en la dirección especificada, guardando la dirección de retorno en la pila y transfiriendo el control a la función.  Esto es similar a `jal` en MIPS, pero en CISC, la instrucción `call` podría manejar más automáticamente el manejo de la pila y los parámetros.

**Instrucciones de Manejo de Cadenas:**

*   `compare_strings string1, string2, length`: Compara dos cadenas de caracteres (`string1` y `string2`) hasta una longitud máxima de `length`.  La instrucción podría establecer flags (banderas) indicando si las cadenas son iguales, cuál es mayor, etc.
*   `search_string string, substring`: Busca la primera ocurrencia de `substring` dentro de `string`.

**Ejemplo (Pseudo-código CISC):**

```assembly
# Ejemplo de pseudo-código CISC

# Mover un bloque de memoria de source a destination
mov destination, source, 100  # Mueve 100 bytes

# Calcular la dirección de un elemento en un arreglo
load_effective_address address, [array_base + index * 4] # array_base es la dirección base del arreglo, index es el índice, 4 es el tamaño de cada elemento

# Sumar un valor a una ubicación de memoria
add memory_location, 5

# Bucle
loop_start:
    # ... hacer algo ...
    loop loop_start, 10  # Repetir 10 veces
```

**Características Clave de las Instrucciones CISC:**

*   **Complejidad:**  Las instrucciones CISC realizan múltiples operaciones en una sola instrucción.
*   **Variabilidad:**  Las instrucciones CISC tienen muchos modos de direccionamiento diferentes (formas de especificar las direcciones de memoria).
*   **Tamaño Variable:**  Las instrucciones CISC pueden tener diferentes longitudes en bytes.
*   **Menos Instrucciones, Más Trabajo:**  El objetivo es realizar más trabajo con menos instrucciones, lo que teóricamente podría simplificar la programación (aunque a menudo complica el diseño del hardware).

**Contraste con RISC:**

En contraste, las instrucciones RISC son típicamente más simples, de longitud fija y realizan una sola operación básica.  La filosofía RISC es que es mejor tener muchas instrucciones simples que se ejecutan rápidamente, en lugar de unas pocas instrucciones complejas que tardan más.

Espero que estos ejemplos te den una buena idea de cómo son las instrucciones CISC.  Ten en cuenta que la arquitectura x86 es el ejemplo más común de CISC en uso hoy en día, pero hay otras arquitecturas CISC históricas.
