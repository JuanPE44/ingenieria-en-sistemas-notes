Las estructuras de iteración, también conocidas como bucles, te permiten repetir un bloque de código varias veces. C++ ofrece tres estructuras principales para esto: `for`, `while` y `do...while`.

**1. Bucle `for`:**

El bucle `for` es ideal cuando conoces de antemano cuántas veces quieres repetir un bloque de código.

*   **Sintaxis General:**

    ```cpp
    for (inicialización; condición; incremento) {
        // Código a ejecutar en cada iteración
    }
    ```

*   **Explicación:**

    *   `inicialización`: Se ejecuta una sola vez al principio del bucle. Generalmente, se utiliza para inicializar una variable de control (contador).
    *   `condición`: Se evalúa al principio de cada iteración. Si la condición es verdadera, el bucle continúa. Si es falsa, el bucle termina.
    *   `incremento`: Se ejecuta al final de cada iteración. Generalmente, se utiliza para modificar la variable de control (incrementar o decrementar).
    *   `{}`: Delimitan el bloque de código que se ejecutará en cada iteración.

*   **Ejemplo:**

    ```cpp
    for (int i = 0; i < 10; i++) {
        std::cout << "Iteración: " << i << std::endl;
    }
    ```

    *   En este ejemplo, el bucle se ejecuta 10 veces. La variable `i` se inicializa en 0, la condición es `i < 10`, y el incremento es `i++`.

**2. Bucle `while`:**

El bucle `while` repite un bloque de código mientras una condición sea verdadera. Es útil cuando no sabes de antemano cuántas iteraciones se necesitarán.

*   **Sintaxis General:**

    ```cpp
    while (condición) {
        // Código a ejecutar mientras la condición sea verdadera
    }
    ```

*   **Explicación:**

    *   `condición`: Se evalúa al principio de cada iteración. Si la condición es verdadera, el bucle continúa. Si es falsa, el bucle termina.
    *   `{}`: Delimitan el bloque de código que se ejecutará en cada iteración.

*   **Ejemplo:**

    ```cpp
    int contador = 0;
    while (contador < 5) {
        std::cout << "Contador: " << contador << std::endl;
        contador++;
    }
    ```

    *   En este ejemplo, el bucle se ejecuta mientras `contador` sea menor que 5. Es importante asegurarse de que la condición eventualmente se vuelva falsa, de lo contrario, el bucle se ejecutará indefinidamente (bucle infinito).

**3. Bucle `do...while`:**

El bucle `do...while` es similar al bucle `while`, pero garantiza que el bloque de código se ejecute al menos una vez, ya que la condición se evalúa al final del bucle.

*   **Sintaxis General:**

    ```cpp
    do {
        // Código a ejecutar al menos una vez
    } while (condición);
    ```

*   **Explicación:**

    *   `{}`: Delimitan el bloque de código que se ejecutará al menos una vez.
    *   `condición`: Se evalúa al final de cada iteración. Si la condición es verdadera, el bucle continúa. Si es falsa, el bucle termina.

*   **Ejemplo:**

    ```cpp
    int opcion;
    do {
        std::cout << "Ingrese una opción (0 para salir): ";
        std::cin >> opcion;
    } while (opcion != 0);
    ```

    *   En este ejemplo, el bucle se ejecuta al menos una vez para pedir al usuario que ingrese una opción. El bucle continúa hasta que el usuario ingrese 0.

**Puntos Clave:**

*   Las estructuras de iteración te permiten repetir bloques de código.
*   `for` es ideal cuando conoces el número de iteraciones.
*   `while` es útil cuando la repetición depende de una condición.
*   `do...while` garantiza que el bloque de código se ejecute al menos una vez.
*   Asegúrate de que la condición de un bucle `while` o `do...while` eventualmente se vuelva falsa para evitar bucles infinitos.

