#### El "Plano" Matemático de un Tipo de Dato

La Especificación Algebraica es una forma **formal y matemática** de definir un Tipo de Dato Abstracto (TDA). En lugar de usar descripciones ambiguas o código específico, usa conceptos del álgebra para crear un "plano" preciso del TDA, enfocándose en su **comportamiento lógico** y **propiedades**.

**Componentes Clave:**

1.  **Signatura (Syntax):** Define los "nombres" y "tipos" involucrados.
    *   **Sorts (Tipos):** Los conjuntos de valores que usa el TDA (ej. `Pila`, `Elemento`, `Boolean`).
    *   **Operations (Funciones):** Las operaciones permitidas en el TDA, indicando sus entradas y el tipo de resultado (ej. `agregarPila: Pila x Elemento -> Pila`). También pueden tener **Precondiciones** ( `pre:` ) que deben cumplirse para que la operación sea válida.
    *   **Constructoras Básicas:** Un grupo especial de operaciones que sirven para construir *cualquier* valor posible del TDA (ej. `inicPila`, `agregarPila`).

2.  **Axiomas (Semántica/Behavior):** Definen el **significado** de las operaciones mediante **ecuaciones**. Estas ecuaciones describen cómo interactúan las operaciones entre sí, definiendo el resultado de las operaciones en términos de las constructoras básicas.
    *   **Ejemplos (Pila):**
        *   `tope(agregarPila(p,e)) = e` (El tope de una pila después de agregar un elemento es ese elemento).
        *   `vaciaPila(inicPila()) = True` (Una pila recién inicializada está vacía).

**¿Por qué usar Especificaciones Algebraicas?**

*   **Precisión:** Evita la ambigüedad.
*   **Abstracción:** Se centra en el *qué* hace el TDA, no en *cómo* lo hace.
*   **Verificación:** Permite comprobar matemáticamente las propiedades del TDA.
*   **Contrato:** Sirve como un acuerdo formal sobre cómo debe comportarse el TDA.

