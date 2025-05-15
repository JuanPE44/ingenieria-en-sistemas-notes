Un thread en Java (y en muchos otros lenguajes con soporte para hilos) pasa por varias etapas durante su vida. Estas etapas se pueden resumir en el siguiente ciclo de vida:

1.  **New (Nuevo):**

    *   Un hilo se encuentra en el estado "New" cuando se crea una instancia de la clase `Thread` (o una clase que implementa `Runnable` y se pasa a un `Thread`), pero aún no se ha llamado al método `start()`.
    *   En este estado, el hilo aún no está activo y no está ejecutando ningún código. Simplemente existe como un objeto en la memoria.

2.  **Runnable (Ejecutable):**

    *   Un hilo entra en el estado "Runnable" cuando se llama al método `start()` en el objeto `Thread`.
    *   El estado "Runnable" significa que el hilo está elegible para ser ejecutado por el planificador de hilos del sistema operativo. Sin embargo, estar en el estado "Runnable" no garantiza que el hilo se esté ejecutando activamente en ese momento.
    *   El planificador de hilos es responsable de asignar tiempo de CPU a los hilos "Runnable". La forma en que el planificador de hilos decide qué hilo ejecutar y cuándo depende del sistema operativo y de la prioridad asignada a los hilos.

3.  **Running (Ejecutándose):**

    *   Un hilo entra en el estado "Running" cuando el planificador de hilos le asigna tiempo de CPU y comienza a ejecutar su método `run()`.
    *   En este estado, el hilo está ejecutando activamente su código.
    *   Un hilo puede pasar del estado "Running" al estado "Runnable" si el planificador de hilos decide que otro hilo debe ejecutarse (por ejemplo, debido a la prioridad o a un tiempo de ejecución asignado).

4.  **Blocked/Waiting/Timed Waiting (Bloqueado/Esperando/Esperando con Tiempo):**

    *   Un hilo entra en uno de estos estados cuando está temporalmente inactivo y no es elegible para ser ejecutado por el planificador de hilos.
    *   **Blocked:** Un hilo entra en el estado "Blocked" cuando está esperando a adquirir un lock (mutex) para acceder a una sección crítica de código. Por ejemplo, si un hilo intenta entrar en un bloque `synchronized` que ya está bloqueado por otro hilo, el primer hilo se bloqueará hasta que el otro hilo libere el lock.
    *   **Waiting:** Un hilo entra en el estado "Waiting" cuando está esperando indefinidamente a que otro hilo realice una acción específica. Esto ocurre cuando un hilo llama a los métodos `wait()`, `join()` (sin un tiempo límite) o `park()` (de la clase `LockSupport`). El hilo permanecerá en este estado hasta que otro hilo llame a los métodos `notify()`, `notifyAll()` (en el mismo objeto en el que se llamó `wait()`), `unpark()` (de `LockSupport`) o el hilo sea interrumpido.
    *   **Timed Waiting:** Un hilo entra en el estado "Timed Waiting" cuando está esperando a que otro hilo realice una acción específica, pero con un tiempo límite. Esto ocurre cuando un hilo llama a los métodos `sleep()`, `wait()` (con un tiempo límite), `join()` (con un tiempo límite) o `parkNanos()`/`parkUntil()` (de la clase `LockSupport`). El hilo saldrá de este estado cuando expire el tiempo límite o cuando otro hilo realice la acción esperada (por ejemplo, llamar a `notify()`, `notifyAll()` o `unpark()`).

5.  **Terminated (Terminado):**

    *   Un hilo entra en el estado "Terminated" cuando ha completado la ejecución de su método `run()` o cuando se produce una excepción no controlada en el método `run()`.
    *   Una vez que un hilo está en el estado "Terminated", no puede volver a ejecutarse. El objeto `Thread` aún existe, pero el hilo de ejecución ha finalizado.

**Diagrama de Transición de Estados:**

Aquí tienes una representación visual simplificada del ciclo de vida de un thread:

```
[New] --> start() --> [Runnable] --> Planificador --> [Running]
    ^                                      |
    |                                      | Tiempo de CPU agotado,
    |                                      | prioridad más baja
    |                                      V
    |                                 [Runnable]
    |                                      |
    |    synchronized, wait(), join()       |
    | -----------------------------------> [Blocked/Waiting/Timed Waiting]
    |    notify(), notifyAll(), timeout      ^
    |                                      |
    |                                      |
    V                                      |
[Terminated] <------------------------------
     run() completa o excepción no controlada
```

**Ejemplo en Código:**

```java
class MiHilo extends Thread {
    @Override
    public void run() {
        System.out.println("Hilo " + getName() + " en estado Running");
        try {
            Thread.sleep(1000); // Hilo en estado Timed Waiting
        } catch (InterruptedException e) {
            System.out.println("Hilo " + getName() + " interrumpido");
        }
        System.out.println("Hilo " + getName() + " finalizando");
    }

    public static void main(String[] args) throws InterruptedException {
        MiHilo hilo = new MiHilo(); // Hilo en estado New
        hilo.setName("MiHilo-1");
        System.out.println("Hilo " + hilo.getName() + " creado");

        hilo.start(); // Hilo en estado Runnable

        hilo.join(); // Esperar a que el hilo termine

        System.out.println("Hilo " + hilo.getName() + " terminado"); // Hilo en estado Terminated
    }
}
```

