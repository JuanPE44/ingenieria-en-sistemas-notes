
**¿Qué son las Variables Compartidas?**

En un entorno multihilo, las variables compartidas son variables que pueden ser accedidas y modificadas por múltiples hilos concurrentemente. Estas variables pueden ser campos de un objeto, variables estáticas de una clase o incluso elementos de una colección.

**El Problema del Acceso Concurrente**

Cuando múltiples hilos acceden y modifican una variable compartida al mismo tiempo, pueden surgir problemas debido a la naturaleza no determinista de la ejecución concurrente. Esto se conoce como una **condición de carrera (race condition)**.

**Condiciones de Carrera (Race Conditions)**

Una condición de carrera ocurre cuando el resultado de una operación depende del orden preciso en que los hilos acceden y modifican la variable compartida. Si el orden de ejecución de los hilos no está controlado, el resultado puede ser impredecible e incorrecto.

**Ejemplo de Condición de Carrera**

Considera el siguiente ejemplo en pseudocódigo:

```
clase Contador {
    private int valor = 0;

    public void incrementar() {
        valor = valor + 1;
    }

    public int getValor() {
        return valor;
    }
}

// Dos hilos acceden al mismo objeto Contador
Contador contador = new Contador();

Hilo hilo1 = new Hilo(() -> {
    for (int i = 0; i < 1000; i++) {
        contador.incrementar();
    }
});

Hilo hilo2 = new Hilo(() -> {
    for (int i = 0; i < 1000; i++) {
        contador.incrementar();
    }
});

hilo1.start();
hilo2.start();

hilo1.join();
hilo2.join();

System.out.println("Valor final: " + contador.getValor()); // ¡Puede ser diferente de 2000!
```

En este ejemplo, dos hilos incrementan el valor de un contador compartido 1000 veces cada uno. Idealmente, el valor final debería ser 2000. Sin embargo, debido a la condición de carrera, el valor final puede ser menor que 2000.

**¿Por qué ocurre esto?**

La operación `valor = valor + 1` no es atómica. En realidad, se descompone en tres pasos:

1.  Leer el valor actual de `valor`.
2.  Sumar 1 al valor leído.
3.  Escribir el nuevo valor en `valor`.

Si dos hilos ejecutan estos pasos simultáneamente, puede ocurrir lo siguiente:

1.  Hilo 1 lee el valor de `valor` (por ejemplo, 10).
2.  Hilo 2 lee el valor de `valor` (también 10).
3.  Hilo 1 suma 1 al valor leído (10 + 1 = 11).
4.  Hilo 2 suma 1 al valor leído (10 + 1 = 11).
5.  Hilo 1 escribe el nuevo valor en `valor` (valor = 11).
6.  Hilo 2 escribe el nuevo valor en `valor` (valor = 11).

Como resultado, el contador se incrementó solo una vez en lugar de dos.

**Soluciones para el Acceso Concurrente**

Para evitar las condiciones de carrera y garantizar la integridad de los datos, es necesario sincronizar el acceso a las variables compartidas. Algunas de las técnicas más comunes son:

1.  **Mutexes (Locks):**

    *   Un mutex (mutual exclusion) es un objeto que permite que solo un hilo acceda a una sección crítica de código a la vez.
    *   En Java, puedes usar la palabra clave `synchronized` para crear un mutex implícito asociado a un objeto.
    *   También puedes usar la clase `ReentrantLock` para crear mutexes más flexibles.

    ```java
    clase Contador {
        private int valor = 0;
        private final Object lock = new Object(); // Mutex

        public void incrementar() {
            synchronized (lock) { // Adquirir el lock
                valor = valor + 1;
            } // Liberar el lock
        }

        public int getValor() {
            synchronized (lock) {
                return valor;
            }
        }
    }
    ```

2.  **Semaforos:**

    *   Un semáforo es un objeto que controla el acceso a un recurso compartido, permitiendo que un número limitado de hilos accedan a él simultáneamente.
    *   Los semáforos se utilizan para controlar el acceso a recursos que tienen una capacidad limitada.

3.  **Variables Atómicas:**

    *   Las variables atómicas son variables que proporcionan operaciones atómicas (indivisibles) para leer y modificar su valor.
    *   En Java, el paquete `java.util.concurrent.atomic` proporciona clases como `AtomicInteger`, `AtomicLong`, `AtomicBoolean`, etc.
    *   Estas clases utilizan instrucciones de hardware atómicas para garantizar que las operaciones sean atómicas y no estén sujetas a condiciones de carrera.

    ```java
    import java.util.concurrent.atomic.AtomicInteger;

    clase Contador {
        private AtomicInteger valor = new AtomicInteger(0);

        public void incrementar() {
            valor.incrementAndGet(); // Operación atómica
        }

        public int getValor() {
            return valor.get();
        }
    }
    ```

4.  **Colecciones Concurrentes:**

    *   El paquete `java.util.concurrent` proporciona colecciones concurrentes que están diseñadas para ser seguras para hilos.
    *   Estas colecciones utilizan mecanismos de sincronización internos para garantizar que las operaciones sean atómicas y no estén sujetas a condiciones de carrera.
    *   Ejemplos de colecciones concurrentes son `ConcurrentHashMap`, `ConcurrentLinkedQueue`, `CopyOnWriteArrayList`, etc.

**Visibilidad de Variables**

Además de la sincronización, es importante garantizar que los hilos tengan una vista consistente de las variables compartidas. Esto se conoce como **visibilidad**.

*   **La palabra clave `volatile`:**

    *   La palabra clave `volatile` se utiliza para indicar que una variable puede ser modificada por múltiples hilos.
    *   Cuando una variable se declara como `volatile`, el compilador y la JVM toman medidas para garantizar que todos los hilos vean el valor más reciente de la variable.
    *   En particular, la lectura de una variable `volatile` siempre se realiza directamente desde la memoria principal, y la escritura de una variable `volatile` siempre se realiza directamente en la memoria principal. Esto evita que los hilos utilicen copias en caché obsoletas de la variable.

**Ejemplo con `volatile`:**

```java
clase Tarea {
    private volatile boolean terminado = false;

    public void ejecutar() {
        // Hilo que realiza una tarea
        while (!terminado) {
            // Realizar trabajo
        }
    }

    public void detener() {
        terminado = true; // Otro hilo establece terminado a true
    }
}
```

En este ejemplo, si `terminado` no fuera `volatile`, el hilo que ejecuta `ejecutar()` podría no ver nunca el cambio realizado por el hilo que llama a `detener()`, lo que provocaría que el bucle `while` se ejecutara indefinidamente.

