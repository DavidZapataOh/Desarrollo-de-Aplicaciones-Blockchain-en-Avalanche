---
icon: square-small
---

# Keccak256

El algoritmo **keccak256** es una función de hashing que toma cualquier cantidad de datos y los convierte en un valor único de 32 bytes (256 bits). Es súper útil para asegurar que los datos no se modifiquen y para evitar colisiones (dos entradas diferentes generando el mismo hash). Es el equivalente digital de meter un pastel entero en una trituradora y obtener un código único, por mucho que intentes, no puedes reconstruir el pastel original solo con ese código.

Keccak256 asegura que cualquier cambio, por mínimo que sea, en los datos originales, producirá un hash completamente diferente. Esto lo convierte en la herramienta perfecta para comparar, validar y asegurar información en los contratos inteligentes.

### El problema con los `strings` y cómo lo resuelve `keccak256`

Imagina que quieres verificar si dos strings son iguales, algo así como comprobar si `"Hola"` es igual a `"hola"`. En Solidity no puedes simplemente hacer `if (string1 == string2)`, porque los strings no se pueden comparar de esa forma directamente. Esto se debe a que Solidity no tiene un operador de comparación para `strings`. Entonces, ¿qué haces?

Aquí entra **keccak256** al rescate. Lo que haces es convertir ambos strings en su hash correspondiente usando `keccak256` y luego comparas esos hashes. Si los hashes son iguales, entonces los strings también lo son.

```solidity
function compararStrings(string memory _a, string memory _b) public pure returns (bool) {
    return keccak256(abi.encodePacked(_a)) == keccak256(abi.encodePacked(_b));
}
```

En este código, ambos strings se convierten en su hash usando `keccak256` y se comparan. Esto te asegura que cualquier variación en los strings, por pequeña que sea, resultará en hashes diferentes.

### Otros usos del `keccak256`

El uso de `keccak256` va mucho más allá de comparar strings. Aquí te dejo algunos ejemplos de cómo se puede utilizar en diferentes contextos:

1.  **Crear identificadores únicos**: Si necesitas un identificador único para algo en tu contrato, como una dirección de billetera o un token, `keccak256` es perfecto. Puedes usarlo para generar un identificador a partir de múltiples datos combinados, como la dirección del usuario, un número aleatorio y un timestamp.

    <pre class="language-solidity" data-full-width="false"><code class="lang-solidity">function generarID(address _usuario, uint _timestamp) public pure returns (bytes32) {
        return keccak256(abi.encodePacked(_usuario, _timestamp));
    }
    </code></pre>
2. **Verificar firmas digitales**: En contratos donde necesitas verificar la autenticidad de una firma, `keccak256` se usa para crear el hash del mensaje firmado. Este hash se compara luego con la firma proporcionada para asegurarse de que no ha sido alterada.
3.  **Generar números pseudoaleatorios**: Aunque Solidity no tiene una función de números aleatorios como tal, puedes usar `keccak256` con datos impredecibles (como `block.timestamp` y `block.difficulty`) para crear algo parecido. Pero ojo, no es realmente seguro para cosas importantes como juegos de azar.

    ```solidity
    function numeroAleatorio(uint256 _input) public view returns (uint256) {
        return uint256(keccak256(abi.encodePacked(block.timestamp, block.difficulty, _input)));
    }
    ```

### ¿Cómo funciona `keccak256` por detrás?

Debajo de la superficie, `keccak256` usa un algoritmo de hashing que transforma la entrada en bloques de datos y realiza operaciones matemáticas y lógicas para generar el hash final. Cada bit en la entrada afecta al hash resultante, y cambiar incluso un solo carácter en la entrada producirá un hash completamente diferente. Esto lo hace ideal para detectar cambios en los datos y proteger contra manipulaciones.
