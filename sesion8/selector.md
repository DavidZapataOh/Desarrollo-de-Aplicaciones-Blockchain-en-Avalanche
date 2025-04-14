---
icon: square-small
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Selector

El **selector** en Solidity es como el “ID” único de cada función. Imagina que cada función en un contrato tiene su propio código que la identifica, permitiendo que Solidity sepa exactamente qué función quieres llamar cuando envías una transacción. Este código, conocido como selector, es una combinación especial de los nombres de la función y sus parámetros, y es fundamental para entender cómo se ejecutan las llamadas a funciones en contratos.

### ¿Qué es un selector?

El selector de una función es un identificador de 4 bytes generado a partir de la firma de la función. La firma de la función incluye el nombre de la función y los tipos de sus parámetros (sin sus nombres). Por ejemplo, si tienes una función como `transfer(address, uint256)`, su selector sería un hash de estos componentes.

**Sintaxis básica para obtener un selector:**

```solidity
bytes4 selector = bytes4(keccak256("nombreFuncion(tipo1,tipo2)"));
```

### ¿Cómo se genera un selector?

El selector se genera aplicando la función hash `keccak256` a la firma de la función y tomando los primeros 4 bytes del resultado. Así es como Solidity sabe exactamente qué función estás intentando llamar cuando envías datos en una transacción.

Por ejemplo, para una función `transfer` en un contrato ERC20, la firma sería:

```solidity
"transfer(address,uint256)"
```

El selector se calcula de la siguiente manera:

```solidity
bytes4 selector = bytes4(keccak256("transfer(address,uint256)"));
```

El resultado sería algo como `0xa9059cbb`. Este selector se incluye en la transacción para indicar qué función se debe ejecutar en el contrato.

### ¿Por qué es importante el selector?

El selector es esencial para identificar qué función de un contrato se debe ejecutar. Esto es especialmente útil cuando interactúas con contratos a través de métodos de bajo nivel como `call`. Además, te permite crear contratos dinámicos que pueden ejecutar diferentes funciones basándose en los selectores recibidos, sin conocer de antemano las funciones específicas.

### Uso del selector en un contrato

Imaginemos que tenemos un contrato que puede llamar dinámicamente a diferentes funciones basadas en el selector recibido:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

// Contrato para realizar operaciones matemáticas básicas
contract OperacionesMatematicas {
    function sumar(uint a, uint b) public pure returns (uint) {
        return a + b;
    }

    function restar(uint a, uint b) public pure returns (uint) {
        return a - b;
    }

    function multiplicar(uint a, uint b) public pure returns (uint) {
        return a * b;
    }
}

// Contrato principal que usa selectores para llamar a las funciones del contrato de operaciones
contract CalculadoraDinamica {
    address public contratoOperaciones;

    // Constructor para inicializar la dirección del contrato de operaciones
    constructor(address _contratoOperaciones) {
        contratoOperaciones = _contratoOperaciones;
    }

    // Función para realizar la operación usando el selector
    function ejecutarOperacion(bytes4 _selector, uint a, uint b) public view returns (uint) {
        (bool exito, bytes memory resultado) = contratoOperaciones.staticcall(
            abi.encodeWithSelector(_selector, a, b)
        );
        require(exito, "La operacion fallo");

        return abi.decode(resultado, (uint));
    }

    // Función para obtener el selector de una operación (opcional)
    function obtenerSelector(string memory nombreOperacion) public pure returns (bytes4) {
        return bytes4(keccak256(bytes(nombreOperacion)));
    }
}
```

* **Contrato `OperacionesMatematicas`**: Contiene tres funciones simples para realizar operaciones matemáticas: `sumar`, `restar` y `multiplicar`.
* **Contrato `CalculadoraDinamica`**:
  * Usa el selector de la función (`_selector`) para llamar a cualquier función del contrato `OperacionesMatematicas`.
  * La función `ejecutarOperacion` realiza la llamada dinámica usando `staticcall`, que ejecuta las operaciones de manera segura sin cambiar el estado del contrato de operaciones.
  * También incluye una función `obtenerSelector` que calcula el selector de cualquier función dada su firma (por ejemplo, `sumar(uint256,uint256)`).

### ¿Cómo se usa en la práctica?

Supongamos que la dirección del contrato `OperacionesMatematicas` es `0x123...`. Queremos realizar una suma de 10 y 20 usando el contrato `CalculadoraDinamica`. Lo haríamos así:

1.  Calculamos el selector de la función `sumar`:

    ```solidity
    bytes4 selectorSuma = bytes4(keccak256("sumar(uint256,uint256)")); 
    // Resultado: 0x2a7f7c85
    ```
2.  Llamamos a la función `ejecutarOperacion` del contrato `CalculadoraDinamica`:

    ```solidity
    uint resultado = calculadora.ejecutarOperacion(0x2a7f7c85, 10, 20); 
    // Resultado esperado: 30
    ```
