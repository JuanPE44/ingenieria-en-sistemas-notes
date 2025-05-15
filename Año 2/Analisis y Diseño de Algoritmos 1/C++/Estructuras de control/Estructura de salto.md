Las estructuras de salto te permiten alterar el flujo normal de ejecución de un programa, ya sea interrumpiendo un bucle, saltando a la siguiente iteración o transfiriendo el control a otra parte del código. C++ ofrece tres estructuras principales para esto: `break`, `continue` y `goto`.

**1. Sentencia `break`:**

La sentencia `break` se utiliza para salir de un bucle (`for`, `while`, `do...while`) o de una estructura `switch`. Cuando se encuentra un `break`, la ejecución del programa continúa en la siguiente instrucción después del bucle o `switch`.

*   **Uso en Bucles:**

    ```cpp
    for (int i = 0; i < 10; i++) {
        if (i == 5) {
            break; // Sale del bucle cuando i es igual a 5
        }
        std::cout << "Iteración: " << i << std::endl;
    }
    std::cout << "Fin del bucle" << std::endl;
    ```

    *   En este ejemplo, el bucle `for` se interrumpirá cuando `i` sea igual a 5, y el programa continuará con la instrucción `std::cout << "Fin del bucle" << std::endl;`.

*   **Uso en `switch`:**

    ```cpp
    int opcion;
    std::cin >> opcion;

    switch (opcion) {
        case 1:
            std::cout << "Opción 1" << std::endl;
            break; // Sale del switch después de ejecutar el caso 1
        case 2:
            std::cout << "Opción 2" << std::endl;
            break; // Sale del switch después de ejecutar el caso 2
        default:
            std::cout << "Opción inválida" << std::endl;
            break; // Sale del switch después de ejecutar el caso default
    }
    ```

    *   Como se explicó anteriormente, `break` es esencial en `switch` para evitar que la ejecución "caiga" al siguiente `case`.

**2. Sentencia `continue`:**

La sentencia `continue` se utiliza para saltar a la siguiente iteración de un bucle (`for`, `while`, `do...while`), omitiendo el resto del código dentro del bucle para la iteración actual.

*   **Ejemplo:**

    ```cpp
    for (int i = 0; i < 10; i++) {
        if (i % 2 == 0) {
            continue; // Salta a la siguiente iteración si i es par
        }
        std::cout << "Iteración impar: " << i << std::endl;
    }
    ```

    *   En este ejemplo, si `i` es par, la sentencia `continue` hará que el programa salte a la siguiente iteración del bucle, omitiendo la instrucción `std::cout << "Iteración impar: " << i << std::endl;`. Por lo tanto, solo se imprimirán los números impares.

**3. Sentencia `goto`:**

La sentencia `goto` permite transferir el control del programa a una etiqueta específica dentro del código.

*   **Sintaxis:**

    ```cpp
    goto etiqueta;
    // ...
    etiqueta:
    // Código al que se salta
    ```

*   **Ejemplo:**

    ```cpp
    int i = 0;
    inicio: // Etiqueta
    std::cout << "Valor de i: " << i << std::endl;
    i++;
    if (i < 5) {
        goto inicio; // Salta de vuelta a la etiqueta "inicio"
    }
    ```

    *   En este ejemplo, el programa saltará de vuelta a la etiqueta `inicio` hasta que `i` sea igual a 5.

*   **¡Advertencia!** El uso de `goto` generalmente se desaconseja porque puede hacer que el código sea difícil de entender, depurar y mantener. Puede crear un flujo de control confuso y spaghetti code. En la mayoría de los casos, se pueden lograr los mismos resultados utilizando estructuras de control más claras como `if`, `else`, `for`, `while` y `switch`.

**Puntos Clave:**

*   Las estructuras de salto te permiten alterar el flujo normal de ejecución de un programa.
*   `break` se utiliza para salir de un bucle o `switch`.
*   `continue` se utiliza para saltar a la siguiente iteración de un bucle.
*   `goto` permite saltar a una etiqueta específica, pero su uso generalmente se desaconseja.

Espero que esta explicación detallada te sea útil. ¡No dudes en preguntar si tienes más preguntas!
