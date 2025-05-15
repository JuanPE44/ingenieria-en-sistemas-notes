Las estructuras de selección permiten que tu programa tome decisiones y ejecute diferentes bloques de código según si una condición es verdadera o falsa. C++ ofrece dos estructuras principales para esto: `if` y `switch`.

**1. Sentencia `if`:**

La sentencia `if` evalúa una expresión lógica y, si es verdadera, ejecuta un bloque de código. Puede combinarse con `else if` y `else` para manejar múltiples condiciones.

*   **Sintaxis General:**

    ```cpp
    if (expresión_lógica) {
        // Código a ejecutar si expresión_lógica es verdadera
    } else if (expresión_lógica2) {
        // Código a ejecutar si expresión_lógica2 es verdadera
    } else {
        // Código a ejecutar si ninguna de las expresiones anteriores es verdadera
    }
    ```

*   **Explicación:**

    *   `expresión_lógica`: Es una expresión que se evalúa como `true` o `false`. Debe estar entre paréntesis.
    *   `{}`: Delimitan el bloque de código que se ejecutará si la condición es verdadera. Si solo hay una sentencia, las llaves son opcionales, pero se recomienda usarlas para mayor claridad.
    *   `else if`: Permite encadenar múltiples condiciones. Se evalúa solo si la condición `if` anterior es falsa. Puedes tener cero o más bloques `else if`.
    *   `else`: Es opcional. Se ejecuta si ninguna de las condiciones `if` o `else if` anteriores es verdadera.

*   **Ejemplo:**

    ```cpp
    int b;
    std::cin >> b;

    if (b > 10) {
        std::cout << "Error: valor mayor de lo permitido" << std::endl;
    } else if (b < 0) {
        std::cout << "Error: valor menor de lo permitido" << std::endl;
    } else {
        procesarValor(b); // Llama a una función para procesar el valor
    }
    ```

**2. Sentencia `switch`:**

La sentencia `switch` permite seleccionar uno de varios bloques de código para ejecutar, basándose en el valor de una expresión (el "selector"). Es especialmente útil cuando tienes múltiples casos posibles para una variable de tipo simple (como `int` o `char`).

*   **Sintaxis General:**

    ```cpp
    switch (expresión) {
        case valor1:
            // Código a ejecutar si expresión == valor1
            break;
        case valor2:
            // Código a ejecutar si expresión == valor2
            break;
        // ... más casos ...
        default:
            // Código a ejecutar si expresión no coincide con ningún valor anterior
            break;
    }
    ```

*   **Explicación:**

    *   `expresión`: Es la expresión que se evalúa. Su valor se compara con los valores de los `case`.
    *   `case valor:`: Cada `case` representa un valor posible de la expresión. Si la expresión coincide con un `valor`, se ejecuta el código asociado a ese `case`.
    *   `break;`: Es crucial al final de cada bloque `case`. Indica que se debe salir de la estructura `switch` después de ejecutar el código del `case` correspondiente. Si se omite `break`, la ejecución "caerá" al siguiente `case`, lo cual rara vez es el comportamiento deseado (se conoce como "fall-through").
    *   `default:`: Es opcional. Se ejecuta si la expresión no coincide con ninguno de los valores de los `case`. Es una buena práctica incluir un `default` para manejar casos inesperados.

*   **Ejemplo:**

    ```cpp
    int opcion;
    std::cin >> opcion;

    switch (opcion) {
        case 1:
            std::cout << "Opción 1" << std::endl;
            break;
        case 2:
        case 3:
            std::cout << "Opción 2 o 3" << std::endl;
            break;
        default: {
            std::cout << "Opción inválida\n" << "Ingrese una nueva opción" << std::endl;
        } break;
    }
    ```

    *   En este ejemplo, si `opcion` es 2 o 3, se ejecutará el mismo bloque de código. Esto se debe a que el `case 2` no tiene un `break`, por lo que la ejecución "cae" al `case 3`.

**Puntos Clave:**

*   Las estructuras de selección te permiten controlar el flujo de tu programa basándose en condiciones.
*   `if` es ideal para condiciones simples o múltiples condiciones encadenadas.
*   `switch` es útil cuando tienes una variable con múltiples valores posibles y quieres ejecutar diferentes acciones para cada valor.
*   No olvides el `break` en los `case` de `switch` para evitar el "fall-through".

