En Java, la palabra clave `implements` se utiliza para que una **clase** indique que va a **implementar** una o más **interfaces**. Cuando una clase implementa una interfaz, se compromete a proporcionar una implementación concreta (cuerpo del método) para todos los métodos abstractos declarados en esa interfaz (o en cualquiera de sus super-interfaces).

Si una clase implementa una interfaz pero no proporciona la implementación para todos sus métodos abstractos, entonces esa clase debe ser declarada como `abstract`.

## Sintaxis

La sintaxis básica para usar `implements` es:

```java
[modificadores_de_acceso] class NombreDeLaClase [extends OtraClase] implements Interfaz1 [, Interfaz2, Interfaz3...] {
    // Cuerpo de la clase

    // Implementación de los métodos de Interfaz1
    @Override
    public tipoDeRetorno metodoDeInterfaz1(...) {
        // ... código de implementación ...
    }

    // Implementación de los métodos de Interfaz2 (si aplica)
    // ... y así sucesivamente ...
}
```

**Puntos clave de la sintaxis:**

1.  **`implements` después de `extends`**: Si una clase extiende otra clase (herencia) y también implementa interfaces, la cláusula `extends` debe ir antes de la cláusula `implements`.
    ```java
    class MiClase extends SuperClase implements MiInterfaz { ... }
    ```
2.  **Múltiples Interfaces**: Una clase puede implementar múltiples interfaces. Los nombres de las interfaces se separan por comas.
    ```java
    class MiClaseCompleja implements InterfazA, InterfazB, InterfazC { ... }
    ```
    Esto es una forma de lograr "herencia múltiple de tipo" en Java, ya que la clase `MiClaseCompleja` adquiere los tipos de `InterfazA`, `InterfazB` e `InterfazC`.
3.  **Obligación de Implementar**: La clase que implementa la interfaz *debe* proporcionar una implementación para todos los métodos abstractos definidos en la interfaz.
    *   La firma del método implementado (nombre, parámetros y tipo de retorno) debe coincidir con la firma del método en la interfaz.
    *   El método implementado en la clase debe ser declarado como `public`. Esto se debe a que todos los métodos abstractos en una interfaz son implícitamente `public`.
4.  **Anotación `@Override`**: Es una buena práctica usar la anotación `@Override` encima de los métodos que implementan métodos de una interfaz. Esto ayuda al compilador a verificar que realmente estás sobrescribiendo un método de la interfaz y no creando uno nuevo por error (por ejemplo, por un error tipográfico en el nombre del método).

## ¿Por qué usar `implements`?

Usar `implements` y, por lo tanto, interfaces, es fundamental para:

1.  **Definir un Contrato**: La interfaz define un "contrato" de lo que una clase puede hacer. Cualquier clase que implemente esa interfaz garantiza que proporcionará la funcionalidad especificada.
    *   Por ejemplo, la interfaz `List` en Java define métodos como `add()`, `get()`, `remove()`, etc. Clases como `ArrayList` y `LinkedList` implementan `List`, asegurando que ambas ofrecen estas operaciones, aunque su implementación interna sea diferente.

2.  **Lograr Abstracción**: Las interfaces permiten interactuar con objetos basándose en su tipo de interfaz, sin necesidad de conocer la clase concreta que los implementa. Esto oculta los detalles de implementación.
    ```java
    // Se puede usar el tipo de la interfaz para referenciar objetos de clases que la implementan
    List<String> miLista = new ArrayList<>();
    List<String> otraLista = new LinkedList<>();

    miLista.add("Hola");
    otraLista.add("Mundo");
    ```
    Aquí, tanto `miLista` como `otraLista` son tratadas como `List`, aunque sean instancias de clases diferentes.

3.  **Permitir Polimorfismo**: Un objeto puede ser tratado como una instancia de su propia clase o como una instancia de cualquiera de las interfaces que implementa. Esto permite escribir código más genérico y flexible.
    ```java
    public void procesarColeccion(List<Object> coleccion) {
        for (Object item : coleccion) {
            System.out.println(item);
        }
    }
    // Esta función puede recibir un ArrayList, un LinkedList, o cualquier otra implementación de List.
    ```

4.  **Facilitar el Desacoplamiento**: Las clases dependen de abstracciones (interfaces) en lugar de implementaciones concretas. Esto reduce las dependencias directas entre clases, haciendo el sistema más modular y fácil de modificar o extender. Si necesitas cambiar la implementación (por ejemplo, de `ArrayList` a `LinkedList`), el resto del código que usa la interfaz `List` no necesita cambiar.

## Ejemplo

Retomando el ejemplo de `Animal`:

```java
// Interfaz Animal
interface Animal {
    void hacerSonido(); // Método abstracto (implícitamente public abstract)
    void moverse();     // Método abstracto
}

// La clase Perro IMPLEMENTA la interfaz Animal
class Perro implements Animal {

    // Debe implementar hacerSonido()
    @Override
    public void hacerSonido() {
        System.out.println("Guau guau");
    }

    // Debe implementar moverse()
    @Override
    public void moverse() {
        System.out.println("El perro corre.");
    }
}

// La clase Gato IMPLEMENTA la interfaz Animal
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

public class DemoImplementacion {
    public static void main(String[] args) {
        // Creamos objetos de clases que implementan Animal
        Animal miPerro = new Perro(); // Perro IS-A Animal (Perro es un tipo de Animal)
        Animal miGato = new Gato();   // Gato IS-A Animal

        // Usamos los métodos definidos en la interfaz Animal
        miPerro.hacerSonido();
        miGato.moverse();
    }
}
```
En este ejemplo:
*   `Perro implements Animal` significa que la clase `Perro` se compromete a definir cómo un perro hace sonido y cómo se mueve.
*   `Gato implements Animal` significa que la clase `Gato` se compromete a definir cómo un gato hace sonido y cómo se mueve.

La palabra clave `implements` es, por lo tanto, el puente entre la definición abstracta de comportamiento (la interfaz) y su realización concreta (la clase).
```