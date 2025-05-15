## La Función Principal: `main`

Todo programa ejecutable en C++ requiere una función especial llamada `main`. Esta función sirve como el **punto de entrada** del programa; es decir, la ejecución del código comienza siempre dentro de la función `main`.

### Estructura Básica

El programa más simple posible en C++ se ve así:

```cpp
int main()
{
    // El código del programa iría aquí
    return 0;
}
```

### Componentes Clave de `main`

1.  **Tipo de Retorno (`int`):**
    *   La función `main` **debe** declararse de forma que retorne un valor de tipo entero (`int`). Este valor entero se devuelve al sistema operativo o al entorno que ejecutó el programa una vez que este finaliza.
2.  **Nombre de la Función (`main`):**
    *   El nombre `main` es obligatorio y distingue a esta función como el punto de inicio del programa.
3.  **Cuerpo de la Función (`{ ... }`):**
    *   Las llaves `{}` delimitan el bloque de código que contiene las instrucciones que ejecutará el programa.
4.  **Sentencia `return`:**
    *   La sentencia `return` dentro de `main` especifica el valor entero que se devolverá al finalizar el programa.
    *   **`return 0;`**: Por convención, retornar `0` indica que el programa se ejecutó **exitosamente** y finalizó sin errores.
    *   **`return [valor distinto de 0];`**: Retornar cualquier valor entero diferente de cero (por ejemplo, `1`, `-1`, etc.) se utiliza convencionalmente para señalar que ocurrió algún **error** durante la ejecución del programa. El valor específico puede, en algunos casos, indicar la naturaleza del error.

