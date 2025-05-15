En C++, las constantes son valores que no pueden ser modificados durante la ejecución de un programa. Son útiles para representar valores que son fijos y conocidos en tiempo de compilación, como el valor de PI o el número máximo de elementos en un array.

**Tipos de Constantes:**

*   **Números enteros:** Se pueden expresar en diferentes bases:
    *   Decimal: La forma más común (ej: `10`).
    *   Octal: Precedidos por un `0` (ej: `012`, que es 10 en decimal).
    *   Hexadecimal: Precedidos por `0x` (ej: `0xA`, que es 10 en decimal).
*   **Números de punto flotante:** Representan números reales. Pueden incluir un punto decimal (ej: `3.14`) o la notación exponencial (ej: `1.0e-6`, que es $1.0 * 10^{-6}$).
*   **Caracteres:** Representan un único carácter y se encierran entre apóstrofos (ej: `'A'`).
*   **Cadenas de caracteres:** Representan una secuencia de caracteres y se encierran entre comillas dobles (ej: `"Hola Mundo"`).

**Declaración de Constantes:**

C++ ofrece dos formas principales de definir constantes:

1.  **`const` (Declaración):**

    *   Se utiliza la palabra clave `const` para declarar una variable como constante.
    *   Se debe especificar el tipo de dato de la constante.
    *   Es la forma recomendada de definir constantes en C++.
    *   Ejemplo: `const double PI = 3.14159;`

    ```c++
    const int MAX_VALUE = 100;
    const string MESSAGE = "Error!";
    ```

    En este caso, `MAX_VALUE` es una constante entera con valor 100, y `MESSAGE` es una constante de cadena con el valor "Error!". Una vez declaradas, no se pueden modificar.

2.  **`#define` (Directiva del Preprocesador):**

    *   Se utiliza la directiva `#define` para definir una constante.
    *   No se especifica el tipo de dato de la constante.  El preprocesador simplemente sustituye el nombre de la constante por su valor antes de la compilación.
    *   Generalmente se considera menos segura y menos flexible que `const`, ya que no proporciona verificación de tipos.
    *   Ejemplo: `#define PI 3.14159`

    ```c++
    #define ARRAY_SIZE 25
    ```

    Aquí, `ARRAY_SIZE` se reemplazará por `25` en todo el código antes de la compilación.

**¿Por qué usar `const` en lugar de `#define`?**

*   **Seguridad de tipos:** `const` permite especificar el tipo de dato de la constante, lo que ayuda al compilador a detectar errores de tipo.  `#define` no tiene tipo, lo que puede llevar a errores difíciles de depurar.
*   **Ámbito:** Las constantes declaradas con `const` tienen un ámbito definido (por ejemplo, dentro de una función o clase), mientras que las constantes definidas con `#define` tienen un ámbito global en el archivo.
*   **Depuración:** Las constantes `const` son visibles para el depurador, lo que facilita la depuración del código.  Las constantes `#define` son reemplazadas por su valor antes de la depuración, lo que dificulta su seguimiento.

