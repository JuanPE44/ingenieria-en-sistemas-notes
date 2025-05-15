La interfaz `java.lang.Comparable<T>` es una interfaz fundamental en Java que permite que los objetos de una clase que la implementa puedan ser **ordenados** según su **orden natural**. Una clase que implementa `Comparable` define cómo sus instancias se comparan entre sí.

## Propósito Principal

El propósito principal de `Comparable` es dotar a los objetos de una clase de una **capacidad intrínseca de comparación**, definiendo lo que se considera su "orden natural". Esto permite que colecciones de estos objetos (como listas o arrays) puedan ser ordenadas automáticamente por métodos como `Collections.sort()` o `Arrays.sort()` sin necesidad de especificar un criterio de ordenación externo. También es crucial para el funcionamiento de estructuras de datos ordenadas como `TreeSet` y `TreeMap` cuando no se proporciona un `Comparator`.

## Implementación

A diferencia de `Comparator`, la interfaz `Comparable` se implementa **directamente dentro de la clase** cuyos objetos se desean comparar.

```java
public class MiClase implements Comparable<MiClase> {
    // Atributos de MiClase...

    @Override
    public int compareTo(MiClase otroObjeto) {
        // Lógica de comparación entre 'this' y 'otroObjeto'
        // ...
    }

    // Otros métodos de MiClase...
}
```

La `T` en `Comparable<T>` suele ser la misma clase que la implementa.

## El Método `compareTo(T o)`

Este es el único método que define la interfaz `Comparable`. Es responsable de comparar el objeto actual (`this`) con otro objeto (`o`) del mismo tipo.

*   **Retorna un entero negativo (`< 0`):** si el objeto actual (`this`) es *menor* que el objeto `o`.
*   **Retorna cero (`0`):** si el objeto actual (`this`) es *igual* al objeto `o` en términos de ordenación.
*   **Retorna un entero positivo (`> 0`):** si el objeto actual (`this`) es *mayor* que el objeto `o`.

**Contrato del `compareTo`:**
La implementación debe cumplir con las siguientes propiedades matemáticas para asegurar un orden total consistente:
*   **Antisimétrica:** `sgn(x.compareTo(y)) == -sgn(y.compareTo(x))` para todo `x` e `y`. (Si `x` es menor que `y`, `y` debe ser mayor que `x`).
*   **Transitiva:** si `x.compareTo(y) > 0` e `y.compareTo(z) > 0`, entonces `x.compareTo(z) > 0`. (Si `x` > `y` e `y` > `z`, entonces `x` > `z`).
*   **Consistente con `equals` (fuertemente recomendado):** si `x.compareTo(y) == 0`, entonces `sgn(x.compareTo(z)) == sgn(y.compareTo(z))` para todo `z`. Además, se recomienda encarecidamente (aunque no es estrictamente obligatorio por el contrato de `compareTo`) que `x.compareTo(y) == 0` implique que `x.equals(y)` sea `true`. Si esta condición no se cumple, las clases `SortedSet` y `SortedMap` (como `TreeSet` y `TreeMap`) pueden comportarse de manera inesperada, ya que consideran que dos objetos son iguales si `compareTo` devuelve 0.

**Manejo de Nulos:**
Por convención, `x.compareTo(null)` debería lanzar una `NullPointerException`.

## Diferencia Clave con `Comparator`

| Característica      | `Comparable<T>`                                  | `Comparator<T>`                                      |
| :------------------ | :----------------------------------------------- | :--------------------------------------------------- |
| **Implementación**  | Dentro de la clase a comparar (`implements`)     | Clase separada, anónima o lambda (externa)           |
| **Método Principal**| `int compareTo(T other)`                         | `int compare(T o1, T o2)`                            |
| **Propósito**       | Define el **orden natural** de la clase.         | Define un **orden específico** (posiblemente externo). |
| **Flexibilidad**    | Solo un orden natural por clase.                 | Permite múltiples criterios de ordenación.           |
| **Modificación**    | Requiere modificar el código fuente de la clase. | No requiere modificar la clase original.             |
| **Uso Típico**      | Clases con un orden obvio (String, Integer, Date). | Ordenaciones personalizadas, múltiples órdenes.      |

## ¿Cuándo Usar `Comparable`?

*   Cuando una clase tiene un **orden natural claro y único**. Ejemplos típicos son clases que representan valores numéricos, cadenas de texto, fechas, etc.
*   Cuando quieres que los objetos de tu clase sean **fácilmente ordenables** por defecto en colecciones y arrays estándar.
*   Cuando necesitas usar tus objetos como claves en un `TreeMap` o elementos en un `TreeSet` **sin** proporcionar explícitamente un `Comparator`.

## Ejemplo

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.util.Objects;

// Clase que representa un estudiante, comparable por su ID
class Estudiante implements Comparable<Estudiante> {
    private int id;
    private String nombre;
    private double promedio;

    public Estudiante(int id, String nombre, double promedio) {
        this.id = id;
        this.nombre = nombre;
        this.promedio = promedio;
    }

    public int getId() { return id; }
    public String getNombre() { return nombre; }
    public double getPromedio() { return promedio; }

    @Override
    public String toString() {
        return "Estudiante{" + "id=" + id + ", nombre='" + nombre + '\'' + ", promedio=" + promedio + '}';
    }

    // Implementación del orden natural: por ID ascendente
    @Override
    public int compareTo(Estudiante otro) {
        // Se usa Integer.compare para manejar la resta de forma segura (evita overflow)
        return Integer.compare(this.id, otro.id);

        // Alternativa (menos segura si los IDs pueden ser muy grandes o negativos):
        // return this.id - otro.id;
    }

    // Es buena práctica sobreescribir equals y hashCode si se implementa Comparable,
    // especialmente si compareTo devuelve 0 para objetos no iguales según equals.
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Estudiante that = (Estudiante) o;
        return id == that.id; // Consideramos iguales si tienen el mismo ID
    }

    @Override
    public int hashCode() {
        return Objects.hash(id);
    }
}

public class EjemploComparable {
    public static void main(String[] args) {
        List<Estudiante> clase = new ArrayList<>();
        clase.add(new Estudiante(101, "Ana", 8.5));
        clase.add(new Estudiante(55, "Luis", 9.1));
        clase.add(new Estudiante(210, "Carlos", 7.8));
        clase.add(new Estudiante(5, "Eva", 8.8));

        System.out.println("Lista original:");
        clase.forEach(System.out::println);

        // Ordenamos usando el orden natural (definido por compareTo)
        Collections.sort(clase);

        System.out.println("\nLista ordenada por ID (orden natural):");
        clase.forEach(System.out::println);
    }
}
```
**Salida:**
```
Lista original:
Estudiante{id=101, nombre='Ana', promedio=8.5}
Estudiante{id=55, nombre='Luis', promedio=9.1}
Estudiante{id=210, nombre='Carlos', promedio=7.8}
Estudiante{id=5, nombre='Eva', promedio=8.8}

Lista ordenada por ID (orden natural):
Estudiante{id=5, nombre='Eva', promedio=8.8}
Estudiante{id=55, nombre='Luis', promedio=9.1}
Estudiante{id=101, nombre='Ana', promedio=8.5}
Estudiante{id=210, nombre='Carlos', promedio=7.8}
```

## Conclusión

`Comparable` es la interfaz estándar en Java para definir el **orden natural** de los objetos de una clase. Al implementar `compareTo`, permites que tus objetos sean ordenados automáticamente por las utilidades de Java y utilizados en estructuras de datos ordenadas sin configuración adicional. Es ideal para clases con un criterio de ordenación principal y obvio. Para criterios de ordenación alternativos o para ordenar clases que no puedes modificar, se utiliza `Comparator`.
```