## Transformada Rápida de Fourier (FFT)

## ¿Qué es?
La Transformada Rápida de Fourier (FFT, por sus siglas en inglés) es un algoritmo eficiente para calcular la Transformada Discreta de Fourier (DFT) de una secuencia. La DFT descompone una secuencia de valores en componentes de diferentes frecuencias.

## ¿Cómo funciona?
1.  **Divide y Conquista:** La FFT aprovecha la simetría de los factores de fase (raíces de la unidad) para descomponer recursivamente la DFT de tamaño N en dos DFTs de tamaño N/2.
2.  **Mariposa (Butterfly):** El cálculo clave es la operación "mariposa", que combina los resultados de las DFTs más pequeñas para obtener los resultados de la DFT más grande. Esta operación se realiza de manera eficiente utilizando números complejos.
3.  **Recursión:** El proceso de división y combinación se repite hasta que se alcanzan DFTs de tamaño 1, que son triviales de calcular.
4.  **Bit-Reversal Permutation:** Antes de comenzar las etapas de cálculo, a menudo se realiza una permutación de los datos de entrada basada en la inversión de bits de los índices, para optimizar el acceso a la memoria.

## Pseudocódigo
```pseudo
FFT(a)  // a es un arreglo de N números complejos, donde N es una potencia de 2
  N = longitud(a)

  SI N == 1 ENTONCES
    RETORNAR a

  // Bit-Reversal Permutation (opcional, para optimización)
  a = PermutarPorInversionDeBits(a)

  // Dividir en partes pares e impares
  a_par = [a[0], a[2], ..., a[N-2]]
  a_impar = [a[1], a[3], ..., a[N-1]]

  // Calcular recursivamente las DFTs de las partes pares e impares
  y_par = FFT(a_par)
  y_impar = FFT(a_impar)

  // Combinar los resultados
  y = nuevo arreglo de tamaño N
  PARA k = 0 HASTA N/2 - 1
    w = exp(-j * 2 * pi * k / N)  // Factor de fase (raíz de la unidad)
    y[k] = y_par[k] + w * y_impar[k]
    y[k + N/2] = y_par[k] - w * y_impar[k]

  RETORNAR y
```

## Complejidad

*   Tiempo: `O(N log N)`, donde N es la longitud de la secuencia de entrada.
*   Espacio: `O(N)` para almacenar los resultados intermedios y finales.

## Ejemplo de uso

**Input:**
Secuencia: `[1, 2, 3, 4]`

**Output:**
Secuencia transformada (números complejos):
`[10+0j, -2+2j, -2+0j, -2-2j]`

(Los valores exactos dependen de la implementación y la normalización utilizada).

## Cuándo usarlo

*   **Procesamiento de señales:** Análisis de audio, imágenes y video para identificar componentes de frecuencia.
*   **Telecomunicaciones:** Modulación y demodulación de señales.
*   **Análisis de datos:** Identificación de patrones y tendencias en series temporales.
*   **Cálculo científico:** Resolución de ecuaciones diferenciales, convolución rápida.
