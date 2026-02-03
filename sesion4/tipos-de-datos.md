---
icon: square-small
---

# Tipos de Datos

Cuando trabajas con contratos inteligentes en Solidity, los **tipos de datos** son la base de todo. Son la forma en la que defines y estructuras la información dentro de tu contrato. A través de ellos puedes controlar desde simples números y cadenas de texto hasta complejas estructuras y colecciones de datos.

Un tipo de dato es la forma en que defines qué tipo de valor puede tener una variable. Así como en la vida real tenemos diferentes formas de representar información (números, palabras, listas), en Solidity tenemos diferentes tipos de datos para definir cómo se almacena y gestiona esa información dentro del contrato.

### Principales tipos de datos en Solidity

1. **Enteros (int y uint)**: Los enteros son uno de los tipos de datos más básicos en cualquier lenguaje de programación y Solidity no es la excepción. Existen dos tipos principales:
   * **int**: Representa números enteros que pueden ser positivos o negativos. Puedes definir el tamaño del entero especificando la cantidad de bits que ocupa (por ejemplo, `int8`, `int16`, `int256`). Si no especificas, el valor por defecto es `int256`.
   * **uint**: Representa números enteros sin signo, es decir, solo positivos. Al igual que con `int`, puedes especificar el tamaño del entero (`uint8`, `uint16`, `uint256`). El valor por defecto es `uint256`.
   *   **Consideraciones de almacenamiento**: Los datos se almacenan en slots de 32 bytes, por lo que si utilizas varios enteros pequeños (como `uint8` y `uint16`) dentro de una misma slot, optimizas el uso del espacio. Sin embargo, si utilizas un `uint256` junto a enteros pequeños, ese `uint256` ocupará una slot completa, y los enteros pequeños se colocarán en otra slot, desperdiciando espacio.

       ```solidity
       uint8 a = 1; // 1 byte
       uint32 b = 2; // 4 bytes
       uint256 c = 3; // 32 bytes
       ```
2.  **Booleanos (bool)**: Los tipos de datos booleanos solo pueden tener dos valores: `true` o `false`. Son extremadamente útiles cuando necesitas definir condiciones o restricciones en tu contrato.

    * **Consideraciones de gas**: Aunque un booleano solo necesita 1 bit para almacenar su valor, en Solidity ocupa un **byte completo**.

    <pre class="language-solidity"><code class="lang-solidity"><strong>bool public esValido = true;
    </strong></code></pre>
3.  **Dirección (address)**: Los tipos `address` se utilizan para almacenar direcciones de cuentas en la blockchain. Una dirección puede ser la de un usuario o la de otro contrato inteligente, y se utiliza para enviar y recibir ether, dar control de acceso o para interactuar con otros contratos.

    ```solidity
    address propietario = 0x5a4e9Bb1f224e8254C1d63e90dE34E8572f8dC71; // 20 bytes
    ```

    Además, Solidity tiene un tipo especial llamado `address payable` que permite enviar ether a esa dirección.
4.  **String y Bytes**:

    * **string**: Se utiliza para almacenar cadenas de texto. Por ejemplo, nombres o descripciones. A diferencia de otros lenguajes, las operaciones con strings en Solidity son limitadas debido a su alto costo en términos de gas.
    * **bytes**: Son secuencias de bytes de longitud fija o variable. Los tipos `bytes` y `bytes1`, `bytes2`, ..., `bytes32` son más eficientes que `string` para almacenar datos binarios o información codificada.
    * **Consideraciones de gas**: Manipular cadenas largas o variables `bytes` dinámicas es costoso. Siempre que sea posible, usa `bytes` de longitud fija para operaciones que no requieran cambios de tamaño dinámicos.

    ```solidity
    string public nombre = "Blockchain";
    bytes32 public hash = keccak256(abi.encodePacked(nombre)); // 32 bytes
    ```



Cada byte de almacenamiento en la blockchain tiene un costo. Usar los tipos de datos más adecuados y estructurarlos eficientemente no solo hace que tu contrato sea más barato de desplegar y ejecutar, sino que también minimiza la posibilidad de errores costosos. Además, al optimizar el almacenamiento, mejoras el rendimiento del contrato y reduces los costos de gas para ti y tus usuarios.

<figure><img src="../.gitbook/assets/image (66) (1).png" alt=""><figcaption></figcaption></figure>

* **Primera slot**:
  * **Variables pequeñas (`uint8`, `uint16`, `bool`)**: Se agrupan para ocupar solo una slot, que tiene capacidad de 32 bytes. Aquí ocupan un total de 26 bytes, aprovechando bien el espacio.
  * **Address (`address`)**: Este tipo ocupa 20 bytes, compartiendo la slot con otras variables pequeñas.
* **Segunda y tercera slot**:
  * **`uint256` y `int256`**: Cada una de estas variables ocupa una slot completa de 32 bytes, ya que son de tamaño fijo y máximo (256 bits).
* **Cuarta slot**:
  * **`bytes32`**: Este tipo de datos ocupa 32 bytes fijos, lo cual es ideal para almacenar identificadores o hashes. Aquí se utiliza para almacenar el identificador "Blockchain!".
* **Quinta slot**:
  * **`string`**: Los `string` son dinámicos y ocupan más de una slot. En la primera slot se almacena un hash que apunta al contenido real de la cadena de texto, que se guarda en otras slots de almacenamiento.
* **Sexta slot**:
  * **`bool` y `uint8`**: Estas variables pequeñas se agrupan para optimizar el uso de espacio. Aún hay 30 bytes disponibles en esta slot, lo que significa que podrías agregar más variables pequeñas sin necesidad de usar una nueva slot.
