## Ocultamiento de Identificadores

En C++, es posible declarar un identificador (como el nombre de una variable) dentro de un bloque o ámbito interno que ya existe con el mismo nombre en un ámbito exterior. Cuando esto sucede, la declaración en el **ámbito interno "oculta"** o **"ensombrece" (shadowing)** a la declaración del ámbito externo.

Esto significa que, dentro del ámbito interno, cualquier referencia a ese identificador se referirá a la versión declarada localmente en ese ámbito, y no a la versión del ámbito exterior.

## Ejemplo de Ocultamiento (Shadowing)

Considera el siguiente código donde una variable local `b` dentro de un sub-bloque oculta a otra variable `b` declarada en la función `main`:

```cpp
#include <iostream> // Necesario para std::cout

// 'a' es una variable global
int a = 20;

int main() {
    // 'b' es local a main (ámbito exterior respecto al sub-bloque)
    int b = 10;

    { // Inicio de un sub-bloque (ámbito interior)
        // Se declara OTRA variable 'b', local a este sub-bloque.
        // Esta 'b' interna OCULTA a la 'b' de main dentro de este bloque.
        int b = 15;

        std::cout << "Dentro del bloque:\n";
        std::cout << "Variable A: " << a << "\n"; // Se accede a la 'a' global (20)
        std::cout << "Variable B: " << b << "\n"; // Se accede a la 'b' local del bloque (15)
    } // Fin del sub-bloque. La 'b' interna (valor 15) deja de existir.

    std::cout << "\nFuera del bloque:\n";
    std::cout << "Variable A: " << a << "\n"; // Se accede a la 'a' global (20)
    std::cout << "Variable B: " << b << "\n"; // Se accede a la 'b' original de main (10)

    return 0;
}
```

## Explicación del Resultado

La ejecución de este código produce la siguiente salida:

```
Dentro del bloque:
Variable A: 20
Variable B: 15

Fuera del bloque:
Variable A: 20
Variable B: 10
```

*   **Dentro del bloque:** La declaración `int b = 15;` crea una nueva variable `b` que solo existe dentro de esas llaves `{}`. Cualquier uso de `b` dentro de este bloque se refiere a esta variable local, que tiene el valor `15`. La variable `b` de `main` (con valor `10`) sigue existiendo pero está temporalmente inaccesible por su nombre `b` debido al ocultamiento.
*   **Fuera del bloque:** Una vez que la ejecución sale del bloque interno, la variable `b` local (con valor `15`) es destruida. Ahora, cualquier referencia a `b` vuelve a apuntar a la variable `b` declarada en el ámbito de `main`, que tiene el valor `10`.

El ocultamiento permite reutilizar nombres de variables en ámbitos locales sin afectar a las variables de ámbitos superiores, pero debe usarse con cuidado para no generar confusión en el código.
