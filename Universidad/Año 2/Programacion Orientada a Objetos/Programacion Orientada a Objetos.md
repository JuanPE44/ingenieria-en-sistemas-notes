La Programación Orientada a Objetos (POO) es un **paradigma de programación** que utiliza "objetos" para diseñar aplicaciones y programas informáticos. Se basa en organizar el software en torno a datos u objetos, en lugar de funciones y lógica. Java es un lenguaje **intrínsecamente orientado a objetos**, lo que significa que sus características fundamentales están diseñadas para soportar y fomentar este paradigma.

El objetivo principal de la POO es modelar entidades del mundo real (o conceptos abstractos) como **objetos** de software, que tienen **estado** (datos/atributos) y **comportamiento** (métodos/funciones).

## Conceptos Fundamentales de la POO en Java

La POO se basa en cuatro pilares principales, además de los conceptos básicos de clases y objetos:

### 1. Clases y Objetos

*   **Clase (`class`):** Es una **plantilla** o **molde** que define las propiedades (atributos) y comportamientos (métodos) comunes a un cierto tipo de objetos. Es un tipo de dato definido por el usuario.
    ```java
    // Definición de una clase simple
    public class Coche {
        // Atributos (Estado)
        String color;
        String marca;
        int velocidadActual;

        // Métodos (Comportamiento)
        void acelerar(int incremento) {
            velocidadActual += incremento;
        }

        void frenar(int decremento) {
            velocidadActual -= decremento;
        }

        void mostrarEstado() {
            System.out.println("Coche [Marca=" + marca + ", Color=" + color + ", Velocidad=" + velocidadActual + "]");
        }
    }
    ```
*   **Objeto:** Es una **instancia** de una clase. Cuando creas un objeto, estás creando una entidad concreta basada en la plantilla definida por la clase. Cada objeto tiene su propio estado (valores específicos para sus atributos) pero comparte el comportamiento definido en la clase. Se crean usando el operador `new`.
    ```java
    // Creación de objetos (instancias) de la clase Coche
    Coche miCoche = new Coche();
    miCoche.marca = "Toyota";
    miCoche.color = "Rojo";
    miCoche.acelerar(50);
    miCoche.mostrarEstado(); // Muestra: Coche [Marca=Toyota, Color=Rojo, Velocidad=50]

    Coche otroCoche = new Coche();
    otroCoche.marca = "Ford";
    otroCoche.color = "Azul";
    otroCoche.acelerar(30);
    otroCoche.mostrarEstado(); // Muestra: Coche [Marca=Ford, Color=Azul, Velocidad=30]
    ```

### 2. Encapsulamiento

*   **Definición:** Es el mecanismo de **agrupar** los datos (atributos) y los métodos que operan sobre esos datos dentro de una única unidad (la clase). También implica **ocultar** el estado interno de un objeto (sus atributos) del mundo exterior y permitir el acceso o modificación solo a través de métodos públicos (getters y setters).
*   **Propósito:** Proteger la integridad de los datos, controlar el acceso, reducir la complejidad y mejorar la mantenibilidad.
*   **Implementación en Java:** Se logra mediante el uso de **modificadores de acceso** (`private`, `protected`, `public`, default/package-private) para los atributos y métodos. Los atributos suelen ser `private`, y se proporcionan métodos `public` (getters y setters) para acceder a ellos de forma controlada.
    ```java
    public class CuentaBancaria {
        private double saldo; // Atributo encapsulado (privado)
        private String titular;

        public CuentaBancaria(String titular, double saldoInicial) {
            this.titular = titular;
            if (saldoInicial >= 0) {
                this.saldo = saldoInicial;
            } else {
                this.saldo = 0;
            }
        }

        // Getter público para obtener el saldo (solo lectura controlada)
        public double getSaldo() {
            return saldo;
        }

        // Método público para depositar
        public void depositar(double cantidad) {
            if (cantidad > 0) {
                saldo += cantidad;
            }
        }

        // Método público para retirar (con validación)
        public boolean retirar(double cantidad) {
            if (cantidad > 0 && saldo >= cantidad) {
                saldo -= cantidad;
                return true;
            }
            return false;
        }
    }
    ```

### 3. Herencia

*   **Definición:** Es un mecanismo por el cual una clase (llamada **subclase** o clase hija) puede **heredar** atributos y métodos de otra clase (llamada **superclase** o clase padre). Establece una relación "ES-UN" (IS-A) entre las clases (ej. un `Perro` ES-UN `Animal`).
*   **Propósito:** Reutilización de código, creación de jerarquías de clases, extensibilidad.
*   **Implementación en Java:** Se usa la palabra clave `extends`. Java soporta herencia simple de clases (una clase solo puede extender de una superclase directa) pero permite herencia múltiple de interfaces (una clase puede implementar múltiples interfaces). La palabra clave `super` se usa para referirse a miembros de la superclase.
    ```java
    // Superclase
    class Animal {
        String nombre;

        public Animal(String nombre) { this.nombre = nombre; }

        public void comer() {
            System.out.println(nombre + " está comiendo.");
        }
    }

    // Subclase que hereda de Animal
    class Perro extends Animal {
        String raza;

        public Perro(String nombre, String raza) {
            super(nombre); // Llama al constructor de la superclase
            this.raza = raza;
        }

        public void ladrar() {
            System.out.println(nombre + " (raza " + raza + ") está ladrando: Guau!");
        }

        @Override // Sobrescribe el método comer (Polimorfismo)
        public void comer() {
            System.out.println("El perro " + nombre + " está comiendo su pienso.");
        }
    }

    // Uso
    Perro miPerro = new Perro("Fido", "Labrador");
    miPerro.comer(); // Llama a la versión de Perro
    miPerro.ladrar();
    ```

### 4. Polimorfismo

*   **Definición:** Significa "muchas formas". Es la capacidad de los objetos de diferentes clases (relacionadas por herencia o implementación de interfaces) de responder al mismo mensaje (llamada a método) de maneras diferentes y específicas a su tipo. Permite tratar objetos de subclases como si fueran objetos de la superclase.
*   **Propósito:** Flexibilidad, extensibilidad, desacoplamiento.
*   **Implementación en Java:**
    *   **Sobrescritura de Métodos (Method Overriding - Polimorfismo en tiempo de ejecución):** Una subclase proporciona una implementación específica para un método que ya está definido en su superclase. Se usa la anotación `@Override` (opcional pero recomendada).
    *   **Sobrecarga de Métodos (Method Overloading - Polimorfismo en tiempo de compilación):** Definir múltiples métodos con el mismo nombre pero con diferentes listas de parámetros (número, tipo o orden) dentro de la misma clase. No está directamente relacionado con la herencia.
    ```java
    // Ejemplo de Polimorfismo con sobrescritura
    Animal miAnimal = new Perro("Buddy", "Golden Retriever"); // Objeto Perro tratado como Animal
    miAnimal.comer(); // Se ejecuta el método comer() de la clase Perro en tiempo de ejecución

    Animal otroAnimal = new Animal("Gato Genérico");
    otroAnimal.comer(); // Se ejecuta el método comer() de la clase Animal

    // Ejemplo de Sobrecarga (en una clase hipotética Calculadora)
    class Calculadora {
        int sumar(int a, int b) { return a + b; }
        double sumar(double a, double b) { return a + b; } // Mismo nombre, diferente tipo de parámetro
        int sumar(int a, int b, int c) { return a + b + c; } // Mismo nombre, diferente número de parámetros
    }
    ```

### 5. Abstracción

*   **Definición:** Consiste en **ocultar los detalles complejos de implementación** y mostrar solo la funcionalidad esencial (la interfaz) de un objeto. Se enfoca en el *qué* hace un objeto, en lugar del *cómo* lo hace.
*   **Propósito:** Simplificar sistemas complejos, reducir el impacto de los cambios, mejorar la modularidad.
*   **Implementación en Java:**
    *   **Clases Abstractas (`abstract class`):** Clases que no pueden ser instanciadas directamente. Pueden contener métodos abstractos (sin implementación, declarados con `abstract`) que deben ser implementados por las subclases concretas, y también métodos concretos.
    *   **Interfaces (`interface`):** Definen un **contrato** de métodos que una clase debe implementar. Antes de Java 8, solo podían contener métodos abstractos y constantes (`public static final`). Desde Java 8, pueden incluir métodos `default` (con implementación) y `static`. Una clase puede implementar múltiples interfaces (`implements`).
    ```java
    // Interfaz (Contrato)
    interface Volador {
        void despegar(); // Método abstracto (implícitamente public abstract)
        void volar();
        void aterrizar();

        default void planear() { // Método default (Java 8+)
             System.out.println("Planeando suavemente...");
        }
    }

    // Clase abstracta
    abstract class Vehiculo {
        abstract void mover(); // Método abstracto

        void detener() { // Método concreto
            System.out.println("Vehículo detenido.");
        }
    }

    // Clase concreta que implementa la interfaz
    class Avion implements Volador {
        @Override public void despegar() { System.out.println("Avión despegando..."); }
        @Override public void volar() { System.out.println("Avión volando alto."); }
        @Override public void aterrizar() { System.out.println("Avión aterrizando."); }
    }

    // Clase concreta que extiende la clase abstracta
    class Bicicleta extends Vehiculo {
        @Override void mover() { System.out.println("Bicicleta pedaleando."); }
    }
    ```

## Beneficios de la POO en Java

*   **Modularidad:** El código fuente de un objeto puede escribirse y mantenerse independientemente del código fuente de otros objetos.
*   **Reutilización de Código:** La herencia permite reutilizar código de superclases.
*   **Extensibilidad:** Es fácil añadir nuevas funcionalidades o clases sin modificar extensivamente el código existente (usando herencia y polimorfismo).
*   **Mantenibilidad:** La encapsulación y la modularidad facilitan la corrección de errores y la actualización del software.
*   **Ocultación de Información / Seguridad:** La encapsulación protege los datos internos de accesos no deseados.
*   **Modelado del Mundo Real:** Facilita la representación de problemas y entidades complejas de forma más intuitiva.

## Conclusión

La Programación Orientada a Objetos es el paradigma central sobre el que se construye Java. Comprender y aplicar correctamente sus principios (Clases/Objetos, Encapsulamiento, Herencia, Polimorfismo y Abstracción) es fundamental para desarrollar aplicaciones Java robustas, escalables y fáciles de mantener.