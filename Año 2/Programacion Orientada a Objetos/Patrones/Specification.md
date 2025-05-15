El patrón de diseño Specification en Java es un patrón de diseño de comportamiento que te permite encapsular reglas de negocio en objetos separados, llamados "Specifications". Estas Specifications pueden combinarse para crear reglas más complejas, y luego usarse para filtrar, validar o seleccionar objetos. En esencia, separa la lógica de selección de objetos de la propia clase de objeto.

**Propósito:**

*   Encapsular reglas de negocio en objetos reutilizables.
*   Combinar reglas de negocio para crear reglas más complejas.
*   Separar la lógica de selección de objetos de la propia clase de objeto.
*   Promover la reutilización y la mantenibilidad del código.

**Componentes:**

*   **Specification Interface:** Define el contrato para todas las Specifications.  Generalmente tiene un método `isSatisfiedBy(T candidate)` que devuelve `true` si el objeto candidato cumple con la regla encapsulada por la Specification, y `false` en caso contrario.
*   **Concrete Specifications:** Implementan la Specification Interface y encapsulan una regla de negocio específica.
*   **Composite Specifications (opcional):**  Implementan la Specification Interface y combinan otras Specifications usando operadores lógicos como AND, OR y NOT.  Esto permite crear reglas más complejas a partir de reglas más simples.
*   **Client:** Utiliza las Specifications para filtrar, validar o seleccionar objetos.

**Ventajas:**

*   **Separación de responsabilidades:** La lógica de selección de objetos se separa de la propia clase de objeto, lo que mejora la cohesión y la mantenibilidad.
*   **Reutilización:** Las Specifications pueden reutilizarse en diferentes partes de la aplicación.
*   **Combinación:** Las Specifications pueden combinarse para crear reglas más complejas.
*   **Facilidad de prueba:** Las Specifications son fáciles de probar porque encapsulan una sola regla de negocio.
*   **Flexibilidad:** Permite cambiar las reglas de negocio sin modificar el código existente.

**Desventajas:**

*   **Complejidad:** Puede aumentar la complejidad del diseño, especialmente si hay muchas reglas de negocio.
*   **Rendimiento:** La combinación de muchas Specifications puede afectar el rendimiento, especialmente si se utilizan para filtrar grandes colecciones de objetos.

**Ejemplo (Filtrar Productos):**

Imagina que tienes una lista de productos y quieres filtrarlos según diferentes criterios, como precio, categoría y disponibilidad.

*   **Specification Interface:** `ProductSpecification` con el método `boolean isSatisfiedBy(Product product)`.
*   **Concrete Specifications:**
    *   `PriceSpecification`:  Filtra productos por precio.
    *   `CategorySpecification`: Filtra productos por categoría.
    *   `AvailabilitySpecification`: Filtra productos por disponibilidad.
*   **Composite Specifications:**
    *   `AndProductSpecification`: Combina dos `ProductSpecification` con un operador AND.
    *   `OrProductSpecification`: Combina dos `ProductSpecification` con un operador OR.

**Código de ejemplo (Java):**

```java
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;

// Clase Producto
class Product {
    private String name;
    private double price;
    private String category;
    private boolean available;

    public Product(String name, double price, String category, boolean available) {
        this.name = name;
        this.price = price;
        this.category = category;
        this.available = available;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }

    public String getCategory() {
        return category;
    }

    public boolean isAvailable() {
        return available;
    }

    @Override
    public String toString() {
        return "Product{" +
                "name='" + name + '\'' +
                ", price=" + price +
                ", category='" + category + '\'' +
                ", available=" + available +
                '}';
    }
}

// Specification Interface
interface ProductSpecification {
    boolean isSatisfiedBy(Product product);
}

// Concrete Specifications
class PriceSpecification implements ProductSpecification {
    private double maxPrice;

    public PriceSpecification(double maxPrice) {
        this.maxPrice = maxPrice;
    }

    @Override
    public boolean isSatisfiedBy(Product product) {
        return product.getPrice() <= maxPrice;
    }
}

class CategorySpecification implements ProductSpecification {
    private String category;

    public CategorySpecification(String category) {
        this.category = category;
    }

    @Override
    public boolean isSatisfiedBy(Product product) {
        return product.getCategory().equals(category);
    }
}

class AvailabilitySpecification implements ProductSpecification {
    @Override
    public boolean isSatisfiedBy(Product product) {
        return product.isAvailable();
    }
}

// Composite Specifications
class AndProductSpecification implements ProductSpecification {
    private ProductSpecification spec1;
    private ProductSpecification spec2;

    public AndProductSpecification(ProductSpecification spec1, ProductSpecification spec2) {
        this.spec1 = spec1;
        this.spec2 = spec2;
    }

    @Override
    public boolean isSatisfiedBy(Product product) {
        return spec1.isSatisfiedBy(product) && spec2.isSatisfiedBy(product);
    }
}

// Client
public class SpecificationExample {
    public static void main(String[] args) {
        List<Product> products = new ArrayList<>();
        products.add(new Product("Laptop", 1200.0, "Electronics", true));
        products.add(new Product("Mouse", 25.0, "Electronics", true));
        products.add(new Product("Keyboard", 75.0, "Electronics", false));
        products.add(new Product("Book", 20.0, "Books", true));
        products.add(new Product("Pen", 2.0, "Stationery", true));

        // Filtrar productos electrónicos con un precio máximo de 100
        ProductSpecification electronicsSpec = new CategorySpecification("Electronics");
        ProductSpecification maxPriceSpec = new PriceSpecification(100.0);
        ProductSpecification combinedSpec = new AndProductSpecification(electronicsSpec, maxPriceSpec);

        List<Product> filteredProducts = products.stream()
                .filter(combinedSpec::isSatisfiedBy)
                .collect(Collectors.toList());

        System.out.println("Filtered Products:");
        filteredProducts.forEach(System.out::println);

        // Filtrar productos disponibles
        ProductSpecification availableSpec = new AvailabilitySpecification();
        List<Product> availableProducts = products.stream()
                .filter(availableSpec::isSatisfiedBy)
                .collect(Collectors.toList());

        System.out.println("\nAvailable Products:");
        availableProducts.forEach(System.out::println);
    }
}
```

**Explicación del código:**

1.  **`Product` Class:** Representa un producto con sus atributos.
2.  **`ProductSpecification` Interface:** Define el contrato para todas las Specifications de productos.
3.  **`PriceSpecification`, `CategorySpecification`, `AvailabilitySpecification` Classes:** Implementan `ProductSpecification` para encapsular reglas de negocio específicas.
4.  **`AndProductSpecification` Class:** Implementa `ProductSpecification` para combinar dos Specifications con un operador AND.
5.  **`SpecificationExample` Class:**  Crea una lista de productos y luego utiliza las Specifications para filtrar la lista.

**Cuándo usar el patrón Specification:**

*   Cuando tienes muchas reglas de negocio que cambian con frecuencia.
*   Cuando quieres reutilizar reglas de negocio en diferentes partes de la aplicación.
*   Cuando quieres combinar reglas de negocio para crear reglas más complejas.
*   Cuando quieres separar la lógica de selección de objetos de la propia clase de objeto.
*   Cuando quieres facilitar la prueba de las reglas de negocio.

