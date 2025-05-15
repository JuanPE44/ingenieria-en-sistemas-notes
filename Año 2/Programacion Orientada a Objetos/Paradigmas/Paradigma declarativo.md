El **paradigma de programación declarativo** representa un enfoque fundamentalmente diferente al imperativo. En lugar de describir *cómo* realizar una tarea mediante una secuencia detallada de pasos y cambios de estado, el paradigma declarativo se centra en **describir *qué* resultado se desea obtener** o **cuál es la lógica** del cómputo, sin especificar explícitamente el flujo de control para lograrlo.

Piensa en ello como **describir el destino** en lugar de dar las indicaciones paso a paso para llegar allí. Le dices a la computadora *qué* quieres, y el sistema (compilador, intérprete, motor de base de datos, etc.) se encarga de averiguar la mejor manera de *cómo* conseguirlo.

## Características Clave

1.  **Enfoque en el "Qué" (Resultado/Lógica):** El código expresa la lógica de la computación o las propiedades del resultado deseado, no la secuencia de operaciones para alcanzarlo.
2.  **Abstracción del Control de Flujo:** El programador no necesita especificar bucles, condicionales detallados o secuencias de ejecución. Estos detalles son manejados por la implementación subyacente del lenguaje o sistema.
3.  **Inmutabilidad y Ausencia de Efectos Secundarios (Frecuente):** Muchos enfoques declarativos, especialmente la programación funcional, tienden a evitar o minimizar el estado mutable (variables que cambian de valor) y los efectos secundarios (modificaciones fuera del ámbito local de una función). Esto hace que el código sea más fácil de razonar y menos propenso a errores.
4.  **Expresión de Lógica, Reglas o Transformaciones:** El código a menudo se parece más a una descripción matemática, lógica o a un conjunto de reglas y restricciones.

## Ejemplos Conceptuales

*   **SQL (Structured Query Language):**
    ```sql
    -- Declaras QUÉ datos quieres, no CÓMO obtenerlos (índices, bucles, etc.)
    SELECT nombre, apellido
    FROM empleados
    WHERE departamento = 'Ventas' AND salario > 50000;
    ```
    El motor de la base de datos decide la estrategia óptima (usar índices, escanear tablas) para ejecutar esta consulta.

*   **HTML (HyperText Markup Language):**
    ```html
    <!-- Declaras la ESTRUCTURA del contenido, no CÓMO dibujarlo pixel a pixel -->
    <h1>Título Principal</h1>
    <p>Este es un párrafo de texto.</p>
    <button>Haz clic aquí</button>
    ```
    El navegador interpreta esta estructura y la renderiza visualmente.

*   **CSS (Cascading Style Sheets):**
    ```css
    /* Declaras las REGLAS de estilo, no CÓMO aplicarlas al renderizar */
    h1 {
      color: blue;
      font-size: 24px;
    }
    p {
      line-height: 1.5;
    }
    ```
    El navegador aplica estas reglas a los elementos HTML correspondientes.

*   **Programación Funcional (Ejemplo conceptual):**
    ```java
    // Enfoque declarativo usando Streams en Java
    List<String> nombresMayusculas = personas
        .stream()
        .filter(p -> p.getEdad() > 18) // QUÉ filtrar (condición)
        .map(Persona::getNombre)       // QUÉ transformar (extraer nombre)
        .map(String::toUpperCase)      // QUÉ transformar (a mayúsculas)
        .collect(Collectors.toList()); // QUÉ recolectar (a una lista)
    ```
    Aquí describes la secuencia de transformaciones y filtros sobre los datos, no los bucles explícitos ni la creación de listas intermedias paso a paso.

## Sub-Paradigmas del Declarativo

El paradigma declarativo engloba varios sub-paradigmas importantes:

1.  **Programación Funcional:**
    *   Trata la computación como la evaluación de funciones matemáticas.
    *   Enfatiza funciones puras (mismo input, siempre mismo output, sin efectos secundarios), inmutabilidad, composición de funciones.
    *   Ejemplos: Haskell, Lisp, Clojure, F#, y características funcionales en lenguajes como Java (Streams), Python (list comprehensions, lambdas), JavaScript.

2.  **Programación Lógica:**
    *   Se basa en la lógica formal (predicados, reglas lógicas).
    *   El programa consiste en un conjunto de hechos y reglas. Se realizan consultas para deducir nueva información.
    *   Ejemplo principal: Prolog.

3.  **Lenguajes de Consulta de Bases de Datos:**
    *   Diseñados para recuperar y manipular datos almacenados en bases de datos.
    *   Ejemplos: SQL, Cypher (para bases de datos de grafos), LINQ (en .NET).

4.  **Lenguajes de Marcado y Hojas de Estilo:**
    *   Describen la estructura, presentación o configuración de datos.
    *   Ejemplos: HTML, XML, CSS, JSON (para estructura de datos), YAML.

5.  **Programación Reactiva (especialmente FRP - Functional Reactive Programming):**
    *   Modela flujos de datos asíncronos y cómo reaccionar a los cambios en esos flujos.
    *   Ejemplos: RxJava, RxJs, Project Reactor.

6.  **Sistemas de Gestión de Configuración / Infraestructura como Código:**
    *   Describen el estado deseado de un sistema o infraestructura.
    *   Ejemplos: Terraform, Ansible (en modo declarativo), Kubernetes manifests.

## Ventajas del Paradigma Declarativo

*   **Código más Conciso y Legible:** A menudo, el código es más corto y se acerca más a la descripción del problema o del dominio.
*   **Más Fácil de Razonar:** La ausencia (o minimización) de efectos secundarios y estado mutable simplifica el seguimiento del flujo y la comprensión del comportamiento.
*   **Mejor Mantenibilidad:** Al abstraer el "cómo", los cambios en la implementación subyacente (optimizaciones del motor) no requieren cambios en el código declarativo.
*   **Facilita la Paralelización:** La falta de estado mutable y efectos secundarios hace que sea intrínsecamente más seguro ejecutar partes del código en paralelo.
*   **Optimización:** Permite que el sistema subyacente elija la implementación más eficiente para el "cómo" (ej. optimizador de consultas SQL).

## Desventajas del Paradigma Declarativo

*   **Curva de Aprendizaje:** Pensar en términos de "qué" en lugar de "cómo" puede requerir un cambio de mentalidad para programadores acostumbrados al enfoque imperativo.
*   **Menor Control Explícito:** Puede ser más difícil controlar o depurar los detalles finos de la ejecución, ya que están abstraídos.
*   **Rendimiento (Potencialmente):** Aunque los sistemas subyacentes suelen estar muy optimizados, una abstracción mal entendida podría llevar a un rendimiento inesperado si no se comprende cómo se traduce el "qué" al "cómo".
*   **No Universalmente Aplicable:** Para tareas que requieren manipulación de bajo nivel o control muy preciso del hardware, un enfoque imperativo puede ser más directo.

## Conclusión

El paradigma declarativo ofrece una forma poderosa de escribir código centrándose en la lógica y el resultado deseado, delegando los detalles de la ejecución al sistema. Es especialmente fuerte en dominios como el manejo de datos, la descripción de interfaces, la lógica formal y la programación funcional. Muchos lenguajes y herramientas modernos incorporan elementos declarativos, a menudo en combinación con enfoques imperativos, para aprovechar las ventajas de ambos mundos.