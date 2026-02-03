---
icon: square-small
---

# Calldata, Memory y Storage

En Solidity, entender cómo funcionan **calldata, memory y storage** es clave para escribir contratos eficientes y evitar errores. Estos tres términos definen dónde y cómo se almacenan los datos en el contrato y tienen un impacto directo en el costo de gas y en la funcionalidad del contrato.

Vamos a desglosarlos y ver cómo usar cada uno de manera efectiva, con especial atención a los strings.

### Calldata, Memory y Storage

**1. Calldata: Datos Temporales y de Solo Lectura**

* Puedes ver los datos, pero no puedes cambiarlos. Se utiliza para los datos de entrada de funciones externas y es **inmutable** (no puedes modificar los datos que llegan aquí).
* **¿Cuándo usarlo?**\
  Úsalo cuando quieras pasar datos a una función y no necesites cambiarlos. Es más eficiente en términos de gas que `memory` porque evita copiar datos innecesarios.
*   **Ejemplo:**

    ```solidity
    function procesarDatos(uint256[] calldata numeros) external pure returns (uint256) {
        return numeros[0] * 2; // Solo estamos leyendo datos, no cambiándolos.
    }
    ```

    Aquí, `numeros` es un array de enteros.

**2. Memory: Memoria Temporal para Datos Cambiantes**

* Es útil mientras lo necesitas, pero no queda nada guardado cuando te vas. Aquí es donde se almacenan datos temporales dentro de una función.
* **¿Cuándo usarlo?**\
  Se usa para datos que necesitas modificar dentro de la función o para manejar datos intermedios. Los strings y arrays que se manipulan en funciones deben estar en `memory` para poder trabajar con ellos sin restricciones.
*   **Ejemplo 1:**

    ```solidity
    function saludoTemporal() public pure returns (string memory) {
        string memory mensaje = "Hola, Avalanche!";
        return mensaje; // El valor de 'mensaje' se guarda solo mientras se ejecuta la función.
    }
    ```

    Al terminar la ejecución de la función, `mensaje` desaparece, y nadie recuerda que existió.
*   **Ejemplo 1:**

    ```solidity
    function cambiarMensaje(string memory mensaje) public pure returns (string memory) {
        mensaje = "Hola, Avalanche!";
        return mensaje; // Se puede modificar 'mensaje' porque está en memory.
    }
    ```

    Aquí puedes hacer lo que quieras con `mensaje`, cambiarlo, combinarlo, etc., porque está en `memory` y no en `calldata`.

**3. Storage: Almacenamiento Permanente en la Blockchain**

* `storage` es la bóveda del contrato, donde se guarda todo lo que quieres que dure para siempre (o hasta que alguien lo cambie). Aquí es donde se almacenan las variables de estado del contrato, como balances o datos de usuario.
* **¿Cuándo usarlo?**\
  Se usa para datos que deben ser persistentes, como el balance de usuarios, el propietario del contrato, o cualquier información que necesites mantener incluso después de que la función termine.
*   **Ejemplo:**

    ```solidity
    uint256 public totalTokens; // Esto está en storage

    function setTokens(uint256 cantidad) public {
        totalTokens = cantidad; // Cambiamos el valor en storage, y esto tiene un costo de gas.
    }
    ```

    Aquí, `totalTokens` se guarda en storage, y cualquier cambio que hagas será permanente (bueno, al menos hasta que se ejecute otra transacción que lo modifique).



Usar bien `calldata`, `memory` y `storage` no solo optimiza el uso de gas, sino que también evita errores y comportamientos inesperados. Por ejemplo, si pasas un string como parámetro sin especificar su ubicación, Solidity no sabrá cómo manejarlo y te lanzará un error de compilación. Es por eso que siempre debes declarar strings y arrays dinámicos como `calldata` o `memory` al pasarlos como parámetros a una función.

**Ejemplo común de error:**

```solidity
function cambiarMensaje(string mensaje) public { 
    // Error: No se especifica si 'mensaje' está en memory o calldata.
}
```

**Versión corregida:**

```solidity
function cambiarMensaje(string memory mensaje) public { 
    // Ahora sí, porque 'mensaje' está en memory.
}
```
