---
icon: square-small
---

# Función Payable

Las **funciones `payable`** en Solidity son las puertas de entrada para que un contrato reciba Ether. Imagina que tienes una hucha digital y quieres permitir que cualquiera pueda meterle monedas (Ether). Bueno, con una función `payable` haces justo eso, le das a tu contrato la capacidad de aceptar pagos.

### ¿Qué es una función `payable`?

Una función `payable` es una función especial en Solidity que permite al contrato recibir Ether. Sin este modificador, cualquier intento de enviar Ether a la función fallará, así que es esencial para cualquier operación que involucre pagos.

**Sintaxis básica:**

```solidity
function recibirPago() public payable {
    // Código de la función que puede recibir Ether
}
```

Aquí, la función `recibirPago` puede aceptar Ether porque lleva el modificador `payable`. Puedes llamarla enviando Ether junto con la transacción, y el contrato almacenará esos fondos.

Cada vez que se llama a una función `payable`, el Ether enviado se almacena en el contrato, y el saldo del contrato aumenta en consecuencia. Esto es útil para aplicaciones como contratos de crowdfunding, tiendas descentralizadas o cualquier caso donde quieras aceptar pagos en tu contrato.

### **Ejemplo práctico: Donaciones a un contrato:**

```solidity
contract Donaciones {
    // Evento para registrar las donaciones recibidas
    event DonacionRecibida(address donante, uint cantidad);

    // Función payable para recibir donaciones
    function donar() public payable {
        require(msg.value > 0, "Debe enviar algo de Ether");
        emit DonacionRecibida(msg.sender, msg.value);
    }

    // Función para consultar el balance del contrato
    function consultarBalance() public view returns (uint) {
        return address(this).balance;
    }
}
```

¿Cómo usar este contrato?

1. **Donar Ether:** Puedes llamar a la función `donar` enviando Ether junto con la transacción. Por ejemplo, si donas 1 ETH, el contrato almacenará ese valor y emitirá un evento `DonacionRecibida` con los detalles de la donación.
2. **Consultar el balance:** La función `consultarBalance` devuelve el saldo total del contrato. Así puedes saber cuánto ha recaudado en donaciones.

### Cosas a tener en cuenta con `payable`:

1. **No todas las funciones aceptan Ether:** Si olvidas poner el modificador `payable`, tu función no podrá recibir Ether, y la transacción fallará.
2. **Uso de `msg.value`:** Dentro de una función `payable`, `msg.value` representa la cantidad de Ether enviada a la función. Es útil para realizar cálculos o condiciones basadas en el monto recibido.
3. **Enviar Ether a otros:** Las funciones `payable` también te permiten enviar Ether a otras direcciones desde el contrato usando `address(beneficiario).transfer(cantidad)`. Eso sí, cuidado con los ataques de reentrancia cuando envíes fondos.

### Ejemplo avanzado: Tienda Descentralizada

Supongamos que quieres crear una tienda donde los usuarios puedan comprar productos pagando con Ether. Vamos a combinar una función `payable` con un `mapping` para gestionar las compras.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Tienda {
    // Producto con su precio y disponibilidad
    struct Producto {
        string nombre;
        uint precio;
        bool disponible;
    }

    // Mapeo de ID de producto a Producto
    mapping(uint => Producto) public productos;

    // Evento para registrar compras
    event ProductoComprado(uint id, address comprador);

    // Constructor para inicializar productos
    constructor() {
        productos[1] = Producto("Camiseta", 0.1 ether, true);
        productos[2] = Producto("Gorra", 0.05 ether, true);
    }

    // Función payable para comprar un producto
    function comprarProducto(uint id) public payable {
        // Verificamos que el producto existe y está disponible
        require(productos[id].disponible, "Producto no disponible");
        require(msg.value == productos[id].precio, "Monto incorrecto");

        // Registrar la compra y emitir un evento
        productos[id].disponible = false;
        emit ProductoComprado(id, msg.sender);
    }

    // Función para consultar el balance de la tienda
    function consultarBalance() public view returns (uint) {
        return address(this).balance;
    }
}
```

¿Cómo funciona esta tienda?

1. **Comprar un producto:** La función `comprarProducto` permite a los usuarios comprar un producto enviando el monto exacto de Ether. Si el producto cuesta 0.1 ETH, deberás enviar justo esa cantidad, de lo contrario, la transacción fallará.
2. **Consultar el balance:** `consultarBalance` muestra el total de fondos recaudados por la tienda.
