En Java, una **interfaz** es un tipo de referencia, similar a una clase, que puede contener solo constantes, firmas de métodos (métodos abstractos), métodos default, métodos estáticos y tipos anidados. Los cuerpos de los métodos solo existen para los métodos default y estáticos.

Las interfaces no se pueden instanciar directamente. En su lugar, son implementadas por clases o extendidas por otras interfaces.

## ¿Para qué sirven las interfaces?

Las interfaces se utilizan para lograr:

1.  **Abstracción:** Ocultan los detalles de implementación y solo muestran la funcionalidad al usuario.
2.  **Herencia múltiple (de tipo):** Java no permite la herencia múltiple de clases, pero una clase puede implementar múltiples interfaces. Esto permite que un objeto adquiera múltiples "tipos".
3.  **Polimorfismo:** Permiten que un objeto tome muchas formas. Una variable de tipo interfaz puede referenciar a cualquier objeto de una clase que implemente esa interfaz.
4.  **Contratos:** Definen un contrato que las clases que la implementan deben seguir. Si una clase implementa una interfaz, se compromete a implementar todos sus métodos abstractos.
5.  **Desacoplamiento:** Ayudan a desacoplar los componentes del sistema, ya que las clases interactúan a través de interfaces en lugar de implementaciones concretas.

## Declaración de una Interfaz

Se utiliza la palabra clave `interface` para declarar una interfaz.

```java
public interface MiInterfaz {
    // Constantes (implícitamente public, static y final)
    int CONSTANTE_VALOR = 100;

    // Métodos abstractos (implícitamente public y abstract)
    void metodoAbstracto1();
    String metodoAbstracto2(int parametro);

    // Métodos default (a partir de Java 8)
    default void metodoDefault() {
        System.out.println("Este es un método default en la interfaz.");
        metodoPrivado(); // Puede llamar a métodos privados de la interfaz
    }

    // Métodos estáticos (a partir de Java 8)
    static void metodoEstatico() {
        System.out.println("Este es un método estático en la interfaz.");
    }

    // Métodos privados (a partir de Java 9, para ayudar a los métodos default y estáticos)
    private void metodoPrivado() {
        System.out.println("Este es un método privado en la interfaz.");
    }
}
```

**Puntos clave sobre la declaración:**

*   Todos los campos en una interfaz son implícitamente `public`, `static` y `final` (constantes). No es necesario declararlos explícitamente con estos modificadores.
*   Todos los métodos abstractos en una interfaz son implícitamente `public` y `abstract`.
*   Los métodos `default` permiten añadir nueva funcionalidad a las interfaces sin romper las clases que ya las implementan. Tienen un cuerpo.
*   Los métodos `static` en interfaces son similares a los métodos estáticos en clases. Se llaman usando el nombre de la interfaz (ej: `MiInterfaz.metodoEstatico();`).
*   Los métodos `private` (desde Java 9) solo pueden ser usados dentro de la propia interfaz, usualmente para ayudar a los métodos `default` o `static` a evitar la duplicación de código.

## Implementación de una Interfaz

Una clase utiliza la palabra clave `implements` para implementar una interfaz. La clase debe proporcionar una implementación concreta para todos los métodos abstractos declarados en la interfaz (o ser declarada abstracta ella misma).

```java
public class MiClase implements MiInterfaz {

    @Override
    public void metodoAbstracto1() {
        System.out.println("Implementación de metodoAbstracto1 en MiClase.");
    }

    @Override
    public String metodoAbstracto2(int parametro) {
        return "Implementación de metodoAbstracto2 en MiClase con parámetro: " + parametro;
    }

    // Opcionalmente, se puede sobrescribir un método default
    @Override
    public void metodoDefault() {
        System.out.println("Sobrescritura del método default en MiClase.");
    }

    public static void main(String[] args) {
        MiClase objeto = new MiClase();
        objeto.metodoAbstracto1();
        System.out.println(objeto.metodoAbstracto2(50));
        objeto.metodoDefault();

        // Acceder a la constante de la interfaz
        System.out.println("Constante de la interfaz: " + MiInterfaz.CONSTANTE_VALOR);

        // Llamar al método estático de la interfaz
        MiInterfaz.metodoEstatico();

        // Polimorfismo
        MiInterfaz interfazRef = new MiClase();
        interfazRef.metodoAbstracto1();
        // interfazRef.metodoDefault(); // También se puede llamar
    }
}
```

**Puntos clave sobre la implementación:**

*   Una clase puede implementar múltiples interfaces separándolas por comas: `class MiClase implements Interfaz1, Interfaz2 { ... }`.
*   Si una clase implementa una interfaz pero no proporciona implementación para todos sus métodos abstractos, la clase debe ser declarada `abstract`.
*   Al sobrescribir un método de una interfaz, el método en la clase implementadora debe ser `public`.

## Ejemplo Sencillo: Animales

```java
// Interfaz Animal
interface Animal {
    void hacerSonido();
    void moverse();
}

// Clase Perro implementa Animal
class Perro implements Animal {
    @Override
    public void hacerSonido() {
        System.out.println("Guau guau");
    }

    @Override
    public void moverse() {
        System.out.println("El perro corre.");
    }
}

// Clase Gato implementa Animal
class Gato implements Animal {
    @Override
    public void hacerSonido() {
        System.out.println("Miau miau");
    }

    @Override
    public void moverse() {
        System.out.println("El gato camina sigilosamente.");
    }
}

public class DemoAnimales {
    public static void main(String[] args) {
        Animal miPerro = new Perro();
        Animal miGato = new Gato();

        miPerro.hacerSonido(); // Salida: Guau guau
        miPerro.moverse();    // Salida: El perro corre.

        miGato.hacerSonido();  // Salida: Miau miau
        miGato.moverse();     // Salida: El gato camina sigilosamente.
    }
}
```
En este ejemplo, la interfaz `Animal` define un contrato para lo que cualquier animal debería poder hacer (`hacerSonido` y `moverse`). Las clases `Perro` y `Gato` implementan esta interfaz, proporcionando sus propias versiones específicas de estos comportamientos.

## Interfaces Funcionales (Java 8+)

Una interfaz funcional es una interfaz que contiene exactamente un método abstracto. Son la base de las expresiones lambda en Java. La anotación `@FunctionalInterface` es opcional pero recomendable para que el compilador verifique que la interfaz cumple con los requisitos.

```java
@FunctionalInterface
interface Calculadora {
    int operar(int a, int b);
    // No puede tener otro método abstracto
    // Puede tener métodos default o static
    default void mostrarInfo() {
        System.out.println("Interfaz Calculadora Funcional");
    }
}

public class DemoFuncional {
    public static void main(String[] args) {
        // Usando una expresión lambda para implementar la interfaz funcional
        Calculadora suma = (a, b) -> a + b;
        Calculadora resta = (a, b) -> a - b;

        System.out.println("Suma: " + suma.operar(10, 5));   // Salida: Suma: 15
        System.out.println("Resta: " + resta.operar(10, 5)); // Salida: Resta: 5
        suma.mostrarInfo(); // Llama al método default
    }
}
```

## Resumen

Las interfaces son una herramienta fundamental en Java para definir contratos, lograr abstracción y permitir una forma de herencia múltiple de tipos. Facilitan la creación de código flexible, modular y fácil de mantener.
```