La sintaxis básica para declarar una o más variables de un mismo tipo es:

```cpp
<tipo> <variable1>, <variable2>, ..., <variablen>;
```

*   `<tipo>`: Es el tipo de dato que almacenarán las variables (ej. `int`, `float`, `char`, `double`, `bool`).
*   `<variable1>`, `<variable2>`, ...: Son los nombres (identificadores) que se asignan a las variables.
*   Se pueden declarar múltiples variables del mismo tipo separándolas por comas (`,`) en una única sentencia.
*   La declaración siempre termina con un punto y coma (`;`).

**Ejemplo:** Declarar tres variables de tipo entero llamadas `a`, `b` y `c`.

```cpp
int a, b, c;
```

## Inicialización durante la Declaración

Es posible (y a menudo recomendable) asignar un valor inicial a una variable en el mismo momento en que se declara. Esto se llama **inicialización**.

La sintaxis para declarar e inicializar variables es:

```cpp
<tipo> <variable1> = <valor_inicial1>, <variable2> = <valor_inicial2>, ...;
```

*   `<valor_inicial>`: Es el valor que se asigna a la variable correspondiente en el momento de su creación. El valor debe ser compatible con el tipo de dato de la variable.

**Ejemplo:** Declarar tres variables enteras e inicializarlas con valores específicos.

```cpp
int a = 1, b = 2, c = 4;
```

También se puede mezclar declaración simple e inicialización en la misma línea para variables del mismo tipo:

```cpp
int x = 10, y, z = 5; // 'x' se inicializa a 10, 'y' no se inicializa, 'z' se inicializa a 5.
```

Declarar las variables antes de usarlas es crucial para que el compilador reserve el espacio de memoria necesario y sepa cómo interpretar los datos almacenados.
