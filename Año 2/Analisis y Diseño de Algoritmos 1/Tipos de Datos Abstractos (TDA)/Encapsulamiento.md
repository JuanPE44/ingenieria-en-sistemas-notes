El encapsulamiento es el mecanismo que **agrupa o empaqueta en una sola unidad sintáctica tanto los datos (el dominio o estado interno) como las operaciones (métodos o funciones) que manipulan esos datos**. Es como poner el dominio y sus operaciones asociadas dentro de una "cápsula".

En el contexto de los TDA:

1.  **La Unidad:** El TDA en sí mismo es la unidad encapsulada. Cuando defines `CLASS Pila [...] END-CLASS` o cuando implementas una clase `Pila` en C++, estás creando esta cápsula.
2.  **Contenido de la Cápsula:**
    *   **Datos (Dominio/Estado):** Aunque la *especificación algebraica* no detalla la representación interna, conceptualmente, la cápsula contiene el estado del TDA (por ejemplo, la secuencia de elementos en la pila). En una *implementación* (como una clase C++), esto serían los miembros de datos privados (ej., un arreglo y un índice `tope`).
    *   **Operaciones (Métodos):** Las funciones definidas que operan sobre esos datos (`inicPila`, `agregarPila`, `tope`, `eliminarPila`, `vaciaPila`). Estas son las únicas formas permitidas para interactuar con el estado interno.
3.  **El Propósito:** El objetivo principal del encapsulamiento es **organizar y vincular estrechamente los datos con las operaciones que tienen sentido para esos datos**. Se asegura que los datos no anden "sueltos" y que solo puedan ser modificados o accedidos a través de los procedimientos diseñados específicamente para ellos.

**Relación con Abstracción e Información Hiding:**

*   **Habilita la Abstracción:** Al agrupar todo, el encapsulamiento permite presentar el TDA como una entidad única con una interfaz clara (las operaciones públicas), ocultando la complejidad interna (abstracción).
*   **Facilita el Ocultamiento de Información:** La "cápsula" creada por el encapsulamiento proporciona la barrera necesaria para implementar el ocultamiento de información. Define claramente qué está *dentro* de la cápsula (y puede ser ocultado/protegido) y qué forma parte de su *interfaz externa*. Lenguajes como C++ usan modificadores de acceso (`public`, `private`) dentro de la clase (la cápsula) para controlar qué es visible y qué está oculto.

**En Resumen:**

Si la **abstracción** es *definir* el TDA por su interfaz (el "qué") y el **ocultamiento de información** es *proteger* los detalles internos (el "cómo"), el **encapsulamiento** es la *práctica de agrupar* físicamente (en el código o la especificación) los datos y las operaciones en una sola unidad (la "cápsula" o TDA), lo que hace posible tanto la abstracción como el ocultamiento efectivo.

En tu texto, se menciona explícitamente:

> DOMINIO + OPERACIONES -> UNIDAD SINTÁCTICA = ENCAPSULAMIENTO
> C++ provee como mecanismo de encapsulamiento a la CLASE

