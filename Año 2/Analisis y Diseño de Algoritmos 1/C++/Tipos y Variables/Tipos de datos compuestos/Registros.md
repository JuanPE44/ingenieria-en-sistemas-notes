En C++, un **registro (estructura - `struct`)** permite agrupar una o más variables (llamadas miembros o campos) bajo un mismo nombre. Estos miembros pueden ser de diferentes tipos de datos.

**Sintaxis:**

```c++
struct <tipo_registro> {
    <tipo> <nombre_campo1>;
    <tipo> <nombre_campo2>;
    ...
    <tipo> <nombre_campon>;
};
```

*   `<tipo_registro>`:  Es el nombre que se le da al tipo de estructura.
*   `<tipo>`: Es el tipo de dato de cada miembro.
*   `<nombre_campo>`: Es el nombre de cada miembro dentro de la estructura.

**Ejemplo:**

```c++
struct Empleado {
    int id;
    string nombre;
    string apellido;
    float salario;
};
```

En este ejemplo, `Empleado` es una estructura que contiene un `id` (entero), un `nombre` (cadena), un `apellido` (cadena) y un `salario` (flotante).

**Declaración de variables del tipo de la estructura:**

Una vez definida la estructura, se puede usar su nombre (`Empleado` en el ejemplo) para declarar variables de ese tipo:

```c++
Empleado emp; // Declara una variable llamada 'emp' de tipo 'Empleado'
```

**Acceso a los miembros:**

Para acceder a los miembros de una estructura, se utiliza el operador punto (`.`) :

```c++
<variable_registro>.<nombre_campo>
```

**Ejemplo de uso:**

```c++
int main() {
    Empleado emp;
    emp.id = 1;
    emp.salario = 999.99;
    emp.nombre = "Juan";
    emp.apellido = "Perez";

    cout << "Nombre: " << emp.nombre << endl;
    cout << "Salario: " << emp.salario << endl;

    return 0;
}
```

**Estructuras anidadas:**

Una estructura puede contener otras estructuras como miembros, lo que permite crear estructuras de datos más complejas:

```c++
struct Seccion {
    int id;
    string nombre;
    Empleado encargado; // Un miembro de tipo 'Empleado'
};
```

**Acceso a miembros de estructuras anidadas:**

Se utiliza el operador punto (`.`) de forma encadenada para acceder a los miembros de las estructuras anidadas:

```c++
int main() {
    Seccion seccion;
    seccion.id = 1;
    seccion.encargado.salario = 999.99; // Accede al salario del empleado encargado
    seccion.encargado.nombre = "Juan";

    return 0;
}
```

**En resumen:**

Las estructuras permiten agrupar datos relacionados de diferentes tipos bajo un mismo nombre, facilitando la organización y manipulación de la información.  Se accede a los miembros de una estructura utilizando el operador punto (`.`).  Las estructuras pueden anidarse para crear estructuras de datos más complejas.
