---
sticker: lucide//alarm-clock
---
Existen varios métodos analíticos para encontrar la solución (o determinar que no existe) de un sistema de ecuaciones lineales. Dos métodos fundamentales son:

## Regla de Cramer
[[Regla de Cramer]]
#### Caracteristicas: 
*   **Aplicabilidad:** Este método se puede utilizar **únicamente** cuando el sistema tiene el **mismo número de ecuaciones que de incógnitas** ($n=m$). Esto implica que la matriz de coeficientes $A$ asociada al sistema es **cuadrada**. Además, requiere que el determinante de la matriz de coeficientes sea **distinto de cero** ($\det(A) \neq 0$), lo que garantiza que el sistema es Compatible Determinado (tiene solución única).
    *   **Método (Idea General):** Calcula la solución para cada incógnita $x_i$ mediante un cociente de determinantes. El denominador es siempre $\det(A)$, y el numerador es el determinante de una matriz obtenida al reemplazar la $i$-ésima columna de $A$ por el vector de términos independientes $\vec{b}$.
    *   **Ventaja:** Proporciona una fórmula explícita para cada incógnita.
    *   **Desventaja:** Solo aplicable a sistemas cuadrados con solución única. Computacionalmente costoso para sistemas grandes debido al cálculo de múltiples determinantes.


## Gauss-Jordan
[[Gauss-Jordan]]
#### Carcteristicas:
2.  **Eliminación de Gauss-Jordan (o Eliminación Gaussiana):**
    *   **Aplicabilidad:** Este método es **general** y se puede aplicar a **cualquier tipo de sistema de ecuaciones lineales**, sin importar si es cuadrado, rectangular, homogéneo, o si tiene solución única, infinitas soluciones o ninguna solución.
    *   **Método (Idea General):** Trabaja con la **matriz ampliada** $(A|\vec{b})$ del sistema. Mediante **operaciones elementales por filas** (intercambiar filas, multiplicar una fila por un escalar no nulo, sumar un múltiplo de una fila a otra), se transforma la matriz ampliada a una forma escalonada reducida por filas (Forma de Gauss-Jordan) o a una forma escalonada por filas (Forma Gaussiana).
    *   **Forma Escalonada Reducida (Gauss-Jordan):** La matriz resultante permite leer directamente la solución (si es única) o parametrizarla (si hay infinitas soluciones). Los pivotes son 1 y los demás elementos de las columnas pivote son 0.
    *   **Forma Escalonada (Gauss):** Requiere un paso adicional de sustitución hacia atrás para encontrar la solución.
    *   **Ventaja:** Método universal, aplicable a todos los SEL. Permite identificar fácilmente el tipo de sistema (SCD, SCI, SI) analizando el rango de la matriz de coeficientes y la matriz ampliada. Es el método más utilizado computacionalmente.
    *   **Desventaja:** El proceso manual puede ser más largo que Cramer para sistemas pequeños y cuadrados con solución única.

**En resumen:**
*   Si tienes un sistema cuadrado $n \times n$ y sabes que $\det(A) \neq 0$, puedes usar la **Regla de Cramer** para obtener fórmulas directas.
*   Para cualquier otro caso, o como método general y robusto, se utiliza la **Eliminación de Gauss-Jordan** (o Gaussiana) trabajando sobre la matriz ampliada.