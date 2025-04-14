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

# Fallback y Receive

Las funciones **`fallback`** y **`receive`** en Solidity son súper útiles cuando tu contrato recibe llamadas que no coinciden con ninguna de sus funciones o cuando alguien le envía Ether a tu contrato.

### `fallback`: el plan de respaldo

La función `fallback` es como el plan B del contrato. Se activa cuando alguien intenta interactuar con tu contrato llamando una función que no existe. Es como si alguien tocara la puerta equivocada y en lugar de quedarse esperando, el contrato abre la puerta y dice: “Lo siento, esa función no está aquí, pero ¿qué necesitas?”.

**Características de `fallback`:**

* No puede tener argumentos ni devolver valores.
* Puede ser declarada como `payable` para aceptar Ether, o no, si solo se usa para manejar llamadas incorrectas.
* No tiene nombre específico, se define simplemente con la palabra clave `fallback`.

**Sintaxis:**

```solidity
fallback() external {
    // Lógica a ejecutar si se llama una función inexistente
}
```

Si quieres que también pueda aceptar Ether, la declaras como `payable`:

```solidity
fallback() external payable {
    // Lógica a ejecutar si se llama una función inexistente o se envía Ether
}
```

### `receive`: el portero de los pagos

La función `receive` se activa específicamente cuando el contrato recibe Ether, pero no se proporcionan datos adicionales ni se especifica ninguna función. Es como un portero que solo abre la puerta si alguien quiere dejar dinero.

**Características de `receive`:**

* Solo se activa cuando se envía Ether sin datos (sin `msg.data`).
* No puede tener argumentos ni devolver valores.
* Debe ser declarada como `payable` para aceptar Ether.

**Sintaxis:**

```solidity
receive() external payable {
    // Lógica a ejecutar al recibir Ether
}
```

### Ejemplo práctico: Contrato de donaciones

Vamos a ver cómo usar `fallback` y `receive` juntos en un contrato de donaciones:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Donaciones {
    // Evento para registrar las donaciones recibidas
    event DonacionRecibida(address donante, uint cantidad);

    // Mapeo para llevar un registro de las donaciones por usuario
    mapping(address => uint) public donaciones;

    // Función `receive` que se activa al recibir Ether sin datos
    receive() external payable {
        donaciones[msg.sender] += msg.value;
        emit DonacionRecibida(msg.sender, msg.value);
    }

    // Función `fallback` para manejar llamadas a funciones inexistentes
    fallback() external payable {
        donaciones[msg.sender] += msg.value;
        emit DonacionRecibida(msg.sender, msg.value);
    }

    // Función para consultar el total donado por un usuario
    function totalDonado(address usuario) public view returns (uint) {
        return donaciones[usuario];
    }
}
```

¿Cómo funciona este contrato?

1. **receive()**: Cuando alguien envía Ether al contrato sin especificar datos, esta función se activa, se registra la donación y se emite un evento para que todos sepan quién donó cuánto.
2. **fallback()**: Si alguien intenta llamar a una función que no existe y, además, envía Ether, se activa `fallback`. En este caso, también se registra la donación como en `receive`.
3. **totalDonado()**: Permite consultar cuánto ha donado un usuario específico. Este tipo de función es útil para llevar un registro y dar transparencia al proceso.

### Diferencias entre `fallback` y `receive`

* **`receive`** solo se activa cuando el contrato recibe Ether sin datos (`msg.data` vacío).
* **`fallback`** se activa cuando se llama a una función inexistente, ya sea con o sin Ether, siempre y cuando `msg.data` no esté vacío (aunque también funciona si no hay función `receive` definida).
