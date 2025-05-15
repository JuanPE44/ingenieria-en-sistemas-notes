Permite tener múltiples funciones con el mismo nombre pero con diferentes listas de parámetros (diferente número, tipo o orden de parámetros).

 **Propósito:** Proporciona una forma de realizar la misma operación en diferentes tipos de datos o con diferentes cantidades de datos.
 
**Ejemplo:**

``` cpp
float operar(int x, int y) { /* ... */ }
float operar(float x, float y) { /* ... */ }
```

  **Resolución:** El compilador determina qué función llamar basándose en los tipos de los argumentos utilizados en la llamada.
  
  **Restricción:** No se pueden sobrecargar funciones solo por el tipo de retorno. Al menos uno de los parámetros debe ser diferente.

