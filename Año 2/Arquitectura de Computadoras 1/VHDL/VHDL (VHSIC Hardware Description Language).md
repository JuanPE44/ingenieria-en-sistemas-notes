VHDL es un **Lenguaje de Descripción de Hardware** (HDL) estandarizado por el IEEE. Se utiliza principalmente para describir, simular y sintetizar (crear) circuitos digitales y sistemas de señales mixtas (analógico/digital), como FPGAs (Field-Programmable Gate Arrays) y ASICs (Application-Specific Integrated Circuits).

## ¿Qué significa?

*   **VHSIC**: Very High Speed Integrated Circuit (Circuito Integrado de Muy Alta Velocidad).
*   **HDL**: Hardware Description Language (Lenguaje de Descripción de Hardware).

## Aspectos Importantes de VHDL

1.  **Describe Hardware, No Software**: A diferencia de los lenguajes de programación tradicionales (como C++ o Python) que describen una secuencia de instrucciones para un procesador, VHDL describe la **estructura** y el **comportamiento** de un circuito electrónico.
2.  **Concurrencia**: El hardware opera de forma inherentemente paralela. VHDL permite describir múltiples operaciones que ocurren simultáneamente, reflejando la naturaleza concurrente del hardware. Las declaraciones fuera de un `PROCESS` se ejecutan en paralelo.
3.  **Abstracción**: Permite describir un diseño en diferentes niveles:
    *   **Comportamental (Behavioral)**: Describe lo que el circuito *hace* (su función) usando construcciones de alto nivel, similar a un lenguaje de programación (if/else, case, loops dentro de `PROCESS`).
    *   **Flujo de Datos (Dataflow)**: Describe cómo los datos fluyen entre registros y unidades lógicas usando asignaciones concurrentes.
    *   **Estructural (Structural)**: Describe el circuito como una interconexión de componentes más simples (puertas lógicas, módulos predefinidos).
4.  **Jerarquía**: Los diseños complejos se construyen conectando módulos o componentes más pequeños. VHDL soporta el diseño jerárquico mediante `ENTITY` (interfaz del componente) y `ARCHITECTURE` (implementación interna), y la instanciación de componentes (`COMPONENT`).
5.  **Simulación**: Antes de fabricar o programar el hardware físico, el código VHDL se puede simular para verificar su correcto funcionamiento lógico y temporal.
6.  **Síntesis**: Las herramientas de síntesis traducen el código VHDL (generalmente en los niveles de flujo de datos o estructural, y un subconjunto del comportamental) en una descripción a nivel de puertas lógicas (netlist) que puede ser implementada en un dispositivo físico (FPGA/ASIC).
7.  **Tipado Fuerte**: VHDL es un lenguaje con tipos de datos estrictos, lo que ayuda a prevenir errores al conectar señales de tipos incompatibles. El tipo más común para señales digitales es `STD_LOGIC` y `STD_LOGIC_VECTOR` (definidos en el paquete `ieee.std_logic_1164`).
8.  **Estructura Básica**:
    *   `LIBRARY` y `USE`: Para importar paquetes de definiciones (ej. `ieee`, `std_logic_1164`).
    *   `ENTITY`: Define el nombre del módulo y sus puertos de entrada/salida (`PORT`).
    *   `ARCHITECTURE`: Contiene la descripción interna del comportamiento o estructura de la `ENTITY`. Puede haber múltiples arquitecturas para una misma entidad.
    *   `PROCESS`: Bloque de código secuencial dentro de una arquitectura concurrente. Se ejecuta cuando cambia una señal en su lista de sensibilidad.
    *   `SIGNAL`: Representa cables o conexiones internas que transportan valores.
    *   `VARIABLE`: Similar a las variables en programación, solo existen dentro de procesos y su asignación es inmediata.
    *   `CONSTANT`: Valores fijos.

## En Resumen

VHDL es una herramienta fundamental en el diseño electrónico digital moderno. Permite a los ingenieros modelar, verificar y crear hardware complejo de manera estructurada y estandarizada, facilitando la creación de desde simples circuitos lógicos hasta sistemas en chip (SoC) completos. Su capacidad para describir concurrencia y diferentes niveles de abstracción lo hace especialmente adecuado para el diseño de hardware.
