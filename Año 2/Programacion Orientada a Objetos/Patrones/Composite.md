El patrón de diseño Composite en Java es un patrón estructural que te permite tratar objetos individuales y composiciones de objetos de manera uniforme.  La clave es que construyes una estructura de árbol donde cada nodo puede ser un objeto simple (una "hoja") o una composición de otros objetos (una "rama").  Esto permite a los clientes interactuar con la estructura completa como si fuera un solo objeto.

**Propósito:**

*   Representar jerarquías de objetos parte-todo.
*   Permitir que los clientes traten objetos individuales y composiciones de objetos de manera uniforme.

**Componentes:**

*   **Componente (Component):**  Define la interfaz común para objetos simples (hojas) y compuestos (contenedores).  Generalmente es una interfaz o una clase abstracta.  Puede definir métodos para acceder y gestionar los componentes hijos, así como operaciones comunes a todos los componentes.
*   **Hoja (Leaf):** Representa los objetos simples de la jerarquía. No tiene hijos. Implementa la interfaz del Componente.
*   **Compuesto (Composite):** Representa los contenedores de objetos. Puede contener objetos Hoja y otros objetos Compuesto. Implementa la interfaz del Componente y también proporciona métodos para agregar, eliminar y acceder a los componentes hijos.

**Ventajas:**

*   **Uniformidad:** Permite tratar objetos individuales y composiciones de objetos de manera uniforme, simplificando el código del cliente.  El cliente no necesita saber si está interactuando con una hoja o un compuesto.
*   **Extensibilidad:** Facilita la adición de nuevos tipos de componentes sin afectar el código existente.  Simplemente implementas la interfaz del Componente.
*   **Flexibilidad:** Permite construir estructuras complejas de objetos de forma jerárquica.

**Desventajas:**

*   **Complejidad:** Puede aumentar la complejidad del diseño, especialmente si la jerarquía es muy profunda.
*   **Restricciones:** A veces puede ser difícil restringir los tipos de componentes que pueden ser hijos de un compuesto.  Java no tiene una forma nativa de restringir esto a nivel de tipo, por lo que a menudo se requiere lógica de validación en tiempo de ejecución.

**Ejemplo (Sistema de Archivos):**

Un ejemplo clásico es modelar un sistema de archivos.  Tienes archivos individuales y directorios que pueden contener archivos y otros directorios.

*   **Componente:** Una interfaz llamada `FileSystemNode` con métodos como `getName()` y `getSize()`.
*   **Hoja:** Una clase `File` que implementa `FileSystemNode` y representa un archivo individual.
*   **Compuesto:** Una clase `Directory` que implementa `FileSystemNode` y puede contener objetos `File` y otros objetos `Directory`.

**Código de ejemplo (Java):**

```java
import java.util.ArrayList;
import java.util.List;

// Componente
interface FileSystemNode {
    String getName();
    int getSize();
    void print(); // Imprime la estructura
}

// Hoja
class File implements FileSystemNode {
    private String name;
    private int size;

    public File(String name, int size) {
        this.name = name;
        this.size = size;
    }

    @Override
    public String getName() {
        return name;
    }

    @Override
    public int getSize() {
        return size;
    }

    @Override
    public void print() {
        System.out.println("  Archivo: " + getName() + " (Tamaño: " + getSize() + " bytes)");
    }
}

// Compuesto
class Directory implements FileSystemNode {
    private String name;
    private List<FileSystemNode> children = new ArrayList<>();

    public Directory(String name) {
        this.name = name;
    }

    @Override
    public String getName() {
        return name;
    }

    @Override
    public int getSize() {
        int totalSize = 0;
        for (FileSystemNode child : children) {
            totalSize += child.getSize();
        }
        return totalSize;
    }

    public void add(FileSystemNode node) {
        children.add(node);
    }

    public void remove(FileSystemNode node) {
        children.remove(node);
    }

    @Override
    public void print() {
        System.out.println("Directorio: " + getName() + " (Tamaño total: " + getSize() + " bytes)");
        for (FileSystemNode child : children) {
            child.print(); // Llama recursivamente a print() para cada hijo
        }
    }
}

// Ejemplo de uso
public class CompositeExample {
    public static void main(String[] args) {
        Directory root = new Directory("Raiz");
        Directory documents = new Directory("Documentos");
        Directory pictures = new Directory("Imagenes");

        File file1 = new File("carta.txt", 100);
        File file2 = new File("informe.docx", 500);
        File image1 = new File("foto1.jpg", 200);
        File image2 = new File("foto2.png", 300);

        documents.add(file1);
        documents.add(file2);
        pictures.add(image1);
        pictures.add(image2);

        root.add(documents);
        root.add(pictures);

        root.print(); // Imprime la estructura completa
        System.out.println("Tamaño total de la raiz: " + root.getSize() + " bytes");
    }
}
```

**Explicación del código:**

1.  **`FileSystemNode` Interface:** Define los métodos comunes a todos los nodos del sistema de archivos.
2.  **`File` Class:** Implementa `FileSystemNode` para representar un archivo.
3.  **`Directory` Class:** Implementa `FileSystemNode` para representar un directorio.  Contiene una lista de `FileSystemNode` (sus hijos).  El método `getSize()` calcula recursivamente el tamaño total del directorio sumando el tamaño de todos sus hijos.  El método `print()` imprime el directorio y luego llama al método `print()` de cada uno de sus hijos, creando una salida jerárquica.
4.  **`CompositeExample` Class:**  Crea una estructura de sistema de archivos de ejemplo y luego llama al método `print()` del directorio raíz para imprimir la estructura completa.

**Cuándo usar el patrón Composite:**

*   Cuando necesitas representar una jerarquía de objetos parte-todo.
*   Cuando quieres que los clientes puedan tratar objetos individuales y composiciones de objetos de manera uniforme.
*   Cuando quieres poder agregar nuevos tipos de componentes sin afectar el código existente.

