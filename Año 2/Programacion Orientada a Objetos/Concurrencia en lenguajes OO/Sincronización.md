**¿Qué es la Sincronización?**

La sincronización es el proceso de coordinar la ejecución de múltiples hilos para que accedan a los recursos compartidos de manera controlada y predecible. El objetivo principal de la sincronización es evitar que múltiples hilos modifiquen los mismos datos al mismo tiempo, lo que podría llevar a resultados incorrectos o inconsistentes.

**Mecanismos de Sincronización**

Existen varios mecanismos de sincronización disponibles en la mayoría de los lenguajes de programación con soporte para hilos. Algunos de los más comunes son:

1.  **Mutexes (Locks):**

    *   Un mutex (mutual exclusion) es un objeto que permite que solo un hilo acceda a una sección crítica de código a la vez.
    *   Cuando un hilo quiere acceder a una sección crítica, primero debe adquirir el mutex. Si el mutex ya está adquirido por otro hilo, el hilo que intenta adquirirlo se bloqueará hasta que el mutex sea liberado.
    *   Una vez que el hilo ha terminado de acceder a la sección crítica, debe liberar el mutex para que otros hilos puedan acceder a ella.
    *   En Java, puedes usar la palabra clave `synchronized` para crear un mutex implícito asociado a un objeto. También puedes usar la clase `ReentrantLock` para crear mutexes más flexibles.

    ```java
    clase RecursoCompartido {
        private int valor;
        private final Object lock = new Object(); // Mutex

        public void modificarValor(int nuevoValor) {
            synchronized (lock) { // Adquirir el lock
                // Sección crítica: solo un hilo puede ejecutar este código a la vez
                valor = nuevoValor;
                System.out.println("Valor modificado por " + Thread.currentThread().getName() + ": " + valor);
            } // Liberar el lock
        }

        public int obtenerValor() {
            synchronized (lock) {
                return valor;
            }
        }
    }
    ```

2.  **Semaforos:**

    *   Un semáforo es un objeto que controla el acceso a un recurso compartido, permitiendo que un número limitado de hilos accedan a él simultáneamente.
    *   Un semáforo mantiene un contador interno que representa el número de permisos disponibles.
    *   Cuando un hilo quiere acceder al recurso, debe adquirir un permiso del semáforo. Si el contador es mayor que cero, el hilo adquiere el permiso y el contador se decrementa. Si el contador es cero, el hilo se bloquea hasta que otro hilo libere un permiso.
    *   Cuando un hilo ha terminado de acceder al recurso, debe liberar un permiso para que otros hilos puedan acceder a él.
    *   Los semáforos se utilizan para controlar el acceso a recursos que tienen una capacidad limitada, como una piscina de conexiones de base de datos.

    ```java
    import java.util.concurrent.Semaphore;

    clase RecursoLimitado {
        private final Semaphore semaphore;

        public RecursoLimitado(int maxPermisos) {
            semaphore = new Semaphore(maxPermisos);
        }

        public void accederRecurso() throws InterruptedException {
            semaphore.acquire(); // Adquirir un permiso
            try {
                // Sección crítica: solo un número limitado de hilos puede ejecutar este código a la vez
                System.out.println("Recurso accedido por " + Thread.currentThread().getName());
                Thread.sleep(1000); // Simula el uso del recurso
            } finally {
                semaphore.release(); // Liberar el permiso
                System.out.println("Recurso liberado por " + Thread.currentThread().getName());
            }
        }
    }
    ```

3.  **Variables de Condición:**

    *   Las variables de condición se utilizan en combinación con los mutexes para permitir que los hilos esperen a que se cumpla una determinada condición antes de acceder a un recurso compartido.
    *   Un hilo que no puede acceder al recurso porque la condición no se cumple puede esperar en la variable de condición. Esto libera el mutex asociado al recurso, permitiendo que otros hilos accedan a él.
    *   Cuando otro hilo modifica el estado del recurso de manera que la condición se cumple, puede notificar a los hilos que están esperando en la variable de condición. Esto despierta a uno o a todos los hilos que están esperando, que luego intentan adquirir el mutex y acceder al recurso.
    *   En Java, las variables de condición se crean utilizando el método `newCondition()` de la clase `Lock`.

    ```java
    import java.util.concurrent.locks.Condition;
    import java.util.concurrent.locks.Lock;
    import java.util.concurrent.locks.ReentrantLock;

    clase Buffer {
        private int contenido;
        private boolean disponible = false;
        private final Lock lock = new ReentrantLock();
        private final Condition condicionProductor = lock.newCondition();
        private final Condition condicionConsumidor = lock.newCondition();

        public void poner(int valor) throws InterruptedException {
            lock.lock();
            try {
                while (disponible) {
                    condicionProductor.await(); // Esperar a que el buffer esté vacío
                }
                contenido = valor;
                disponible = true;
                System.out.println("Productor puso: " + valor);
                condicionConsumidor.signalAll(); // Notificar a los consumidores
            } finally {
                lock.unlock();
            }
        }

        public int obtener() throws InterruptedException {
            lock.lock();
            try {
                while (!disponible) {
                    condicionConsumidor.await(); // Esperar a que el buffer esté lleno
                }
                disponible = false;
                System.out.println("Consumidor obtuvo: " + contenido);
                condicionProductor.signalAll(); // Notificar a los productores
                return contenido;
            } finally {
                lock.unlock();
            }
        }
    }
    ```

4.  **Barreras:**

    *   Una barrera es un punto de sincronización en el que múltiples hilos deben esperar hasta que todos hayan alcanzado ese punto antes de continuar.
    *   Las barreras se utilizan para coordinar la ejecución de hilos que realizan tareas paralelas y necesitan sincronizarse en ciertos puntos.
    *   En Java, puedes usar la clase `CyclicBarrier` para crear barreras.

    ```java
    import java.util.concurrent.BrokenBarrierException;
    import java.util.concurrent.CyclicBarrier;

    clase TareaParalela implements Runnable {
        private final CyclicBarrier barrera;

        public TareaParalela(CyclicBarrier barrera) {
            this.barrera = barrera;
        }

        @Override
        public void run() {
            try {
                System.out.println(Thread.currentThread().getName() + " realizando tarea...");
                Thread.sleep(2000); // Simula trabajo
                System.out.println(Thread.currentThread().getName() + " esperando en la barrera...");
                barrera.await(); // Esperar a que todos los hilos lleguen a la barrera
                System.out.println(Thread.currentThread().getName() + " continuando después de la barrera...");
            } catch (InterruptedException | BrokenBarrierException e) {
                e.printStackTrace();
            }
        }
    }
    ```

**Problemas Comunes de Sincronización**

*   **Deadlock (Interbloqueo):** Un deadlock ocurre cuando dos o más hilos se bloquean mutuamente, esperando a que el otro libere un recurso.
*   **Starvation (Inanición):** La inanición ocurre cuando un hilo no puede acceder a los recursos que necesita para completar su tarea, debido a que otros hilos los están utilizando constantemente.
*   **Priority Inversion (Inversión de Prioridad):** La inversión de prioridad ocurre cuando un hilo de alta prioridad se bloquea esperando a que un hilo de baja prioridad libere un recurso.

