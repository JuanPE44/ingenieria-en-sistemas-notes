En C++, además de los tipos de datos básicos, existen los **tipos de datos compuestos** o **estructurados**. Estos tipos permiten agrupar múltiples valores, posiblemente de diferentes tipos, bajo un mismo nombre. Los tipos de datos compuestos incluyen:

*   **[[Enumeraciones]] (`enum`):** Definen un conjunto de constantes con nombre.
*   **[[Registros]] (Estructuras - `struct`):** Agrupan variables de diferentes tipos bajo un mismo nombre.  Permiten crear tipos de datos personalizados.
*   **Uniones (`union`):** Similares a las estructuras, pero todos los miembros comparten la misma ubicación de memoria.  Útiles para ahorrar memoria cuando solo se necesita usar un miembro a la vez.
*   **Arreglos (Arrays):** Colecciones de elementos del mismo tipo, almacenados en posiciones de memoria contiguas.
*   **Cadenas de caracteres (Strings):** Secuencias de caracteres.  En C++, se pueden manejar como arreglos de caracteres o utilizando la clase `std::string`.
*   **Punteros:** Variables que almacenan direcciones de memoria.  Permiten acceder y manipular datos indirectamente.
*   **Memoria dinámica:**  Permite asignar y liberar memoria durante la ejecución del programa, lo que es útil para crear estructuras de datos que crecen o se reducen según sea necesario. (Se verá en detalle más adelante).

