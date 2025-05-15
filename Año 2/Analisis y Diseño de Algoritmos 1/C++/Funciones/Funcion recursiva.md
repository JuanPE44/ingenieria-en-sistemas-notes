
 **Definición:** Una función que se llama a sí misma.
***Tipos:**
*   Directa: La función se llama directamente a sí misma.
*   Indirecta: La función llama a otra función, que a su vez llama a la función original.
**Requisitos:**
*   Debe tener un caso base: Una condición que detiene la recursión y devuelve un valor directamente.
*   Debe avanzar hacia el caso base: Cada llamada recursiva debe acercarse al caso base.
*   **Ejemplo:**

```cpp
int factorial(int numero) {
	if (numero == 0) // Caso base
		return 1;
	else
		return (numero * factorial(numero - 1)); // Llamada recursiva
}
```

   **Consideraciones:**
*   La recursión puede ser elegante para ciertos problemas, pero puede ser ineficiente en términos de memoria y tiempo debido a las múltiples llamadas a la función y la gestión de la pila.
*   Es importante evitar la recursión infinita (cuando no se alcanza el caso base), lo que puede provocar un desbordamiento de pila.

**Comparación entre Iteración y Recursión:**

| Característica | Iteración                                  | Recursión                                     |
| :------------- | :----------------------------------------- | :-------------------------------------------- |
| Mecanismo      | Repetición de sentencias con bucles       | Llamada a la función dentro de sí misma       |
| Memoria        | Generalmente más eficiente en memoria     | Puede consumir más memoria (pila de llamadas) |
| Complejidad    | A veces más compleja de implementar       | A veces más simple de implementar             |
| Problemas      | Bucle infinito si la condición no se cumple | Desbordamiento de pila si no hay caso base   |

