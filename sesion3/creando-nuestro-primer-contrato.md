---
icon: square-small
---

# Creando nuestro primer contrato

Ya conoces la estructura inicial de un contrato. Ahora, vamos a crear nuestro primer contrato inteligente sencillo. En esta ocasión yo te daré el código y lo único que tendrás que hacer es copiarlo y pegarlo. No te preocupes si aún no entiendes nada del código, en las siguientes secciones explicaremos cada cosa paso a paso.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract MiPrimerContrato {

    string mensaje;

    function enviarMensaje(string memory _nuevoMensaje) public {
        mensaje = _nuevoMensaje;
    }

    function leerMensaje() public view returns(string memory){
        return mensaje;
    }
}
```

Este contrato cuenta con dos funciones:

* `enviarMensaje`: Actualiza el valor de la variable mensaje.
* `leerMensaje`: Muestra el valor actual de la variable mensaje.

La variable `mensaje` es tipo `string`, lo que quiere decir que es una cadena de caracteres, es decir, un texto.



Al intentar pegar este código a tu contrato, te saldrá la siguiente advertencia:

<figure><img src="../.gitbook/assets/image (18) (1).png" alt=""><figcaption></figcaption></figure>

Esto se debe a que Remix te pide que tengas cuidado de que la fuente de donde sacaste el código sea segura y confiable, porque podría haber la posibilidad de interactuar con un código malicioso que saquee todos tus fondos.
