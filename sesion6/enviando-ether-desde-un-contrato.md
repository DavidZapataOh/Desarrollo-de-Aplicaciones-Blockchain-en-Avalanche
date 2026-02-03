---
icon: square-small
---

# Enviando Ether desde un Contrato

Enviar **Ether** desde un contrato en Solidity puede parecer complicado al principio, pero con los métodos correctos, es bastante sencillo. Ya sea que quieras hacer pagos automáticos, distribuir recompensas o simplemente enviar fondos a otra dirección, es importante entender cómo hacerlo de forma segura y eficiente. Vamos a explorar cómo enviar Ether desde un contrato y qué cosas debes tener en cuenta para evitar problemas.

### ¿Cómo se envía Ether desde un contrato?

En Solidity, hay tres maneras principales de enviar Ether:

1. **Transfer**: Es la forma más simple y directa. Envía 2300 gas, suficiente para registrar un evento y cambiar el saldo, pero no para ejecutar funciones complejas.
2. **Send**: Similar a `transfer`, pero en lugar de lanzar un error si la transacción falla, devuelve `true` o `false`. Envía 2300 gas.
3. **Call**: Es el más versátil y seguro. Permite enviar Ether y ejecutar funciones, además de controlar el gas enviado.

#### Método 1: `transfer`

`transfer` es como la transferencia bancaria más directa y segura, pero también la más limitada. Si el envío falla, lanza un error y revierte la transacción.

```solidity
function enviarEtherTransfer(address payable destino) public payable {
    destino.transfer(msg.value);
}
```

* **Ventajas**: Simple y seguro.
* **Desventajas**: Si el destinatario necesita más de 2300 gas para completar su lógica, la transacción fallará.

#### Método 2: `send`

`send` funciona igual que `transfer`, pero en lugar de lanzar un error, simplemente devuelve `false` si la transacción falla. Esto es útil si quieres manejar manualmente los errores, pero debes asegurarte de verificar siempre el valor de retorno.

```solidity
function enviarEtherSend(address payable destino) public payable {
    bool exito = destino.send(msg.value);
    require(exito, "Envio de Ether fallido");
}
```

* **Ventajas**: Permite manejar errores manualmente.
* **Desventajas**: Al igual que `transfer`, solo envía 2300 gas, y si no verificas el retorno, podrías no darte cuenta de que la transacción falló.

#### Método 3: `call`

`call` es como el navaja suiza de Solidity. No solo puedes enviar Ether, sino también ejecutar funciones en el contrato de destino, además de controlar cuánto gas se envía. Esta es la forma recomendada para la mayoría de los casos, ya que te da más control y flexibilidad.

```solidity
function enviarEtherCall(address payable destino) public payable {
    (bool exito, ) = destino.call{value: msg.value}("");
    require(exito, "Envio de Ether fallido con call");
}
```

* **Ventajas**: Control total sobre el gas y puede ejecutar funciones en el destino.
* **Desventajas**: Debes ser muy cuidadoso con su uso, porque mal configurado puede permitir ataques como **reentrancy**.

### Ejemplo práctico: Reparto de ganancias

Vamos a ver un ejemplo donde usamos `call` para repartir Ether entre varios destinatarios:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Reparto {
    address payable[] public beneficiarios;
    
    // Añade un beneficiario
    function agregarBeneficiario(address payable _nuevoBeneficiario) public {
        beneficiarios.push(_nuevoBeneficiario);
    }
    
    // Función para repartir Ether equitativamente entre todos los beneficiarios
    function repartirGanancias() public payable {
        uint256 cantidadPorPersona = msg.value / beneficiarios.length;
        for (uint256 i = 0; i < beneficiarios.length; i++) {
            (bool exito, ) = beneficiarios[i].call{value: cantidadPorPersona}("");
            require(exito, "Envio de Ether fallido");
        }
    }
}
```

En este contrato, `repartirGanancias` distribuye el Ether enviado a la función entre todos los beneficiarios almacenados. Usa `call` para enviar el Ether, asegurando que cada transacción se complete correctamente.

### Cosas que debes tener en cuenta

1. **Ataques de Reentrancia**: Cuando usas `call` para enviar Ether, asegúrate de que tu lógica esté bien estructurada para evitar ataques de reentrancia. Un atacante podría intentar llamar a tu contrato nuevamente antes de que la primera llamada termine, lo que podría causar problemas graves. Usa siempre el patrón **Checks-Effects-Interactions**: primero verifica las condiciones, luego actualiza el estado, y finalmente realiza la interacción externa (enviar Ether).
2. **Uso de gas**: `transfer` y `send` solo envían 2300 gas, lo que no es suficiente para funciones complejas en el contrato receptor. Si necesitas más gas, usa `call` y especifica la cantidad necesaria.
3. **Direcciones `payable`**: Solo puedes enviar Ether a direcciones marcadas como `payable`. Asegúrate de usar `address payable` para los destinatarios.
