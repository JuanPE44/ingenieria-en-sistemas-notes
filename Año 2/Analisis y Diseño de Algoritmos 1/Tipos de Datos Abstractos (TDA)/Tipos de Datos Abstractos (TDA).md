## Definición y Concepto

*   Un **Tipo de Dato Abstracto (TDA)** es un tipo de dato definido por el programador que encapsula un **Dominio** (conjunto de valores) y un conjunto de **Operaciones** permitidas sobre ese dominio.
*   Se basa en los principios de:
    *   **[[Abstraccion de Datos]]:** Separar la especificación lógica del tipo de su implementación física.
    *   **[[Ocultamiento de Informacion]]:** La representación interna y los detalles de implementación están ocultos al usuario del TDA.
    *   **[[Encapsulamiento]]:** Agrupar el dominio y las operaciones en una unidad sintáctica (ej. `CLASE` en C++).
*   Los TDA permiten operar sobre los datos únicamente a través de un **[[Conjunto preestablecido de operaciones]]**, similar a los tipos primitivos (`int`, `bool`, etc.).
*   Superan las limitaciones de las estructuras de datos simples (arreglos, registros) que no garantizan inherentemente el ocultamiento o un conjunto fijo de operaciones.
*   Son un pilar fundamental en la **Programación Orientada a Objetos**.

## Especificación Algebraica

La **Especificación Algebraica** es una forma **formal y matemática** de definir un Tipo de Dato Abstracto (TDA). En lugar de describir el TDA con lenguaje natural (que puede ser ambiguo) o con código de un lenguaje de programación específico (que revela la implementación), se utilizan conceptos del álgebra.

Piensa en ello como crear un "plano" matemático muy preciso del TDA, centrándose exclusivamente en su **comportamiento lógico** y sus **propiedades**, sin decir nada sobre cómo se construirá internamente (cómo se implementará en C++, Java, etc.).

Los componentes clave de una Especificación Algebraica, como se ve en tu texto, son:

1.  **Signatura (Syntax):** Define los "nombres" y "tipos" involucrados. Es como declarar las piezas del TDA:
    *   **Sorts (Tipos/Dominios):** Los conjuntos de valores que participan. Siempre incluye el tipo principal que se está definiendo (ej. `Pila`, `Fila`, `Lista`) y cualquier otro tipo que use (ej. `Elemento`, `Boolean`, `Nat`). En tu texto, esto se indica con `EFFECTIVE TYPE` y `IMPORTS`.
    *   **Operations (Funciones):** Las operaciones permitidas en el TDA. Para cada operación, la signatura define:
        *   Su nombre (ej. `agregarPila`).
        *   Los tipos (sorts) de sus argumentos de entrada (ej. `Pila`, `Elemento`).
        *   El tipo (sort) del resultado que devuelve (ej. `Pila`).
        *   **Precondiciones (`pre:`):** Condiciones que deben ser verdaderas *antes* de llamar a la operación para que ésta tenga sentido o sea válida (ej. `pre: not vaciaPila(p)` para `tope`).
    *   **Constructoras Básicas (`BASIC CONSTRUCTORS`):** Un subconjunto especial de operaciones que son suficientes para *construir* cualquier valor posible del TDA. Son los "ladrillos" fundamentales. Por ejemplo, para la Pila, `inicPila` y `agregarPila` permiten crear cualquier pila posible.

2.  **Axiomas (Semántica/Behavior):** Definen el **significado** o **comportamiento** de las operaciones. Son un conjunto de **ecuaciones** que establecen cómo interactúan las diferentes operaciones entre sí. La idea clave es definir el resultado de las operaciones observadoras y modificadoras *en términos de las constructoras básicas*.
    *   Se escriben usando variables de los tipos definidos (ej. `p: Pila; e: Elemento;`).
    *   Describen qué sucede cuando aplicas una operación (como `tope` o `eliminarPila`) a un valor construido con una de las constructoras básicas (como `inicPila` o `agregarPila(p,e)`).
    *   **Ejemplos de Axiomas (Pila):**
        *   `tope(agregarPila(p,e)) = e`: Dice que si agregas un elemento `e` a una pila `p` y luego pides el tope, obtienes ese mismo elemento `e`.
        *   `vaciaPila(inicPila()) = True`: Dice que la pila creada con `inicPila` está vacía.
        *   `vaciaPila(agregarPila(p,e)) = False`: Dice que cualquier pila creada agregando un elemento a otra pila (`p`) no está vacía.
        *   `eliminarPila(agregarPila(p,e)) = p`: Dice que si agregas `e` a `p` y luego eliminas el tope, vuelves a obtener la pila original `p`.
    *   Los axiomas pueden ser condicionales (usando `=>`) como se ve en Fila y Lista, definiendo diferentes comportamientos según el estado.

**¿Por qué usar Especificaciones Algebraicas?**

*   **Precisión:** Eliminan la ambigüedad del lenguaje natural.
*   **Abstracción Pura:** Se centran *solo* en el comportamiento observable, ignorando completamente la implementación. Un mismo TDA especificado algebraicamente puede tener muchas implementaciones diferentes (con arreglos, listas enlazadas, etc.), pero todas deben cumplir los axiomas.
*   **Base para Verificación:** Permiten razonar matemáticamente sobre las propiedades del TDA.
*   **Contrato Claro:** Sirven como un contrato formal entre el diseñador del TDA y quien lo va a usar.

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