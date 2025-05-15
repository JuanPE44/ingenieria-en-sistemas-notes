
Una matriz $A$ está en **forma escalonada** si cumple las siguientes condiciones:

1.  **Filas de Ceros:** Todas las filas que consisten enteramente de ceros (si las hay) se encuentran en la parte inferior de la matriz.
2.  **Posición de Pivotes:** Por cada fila no nula, el pivote se encuentra en una columna a la **derecha** de la columna del pivote de la fila superior.
3.  **Ceros Debajo de Pivotes:** Todos los elementos en una columna que están **debajo** de un pivote son cero.

*(El primer ejemplo anterior SÍ está en forma escalonada. El segundo NO lo está porque el pivote de la fila 2 no está a la derecha del pivote de la fila 1, y hay un elemento no nulo debajo del pivote de la fila 1)*.