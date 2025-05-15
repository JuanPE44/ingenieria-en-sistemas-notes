El principio de **Aceleración del Caso Común** (o *Speedup the Common Case* en inglés) es una regla fundamental en el diseño y optimización de sistemas, especialmente en arquitectura de computadoras y desarrollo de software.

**La idea central es:** Al optimizar el rendimiento, se debe dar **prioridad a mejorar la velocidad de las operaciones o eventos que ocurren con mayor frecuencia** (los "casos comunes"), en lugar de invertir un esfuerzo desproporcionado en optimizar las operaciones que suceden raramente (los "casos raros" o "casos esquina").

**¿Por qué es importante?**

1.  **Mayor Impacto Global:** Una pequeña mejora en una operación muy frecuente tendrá un impacto mucho mayor en el rendimiento general del sistema que una gran mejora en una operación muy infrecuente.
    *   *Ejemplo:* Si una instrucción se ejecuta el 90% del tiempo, hacerla un 10% más rápida mejora significativamente el rendimiento total. Si otra instrucción se ejecuta solo el 1% del tiempo, incluso hacerla 5 veces más rápida apenas afectará el rendimiento global.
2.  **Costo y Complejidad:** Intentar optimizar *todos* los casos posibles, incluyendo los más raros y complejos, a menudo requiere añadir lógica adicional (hardware o software).
    *   Esto **incrementa los costos** de diseño y producción.
    *   Peor aún, esta complejidad añadida puede **introducir retrasos o sobrecargas** que *ralenticen* las operaciones comunes, resultando en un rendimiento general inferior en el uso normal del sistema. Es decir, la optimización para el caso raro puede perjudicar al caso común.


**En el contexto de diseño de CPU (como MIPS):**

*   Los diseñadores se enfocan en acelerar las instrucciones más utilizadas (ej. sumas, restas, carga/almacenamiento de datos).
*   Instrucciones muy complejas pero raramente usadas podrían no recibir el mismo nivel de optimización, ya que el hardware extra necesario para acelerarlas podría ralentizar las instrucciones comunes o encarecer demasiado el procesador sin un beneficio proporcional en el rendimiento típico.

