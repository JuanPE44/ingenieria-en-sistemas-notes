**Propósito:** Informa al compilador sobre la existencia de una función antes de que se utilice.
  **Sintaxis:**

```cpp
<tipo_retorno> <nombre_función>(<lista_de_parámetros>);
```

*   `<tipo_retorno>`: Tipo de dato del valor que devuelve la función (o `void` si no devuelve nada).
*   `<nombre_función>`: Nombre de la función.
*   `<lista_de_parámetros>`: Lista de declaraciones de parámetros (tipo y nombre) separados por comas. Puede estar vacía si la función no recibe parámetros. En el prototipo, a veces solo se especifican los tipos de los parámetros.
 **Ejemplo:**

```cpp
float obtenerPromedio(int enteros[], int cantidad); // Declaración
```

  **Importancia:** Permite al compilador verificar que las llamadas a la función sean correctas (tipos de argumentos, etc.) antes de que la función se defina por completo. Una función puede ser declarada varias veces.
