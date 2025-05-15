
**Pasaje por Valor (Copia):**
*   Se crea una copia del valor del argumento y se pasa a la función.
*   Los cambios realizados al parámetro dentro de la función no afectan al argumento original.
*   **Sintaxis:**

```cpp
<tipo> <parámetro>
```

 **Ejemplo:**

```cpp
void modificar(int variable) {
	variable = 10;
	std::cout << "modificar – valor variable: " << variable << std::endl; // Imprime 10
}

int main() {
	int variable = 2;
	modificar(variable);
	std::cout << "main – valor variable: " << variable << std::endl; // Imprime 2 (no se modificó)
}
```

 **Pasaje por Referencia:**
*   El parámetro se convierte en un alias del argumento original.
*   Los cambios realizados al parámetro dentro de la función sí afectan al argumento original.
*   **Sintaxis:**

```cpp
<tipo> & <parámetro>
```

**Ejemplo:**

```cpp
void modificar(int & variable) {
	variable = 10;
	std::cout << "modificar – valor variable: " << variable << std::endl; // Imprime 10
}

int main() {
	int variable = 2;
	modificar(variable);
	std::cout << "main – valor variable: " << variable << std::endl; // Imprime 10 (se modificó)
}
```

 **Cuándo usar cada uno:**
*   Por valor: Cuando no necesitas modificar el argumento original.
*   Por referencia: Cuando necesitas que la función modifique el argumento original (por ejemplo, para "devolver" múltiples valores).


