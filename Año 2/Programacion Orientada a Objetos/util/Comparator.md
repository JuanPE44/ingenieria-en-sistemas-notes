La interfaz `java.util.Comparator<T>` es una interfaz funcional fundamental en Java que se utiliza para definir un **orden total** sobre una colección de objetos de un tipo específico `T`. En esencia, un `Comparator` encapsula la lógica para comparar dos objetos y determinar cuál debe ir "antes" que el otro según un criterio específico.

## Propósito Principal

El propósito principal de `Comparator` es proporcionar un **mecanismo de ordenación externo** para objetos. Esto es útil cuando:

1.  La clase de los objetos que quieres ordenar **no implementa** la interfaz `Comparable`.
2.  La clase implementa `Comparable`, pero necesitas un **orden diferente** al "orden natural" definido por su método `compareTo`.
3.  Necesitas **múltiples criterios de ordenación** para la misma clase de objetos.

## Diferencia Clave con `Comparable`

*   **`Comparable<T>`:** Se implementa **dentro** de la propia clase cuyos objetos se van a comparar (ej. `class Persona implements Comparable<Persona>`). Define el "orden natural" de los objetos de esa clase. Solo puede haber un orden natural por clase. Su método principal es `int compareTo(T other)`.
*   **`Comparator<T>`:** Se implementa como una **clase separada** o mediante una **expresión lambda/clase anónima**. Define un orden específico que puede ser diferente del orden natural o aplicarse a clases que no son `Comparable`. Puedes tener múltiples `Comparator` para la misma clase. Su método principal es `int compare(T o1, T o2)`.

## El Método `compare(T o1, T o2)`

Este es el único método abstracto que *debes* implementar (antes de Java 8). Define la lógica de comparación entre dos objetos `o1` y `o2`:

*   **Retorna un entero negativo (`< 0`):** si `o1` debe ir *antes* que `o2`.
*   **Retorna cero (`0`):** si `o1` y `o2` son considerados *iguales* en términos de ordenación.
*   **Retorna un entero positivo (`> 0`):** si `o1` debe ir *después* que `o2`.

**Contrato del `compare`:**
La implementación debe ser:
*   **Antisimétrica:** `sgn(compare(x, y)) == -sgn(compare(y, x))`
*   **Transitiva:** si `compare(x, y) > 0` y `compare(y, z) > 0`, entonces `compare(x, z) > 0`.
*   **Consistente con `equals` (recomendado, pero no obligatorio):** si `compare(x, y) == 0`, entonces `sgn(compare(x, z)) == sgn(compare(y, z))` para cualquier `z`. Es fuertemente recomendable que `compare(x, y) == 0` implique que `x.equals(y)` sea `true`, especialmente si se usa en `SortedSet` o `SortedMap`.

## Formas de Implementación

### 1. Clase Separada

```java
import java.util.Comparator;

class ComparadorPorLongitud implements Comparator<String> {
    @Override
    public int compare(String s1, String s2) {
        return Integer.compare(s1.length(), s2.length()); // Ordena de más corto a más largo
    }
}

// Uso:
// List<String> lista = ...;
// Collections.sort(lista, new ComparadorPorLongitud());
```

### 2. Clase Anónima (Pre-Java 8)

```java
import java.util.Comparator;
import java.util.List;
import java.util.Collections;
import java.util.ArrayList;

// ...

List<String> lista = new ArrayList<>(List.of("manzana", "banana", "kiwi"));

Comparator<String> comparadorLongitud = new Comparator<String>() {
    @Override
    public int compare(String s1, String s2) {
        return Integer.compare(s1.length(), s2.length());
    }
};

Collections.sort(lista, comparadorLongitud);
System.out.println(lista); // Output: [kiwi, banana, manzana]
```

### 3. Expresión Lambda (Java 8+)

Esta es la forma más concisa y común hoy en día.

```java
import java.util.Comparator;
import java.util.List;
import java.util.Collections;
import java.util.ArrayList;

// ...

List<String> lista = new ArrayList<>(List.of("manzana", "banana", "kiwi"));

// Usando lambda directamente
Collections.sort(lista, (s1, s2) -> Integer.compare(s1.length(), s2.length()));

System.out.println(lista); // Output: [kiwi, banana, manzana]
```

## Métodos Estáticos y por Defecto (Java 8+)

Java 8 introdujo métodos muy útiles en la interfaz `Comparator` que facilitan la creación y composición de comparadores:

*   **`comparing(Function<? super T, ? extends U> keyExtractor)`:** Crea un comparador que compara usando una "clave" extraída mediante una función. La clave debe ser `Comparable`.
    ```java
    // Compara Personas por edad (asumiendo getEdad() devuelve Integer)
    Comparator<Persona> porEdad = Comparator.comparing(Persona::getEdad);
    ```
*   **`comparing(Function<? super T, ? extends U> keyExtractor, Comparator<? super U> keyComparator)`:** Similar al anterior, pero usa un comparador específico para la clave extraída.
    ```java
    // Compara Strings ignorando mayúsculas/minúsculas
    Comparator<String> ignoraCase = Comparator.comparing(s -> s, String.CASE_INSENSITIVE_ORDER);
    ```
*   **`thenComparing(Comparator<? super T> other)`:** Permite encadenar comparadores. Si el primer comparador considera dos elementos iguales, se usa el segundo para desempatar.
    ```java
    // Compara Personas por apellido, y luego por nombre si los apellidos son iguales
    Comparator<Persona> porApellidoLuegoNombre = Comparator.comparing(Persona::getApellido)
                                                          .thenComparing(Persona::getNombre);
    ```
*   **`thenComparing(Function<? super T, ? extends U> keyExtractor)`:** Versión de `thenComparing` que usa una función extractora de clave.
*   **`naturalOrder()`:** Devuelve un comparador que usa el orden natural (el objeto debe implementar `Comparable`).
*   **`reverseOrder()`:** Devuelve un comparador que impone el orden inverso al natural.
*   **`reversed()`:** Invierte el orden del comparador sobre el que se llama.
    ```java
    Comparator<String> porLongitudDesc = ((Comparator<String>)(s1, s2) -> Integer.compare(s1.length(), s2.length())).reversed();
    // O más fácil:
    Comparator<String> porLongitudDesc2 = Comparator.comparingInt(String::length).reversed();
    ```
*   **`nullsFirst(Comparator<? super T> comparator)`:** Adapta un comparador existente para que considere los `null` menores que los no nulos.
*   **`nullsLast(Comparator<? super T> comparator)`:** Adapta un comparador existente para que considere los `null` mayores que los no nulos.

## Casos de Uso Comunes

*   **Ordenar Colecciones:** `Collections.sort(List<T> list, Comparator<? super T> c)` o `List.sort(Comparator<? super T> c)`.
*   **Ordenar Arrays:** `Arrays.sort(T[] a, Comparator<? super T> c)`.
*   **Estructuras de Datos Ordenadas:**
    *   `PriorityQueue(Comparator<? super E> comparator)`: Para definir la prioridad.
    *   `TreeSet(Comparator<? super E> comparator)`: Para definir el orden de los elementos en el conjunto.
    *   `TreeMap(Comparator<? super K> comparator)`: Para definir el orden de las claves en el mapa.
*   **Streams API:** En operaciones como `sorted(Comparator<? super T> comparator)`.

## Ejemplo Completo (Java 8+)

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

class Producto {
    String nombre;
    double precio;
    int stock;

    public Producto(String nombre, double precio, int stock) {
        this.nombre = nombre;
        this.precio = precio;
        this.stock = stock;
    }

    public String getNombre() { return nombre; }
    public double getPrecio() { return precio; }
    public int getStock() { return stock; }

    @Override
    public String toString() {
        return "Producto{" + "nombre='" + nombre + '\'' + ", precio=" + precio + ", stock=" + stock + '}';
    }
}

public class EjemploComparator {
    public static void main(String[] args) {
        List<Producto> inventario = new ArrayList<>();
        inventario.add(new Producto("Laptop", 1200.50, 10));
        inventario.add(new Producto("Mouse", 25.99, 50));
        inventario.add(new Producto("Teclado", 75.00, 30));
        inventario.add(new Producto("Monitor", 300.00, 15));
        inventario.add(new Producto("Webcam", 50.00, 25));
        inventario.add(new Producto("Mouse", 20.00, 5)); // Otro mouse

        // 1. Ordenar por precio (ascendente) usando comparing
        Comparator<Producto> porPrecio = Comparator.comparing(Producto::getPrecio);
        inventario.sort(porPrecio);
        System.out.println("Ordenado por precio (asc):");
        inventario.forEach(System.out::println);
        System.out.println("----");

        // 2. Ordenar por nombre (alfabético)
        Comparator<Producto> porNombre = Comparator.comparing(Producto::getNombre);
        inventario.sort(porNombre);
        System.out.println("Ordenado por nombre (asc):");
        inventario.forEach(System.out::println);
        System.out.println("----");

        // 3. Ordenar por stock (descendente)
        Comparator<Producto> porStockDesc = Comparator.comparingInt(Producto::getStock).reversed();
        inventario.sort(porStockDesc);
        System.out.println("Ordenado por stock (desc):");
        inventario.forEach(System.out::println);
        System.out.println("----");

        // 4. Ordenar por nombre y luego por precio (ascendente) si los nombres son iguales
        Comparator<Producto> porNombreLuegoPrecio = Comparator.comparing(Producto::getNombre)
                                                             .thenComparing(Producto::getPrecio);
        inventario.sort(porNombreLuegoPrecio);
        System.out.println("Ordenado por nombre (asc) y luego precio (asc):");
        inventario.forEach(System.out::println);
        System.out.println("----");
    }
}
```

## Conclusión

`Comparator` es una interfaz esencial en Java para definir criterios de ordenación personalizados y flexibles. Permite desacoplar la lógica de comparación de las clases que se comparan y ofrece múltiples formas de implementación, siendo las expresiones lambda y los métodos de utilidad de Java 8+ las opciones más modernas y convenientes. Es fundamental para trabajar eficazmente con colecciones ordenadas, colas de prioridad y la API de Streams.
```