---
sticker: lucide//alarm-check
---

Dado un sistema de $n$ ecuaciones lineales con $m$ incógnitas:
$$
\begin{cases}
a_{11}x_1 + a_{12}x_2 + \dots + a_{1m}x_m = b_1 \\
a_{21}x_1 + a_{22}x_2 + \dots + a_{2m}x_m = b_2 \\
\vdots \\
a_{n1}x_1 + a_{n2}x_2 + \dots + a_{nm}x_m = b_n
\end{cases}
$$
Este sistema puede escribirse en forma matricial como $A\vec{x} = \vec{b}$, donde $A$ es la matriz de coeficientes, $\vec{x}$ el vector de incógnitas y $\vec{b}$ el vector de términos independientes.

## Definición
La **matriz ampliada** (o aumentada) del sistema es una matriz que combina la matriz de coeficientes $A$ y el vector de términos independientes $\vec{b}$ en una sola estructura. Se forma añadiendo $\vec{b}$ como una última columna a la matriz $A$.

## Notación y Forma
Se denota comúnmente como $(A|\vec{b})$ o $[A|\vec{b}]$. Su forma general es:
$$ (A|\vec{b}) = \left( \begin{array}{cccc|c} a_{11} & a_{12} & \cdots & a_{1m} & b_1 \\ a_{21} & a_{22} & \cdots & a_{2m} & b_2 \\ \vdots & \vdots & \ddots & \vdots & \vdots \\ a_{n1} & a_{n2} & \cdots & a_{nm} & b_n \end{array} \right) $$
La línea vertical (opcional) separa la matriz de coeficientes $A$ del vector de términos independientes $\vec{b}$.

## Utilidad
*   Proporciona una **representación compacta** de todo el sistema de ecuaciones.
*   Es la herramienta principal para resolver sistemas lineales mediante **eliminación gaussiana** y **Gauss-Jordan**. Las operaciones por filas sobre $(A|\vec{b})$ equivalen a operaciones sobre las ecuaciones originales, simplificando el proceso de encontrar la solución.