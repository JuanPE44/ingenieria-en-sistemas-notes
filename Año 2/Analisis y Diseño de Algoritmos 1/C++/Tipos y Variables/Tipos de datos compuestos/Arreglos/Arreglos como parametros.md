En C++, no se puede pasar un arreglo completo por valor (copia) a una función. En su lugar, se pasa la dirección del primer elemento del arreglo, lo que permite a la función acceder y modificar los elementos originales del arreglo.

**Sintaxis para declarar un arreglo como parámetro:**

```c++
void imprimir(int arreglo[]);
```

*   `int arreglo[]`: Indica que la función recibe un arreglo de enteros como argumento. No es necesario especificar el tamaño del arreglo dentro de los corchetes.

**Invocación de la función:**

```c++
int valores[5];
imprimir(valores);
```

*   Se pasa el nombre del arreglo (`valores`) como argumento. Esto pasa la dirección del primer elemento del arreglo a la función.

**Tamaño del arreglo:**

Dado que la función no conoce el tamaño del arreglo que se le pasa, es común agregar un segundo parámetro para indicar la capacidad del arreglo:

```c++
void imprimir(int arreglo[], int capacidad);
```

**Arreglos multidimensionales como parámetros:**

Al pasar un arreglo multidimensional como parámetro, se debe especificar el tamaño de todas las dimensiones *excepto* la primera:

```c++
void imprimir(int arreglo[][4], int capacidad);
```

*   `int arreglo[][4]`: Indica que la función recibe un arreglo bidimensional de enteros como argumento. El tamaño de la segunda dimensión (4) debe especificarse.
*   `int capacidad`: Representa el número de filas en el arreglo.

**Paso por referencia (implícito):**

Cuando se pasa un arreglo a una función, en realidad se está pasando un *puntero* al primer elemento del arreglo. Esto significa que la función puede modificar los elementos originales del arreglo.

**Ejemplo:**

```c++
void inicializar(int arreglo[], int capacidad) {
    for (int i = 0; i < capacidad; i++) {
        arreglo[i] = 0; // Modifica el arreglo original
    }
}

int main() {
    int numeros[5] = {1, 2, 3, 4, 5};
    inicializar(numeros, 5); // Pasa el arreglo 'numeros' a la función

    // Después de llamar a la función, todos los elementos de 'numeros' serán 0
    for (int i = 0; i < 5; i++) {
        cout << numeros[i] << " "; // Imprime: 0 0 0 0 0
    }
    cout << endl;

    return 0;
}
```

**Consideraciones importantes:**

*   **Modificación del arreglo original:** Debido a que se pasa un puntero al arreglo, cualquier modificación realizada dentro de la función afectará al arreglo original.
*   **Errores inesperados:** Es importante tener en cuenta esta característica al estructurar los programas, ya que puede generar errores inesperados si no se tiene cuidado.

**En resumen:**

En C++, los arreglos se pasan a las funciones pasando la dirección del primer elemento. Esto permite a la función modificar los elementos originales del arreglo. Al pasar arreglos multidimensionales, se debe especificar el tamaño de todas las dimensiones excepto la primera. Es crucial tener en cuenta que las modificaciones dentro de la función afectarán al arreglo original, lo que puede generar errores si no se maneja con cuidado.
