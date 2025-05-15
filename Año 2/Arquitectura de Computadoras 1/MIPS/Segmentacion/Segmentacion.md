**¿Qué es la Segmentación (Pipelining)?**

La segmentación es una técnica de optimización que divide un proceso en etapas secuenciales. Cada etapa se ejecuta en un recurso independiente, permitiendo que múltiples procesos se ejecuten simultáneamente en diferentes etapas.

*Analogía:* Imagina una línea de ensamblaje, como el proceso de lavado de ropa.

**Ejemplo: Proceso de Lavado de Ropa**

*   Tarea 1: Lavar (½ hora)
*   Tarea 2: Secar (½ hora)
*   Tarea 3: Doblar (½ hora)
*   Tarea 4: Guardar (½ hora)

Tiempo total por proceso completo (sin segmentar): 2 horas.

**Funcionamiento: Secuencial vs. Segmentado**

*   **Funcionamiento Secuencial:** Cada proceso se completa antes de comenzar el siguiente.

    *   Tiempo para M procesos ($TP(M)$): $TP(M) = TP(1) \cdot M$
        *   $TP(1)$: Tiempo para completar un proceso (ej: 2 horas para el lavado).
        *   Ejemplo: 4 procesos de lavado tardan $TP(4) = 2 \text{ hs} \cdot 4 = 8 \text{ hs}$.

*   **Funcionamiento Segmentado:** Las etapas de diferentes procesos se ejecutan en paralelo.

    *   El primer proceso tarda el tiempo completo en salir ($TS(1) = TP(1)$).
    *   Los siguientes procesos salen al ritmo de la etapa más larga ($T_{ETAPA}$).
    *   Tiempo para M procesos ($TS(M)$): $TS(M) = TS(1) + (M-1) \cdot T_{ETAPA}$
        *   $TS(1)$: Latencia del pipeline (tiempo del primer proceso).
        *   $T_{ETAPA}$: Tiempo de la etapa más larga.
        *   Ejemplo (lavado, $T_{ETAPA} = ½$ hora): Para 4 procesos, $TS(4) = 2 \text{ hs} + (4-1) \cdot 0.5 \text{ hs} = 3.5 \text{ hs}$.

**Comparación de Tiempos (Ejemplo Lavado):**

| Nº Procesos | Tiempo Secuencial ($TP(M)$) | Tiempo Segmentado ($TS(M)$) |
|-------------|-----------------------------|------------------------------|
| 1           | 2 hs                        | 2 hs                         |
| 4           | 8 hs                        | 3.5 hs                       |
| 10          | 20 hs                       | 6.5 hs                       |

**Aceleración (Speedup - S)**

Mide la mejora en velocidad del sistema segmentado.

*   Fórmula: $S = \frac{TP(M)}{TS(M)}$
*   Para un solo proceso (M=1): No hay aceleración ($S=1$).
*   Para M procesos (M → ∞): Aceleración máxima ($S_{max}$) ≈ $\frac{TP(1)}{T_{ETAPA}}$
*   Caso Ideal (etapas iguales): $S_{max} = N$ (N = número de etapas).

**Impacto de Etapas Desiguales**

La etapa más lenta ($T_{ETAPA}$) limita el rendimiento.

*   Ejemplo: Etapas de lavado con tiempos E1=½ hs, E2=½ hs, E3=¾ hs, E4=¼ hs.
    *   $T_{ETAPA} = 0.75$ hs (45 minutos).
    *   $S_{max} = \frac{2 \text{ hs}}{0.75 \text{ hs}} \approx 2.66$.

**Latencia**

Tiempo total para que un proceso se complete en el pipeline.

*   $TS(1)$: Latencia del primer proceso.
*   Si las etapas son desiguales, la latencia es la suma de los tiempos de cada etapa.
*   La latencia de un proceso segmentado es siempre mayor o igual a la latencia del proceso sin segmentar.
*   Ejemplo (E1=30’, E2=30’, E3=45’, E4=15’, E5=30’): Latencia = 150 minutos.

**Throughput (Productividad)**

Cantidad de procesos completados por unidad de tiempo.

*   Fórmula: Throughput = $1 / T_{ETAPA}$
*   Ejemplo (E1=30’, E2=30’, E3=45’, E4=15’, E5=30’): Throughput = 1 proceso / 45 minutos.

**Consideraciones Adicionales**

*   **Overhead:** Retardos adicionales por registros entre etapas.
*   **Hazards (Riesgos):** Dependencias entre instrucciones que pueden detener el pipeline.

