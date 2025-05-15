El ocultamiento de información es un principio de [[Diseño de Software]], y en los TDA, significa **proteger los detalles internos de la implementación de un TDA del mundo exterior**. Es el mecanismo que *hace cumplir* la separación entre la interfaz y la implementación que logramos con la abstracción de datos.

Piensa en ello como una "barrera" o un "muro" alrededor de los componentes internos del TDA.

**¿Qué se oculta específicamente?**

1.  **La Representación de Datos Interna:** La estructura de datos concreta que se elige para almacenar los elementos del TDA.
    *   *Ejemplo (TDA Pila):* ¿La pila se implementa internamente usando un arreglo de tamaño fijo? ¿Un arreglo dinámico (como `std::vector` en C++)? ¿Una lista enlazada? El usuario del TDA `Pila` *no sabe* y *no necesita saber* cuál de estas opciones se usó.
2.  **Los Algoritmos de las Operaciones:** El código específico que manipula la representación interna para llevar a cabo las operaciones.
    *   *Ejemplo (TDA Pila):* El código exacto dentro de la función `agregarPila` que coloca el nuevo elemento en la estructura de datos (ya sea asignándolo a un índice de arreglo y actualizando un contador, o creando un nuevo nodo en una lista enlazada) está oculto.

**¿Qué NO se oculta (La Interfaz Pública)?**

*   El nombre del tipo (ej. `Pila`).
*   Los nombres, parámetros y tipos de retorno de las operaciones públicas (ej. `agregarPila: Pila x Elemento -> Pila`).
*   El comportamiento esperado o la semántica de esas operaciones (definido por los axiomas o la documentación).

**¿Por qué es crucial el Ocultamiento de Información en los TDA?**

1.  **Protección e Integridad de Datos:** Es la razón principal. Al ocultar la representación interna, se evita que el código externo (el que usa el TDA) la modifique directamente de formas inesperadas o incorrectas. Solo se puede interactuar con los datos a través de las operaciones definidas, las cuales están diseñadas para mantener la consistencia y las reglas del TDA (sus invariantes).
    *   *Ejemplo:* Si la Pila usa un arreglo y un índice `tope`, el ocultamiento impide que el usuario externo cambie directamente el valor de `tope` a un índice inválido, lo que corrompería la Pila. Solo puede modificarlo indirectamente usando `agregarPila` o `eliminarPila`.
2.  **Simplificación para el Usuario:** El usuario no se ve abrumado por detalles de implementación que no son relevantes para usar el TDA. Solo necesita entender la interfaz pública.
3.  **Facilita Cambios y Mantenimiento (Modularidad):** Puedes cambiar *totalmente* la implementación interna de un TDA (por ejemplo, optimizarla) sin afectar a ningún código que lo utilice, siempre que la interfaz pública (operaciones y su comportamiento) permanezca sin cambios. El "muro" del ocultamiento aísla el impacto de los cambios internos.
    *   *Ejemplo:* Puedes decidir que tu `Pila` basada en arreglos es ineficiente y re-implementarla usando listas enlazadas. El código que usa `inicPila`, `agregarPila`, etc., seguirá funcionando exactamente igual sin necesidad de modificaciones, porque nunca dependió de que fuera un arreglo.
4.  **Reduce Acoplamiento:** El código que usa el TDA depende menos de los detalles específicos de cómo está hecho el TDA, lo que hace al sistema más flexible.

