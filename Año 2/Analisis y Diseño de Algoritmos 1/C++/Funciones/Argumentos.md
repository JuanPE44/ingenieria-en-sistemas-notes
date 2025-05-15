La función `main` puede recibir argumentos desde la línea de comandos.
**Sintaxis:**

```cpp
int main(int argc, char *argv[]) {
	// ...
}
```

*   `argc`: Entero que indica el número de argumentos (incluyendo el nombre del programa).
*   `argv`: Arreglo de punteros a caracteres (cadenas) que contiene los argumentos. `argv[0]` es el nombre del programa.
*   **Ejemplo:**

```cpp
int main(int argc, char *argv[]) {
	std::cout << "Cantidad de argumentos: " << argc << std::endl;
	std::cout << "Argumentos: ";
	for (int i = 0; i < argc; i++)
		std::cout << argv[i] << " ";
	std::cout << std::endl;
	return 0;
}
```

   Si compilas y ejecutas este programa como `ejemplo arg1 arg2 arg3`, la salida será:

```
Cantidad de argumentos: 4
Argumentos: ejemplo arg1 arg2 arg3
```
