La programación dinámica es una técnica algorítmica utilizada para resolver problemas de optimización que exhiben dos propiedades clave:

1.  **Subestructura Óptima:** Una solución óptima al problema contiene soluciones óptimas a subproblemas.
2.  **Subproblemas Superpuestos:** El problema se puede dividir en subproblemas que se resuelven repetidamente.

En lugar de resolver repetidamente los mismos subproblemas (como lo haría un enfoque recursivo ingenuo), la programación dinámica resuelve cada subproblema solo una vez y almacena su solución en una tabla (o matriz) para su uso posterior. Esto evita la redundancia y mejora significativamente la eficiencia.

**Conceptos Clave:**

*   **Subproblema:** Una versión más pequeña del problema original.
*   **Tabla de Memorización (o Matriz DP):** Una estructura de datos (generalmente una matriz) que almacena las soluciones a los subproblemas.
*   **Relación de Recurrencia:** Una fórmula que define la solución a un subproblema en términos de las soluciones a subproblemas más pequeños.
*   **Caso Base:** La solución a los subproblemas más pequeños (que no dependen de otros subproblemas).

**Dos Enfoques Principales:**

1.  **Top-Down (Memorización):**
    *   Comienza con el problema original y lo divide en subproblemas.
    *   Resuelve los subproblemas de forma recursiva, pero almacena las soluciones en la tabla de memorización.
    *   Si un subproblema ya se ha resuelto, se recupera su solución de la tabla en lugar de volver a calcularla.
2.  **Bottom-Up (Tabulación):**
    *   Comienza con los subproblemas más pequeños y los resuelve primero.
    *   Almacena las soluciones en la tabla de memorización.
    *   Utiliza las soluciones a los subproblemas más pequeños para resolver subproblemas más grandes, hasta llegar al problema original.

**Ejemplo Clásico: La Secuencia de Fibonacci:**

La secuencia de Fibonacci se define como:

*   F(0) = 0
*   F(1) = 1
*   F(n) = F(n-1) + F(n-2) para n > 1

**1. Enfoque Recursivo Ingenuo (Ineficiente):**

```cpp
int fibonacciRecursivo(int n) {
    if (n <= 1) {
        return n;
    } else {
        return fibonacciRecursivo(n - 1) + fibonacciRecursivo(n - 2);
    }
}
```

Este enfoque es muy ineficiente porque calcula repetidamente los mismos valores de Fibonacci.

**2. Enfoque Top-Down (Memorización):**

```cpp
int fibonacciMemorizacion(int n, int memo[]) {
    if (memo[n] != -1) {
        return memo[n]; // Valor ya calculado
    }

    if (n <= 1) {
        memo[n] = n;
    } else {
        memo[n] = fibonacciMemorizacion(n - 1, memo) + fibonacciMemorizacion(n - 2, memo);
    }

    return memo[n];
}

// Función auxiliar para inicializar la tabla de memorización
int fibonacciTopDown(int n) {
    int memo[n + 1];
    for (int i = 0; i <= n; i++) {
        memo[i] = -1; // Inicializar con -1 para indicar que no se ha calculado
    }
    return fibonacciMemorizacion(n, memo);
}
```

**3. Enfoque Bottom-Up (Tabulación):**

```cpp
int fibonacciTabulacion(int n) {
    int tabla[n + 1];
    tabla[0] = 0;
    tabla[1] = 1;

    for (int i = 2; i <= n; i++) {
        tabla[i] = tabla[i - 1] + tabla[i - 2];
    }

    return tabla[n];
}
```

**Características de la Programación Dinámica:**

*   **Optimización:** Se utiliza para resolver problemas de optimización (encontrar el máximo, el mínimo, etc.).
*   **Eficiencia:** Evita la redundancia al almacenar las soluciones a los subproblemas.
*   **Complejidad:** Generalmente tiene una complejidad polinómica (en comparación con la complejidad exponencial de algunos enfoques recursivos).
*   **Memoria:** Requiere memoria adicional para almacenar la tabla de memorización.

**Cuándo Usar Programación Dinámica:**

*   Problemas de optimización con subestructura óptima y subproblemas superpuestos.
*   Problemas donde se puede definir una relación de recurrencia.
*   Problemas donde el espacio de búsqueda es relativamente pequeño.

**Ventajas de la Programación Dinámica:**

*   Mejora significativamente la eficiencia al evitar la redundancia.
*   Garantiza encontrar la solución óptima.
*   Puede ser más fácil de entender y depurar que algunos enfoques recursivos complejos.

**Desventajas de la Programación Dinámica:**

*   Requiere memoria adicional para almacenar la tabla de memorización.
*   Puede ser difícil de aplicar a problemas que no tienen subestructura óptima o subproblemas superpuestos.
*   La implementación puede ser más compleja que un enfoque recursivo simple.

