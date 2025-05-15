En C++, una **enumeración (`enum`)** define un conjunto de valores enteros constantes con nombre. Su sintaxis básica es:

```c++
enum <tipo_enumeración> {<constante1>, <constante2>, ..., <constanten>};
```

*   `<tipo_enumeración>` es el nombre que se le da a la enumeración (opcional).
*   `<constante1>`, `<constante2>`, ..., `<constanten>` son los nombres de las constantes que forman la enumeración.

**Comportamiento por defecto:**

Por defecto, a la primera constante se le asigna el valor `0`, a la segunda el valor `1`, y así sucesivamente, incrementando de uno en uno.

**Asignación explícita de valores:**

Es posible asignar valores específicos a las constantes de la enumeración:

```c++
enum <tipo_enumeración> {<constante1>=<valor_constante>, <constante2>=<valor_constante>, ...};
```

**Ejemplo:**

```c++
enum posicion {primero, segundo, tercero};
```

En este ejemplo:

*   `primero` tendrá el valor `0`.
*   `segundo` tendrá el valor `1`.
*   `tercero` tendrá el valor `2`.

**Otro ejemplo con asignación explícita:**

```c++
enum dias_semana {
    lunes = 1,
    martes,      // martes será 2 (el siguiente a lunes)
    miercoles,   // miercoles será 3
    jueves = 10,
    viernes,     // viernes será 11
    sabado,      // sabado será 12
    domingo      // domingo será 13
};
```

**En resumen:**

Las enumeraciones proporcionan una forma de crear un conjunto de constantes con nombre, lo que mejora la legibilidad y el mantenimiento del código. Se pueden usar los valores por defecto (0, 1, 2, ...) o asignar valores específicos a cada constante.
