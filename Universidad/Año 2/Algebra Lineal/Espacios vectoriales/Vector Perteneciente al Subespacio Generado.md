**Notación:** La expresión $\mathbf{v} \in \langle \mathbf{v}_1, \mathbf{v}_2, \dots, \mathbf{v}_k \rangle$ (a veces también escrita como $\mathbf{v} \in \text{span}\{\mathbf{v}_1, \dots, \mathbf{v}_k\}$ o $\mathbf{v} \in \text{gen}\{\mathbf{v}_1, \dots, \mathbf{v}_k\}$) significa que el vector $\mathbf{v}$ **pertenece al subespacio vectorial generado** por el conjunto de vectores $\{\mathbf{v}_1, \mathbf{v}_2, \dots, \mathbf{v}_k\}$.

**Definición:**
Decimos que un vector $\mathbf{v}$ pertenece al subespacio generado por $\{\mathbf{v}_1, \mathbf{v}_2, \dots, \mathbf{v}_k\}$, es decir, $\mathbf{v} \in \langle \mathbf{v}_1, \dots, \mathbf{v}_k \rangle$, si y solo si $\mathbf{v}$ **es una combinación lineal** de los vectores $\mathbf{v}_1, \mathbf{v}_2, \dots, \mathbf{v}_k$.

**¿Qué significa ser una combinación lineal?**
Significa que existen escalares (números) $\alpha_1, \alpha_2, \dots, \alpha_k$ tales que podemos "construir" el vector $\mathbf{v}$ multiplicando cada vector $\mathbf{v}_i$ por su escalar $\alpha_i$ y sumando los resultados:

$$ \mathbf{v} = \alpha_1 \mathbf{v}_1 + \alpha_2 \mathbf{v}_2 + \dots + \alpha_k \mathbf{v}_k $$

**En palabras sencillas:**
Un vector $\mathbf{v}$ está en el espacio generado de otros vectores $\{\mathbf{v}_1, \dots, \mathbf{v}_k\}$ si puedes obtener $\mathbf{v}$ simplemente estirando, encogiendo o invirtiendo la dirección de los vectores $\mathbf{v}_1, \dots, \mathbf{v}_k$ (multiplicando por escalares) y luego sumándolos todos. Si no puedes construir $\mathbf{v}$ de esta manera, entonces $\mathbf{v}$ no pertenece al subespacio generado por ellos.

**El conjunto $\langle \mathbf{v}_1, \dots, \mathbf{v}_k \rangle$ es, de hecho, el conjunto de *todas* las posibles combinaciones lineales que puedes formar con $\mathbf{v}_1, \dots, \mathbf{v}_k$.**
