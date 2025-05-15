En C++, una **unión (`union`)** es similar a una estructura (`struct`) en su declaración, pero difiere fundamentalmente en cómo se utiliza la memoria. Una unión permite almacenar diferentes tipos de datos en la misma ubicación de memoria.

**Sintaxis:**

```c++
union <tipo_union> {
    <tipo> <nombre_campo1>;
    <tipo> <nombre_campo2>;
    ...
};
```

*   `<tipo_union>`: Es el nombre que se le da al tipo de unión.
*   `<tipo>`: Es el tipo de dato de cada miembro.
*   `<nombre_campo>`: Es el nombre de cada miembro dentro de la unión.

**Características principales:**

*   **Comparten memoria:** Todos los miembros de una unión comparten la misma área de memoria. Esto significa que solo un miembro de la unión puede contener un valor válido en un momento dado.
*   **Tamaño:** El tamaño de la unión es igual al tamaño del miembro más grande.
*   **Modificación:** Modificar un miembro de la unión afecta a todos los demás, ya que todos comparten la misma memoria. Esto puede llevar a resultados impredecibles si no se tiene cuidado.

**Ejemplo:**

```c++
union Descuento {
    int monto;
    float porcentaje;
};
```

En este ejemplo, `Descuento` es una unión que puede almacenar un entero (`monto`) o un flotante (`porcentaje`), pero no ambos al mismo tiempo.

**Uso:**

```c++
Descuento descuento;
descuento.monto = 10; // Almacena un entero en la unión
cout << descuento.monto << endl; // Imprime el valor del entero

descuento.porcentaje = 0.20; // Almacena un flotante en la unión (¡el valor de monto se pierde!)
cout << descuento.porcentaje << endl; // Imprime el valor del flotante
cout << descuento.monto << endl; // Imprime un valor basura, porque la memoria ahora contiene un float
```

**Problemas y soluciones:**

Debido a que solo un miembro de la unión puede ser válido a la vez, es importante saber qué tipo de dato se almacenó en la unión antes de acceder a él. Una forma común de hacer esto es usar una estructura que contenga un miembro que indique el tipo de dato almacenado en la unión:

```c++
struct Descuento {
    char tipo; // 'm' para monto, 'p' para porcentaje
    union {
        int monto;
        float porcentaje;
    } metodo;
};
```

**Acceso con la estructura:**

```c++
Descuento descuento;
descuento.tipo = 'm';
descuento.metodo.monto = 10;

if (descuento.tipo == 'm') {
    cout << "Monto: " << descuento.metodo.monto << endl;
} else if (descuento.tipo == 'p') {
    cout << "Porcentaje: " << descuento.metodo.porcentaje << endl;
}
```

**En resumen:**

Las uniones permiten almacenar diferentes tipos de datos en la misma ubicación de memoria, lo que puede ser útil para ahorrar espacio. Sin embargo, es importante tener cuidado al usar uniones para evitar resultados impredecibles. Una práctica común es combinar una unión con un miembro adicional que indique el tipo de dato almacenado en la unión.
