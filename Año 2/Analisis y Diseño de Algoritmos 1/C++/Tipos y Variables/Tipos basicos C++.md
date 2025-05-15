C++ proporciona un conjunto de tipos de datos fundamentales para representar diferentes clases de información. Estos son los más comunes:

*   **`char`**: Se utiliza para almacenar caracteres individuales (como letras, números o símbolos) o enteros muy pequeños. Generalmente representa caracteres del conjunto ASCII. Los caracteres no imprimibles se representan mediante secuencias de escape (ej. `\n` para nueva línea).
*   **`wchar_t`**: Diseñado para almacenar caracteres "anchos", típicamente utilizados para representar caracteres de conjuntos más extensos como Unicode, que soporta caracteres de múltiples idiomas.
*   **`int`**: Es el tipo fundamental para almacenar números enteros (sin parte decimal). Pueden ser positivos, negativos o cero. El rango exacto puede variar según la arquitectura del sistema y el compilador, pero comúnmente abarca desde -2,147,483,648 hasta 2,147,483,647 para un entero con signo de 32 bits.
*   **`float`**: Se usa para almacenar números de punto flotante (números con parte decimal) de precisión simple. Ofrece aproximadamente 7 dígitos de precisión decimal.
*   **`double`**: Similar a `float`, pero almacena números de punto flotante de doble precisión. Proporciona una mayor precisión (aproximadamente 15 dígitos decimales) y un rango de valores más amplio que `float`. Es el tipo preferido para cálculos con decimales en muchas aplicaciones.
*   **`bool`**: Representa valores booleanos o lógicos. Solo puede tener dos valores posibles: `true` (verdadero) o `false` (falso). Se utiliza comúnmente en operaciones lógicas y estructuras de control.
*   **`void`**: Es un tipo especial que indica la **ausencia de valor**. No se pueden declarar variables de tipo `void`. Sus usos principales son:
    *   Indicar que una función no devuelve ningún valor (`void miFuncion() { ... }`).
    *   Indicar que una función no recibe parámetros (`int miFuncion(void) { ... }`, aunque es más común `int miFuncion() { ... }` en C++).
    *   En programación avanzada con punteros (punteros genéricos `void*`).

## Tabla Resumen de Tipos Básicos

| Nombre      | Descripción                             | Valores Típicos / Rango (Puede variar)                     |
| :---------- | :-------------------------------------- | :--------------------------------------------------------- |
| `char`      | Carácter / Entero pequeño               | Caracteres ASCII (ej. 'a', 'Z', '7', '$') o enteros pequeños |
| `wchar_t`   | Carácter ancho                          | Caracteres Unicode                                         |
| `int`       | Entero                                  | -2,147,483,648 a 2,147,483,647 (típico 32 bits con signo) |
| `float`     | Punto flotante (precisión simple)       | Aprox. ±3.4e +/- 38 (7 dígitos de precisión)               |
| `double`    | Punto flotante (doble precisión)        | Aprox. ±1.7e +/- 308 (15 dígitos de precisión)             |
| `bool`      | Booleano (lógico)                       | `true` o `false`                                           |
| `void`      | Ausencia de tipo/valor                  | No almacena valores; usado en funciones/punteros           |

**Nota:** Los rangos numéricos exactos para `int`, `float` y `double` pueden depender de la plataforma y el compilador específicos que se utilicen. Los valores mostrados son representativos de sistemas comunes (ej., 32 bits para `int`, estándar IEEE 754 para `float`/`double`). Existen modificadores como `short`, `long`, `signed`, `unsigned` que alteran el tamaño o el rango de los tipos numéricos.