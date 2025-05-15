El patrón de diseño Decorator es un patrón estructural que te permite añadir dinámicamente nuevas responsabilidades a un objeto existente sin modificar su estructura.  Proporciona una alternativa flexible a la herencia para extender la funcionalidad.  En lugar de crear subclases para añadir funcionalidad, envuelves el objeto original con uno o más "decoradores" que añaden la funcionalidad adicional.

**Propósito:**

*   Añadir responsabilidades a un objeto dinámicamente.
*   Evitar la proliferación de subclases.
*   Proporcionar una alternativa flexible a la herencia para extender la funcionalidad.

**Componentes:**

*   **Componente (Component):** Define la interfaz para los objetos a los que se les pueden añadir responsabilidades.  Puede ser una interfaz o una clase abstracta.
*   **Concrete Component:** Implementa la interfaz del Componente y define el objeto al que se le pueden añadir responsabilidades.
*   **Decorator:** Implementa la interfaz del Componente y mantiene una referencia a un objeto Componente.  Delega la solicitud al objeto Componente y puede añadir funcionalidad adicional antes o después de la delegación.
*   **Concrete Decorators:** Implementan la interfaz del Decorator y añaden responsabilidades específicas al objeto Componente.

**Ventajas:**

*   **Flexibilidad:** Permite añadir responsabilidades a un objeto dinámicamente, en tiempo de ejecución.
*   **Evita la proliferación de subclases:** En lugar de crear una subclase para cada combinación de responsabilidades, puedes usar decoradores para combinar responsabilidades de forma flexible.
*   **Principio de responsabilidad única:** Cada decorador tiene una sola responsabilidad, lo que mejora la cohesión y la mantenibilidad.
*   **Principio de abierto/cerrado:** Permite añadir nuevas responsabilidades sin modificar el código existente.

**Desventajas:**

*   **Complejidad:** Puede aumentar la complejidad del diseño, especialmente si hay muchos decoradores.
*   **Dificultad de configuración:** Puede ser difícil configurar la combinación correcta de decoradores.
*   **Identidad del objeto:**  Un objeto decorado no es idéntico al objeto original.  Si la identidad es importante, este patrón puede no ser adecuado.

**Ejemplo (Café con Adicionales):**

Imagina que estás modelando un sistema para pedir café.  Tienes un café base y quieres poder añadir diferentes adicionales, como leche, azúcar, chocolate, etc.

*   **Componente:** Una interfaz llamada `Coffee` con el método `String getDescription()` y `double getCost()`.
*   **Concrete Component:** Una clase `SimpleCoffee` que implementa `Coffee` y representa un café base.
*   **Decorator:** Una clase abstracta `CoffeeDecorator` que implementa `Coffee` y tiene una referencia a un objeto `Coffee`.
*   **Concrete Decorators:**
    *   `MilkDecorator`: Añade leche al café.
    *   `SugarDecorator`: Añade azúcar al café.
    *   `ChocolateDecorator`: Añade chocolate al café.

**Código de ejemplo (Java):**

```java
// Componente
interface Coffee {
    String getDescription();
    double getCost();
}

// Concrete Component
class SimpleCoffee implements Coffee {
    @Override
    public String getDescription() {
        return "Simple Coffee";
    }

    @Override
    public double getCost() {
        return 1.0;
    }
}

// Decorator
abstract class CoffeeDecorator implements Coffee {
    protected Coffee coffee;

    public CoffeeDecorator(Coffee coffee) {
        this.coffee = coffee;
    }

    @Override
    public String getDescription() {
        return coffee.getDescription();
    }

    @Override
    public double getCost() {
        return coffee.getCost();
    }
}

// Concrete Decorators
class MilkDecorator extends CoffeeDecorator {
    public MilkDecorator(Coffee coffee) {
        super(coffee);
    }

    @Override
    public String getDescription() {
        return super.getDescription() + ", with Milk";
    }

    @Override
    public double getCost() {
        return super.getCost() + 0.5;
    }
}

class SugarDecorator extends CoffeeDecorator {
    public SugarDecorator(Coffee coffee) {
        super(coffee);
    }

    @Override
    public String getDescription() {
        return super.getDescription() + ", with Sugar";
    }

    @Override
    public double getCost() {
        return super.getCost() + 0.2;
    }
}

// Ejemplo de uso
public class DecoratorExample {
    public static void main(String[] args) {
        Coffee coffee = new SimpleCoffee();
        System.out.println("Description: " + coffee.getDescription());
        System.out.println("Cost: " + coffee.getCost());

        Coffee milkCoffee = new MilkDecorator(coffee);
        System.out.println("Description: " + milkCoffee.getDescription());
        System.out.println("Cost: " + milkCoffee.getCost());

        Coffee sugarMilkCoffee = new SugarDecorator(milkCoffee);
        System.out.println("Description: " + sugarMilkCoffee.getDescription());
        System.out.println("Cost: " + sugarMilkCoffee.getCost());
    }
}
```

**Explicación del código:**

1.  **`Coffee` Interface:** Define los métodos comunes a todos los tipos de café.
2.  **`SimpleCoffee` Class:** Implementa `Coffee` para representar un café base.
3.  **`CoffeeDecorator` Class:** Implementa `Coffee` y tiene una referencia a un objeto `Coffee`.  Delega las llamadas a los métodos `getDescription()` y `getCost()` al objeto `Coffee` que decora.
4.  **`MilkDecorator`, `SugarDecorator` Classes:** Implementan `CoffeeDecorator` para añadir leche y azúcar al café, respectivamente.  Sobrescriben los métodos `getDescription()` y `getCost()` para añadir la descripción y el costo del adicional.
5.  **`DecoratorExample` Class:**  Crea un café base y luego lo decora con leche y azúcar.

**Cuándo usar el patrón Decorator:**

*   Cuando quieres añadir responsabilidades a un objeto dinámicamente.
*   Cuando quieres evitar la proliferación de subclases.
*   Cuando quieres poder combinar responsabilidades de forma flexible.
*   Cuando quieres que los objetos puedan tener responsabilidades que se pueden añadir y quitar en tiempo de ejecución.

