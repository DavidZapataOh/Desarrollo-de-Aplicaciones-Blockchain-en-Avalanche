---
icon: square-small
---

# Tipos de Variables

Los **tipos de variables** son fundamentales para definir cómo se almacena y manipula la información en la blockchain. Saber cómo funcionan y las particularidades de cada tipo de variable te permitirá escribir contratos más eficientes y seguros. Vamos a explorar los diferentes tipos de variables y sus características principales.

### 1. **Variables de Estado**

Las **variables de estado** se almacenan directamente en la blockchain y mantienen su valor entre llamadas de función y transacciones. Son persistentes y cualquier cambio en su valor implica una modificación permanente en la blockchain.

<pre class="language-solidity"><code class="lang-solidity">// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract AlmacenamientoDeTipos {

<strong>uint256 public totalSuministro; // Se almacena permanentemente en la blockchain
</strong>address public propietario; // Almacena la dirección del propietario del contrato

// resto del contrato...
}
</code></pre>

### 2. **Variables Locales**

Las **variables locales** solo existen durante la ejecución de una función. Se almacenan en la memoria y no persisten después de que la función ha terminado. No ocupan espacio en la blockchain y, por lo tanto, son más baratas de usar.

```solidity
function calcularSuma(uint256 a, uint256 b) public pure returns (uint256) {
    uint256 suma = a + b; // Variable local
    return suma;
}
```

#### 3. **Variables Globales**

Solidity ofrece varias **variables globales** que proporcionan información sobre el entorno del contrato, como la dirección del remitente de la transacción o la cantidad de gas disponible. A continuación, te muestro una tabla con todas las variables globales más importantes y su descripción:

| **Variable Global**      | **Descripción**                                                                            | **Tipo de Dato** |
| ------------------------ | ------------------------------------------------------------------------------------------ | ---------------- |
| `msg.sender`             | Dirección de la cuenta que invocó la función.                                              | `address`        |
| `msg.value`              | Cantidad de Ether (en wei) enviada junto con la transacción.                               | `uint`           |
| `msg.data`               | Datos completos enviados junto con la llamada a la función.                                | `bytes`          |
| `msg.sig`                | Primera palabra (4 bytes) de `msg.data`, que identifica la función que se está llamando.   | `bytes4`         |
| `tx.origin`              | Dirección de la cuenta que inició la transacción (no solo la llamada actual).              | `address`        |
| `block.timestamp`        | Timestamp actual del bloque en segundos desde el epoch.                                    | `uint`           |
| `block.number`           | Número del bloque actual.                                                                  | `uint`           |
| `block.coinbase`         | Dirección del minero que validó el bloque actual.                                          | `address`        |
| `block.difficulty`       | Dificultad del bloque actual.                                                              | `uint`           |
| `block.gaslimit`         | Límite de gas del bloque actual.                                                           | `uint`           |
| `block.chainid`          | ID de la cadena en la que se ejecuta el contrato (disponible desde Solidity 0.8.0).        | `uint`           |
| `block.basefee`          | Tarifa base de gas del bloque (disponible desde Solidity 0.8.7).                           | `uint`           |
| `gasleft()`              | Cantidad de gas restante en la transacción actual.                                         | `uint`           |
| `tx.gasprice`            | Precio del gas de la transacción.                                                          | `uint`           |
| `tx.origin`              | Dirección de la cuenta que inició la transacción (similar a `msg.sender` pero más amplia). | `address`        |
| `blockhash(blockNumber)` | Devuelve el hash del bloque dado como argumento (solo para los 256 bloques más recientes). | `bytes32`        |

```solidity
function mostrarInfo() public view returns (address, uint256) {
    return (msg.sender, block.timestamp);
}
```

* `msg.sender`: Proporciona la dirección del remitente de la llamada a la función.
* `block.timestamp`: Muestra el tiempo actual del bloque, útil para funciones que dependen del tiempo.
