---
icon: square-small
---

# Interactuando con contratos

Ya con nuestro primer contrato desplegado en local, ahora veremos como interactuar con él usando **Cast**.

Este es el contrato que Foundry crea por defecto:

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;

contract Counter {
    uint256 public number;

    function setNumber(uint256 newNumber) public {
        number = newNumber;
    }

    function increment() public {
        number++;
    }
}
```

Es un contrato muy simple. Tiene dos funciones de escritura, `setNumber` e `increment` y una variable pública `number`.

## Escribir

Foundry incluye una herramienta llamada **Cast**, que trae muchos comandos para interactuar con contratos. En esta sección nos enfocaremos en **`cast send`,** firma y envía una transacción.

Copía el address del contrato desplegado en el capitulo anterior, lo necesitaremos.

Primero, copia el **address del contrato** que desplegaste en el capítulo anterior, porque lo vamos a necesitar.

```bash
cast send 0xaddresscontrato "increment()" --rpc-url 127.0.0.1:8545 --account localKey
```

Desglosemos este comando:

* `cast send`: firma y envía la transacción.
* `0xaddresscontrato`: dirección del contrato (reemplázala por la tuya).
* `"increment()"`: firma de la función que quieres llamar.
* `--rpc-url http://127.0.0.1:8545`: RPC de tu nodo local (Anvil).
* `--account localKey`: la cuenta con la que vas a firmar (tu llave local configurada).

¿Y que sucede en el caso donde la función requiera parametros? como en el caso de `setNumber` :

```bash
cast send 0xaddresscontrato "setNumber(uint256)" 100 --rpc-url 127.0.0.1:8545 --account localKey
```

Acá hicimos dos cosas diferente, en la firma pusimos el tipo del parámetro, y seguido pasamos el valor.

## Leer

Para leer información de un contrato es muy similar, solo que ahora, en lugar de `cast send`, usaremos `cast call`.

```bash
cast call 0xaddresscontrato "number()" --rpc-url 127.0.0.1:8545
```

Como esto **no escribe**, no necesitas firmar ni pasar llave privada.

Probablemente verás algo como:

```bash
0x0000000000000000000000000000000000000000000000000000000000000064
```

¿64? ¿No debería ser 100?

El valor viene en formato hexadecimal, por lo tanto, para acceder a su valor decimal debemos ejecutar el siguiente comando:

```bash
cast --to-base 0x0000000000000000000000000000000000000000000000000000000000000064 dec
```

Y ahí sí verás el número real (por ejemplo, `100`).
