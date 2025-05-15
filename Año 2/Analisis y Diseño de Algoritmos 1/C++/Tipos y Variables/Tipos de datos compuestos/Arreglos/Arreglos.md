En C++, un **arreglo (array)** es una colección de elementos del mismo tipo de dato, almacenados en ubicaciones de memoria contiguas. Se accede a cada elemento del arreglo mediante un índice.

**Sintaxis de declaración:**

```c++
<tipo> <nombre_arreglo>[<tamaño>];
```

*   `<tipo>`: El tipo de dato de los elementos del arreglo (ej: `int`, `float`, `char`).
*   `<nombre_arreglo>`: El nombre que se le da al arreglo.
*   `<tamaño>`: Una constante entera positiva que indica el número de elementos que puede contener el arreglo.

**Ejemplo:**

```c++
int arr[10]; // Declara un arreglo de 10 enteros llamado 'arr'
```

**Acceso a los elementos:**

Se accede a los elementos del arreglo utilizando el operador corchete `[]` y un índice:

```c++
<nombre_arreglo>[<índice>]
```

*   `<índice>`: Un valor entero que indica la posición del elemento al que se quiere acceder. Los índices en C++ comienzan en 0, por lo que el primer elemento tiene índice 0, el segundo tiene índice 1, y así sucesivamente. El último elemento tiene índice `<tamaño> - 1`.

**Ejemplo:**

```c++
arr[2] = 10; // Asigna el valor 10 al elemento en la posición 2 del arreglo
int variable = arr[4]; // Obtiene el valor del elemento en la posición 4 y lo asigna a la variable 'variable'
```

**Importante:**

*   **No hay verificación de límites:** C++ no realiza ninguna verificación de acceso a los límites del arreglo. Si se intenta acceder a un elemento fuera del rango válido (0 a `<tamaño> - 1`), el comportamiento es indefinido y puede provocar errores en el programa, como corrupción de memoria o terminación inesperada.
*   **Índices fuera de rango:** Acceder a un índice fuera del rango válido puede resultar en la lectura o escritura de datos en ubicaciones de memoria incorrectas, lo que puede ser difícil de depurar.

**Arreglos multidimensionales:**

C++ permite declarar arreglos con múltiples dimensiones:

```c++
<tipo> <nombre_arreglo>[<tamaño_dim1>][<tamaño_dim2>]...[<tamaño_dimn>];
```

**Ejemplo:**

```c++
int matriz[2][3]; // Declara una matriz de 2 filas y 3 columnas de enteros
```

**Inicialización de arreglos:**

Los arreglos se pueden inicializar al momento de la declaración:

```c++
<tipo> <nombre_arreglo>[<tamaño>] = {<valor1>, <valor2>, ... <valorn>};
```

**Ejemplos:**

```c++
char vocales[5] = {'a', 'e', 'i', 'o', 'u'};

// Si se inicializa al declarar, se puede omitir el tamaño:
char vocales[] = {'a', 'e', 'i', 'o', 'u'}; // El compilador deduce el tamaño (5)

int matriz[2][3] = {{1, 2, 3}, {4, 5, 6}}; // Inicializa una matriz 2x3
int matriz2[2][3] = {1, 2, 3, 4, 5, 6};   // Otra forma de inicializar la misma matriz
```

**Matrices:**

Los arreglos de dos dimensiones se conocen comúnmente como matrices. Se pueden imaginar como una tabla con filas y columnas.

**Limitaciones:**

Los arreglos en C++ tienen un tamaño fijo que se debe conocer en tiempo de compilación. Si se necesita un arreglo cuyo tamaño pueda variar durante la ejecución del programa, se deben utilizar otras estructuras de datos, como los vectores (`std::vector`).

**En resumen:**

Los arreglos son colecciones de elementos del mismo tipo, almacenados en memoria contigua. Se accede a los elementos mediante un índice, que comienza en 0. Es importante tener cuidado de no acceder a índices fuera del rango válido del arreglo, ya que esto puede provocar errores. Los arreglos pueden ser multidimensionales, y se pueden inicializar al momento de la declaración.
