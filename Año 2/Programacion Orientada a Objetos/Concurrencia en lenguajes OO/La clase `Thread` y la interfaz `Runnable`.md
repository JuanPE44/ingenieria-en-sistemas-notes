
**La Clase `Thread`**

En Java, la clase `Thread` es la base para crear y controlar hilos. Representa un hilo de ejecución. Puedes crear un nuevo hilo de dos maneras principales utilizando la clase `Thread`:

1.  **Extender la clase `Thread`:**

    *   Creas una nueva clase que hereda de `Thread`.
    *   Sobreescribes el método `run()` de la clase `Thread`. Este método contiene el código que se ejecutará cuando el hilo se inicie.
    *   Creas una instancia de tu clase `Thread` y llamas al método `start()` para iniciar el hilo. El método `start()` crea un nuevo hilo de ejecución y llama al método `run()` en ese nuevo hilo.

    ```java
    class MiHilo extends Thread {
        @Override
        public void run() {
            // Código que se ejecutará en el hilo
            System.out.println("Hilo ejecutándose: " + Thread.currentThread().getName());
        }

        public static void main(String[] args) {
            MiHilo hilo = new MiHilo();
            hilo.start(); // Inicia el hilo
        }
    }
    ```

2.  **Implementar la interfaz `Runnable`:**

    *   Creas una clase que implementa la interfaz `Runnable`.
    *   Implementas el método `run()` de la interfaz `Runnable`. Este método contiene el código que se ejecutará cuando el hilo se inicie.
    *   Creas una instancia de tu clase `Runnable`.
    *   Creas una instancia de la clase `Thread`, pasando tu objeto `Runnable` al constructor de `Thread`.
    *   Llamas al método `start()` en el objeto `Thread` para iniciar el hilo.

    ```java
    class MiRunnable implements Runnable {
        @Override
        public void run() {
            // Código que se ejecutará en el hilo
            System.out.println("Hilo ejecutándose: " + Thread.currentThread().getName());
        }

        public static void main(String[] args) {
            MiRunnable runnable = new MiRunnable();
            Thread hilo = new Thread(runnable);
            hilo.start(); // Inicia el hilo
        }
    }
    ```

**La Interfaz `Runnable`**

La interfaz `Runnable` es una interfaz funcional que define un único método: `run()`. Su propósito es proporcionar una forma de definir el código que se ejecutará en un hilo sin necesidad de extender la clase `Thread`.

**¿Cuándo usar `Thread` vs. `Runnable`?**

*   **`Runnable` es preferible:** En general, es preferible implementar la interfaz `Runnable` en lugar de extender la clase `Thread`. Esto se debe a que Java no permite la herencia múltiple. Si extiendes la clase `Thread`, tu clase no podrá heredar de ninguna otra clase. Al implementar `Runnable`, tu clase puede heredar de otra clase si es necesario.
*   **`Thread` si necesitas modificar el comportamiento del hilo:** Si necesitas modificar el comportamiento de la clase `Thread` (por ejemplo, sobreescribir otros métodos además de `run()`), entonces extender la clase `Thread` puede ser apropiado. Sin embargo, esto es menos común.

**Métodos Importantes de la Clase `Thread`:**

*   `start()`: Inicia un nuevo hilo de ejecución y llama al método `run()` en ese nuevo hilo.
*   `run()`: Contiene el código que se ejecutará en el hilo.
*   `join()`: Espera a que el hilo termine su ejecución.
*   `sleep(long millis)`: Pausa la ejecución del hilo actual durante un número especificado de milisegundos.
*   `currentThread()`: Devuelve una referencia al hilo que se está ejecutando actualmente.
*   `getName()`: Devuelve el nombre del hilo.
*   `setName(String name)`: Establece el nombre del hilo.
*   `isAlive()`: Devuelve `true` si el hilo está vivo (es decir, ha sido iniciado y aún no ha terminado su ejecución).

**Ejemplo Combinado:**

```java
class MiTarea implements Runnable {
    private String nombre;

    public MiTarea(String nombre) {
        this.nombre = nombre;
    }

    @Override
    public void run() {
        System.out.println("Tarea " + nombre + " iniciada por el hilo: " + Thread.currentThread().getName());
        try {
            Thread.sleep(2000); // Simula un trabajo que lleva tiempo
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("Tarea " + nombre + " finalizada por el hilo: " + Thread.currentThread().getName());
    }

    public static void main(String[] args) {
        MiTarea tarea1 = new MiTarea("A");
        MiTarea tarea2 = new MiTarea("B");

        Thread hilo1 = new Thread(tarea1, "Hilo-1"); // Asigna un nombre al hilo
        Thread hilo2 = new Thread(tarea2, "Hilo-2");

        hilo1.start();
        hilo2.start();
    }
}
```

En este ejemplo:

*   `MiTarea` implementa `Runnable`, definiendo la tarea que cada hilo ejecutará.
*   Creamos dos instancias de `MiTarea`.
*   Creamos dos instancias de `Thread`, pasando cada tarea `Runnable` al constructor. También asignamos nombres a los hilos.
*   Iniciamos los hilos con `start()`.

