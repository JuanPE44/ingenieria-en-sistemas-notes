
**Definición de Funciones:**

  **Propósito:** Proporciona la implementación real de la función (el código que se ejecuta).
  **Sintaxis:**

```cpp
<tipo_retorno> <nombre_función>(<lista_de_parámetros>) {
	// <sentencias> (cuerpo de la función)
}
```

*   Incluye la misma información que la declaración (tipo de retorno, nombre, lista de parámetros) más el cuerpo de la función entre llaves `{}`.
**Ejemplo:**

```cpp
float obtenerPromedio(int enteros[], int cantidad) {
	float suma = 0;
	for (int i = 0; i < cantidad; i++) {
		suma = suma + enteros[i];
	}
	return suma / cantidad;
}
```

  **Requisitos:**
*   Cada función debe tener una única definición en todo el programa.
*   Si el tipo de retorno no es `void`, la función debe tener al menos una sentencia `return` que devuelva un valor del tipo correcto.
*   La definición puede servir como declaración si aparece antes de cualquier uso de la función.

**Sentencia `return`:**

*   **Propósito:** Devuelve un valor desde la función al código que la llamó y finaliza la ejecución de la función.
*   **Sintaxis:**

```cpp
return <expresión>;
```

*   `<expresión>`: El valor que se devuelve. Su tipo debe coincidir con el tipo de retorno de la función.
   **Consideraciones:**
*   Una función puede tener múltiples sentencias `return`, pero solo se ejecutará una.
*   Es buena práctica tener un único punto de salida (un solo `return` al final de la función) para facilitar la lectura y el mantenimiento del código.
*   El código después de un `return` no se ejecuta.

