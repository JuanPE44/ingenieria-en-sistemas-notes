Los tipos de datos básicos en C++ (excepto `void` y `bool`) pueden ser alterados mediante **modificadores opcionales**. Estos modificadores cambian el significado del tipo base, principalmente afectando su **rango de valores** y, a veces, el **espacio de almacenamiento** que ocupan en memoria.

## Modificadores Comunes

Los modificadores más utilizados son:

*   **`signed`**: Indica que el tipo numérico puede almacenar tanto valores positivos como negativos (incluyendo el cero). Para los tipos enteros (`char`, `short`, `int`, `long`, `long long`), este suele ser el comportamiento por defecto si no se especifica `unsigned`.
*   **`unsigned`**: Indica que el tipo numérico solo almacenará valores no negativos (cero y positivos). Al eliminar la necesidad de representar números negativos, el rango de valores positivos se duplica en comparación con su contraparte `signed` del mismo tamaño.
*   **`short`**: Sugiere al compilador que utilice menos almacenamiento para el tipo entero que el `int` estándar (generalmente 16 bits). Esto reduce el rango de valores.
*   **`long`**: Sugiere al compilador que utilice al menos tanto almacenamiento como un `int` estándar (generalmente 32 bits o más). Para `double`, existe `long double` para una precisión extendida.
*   **`long long`**: (Introducido en C++11) Sugiere un tamaño aún mayor que `long` para tipos enteros (generalmente 64 bits), permitiendo un rango de valores mucho más amplio.

## Sintaxis General

Los modificadores se colocan antes del nombre del tipo base:

```cpp
[signed|unsigned] [short|long|long long] <tipo_base_entero> <identificador>;
[long] double <identificador>; // Caso especial para double
```

**Ejemplos:**

```cpp
signed int a;      // Explícitamente con signo (equivalente a 'int a;')
unsigned int b;    // Entero sin signo
short c;           // Entero corto (implícitamente signed short int)
unsigned short d;  // Entero corto sin signo
long e;            // Entero largo (implícitamente signed long int)
unsigned long f;   // Entero largo sin signo
long long g;       // Entero muy largo (implícitamente signed long long int)
unsigned long long h; // Entero muy largo sin signo
long double i;     // Punto flotante de precisión extendida
```

## Creación de Nuevos Tipos

Es importante entender que aplicar un modificador a un tipo base **define un nuevo tipo distinto**. Por ejemplo, `int`, `unsigned int`, `short int` y `unsigned short int` son todos tipos diferentes con distintos rangos y, potencialmente, tamaños.

## Reglas Específicas

*   **`char`**: Puede ser `signed char` o `unsigned char`. El tipo `char` simple (sin modificador explícito) puede ser `signed` o `unsigned` dependiendo de la implementación del compilador, aunque a menudo es `signed` por defecto.
*   **`double`**: Solo admite el modificador `long`, resultando en `long double`.

## Tabla de Tipos Fundamentales y Rangos (Valores Típicos)

La siguiente tabla muestra los tipos fundamentales, incluyendo los modificados, y sus rangos de valores típicos en arquitecturas comunes. Ten en cuenta que los tamaños exactos (y por lo tanto los rangos) pueden variar entre diferentes sistemas y compiladores.

| Tipo                 | Rango de Valores Típico (Puede Variar)             | Tamaño Típico (bits) |
| :------------------- | :------------------------------------------------- | :------------------- |
| `unsigned char`      | 0 a 255                                            | 8                    |
| `char` / `signed char` | -128 a 127                                         | 8                    |
| `short` / `signed short` | -32,768 a 32,767                                   | 16                   |
| `unsigned short`     | 0 a 65,535                                         | 16                   |
| `int` / `signed int`   | -2,147,483,648 a 2,147,483,647                     | 32                   |
| `unsigned int`       | 0 a 4,294,967,295                                  | 32                   |
| `long` / `signed long` | -2,147,483,648 a 2,147,483,647 (o mayor)          | 32 / 64              |
| `unsigned long`      | 0 a 4,294,967,295 (o mayor)                        | 32 / 64              |
| `long long` / `signed long long` | -9,223,372,036,854,775,808 a 9,223,372,036,854,775,807 | 64                   |
| `unsigned long long` | 0 a 18,446,744,073,709,551,615                     | 64                   |
| `float`              | ±1.18e-38 a ±3.40e+38 (aprox. 7 dígitos)           | 32                   |
| `double`             | ±2.23e-308 a ±1.79e+308 (aprox. 15 dígitos)         | 64                   |
| `long double`        | ±3.37e-4932 a ±1.18e+4932 (precisión extendida)    | 80 / 96 / 128        |

*Nota: Los rangos para `long` y `unsigned long` pueden ser iguales a los de `int` y `unsigned int` en algunas plataformas (como Windows de 64 bits) o mayores (como en Linux de 64 bits).*
