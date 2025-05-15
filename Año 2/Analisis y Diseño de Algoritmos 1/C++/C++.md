## Origen y Relación con C

*   **C++** es el lenguaje utilizado en las cátedras de Análisis y Diseño de Algoritmos I y II.
*   Se basa en el lenguaje **C**, que es imperativo, procedural y de **bajo nivel**, orientado principalmente al desarrollo de software de sistemas (sistemas operativos, compiladores, etc.) debido a su cercanía con la arquitectura de la máquina, lo que permite optimizaciones detalladas.

## Características de C++

*   Desarrollado en 1979, C++ **extiende C** introduciendo soporte para:
    *   Abstracción de datos
    *   Programación Orientada a Objetos (POO)
    *   Programación Genérica
*   Se considera un lenguaje **multi-paradigma** (permite mezclar programación procedural y POO).
*   Añade características de **alto nivel** como:
    *   Clases
    *   Herencia múltiple
    *   Polimorfismo
    *   Sobrecarga de operadores
    *   Plantillas (Templates)
    *   Manejo de excepciones
*   Aunque C++ ofrece un **mayor nivel de abstracción** que C, mantiene las capacidades de bajo nivel de este último.
*   Es más adecuado que C para el desarrollo de **aplicaciones grandes** por su facilidad y rapidez de desarrollo.

## Compatibilidad y Estándares

*   C++ comparte gran parte de la **sintaxis de C**, y la mayoría de los programas C compilan en C++.
*   A pesar de la compatibilidad, C y C++ son **lenguajes independientes** con estándares propios que pueden diferir en algunos puntos. Conceptualmente, C++ puede verse como un **superconjunto de C**.
*   El estándar de C++ evoluciona con el tiempo (ej. actualizaciones en 2011, se esperaba otra en 2014).
*   Existen múltiples **compiladores**; se recomienda usar aquellos que se adhieran lo más posible al estándar oficial.

## Aprendizaje

*   La capacidad de C++ para usar tanto mecanismos de C como los suyos propios puede hacerlo **complejo de aprender y dominar**.
*   Esta guía introductoria se enfoca en los mecanismos más relevantes y no pretende cubrir todos los aspectos del lenguaje.




CLASS Arbin

BASIC CONSTRUCTORS:
  inicArbin, crearArbin

EFFECTIVE TYPE:
  Arbin

OPERATIONS:

  inicArbin: → Arbin                            / Constructor
  crearArbin: Arbin × Arbin × Elemento → Arbin / Constructor

  vacioArbin: Arbin → Boolean                  / Observador

  raiz: Arbin → Elemento                       / Observador
    pre: not vacioArbin(t)

  subIzquierdo: Arbin → Arbin                 / Observador
    pre: not vacioArbin(t)

  subDerecho: Arbin → Arbin                   / Observador
    pre: not vacioArbin(t)

  existeElemento: Arbin × Elemento → Boolean  / Observador

  altura: Arbin → Nat                         / Observador

  cantidadNodos: Arbin → Nat                  / Observador

  esHoja: Arbin → Boolean                     / Observador

  ==: Arbin × Arbin → Boolean               / Comparación estructural

AXIOMS:

  t1, t2, t3, t4: Arbin
  e, e1, e2: Elemento

  vacioArbin(inicArbin()) = true

  vacioArbin(crearArbin(t1, t2, e)) = false

  subIzquierdo(crearArbin(t1, t2, e)) = t1

  subDerecho(crearArbin(t1, t2, e)) = t2

  existeElemento(inicArbin(), e) = false

  existeElemento(crearArbin(t1, t2, e), e) = true

  e1 ≠ e ⇒
    existeElemento(crearArbin(t1, t2, e1), e) =
      existeElemento(t1, e) or existeElemento(t2, e)

  altura(inicArbin()) = 0

  altura(crearArbin(t1, t2, e)) =
    1 + max(altura(t1), altura(t2))

  cantidadNodos(inicArbin()) = 0

  cantidadNodos(crearArbin(t1, t2, e)) =
    1 + cantidadNodos(t1) + cantidadNodos(t2)

  esHoja(inicArbin()) = true

  esHoja(crearArbin(t1, t2, e)) =
    vacioArbin(t1) and vacioArbin(t2)

  inicArbin() == inicArbin() = true

  crearArbin(t1, t2, e1) == inicArbin() = false

  inicArbin() == crearArbin(t1, t2, e1) = false

  crearArbin(t1, t2, e1) == crearArbin(t3, t4, e2) =
    (e1 == e2) and (t1 == t3) and (t2 == t4)

END-CLASS