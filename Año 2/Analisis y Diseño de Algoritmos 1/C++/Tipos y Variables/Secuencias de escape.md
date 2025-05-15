Las **secuencias de escape** son combinaciones especiales de caracteres que comienzan con una barra invertida (`\`) seguida por otro carácter o una secuencia de dígitos. Se utilizan dentro de literales de carácter (encerrados en comillas simples `' '`) y literales de cadena (encerrados en comillas dobles `" "`) para representar:

1.  **Caracteres no imprimibles:** Como el salto de línea, la tabulación, el retroceso, etc.
2.  **Caracteres que tienen un significado especial:** Como la propia barra invertida (`\`), las comillas simples (`'`) y las comillas dobles (`"`), que de otro modo terminarían el literal.
3.  **Caracteres representados por su valor numérico** (no mostrado en la tabla del usuario, pero relevante, ej. `\x41` para 'A').

Cuando el compilador encuentra una secuencia de escape, la reemplaza por el carácter único que representa.

## Tabla de Secuencias de Escape Comunes

| Secuencia | Carácter Representado | Descripción                                  |
| :-------- | :-------------------- | :------------------------------------------- |
| `\\`      | `\`                   | Barra invertida                              |
| `\'`      | `'`                   | Comilla simple (apóstrofo)                   |
| `\"`      | `"`                   | Comillas dobles                              |
| `\?`      | `?`                   | Signo de interrogación (útil para evitar trigrafos) |
| `\0`      | `<NULL>`              | Carácter nulo (valor binario cero)           |
| `\a`      | `<BEL>`               | Alerta / Campana (produce un sonido audible) |
| `\b`      | `<BS>`                | Retroceso (mueve el cursor una posición atrás) |
| `\f`      | `<FF>`                | Salto de página (Form Feed)                  |
| `\n`      | `<NL>` / `<LF>`       | Nueva línea (Salta a la siguiente línea)     |
| `\r`      | `<CR>`                | Retorno de carro (Mueve el cursor al inicio de la línea) |
| `\t`      | `<HT>`                | Tabulación horizontal                        |
| `\v`      | `<VT>`                | Tabulación vertical                          |

**Ejemplo de uso:**

```cpp
#include <iostream>

int main() {
    // Imprime: Él dijo: "¡Hola!\n\tEsto está tabulado."
    std::cout << "Él dijo: \"¡Hola!\\n\\tEsto está tabulado.\"\n";
    // Imprime un carácter de comilla simple
    char comillaSimple = '\'';
    std::cout << "Carácter de comilla simple: " << comillaSimple << std::endl;
    return 0;
}
```
```