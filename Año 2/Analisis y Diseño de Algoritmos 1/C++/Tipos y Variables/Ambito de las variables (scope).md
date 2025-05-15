El **ámbito** (o *scope*) de una variable se refiere a la porción del código fuente donde esa variable es reconocida y puede ser utilizada. En C++, existen principalmente dos tipos de ámbito para las variables:

## 1. Variables Locales

*   **Declaración:** Se declaran **dentro** de una función o un bloque de código (`{ ... }`).
*   **Visibilidad:** Son únicamente visibles y accesibles **dentro** de la función o bloque específico donde fueron declaradas.
*   **Existencia:** No existen fuera de su ámbito. Se crean cuando la ejecución del programa entra en su bloque/función y se destruyen cuando la ejecución sale de él.
*   **Punto de Declaración:** Aunque pueden declararse en cualquier parte dentro de su bloque/función, solo pueden ser utilizadas en sentencias que aparecen **después** de su punto de declaración.

## 2. Variables Globales

*   **Declaración:** Se declaran **fuera** de todas las funciones (generalmente cerca del inicio del archivo de código fuente).
*   **Visibilidad:** Pueden ser utilizadas por **cualquier función** que se defina en el mismo archivo *después* de la declaración de la variable global.
*   **Existencia:** Existen durante toda la ejecución del programa.

## Alcance o Ámbito

La porción de código donde cada variable es visible se denomina **alcance** o **ámbito**.

*   Para las **variables locales**, el alcance comienza en la sentencia donde la variable es declarada y termina en la llave de cierre (`}`) que delimita el bloque o función en el cual fue definida.

## Ejemplo Ilustrativo

Considera el siguiente código:

```cpp
#include <iostream> // Necesario para std::cout

// 'a' es una variable global
int a = 20;

int main() {
    // 'b' es una variable local a la función main
    int b = 10;

    { // Inicio de un bloque interno (sub-bloque)
        // 'c' es una variable local a este sub-bloque
        int c = 15;
        std::cout << "Dentro del bloque:\n";
        std::cout << "Variable a: " << a << "\n"; // OK: 'a' es global, visible aquí
        std::cout << "Variable b: " << b << "\n"; // OK: 'b' es local a main, visible en bloques internos
        std::cout << "Variable c: " << c << "\n"; // OK: 'c' es local a este bloque
    } // Fin del sub-bloque. La variable 'c' deja de existir aquí.

    std::cout << "\nFuera del bloque:\n";
    std::cout << "Variable a: " << a << "\n"; // OK: 'a' sigue siendo visible
    std::cout << "Variable b: " << b << "\n"; // OK: 'b' sigue siendo visible dentro de main
    // std::cout << "Variable c: " << c << "\n"; // ERROR: 'c' no está declarada en este ámbito.
                                             // Descomentar esta línea causaría un error de compilación.
    return 0;
}
```

**Análisis del Ejemplo:**

*   `a`: Es **global**. Visible y utilizable en `main` y dentro del sub-bloque.
*   `b`: Es **local** a la función `main`. Visible y utilizable dentro de `main` y también dentro del sub-bloque (ya que el sub-bloque está contenido en `main`).
*   `c`: Es **local** al sub-bloque. Solo es visible y utilizable *dentro* de las llaves `{}` de ese bloque. Intentar usar `c` fuera de esas llaves resulta en un error porque la variable ya no existe o no está en el ámbito actual.
