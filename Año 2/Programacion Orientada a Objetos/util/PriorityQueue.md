La clase `java.util.PriorityQueue` es una implementación especializada de la interfaz `Queue` en Java. A diferencia de las colas estándar como `LinkedList` (que suelen seguir el orden FIFO - First-In, First-Out), `PriorityQueue` ordena sus elementos según su **prioridad**.

## ¿Qué es la Prioridad?

La "prioridad" se determina de dos maneras:

1.  **Orden Natural:** Si los objetos almacenados en la cola implementan la interfaz `Comparable`, se utiliza su método `compareTo` para establecer el orden. Por defecto, el elemento "menor" según `compareTo` tiene la mayor prioridad.
2.  **Comparador Personalizado:** Se puede proporcionar un objeto `Comparator` al constructor de `PriorityQueue`. Este comparador definirá explícitamente cómo se ordenan los elementos y, por lo tanto, cuál tiene mayor prioridad.

El elemento con la **mayor prioridad** siempre se encuentra en la "cabeza" de la cola (`head`).

## Implementación Interna

`PriorityQueue` generalmente se implementa utilizando una estructura de datos llamada **montículo binario (binary heap)**. Esto permite operaciones eficientes de inserción y extracción del elemento con mayor prioridad.

## Características Clave

*   **Ordenación por Prioridad:** Los elementos se recuperan según su prioridad, no necesariamente en el orden en que se insertaron.
*   **No Permite Nulos:** Intentar añadir `null` a una `PriorityQueue` lanzará una `NullPointerException`.
*   **No Sincronizada (Not Thread-Safe):** Si necesitas una cola de prioridad segura para subprocesos múltiples, considera usar `java.util.concurrent.PriorityBlockingQueue`.
*   **Capacidad Ilimitada (Unbounded):** Por defecto, la cola crece dinámicamente según sea necesario, aunque se puede especificar una capacidad inicial para optimizar.
*   **Iterador Débil:** El iterador (`iterator()`) proporcionado por `PriorityQueue` **no garantiza** recorrer los elementos en orden de prioridad. Si necesitas procesar los elementos en orden, debes extraerlos usando `poll()` o `remove()`.

## Métodos Principales

Hereda métodos de `Collection` y `Queue`, siendo los más relevantes:

*   `boolean add(E e)` / `boolean offer(E e)`: Añaden un elemento a la cola. `offer` es preferible en colas con capacidad restringida (aunque `PriorityQueue` es ilimitada por defecto). Ambas tienen una complejidad de **O(log n)**.
*   `E remove()` / `E poll()`: Recuperan y eliminan el elemento en la cabeza de la cola (el de mayor prioridad). `remove()` lanza una excepción si la cola está vacía, mientras que `poll()` devuelve `null`. Ambas tienen una complejidad de **O(log n)**.
*   `E element()` / `E peek()`: Recuperan, pero **no eliminan**, el elemento en la cabeza de la cola. `element()` lanza una excepción si la cola está vacía, mientras que `peek()` devuelve `null`. Ambas tienen una complejidad de **O(1)**.
*   `int size()`: Devuelve el número de elementos en la cola. **O(1)**.
*   `void clear()`: Elimina todos los elementos. **O(1)**.
*   `boolean contains(Object o)`: Comprueba si la cola contiene el elemento especificado. **O(n)**.
*   `Object[] toArray()` / `<T> T[] toArray(T[] a)`: Devuelven un array con los elementos de la cola, pero **sin garantía de orden** específico.

## Complejidad Temporal

*   **Inserción (`add`, `offer`):** O(log n)
*   **Eliminación (`remove`, `poll`):** O(log n)
*   **Consulta (`element`, `peek`):** O(1)
*   **Búsqueda (`contains`):** O(n)
*   **Eliminación arbitraria (`remove(Object)`):** O(n)

## Casos de Uso Comunes

*   **Planificación de Tareas:** Ejecutar tareas según su prioridad (ej. en sistemas operativos o simulaciones).
*   **Algoritmos de Grafos:**
    *   **Algoritmo de Dijkstra:** Para encontrar el camino más corto, se usa una cola de prioridad para seleccionar el siguiente nodo a visitar con la menor distancia acumulada.
    *   **Algoritmo de Prim:** Para encontrar el árbol de expansión mínima, se usa para seleccionar la siguiente arista de menor peso.
*   **Encontrar los K Elementos Mayores/Menores:** Mantener una cola de prioridad de tamaño K para rastrear eficientemente los elementos más grandes o pequeños de un flujo de datos.
*   **Fusión de Listas Ordenadas:** Combinar múltiples listas ordenadas en una sola lista ordenada.
*   **Simulación de Eventos Discretos:** Procesar eventos en orden cronológico.

## Ejemplos

### Ejemplo 1: Orden Natural (Enteros)

```java
import java.util.PriorityQueue;

public class PriorityQueueNaturalOrder {
    public static void main(String[] args) {
        // Por defecto, usa el orden natural (menor número = mayor prioridad)
        PriorityQueue<Integer> pq = new PriorityQueue<>();

        pq.offer(5);
        pq.offer(1);
        pq.offer(10);
        pq.offer(3);

        System.out.println("Cabeza de la cola (peek): " + pq.peek()); // Muestra 1

        System.out.println("Procesando elementos:");
        while (!pq.isEmpty()) {
            System.out.println(pq.poll()); // Imprime 1, 3, 5, 10
        }
    }
}
```

### Ejemplo 2: Comparador Personalizado (Strings por Longitud)

```java
import java.util.Comparator;
import java.util.PriorityQueue;

public class PriorityQueueCustomOrder {
    public static void main(String[] args) {
        // Comparador para dar mayor prioridad a los Strings más largos
        Comparator<String> stringLengthComparator = new Comparator<String>() {
            @Override
            public int compare(String s1, String s2) {
                // Invertimos el orden para que el más largo tenga mayor prioridad
                return Integer.compare(s2.length(), s1.length());
            }
        };

        PriorityQueue<String> pq = new PriorityQueue<>(stringLengthComparator);

        pq.offer("corto");
        pq.offer("muy largo");
        pq.offer("medio");
        pq.offer("a");

        System.out.println("Cabeza de la cola (peek): " + pq.peek()); // Muestra "muy largo"

        System.out.println("Procesando elementos:");
        while (!pq.isEmpty()) {
            System.out.println(pq.poll()); // Imprime "muy largo", "corto", "medio", "a"
        }
    }
}
```

## Conclusión

`PriorityQueue` es una herramienta poderosa y eficiente cuando necesitas procesar elementos basados en una prioridad específica en lugar del orden de llegada. Su implementación basada en montículos garantiza un buen rendimiento para las operaciones clave de inserción y extracción del elemento prioritario. Es fundamental entender cómo se define la prioridad (orden natural o comparador) y recordar que la iteración directa no sigue necesariamente el orden de prioridad.
```