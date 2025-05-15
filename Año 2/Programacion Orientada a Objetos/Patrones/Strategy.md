El patrón de diseño Strategy en Java es un patrón de diseño de comportamiento que te permite definir una familia de algoritmos, encapsular cada uno de ellos y hacerlos intercambiables.  Permite que el algoritmo varíe independientemente de los clientes que lo utilizan.  En esencia, delega la elección del algoritmo a tiempo de ejecución.

**Propósito:**

*   Definir una familia de algoritmos.
*   Encapsular cada algoritmo en una clase separada.
*   Hacer que los algoritmos sean intercambiables.
*   Permitir que el algoritmo varíe independientemente de los clientes que lo utilizan.

**Componentes:**

*   **Strategy Interface:** Define la interfaz común para todos los algoritmos.  Generalmente tiene un solo método que realiza la operación principal.
*   **Concrete Strategies:** Implementan la Strategy Interface y encapsulan un algoritmo específico.
*   **Context:** Contiene una referencia a un objeto Strategy.  Delega la ejecución del algoritmo al objeto Strategy.  El Context puede cambiar el objeto Strategy en tiempo de ejecución.

**Ventajas:**

*   **Flexibilidad:** Permite cambiar el algoritmo en tiempo de ejecución sin modificar el código del cliente.
*   **Reutilización:** Los algoritmos pueden reutilizarse en diferentes partes de la aplicación.
*   **Separación de responsabilidades:** La lógica de cada algoritmo se encapsula en una clase separada, lo que mejora la cohesión y la mantenibilidad.
*   **Principio de abierto/cerrado:** Permite agregar nuevos algoritmos sin modificar el código existente.

**Desventajas:**

*   **Complejidad:** Puede aumentar la complejidad del diseño, especialmente si hay muchos algoritmos.
*   **Conocimiento de las estrategias:** El cliente debe conocer las diferentes estrategias disponibles para poder elegir la adecuada.

**Ejemplo (Algoritmos de Ordenamiento):**

Imagina que tienes una clase que necesita ordenar una lista de datos, pero quieres poder usar diferentes algoritmos de ordenamiento (por ejemplo, Bubble Sort, Quick Sort, Merge Sort).

*   **Strategy Interface:** `SortingStrategy` con el método `void sort(List<Integer> list)`.
*   **Concrete Strategies:**
    *   `BubbleSortStrategy`: Implementa el algoritmo Bubble Sort.
    *   `QuickSortStrategy`: Implementa el algoritmo Quick Sort.
    *   `MergeSortStrategy`: Implementa el algoritmo Merge Sort.
*   **Context:** `Sorter` con un atributo `SortingStrategy` y un método `sort(List<Integer> list)` que delega la ordenación al objeto `SortingStrategy`.

**Código de ejemplo (Java):**

```java
import java.util.ArrayList;
import java.util.List;

// Strategy Interface
interface SortingStrategy {
    void sort(List<Integer> list);
}

// Concrete Strategies
class BubbleSortStrategy implements SortingStrategy {
    @Override
    public void sort(List<Integer> list) {
        System.out.println("Sorting using Bubble Sort");
        // Implementación del algoritmo Bubble Sort
        int n = list.size();
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (list.get(j) > list.get(j + 1)) {
                    // swap list[j+1] and list[j]
                    int temp = list.get(j);
                    list.set(j, list.get(j + 1));
                    list.set(j + 1, temp);
                }
            }
        }
    }
}

class QuickSortStrategy implements SortingStrategy {
    @Override
    public void sort(List<Integer> list) {
        System.out.println("Sorting using Quick Sort");
        // Implementación del algoritmo Quick Sort (puedes usar Collections.sort para simplificar)
        list.sort(null); // Uses the natural ordering of Integers
    }
}

// Context
class Sorter {
    private SortingStrategy strategy;

    public Sorter(SortingStrategy strategy) {
        this.strategy = strategy;
    }

    public void setStrategy(SortingStrategy strategy) {
        this.strategy = strategy;
    }

    public void sort(List<Integer> list) {
        strategy.sort(list);
    }
}

// Ejemplo de uso
public class StrategyExample {
    public static void main(String[] args) {
        List<Integer> data = new ArrayList<>();
        data.add(5);
        data.add(1);
        data.add(4);
        data.add(2);
        data.add(8);

        // Usar Bubble Sort
        Sorter sorter = new Sorter(new BubbleSortStrategy());
        sorter.sort(data);
        System.out.println("Sorted data (Bubble Sort): " + data);

        // Cambiar a Quick Sort
        sorter.setStrategy(new QuickSortStrategy());
        data.clear(); // Reset the data
        data.add(5);
        data.add(1);
        data.add(4);
        data.add(2);
        data.add(8);
        sorter.sort(data);
        System.out.println("Sorted data (Quick Sort): " + data);
    }
}
```

**Explicación del código:**

1.  **`SortingStrategy` Interface:** Define el contrato para todos los algoritmos de ordenamiento.
2.  **`BubbleSortStrategy`, `QuickSortStrategy` Classes:** Implementan `SortingStrategy` para encapsular algoritmos de ordenamiento específicos.
3.  **`Sorter` Class:**  El Context.  Contiene una referencia a un objeto `SortingStrategy` y delega la ordenación a ese objeto.  Puede cambiar la estrategia en tiempo de ejecución usando el método `setStrategy()`.
4.  **`StrategyExample` Class:**  Crea una lista de datos y luego utiliza la clase `Sorter` con diferentes estrategias de ordenamiento para ordenar la lista.

**Cuándo usar el patrón Strategy:**

*   Cuando tienes muchos algoritmos relacionados y quieres que sean intercambiables.
*   Cuando quieres evitar el uso de múltiples sentencias condicionales (if-else o switch) para seleccionar el algoritmo.
*   Cuando quieres que los clientes puedan elegir el algoritmo que se va a utilizar.
*   Cuando quieres agregar nuevos algoritmos sin modificar el código existente.

