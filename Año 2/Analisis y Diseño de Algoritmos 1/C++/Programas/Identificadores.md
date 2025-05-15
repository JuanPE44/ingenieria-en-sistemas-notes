Un **identificador** es el nombre que se utiliza para referenciar elementos dentro de un programa C++, tales como:

*   Constantes
*   Variables
*   Funciones

## Reglas de Nomenclatura

Para que un identificador sea válido en C++, debe seguir las siguientes reglas:

1.  **Carácter Inicial:** Debe comenzar obligatoriamente con:
    *   Una letra (mayúscula `A-Z` o minúscula `a-z`).
    *   Un guión bajo (`_`).
2.  **Caracteres Siguientes:** Después del primer carácter, el identificador puede contener:
    *   Letras (`A-Z`, `a-z`).
    *   Dígitos (`0-9`).
    *   Guión bajo (`_`).

*Nota: No se permiten espacios ni otros símbolos especiales (como `+`, `-`, `*`, `/`, `@`, etc.) dentro de un identificador.*

## Sensibilidad a Mayúsculas y Minúsculas (Case Sensitive)

Una característica fundamental de C++ es que **distingue entre letras mayúsculas y minúsculas** en los identificadores. Esto significa que:

*   `miVariable`
*   `mivariable`
*   `MiVariable`
*   `MIVARIABLE`

Son considerados **identificadores completamente distintos** por el compilador de C++.

Esta sensibilidad diferencia a C++ de otros lenguajes como Pascal o BASIC, donde no se hace distinción entre mayúsculas y minúsculas para los identificadores. Por ejemplo, en C++, `main`, `Main`, y `MAIN` son tres nombres diferentes, pero solo `main` (en minúsculas) es reconocido como la función principal del programa.
