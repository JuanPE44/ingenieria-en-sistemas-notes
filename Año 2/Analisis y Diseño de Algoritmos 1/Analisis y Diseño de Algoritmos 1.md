## **Tareas pendientes**
- [ ] (3) Divide y consquista
- [ ] (4) Greedy
- [x] Recursion
- [ ] Resumenes

# **Parcial:** 05/06/2025

# **Recuperatorio:** 19/06/2025

# **Prefinal:** 04/07/2025


## Objetivo General

Proporcionar al alumno técnicas algorítmicas básicas que le permitan construir programas para resolver problemas de mediana escala, poniendo especial énfasis en criterios de corrección y eficiencia. Adquirir una metodología de construcción de algoritmos a partir de Tipos de Datos Abstractos (TDA) para la especificación, diseño e implementación de soluciones basadas en la elección de técnicas de diseño e implementaciones de TDA.

---

## UNIDAD 1. [[Analisis de eficiencia]]

### Contenidos
*   Definiciones básicas: algoritmos, eficiencia, complejidad temporal y complejidad espacial.
*   El rol del análisis de eficiencia en el desarrollo de programas.
*   Análisis asintótico de cotas de complejidad.
*   Las notaciones “big-O”, “big-Ω” y “big-Θ” para cotas asintóticas superior, inferior y exacta de la complejidad temporal y espacial de algoritmos.
*   Análisis de eficiencia de algoritmos iterativos.
*   Análisis de eficiencia de algoritmos recursivos mediante el uso de relaciones de recurrencia.
*   Análisis empírico de eficiencia de algoritmos versus análisis teórico.

### Objetivos de aprendizaje
Al finalizar el dictado de la Unidad 1 se espera que el alumno sea capaz de:
*   Comprender el uso de las notaciones “big-O”, “big-Ω” y “big-Θ” para evaluar algoritmos y usarlas para acotar en tiempo y espacio su complejidad.
*   Determinar la complejidad temporal y espacial de algoritmos iterativos.
*   Deducir relaciones de recurrencia que describan la complejidad temporal de algoritmos recursivos.
*   Resolver relaciones de recurrencia.

---

## UNIDAD 2. [[Tipos de Datos Abstractos (TDA)]] 

### Contenidos
*   **2.1. Introducción a TDA.**
    *   Especificación de TDA por contratos (precondiciones, postcondiciones e invariantes).
    *   Implementación de TDA en lenguajes orientados a objetos.
*   **2.2. TDA para estructuras de datos elementales:**
    *   Pilas, Filas, Listas, árboles binarios, colecciones.
*   **2.3. Diccionarios.**
    *   Operaciones de diccionarios y diccionarios ordenados.
    *   Implementaciones básicas: tablas y listas.
    *   Implementaciones avanzadas: tablas de dispersión, árboles binarios de búsqueda, árboles AVL.
*   **2.4. Colas con Prioridades.**
    *   Operaciones de colas con prioridades.
    *   Implementaciones con heaps.
*   **2.5. TDA Union-Find.**
    *   Implementación y aplicaciones.

### Objetivos de aprendizaje
Al finalizar el dictado de la Unidad 2 se espera que el alumno sea capaz de:
*   Poder abstraer las propiedades esenciales de los tipos de datos involucrados en un problema algorítmico e identificar cómo se relacionan en forma independientemente de una implementación en un lenguaje de programación.
*   Especificar tipos de datos abstractos básicos.
*   Elegir eficientes estructuras de datos para implementar tipos de datos.
*   Evaluar la eficiencia de algoritmos que involucren el uso de varios TDA.

---

## UNIDAD 3. [[Tecnicas de Diseños de Algoritmos]]

### Contenidos
*   **3.1. Divide y conquista.**
    *   Caracterización del tipo de problemas resolubles por divide y conquista.
    *   Esquema algorítmico.
    *   Problemas representativos: ordenamiento (Mergesort, Quicksort), multiplicación de matrices por el algoritmo de Strassen y algoritmo de Karatsuba para multiplicar números grandes.
*   **3.2. Greedy.**
    *   Caracterización del tipo de problema.
    *   Esquema algorítmico.
    *   Principio de optimalidad y función de selección.
    *   Problemas representativos: el problema de la mochila, minimización de tiempos de espera y planificación de tareas y heapsort.
*   **3.3. Programación dinámica.**
    *   Caracterización del tipo de problemas resolubles por programación dinámica.
    *   Principio de optimalidad.
    *   Formulación recursiva y memorización.
    *   Problemas representativos: multiplicación de secuencias de matrices, construcción de árboles binarios de mínimo costo, triangulación óptima de polígonos convexos y el problema de la subsecuencia más larga entre cadenas.

### Objetivos de aprendizaje
Al finalizar el dictado de la Unidad 3 se espera que el alumno sea capaz de:
*   Captar la esencia de las técnicas de diseño de algoritmos y poder identificar para cada una de ellas problemas que ejemplifiquen los conceptos subyacentes.
*   Implementar algoritmos basados en la técnica de diseño “Divide y Conquista”.
*   Implementar algoritmos basados en la técnica de diseño “Greedy”.
*   Implementar algoritmos basados en la técnica de diseño “Programación dinámica”.
*   Poder analizar críticamente cuál es la técnica de diseño adecuada para resolver un problema y adaptar esquemas algorítmicos para resolver problemas específicos.
*   Adquirir una metodología para la especificación, diseño e implementación de soluciones algorítmicas basada en la elección de técnicas de diseño e implementaciones de TDA.
*   Producir programas de tamaño medio, fiables y fáciles de entender, modificar, mantener y reutilizar a partir de una metodología de programación basada en TDA.

# indice C++
- Introduccion [[C++]]
- [[Programas]]
	  - [[Identificadores]]
	  - [[Bloques]]
- [[Tipos y Variables]]
	  -  [[Universidad/Año 2/Analisis y Diseño de Algoritmos 1/C++/Tipos y Variables/Declaracion]]
	  - [[Ambito de las variables (scope)]]
	  - [[Visibilidad y Ocultamiento de Variables (Shadowing)]]
	  - [[Tipos basicos C++]]
	  - [[Modificadores opcionales]]
	  - [[Secuencias de escape]]
	  - [[Constantes]]
	  - [[Tipos de datos compuestos]]
	    - [[Enumeraciones]]
	    - [[Registros]]
	    - [[Uniones]]
		- [[Arreglos]]
		    - [[Arreglos como parametros]]
- [[Operadores]]
- [[Estructuras de control]]
	  - Estructuras de selección
	    - Sentencia if
	    - Sentencia switch
	  - Estructuras de iteración
	    - Sentencia while
	    - Sentencia do-while
	    - Sentencia for
- Funciones
	  - Declaración
	  - Definición
	  - Pasaje de parámetros
	  - Sobrecarga de funciones
	  - Funciones recursivas
	  - Comparación entre iteración y recursión
	  - Argumentos de los programas
- Bibliotecas
	  - Directiva include
	  - Espacios de nombres
	  - Bibliotecas para las funciones más comunes
- Manejo de entrada/salida por consola
	  - Manejo de la consola en C++
	    - Salida por consola
	    - Entrada por consola
	      - Sincronización de la entrada
	      - Leer líneas completas
	    - Configuración del formato de la entrada y la salida
	  - Manejo de la consola en C
	    - Entrada por consola
- Manejo de cadenas
	  - Cadenas de C++
	  - Cadenas de C
	    - Inicialización de las cadenas de caracteres
	    - Operaciones de entrada/salida por consola
	    - Funciones para el manejo de cadenas
- Manejo de archivos
	  - Streams de archivos de C++
	    - Archivos de texto
	    - Archivos binarios
	  - Streams de archivos de C
	    - Archivos de texto
	    - Archivos binarios
- Punteros y manejo de memoria
	  - Operadores relacionados con punteros
	  - Operaciones para obtener y liberar memoria
	    - Operaciones para obtener memoria
	    - Operaciones para liberar memoria
	  - Consideraciones sobre la utilización de malloc y free
	  - Obteniendo bloques de memoria contigua
	  - Arreglos y punteros
	  - Arreglos como parámetros de funciones
	  - Arreglos dinámicos
	  - Aritmética de punteros
- Clases
	  - Definición de clases - Declaración de la interfaz
	  - Instanciación y uso
	  - Definición/Implementación de la interfaz
	  - Métodos consultores
	  - Constructores
	  - Destructor
	  - Sobrecarga de operadores
	    - Operador de salida de streams
	    - Operador de asignación
	  - La palabra reservada this
	  - Clases parametrizadas
	  - Herencia
	    - Creación de una clase derivada
	    - Constructores y destructores de las clases derivadas
	    - Redefinición de miembros en las clases derivadas
	    - Polimorfismo
	    - Métodos virtuales
	    - Clases abstractas



# [[Diseño de Software]]

