## Definición y Concepto

*   Un **Tipo de Dato Abstracto (TDA)** es un tipo de dato definido por el programador que encapsula un **Dominio** (conjunto de valores) y un conjunto de **Operaciones** permitidas sobre ese dominio.
*   Se basa en los principios de:
    *   **[[Abstraccion de Datos]]:** Separar la especificación lógica del tipo de su implementación física.
    *   **[[Ocultamiento de Informacion]]:** La representación interna y los detalles de implementación están ocultos al usuario del TDA.
    *   **[[Encapsulamiento]]:** Agrupar el dominio y las operaciones en una unidad sintáctica (ej. `CLASE` en C++).
*   Los TDA permiten operar sobre los datos únicamente a través de un **[[Conjunto preestablecido de operaciones]]**, similar a los tipos primitivos (`int`, `bool`, etc.).
*   Superan las limitaciones de las estructuras de datos simples (arreglos, registros) que no garantizan inherentemente el ocultamiento o un conjunto fijo de operaciones.
*   Son un pilar fundamental en la **Programación Orientada a Objetos**.


# [[Especificacion algebraica]]
## Tipos de Operaciones TDA

*   **Constructoras:** Crean o modifican instancias del TDA (ej: `inicPila`, `agregarPila`). Las *básicas* son el conjunto mínimo para generar todos los valores.
*   **Observadoras:** Devuelven información sobre el estado del TDA sin alterarlo (ej: `vaciaPila`, `tope`, `longLista`, `recuperarFila`).
*   **Transformadoras/Modificadoras:** Modifican el estado del TDA (ej: `eliminarPila`, `eliminarFila`). Su comportamiento se define mediante axiomas sobre las constructoras.

## Ejemplos de TDA

### TDA Pila (Stack)

*   **Característica:** Secuencia LIFO (Last-In, First-Out). El acceso es siempre por el `tope`.
*   **Operaciones Clave:** `inicPila`, `agregarPila`, `tope`, `eliminarPila`, `vaciaPila`.
*   **Axiomas:** Definen cómo `tope`, `eliminarPila` y `vaciaPila` actúan sobre `inicPila` y `agregarPila(p,e)`.

### TDA Fila (Queue)

*   **Característica:** Secuencia FIFO (First-In, First-Out). Se agrega por un extremo (`último`) y se accede/elimina por el otro (`primero`).
*   **Operaciones Clave:** `inicFila`, `agregarFila`, `recuperarFila`, `eliminarFila`, `vaciaFila`.
*   **Axiomas:** Más complejos que la Pila, a menudo recursivos, para mantener el orden FIFO al eliminar o recuperar.

### TDA Lista (List)

*   **Característica:** Secuencia ordenada donde se puede agregar, eliminar y acceder a elementos en cualquier posición válida `i`.
*   **Operaciones Clave:** `inicLista`, `agregarLista(l, i, e)`, `recuperarLista(l, i)`, `eliminarLista(l, i)`, `longLista`.
*   **Axiomas:** Los más complejos, involucran la posición (`i`, `j`) y a menudo casos distintos según la relación entre las posiciones de inserción/eliminación/acceso.

## Especificaciones Parametrizadas

*   Permiten definir TDAs genéricos que pueden trabajar con diferentes tipos de elementos base (ej. `Pila[Natural]`, `Pila[String]`).
*   Se declaran con un parámetro de tipo, como `CLASS Pila [Elemento: ANY]` o simplemente `CLASS Lista [Elemento]`.

## TDAs y Abstracciones Procedurales

*   Las operaciones definidas en un TDA se utilizan como bloques de construcción para implementar algoritmos más complejos (funciones, procedimientos).
*   La **ejecución simbólica** es una técnica para trazar el comportamiento de estos algoritmos, aplicando los axiomas del TDA para simplificar las expresiones y seguir el estado de las variables TDA.