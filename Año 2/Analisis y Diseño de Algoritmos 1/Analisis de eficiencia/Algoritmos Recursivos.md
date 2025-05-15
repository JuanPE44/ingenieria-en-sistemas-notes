## ¿Qué es la Recursión?

La recursión es una forma de definir o resolver un problema haciendo que la solución dependa de soluciones a instancias más pequeñas del mismo problema. En programación, esto se logra mediante **funciones recursivas**.

## Funciones Recursivas

Una función recursiva es aquella que se llama a sí misma dentro de su propia definición. El esquema general para construir una función recursiva incluye dos tipos de casos fundamentales:

1.  **Caso Base:**
    *   Representa la(s) condición(es) más simple(s) del problema, cuya solución se conoce directamente o es trivial de calcular.
    *   **Importante:** Este caso **no** incluye ninguna llamada recursiva a la propia función.
    *   Es esencial para detener la secuencia de llamadas recursivas y evitar un bucle infinito.

2.  **Caso General (o Recursivo):**
    *   Define la solución del problema en términos de una o más llamadas a la misma función, pero aplicadas a versiones "más pequeñas" o "más simples" del problema original.
    *   Estas **llamadas recursivas** descomponen el problema original en subproblemas que eventualmente convergerán hacia el caso base.
    *   La idea es que cada llamada recursiva resuelva una versión más pequeña de la tarea, acercándose progresivamente a la solución del caso base.

**En resumen:** Una función recursiva funciona dividiendo el problema en:
*   Una parte que sabe cómo resolver directamente (el **caso base**).
*   Otra parte que se resuelve haciendo una llamada a sí misma con una versión reducida del problema (el **caso general**), confiando en que esta llamada eventualmente llegará al caso base.




## Análisis de Complejidad Temporal: Funcion1

## Código de la Función

```cpp
unsigned int Funcion1 (unsigned int i){
  if (i <= 1)
    return 1;
  else {
    unsigned int aux = Funcion1 (i-1);
    return 2 * aux;
  }
}
```

## Explicación del Funcionamiento

1.  **Caso Base:** Si el valor de entrada `i` es menor o igual a 1, la función retorna inmediatamente el valor 1.
2.  **Caso Recursivo:** Si `i` es mayor que 1:
    *   La función se llama a sí misma con el argumento `i-1`. Esta es la llamada recursiva que reduce el tamaño del problema.
    *   El resultado de esta llamada recursiva se guarda en la variable `aux`.
    *   Finalmente, la función retorna el doble del valor almacenado en `aux`.

## Análisis de Complejidad Temporal

Para determinar la complejidad temporal, estableceremos una ecuación de recurrencia $T(i)$ que represente el tiempo de ejecución de `Funcion1` para una entrada `i`.

1.  **Caso Base (i <= 1):**
    *   Se realiza una comparación (`i <= 1`).
    *   Se ejecuta una instrucción `return`.
    *   El tiempo es constante. Lo denotamos como $c_0$.
    *   $T(i) = c_0$ si $i \le 1$

2.  **Caso Recursivo (i > 1):**
    *   Se realiza una comparación (`i <= 1`).
    *   Se realiza una llamada recursiva `Funcion1(i-1)`, que toma $T(i-1)$ tiempo.
    *   Se realiza una asignación (`aux = ...`).
    *   Se realiza una multiplicación (`2 * aux`).
    *   Se ejecuta una instrucción `return`.
    *   Las operaciones de comparación, asignación, multiplicación y retorno toman un tiempo constante en conjunto. Lo denotamos como $c_1$.
    *   El tiempo total es la suma del tiempo de la llamada recursiva y el tiempo constante de las otras operaciones.
    *   $T(i) = T(i-1) + c_1$ si $i > 1$

## Resolución de la Ecuación de Recurrencia

Tenemos la siguiente recurrencia:
*   $T(i) = c_0$ si $i \le 1$
*   $T(i) = T(i-1) + c_1$ si $i > 1$

Utilizamos el método de sustitución (o expansión) para resolverla (asumiendo $i > 1$):

*   $T(i) = T(i-1) + c_1$
*   $T(i) = [T(i-2) + c_1] + c_1 = T(i-2) + 2c_1$
*   $T(i) = [T(i-3) + c_1] + 2c_1 = T(i-3) + 3c_1$
*   ... (después de $k$ pasos) ...
*   $T(i) = T(i-k) + k c_1$

Queremos llegar al caso base, por ejemplo $T(1)$. Esto ocurre cuando $i-k = 1$, lo que implica $k = i-1$. Sustituimos $k = i-1$:

*   $T(i) = T(i - (i-1)) + (i-1) c_1$
*   $T(i) = T(1) + (i-1) c_1$

Usando la definición del caso base $T(1) = c_0$:

*   $T(i) = c_0 + (i-1) c_1$
*   $T(i) = c_0 + i c_1 - c_1$

## Conclusión: Notación Big-Oh

La expresión del tiempo de ejecución es $T(i) = c_1 \cdot i + (c_0 - c_1)$. Esta es una función lineal de $i$.

En la notación Big-Oh, nos centramos en el término dominante y despreciamos las constantes. El término dominante es $c_1 \cdot i$.

Por lo tanto, la complejidad temporal de `Funcion1` es:

**$O(i)$**
