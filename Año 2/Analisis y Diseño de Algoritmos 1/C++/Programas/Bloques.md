Un **bloque** en C++ es una **sentencia compuesta**. Consiste en una secuencia de cero o más sentencias individuales agrupadas y delimitadas por un par de llaves `{}`.

```cpp
{
    <sentencia1>;
    <sentencia2>;
    <sentencia3>;
    // ... más sentencias ...
}
```

## Características Principales

1.  **Agrupación:** Los bloques permiten agrupar múltiples sentencias para que sean tratadas como una unidad lógica.
2.  **Sintaxis:** Desde el punto de vista de la sintaxis del lenguaje, un bloque completo (incluyendo las llaves y las sentencias internas) puede ser considerado como **una única sentencia**. Esto es importante en estructuras de control como `if`, `for`, `while`, etc., que esperan una sentencia después de ellas. Si se necesita ejecutar más de una sentencia en esos casos, se debe usar un bloque.
3.  **Bloques Vacíos:** Un bloque puede no contener ninguna sentencia en su interior: `{}`. Esto es sintácticamente válido.
4.  **Anidamiento:** Los bloques pueden ser **anidados**, es decir, un bloque puede contener otros bloques dentro de él, teóricamente a cualquier nivel de profundidad.

    ```cpp
    { // Bloque exterior
        // Sentencias del bloque exterior
        ...
        { // Bloque interior (anidado)
            <sentencia1_interna>;
            <sentencia2_interna>;
            // ...
        }
        // Más sentencias del bloque exterior
        ...
    }
    ```

Los bloques son fundamentales para definir el cuerpo de funciones (como `main`), estructuras de control y para delimitar el alcance (scope) de las variables.
