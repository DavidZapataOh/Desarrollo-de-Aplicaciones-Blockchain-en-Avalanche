---
icon: square-small
---

# Modifiers

Los **modifiers** en Solidity son como pequeños guardianes de las funciones, encargados de verificar que se cumplan ciertas condiciones antes de que se ejecute el código. Piensa en ellos como un filtro que decide si la función sigue adelante o no. Son súper útiles para evitar repetir código y para asegurarte de que ciertas funciones solo se ejecuten bajo circunstancias específicas.

### ¿Qué es un modifier?

Un `modifier` es un fragmento de código que puedes aplicar a una función para agregarle lógica adicional. Es como ponerle un candado a la función, y el modifier es la llave que verifica si tienes permiso para entrar o no. Se definen con la palabra clave `modifier` y, al igual que las funciones, pueden recibir parámetros.

**Sintaxis básica:**

```solidity
modifier nombreDelModifier() {
    // Lógica antes de ejecutar la función
    _;
    // Lógica después de ejecutar la función (opcional)
}
```

La palabra `_` (underscore) indica dónde se ejecutará el resto de la función que usa el modifier. Puedes colocarla antes, después o incluso rodearla con código si quieres ejecutar lógica antes y después de la función.

Por ejemplo:

<pre class="language-solidity"><code class="lang-solidity">modifier soloPropietario() {
    require(msg.sender == propietario, "No eres el propietario");
<strong>    _;
</strong>}
</code></pre>

### Ejemplo práctico: Solo el Propietario

Imaginemos un contrato donde solo el propietario puede ejecutar ciertas funciones. Definimos un modifier `soloPropietario` que verifica si quien llama a la función es el propietario del contrato:

<pre class="language-solidity"><code class="lang-solidity">// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;
<strong>
</strong><strong>contract SoloPropietario {
</strong>    address propietario = 0x1234567890123456789012345678901234567890;
   
    // Modifier para verificar si quien llama es el propietario
    modifier soloPropietario() {
        require(msg.sender == propietario, "No eres el propietario");
        _;
    }

    // Función protegida con el modifier
    function cambiarPropietario(address nuevoPropietario) public soloPropietario {
        propietario = nuevoPropietario;
    }

    // Función solo para el propietario
    function funcionSoloPropietario() public soloPropietario {
        // Código exclusivo para el propietario
    }
}
</code></pre>

Aquí, el modifier `soloPropietario` comprueba que `msg.sender` (la dirección que llama a la función) sea igual a `propietario`. Si no lo es, la transacción falla con el mensaje "No eres el propietario".

### ¿Para qué sirven los modifiers?

1. **Reutilización de código**: En lugar de escribir la misma lógica de validación en cada función, puedes crear un modifier y aplicarlo a todas las funciones que necesiten esa lógica.
2. **Mejora la legibilidad**: Al tener la lógica separada en modifiers, las funciones quedan más limpias y fáciles de leer.
3. **Control de acceso**: Los modifiers son perfectos para restringir quién puede ejecutar una función, cuándo se puede ejecutar o bajo qué condiciones.

### Modifiers con parámetros

Los modifiers también pueden recibir parámetros para hacer la validación más específica. Por ejemplo, puedes verificar que una función solo pueda ejecutarse después de una fecha específica:

```solidity
modifier soloDespues(uint tiempo) {
    require(block.timestamp >= tiempo, "No puedes ejecutar esta funcion todavia");
    _;
}

function ejecutarDespues(uint _tiempo) public soloDespues(_tiempo) {
    // Código que solo se ejecuta después del tiempo especificado
}
```

En este caso, `soloDespues` comprueba que el tiempo actual (`block.timestamp`) sea mayor o igual al tiempo especificado como parámetro. Si no lo es, la función no se ejecuta.

### Ejemplo práctico: Control de acceso avanzado

Imaginemos un contrato donde se gestionan fondos, y solo los administradores pueden retirar dinero después de una fecha específica:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract FondoSeguro {
    address public administrador;
    uint public fechaDesbloqueo;

    constructor() {
        administrador = msg.sender;
        fechaDesbloqueo = block.timestamp + 30 days; // Bloqueado por 30 días
    }

    // Modifier para verificar administrador y fecha de desbloqueo
    modifier soloAdministradorDespues() {
        require(msg.sender == administrador, "No eres el administrador");
        require(block.timestamp >= fechaDesbloqueo, "Fondos bloqueados hasta la fecha de desbloqueo");
        _;
    }

    // Función protegida para retirar fondos
    function retirarFondos(uint cantidad) public soloAdministradorDespues {
        // Código para retirar fondos
    }
}
```

Aquí, `soloAdministradorDespues` asegura que solo el administrador pueda retirar fondos y solo después de la fecha de desbloqueo. Esto evita retiros antes de tiempo y por personas no autorizadas.

### Cosas a tener en cuenta con los modifiers

1. **Requieren gas**: Los modifiers, al igual que cualquier otra lógica, consumen gas. Asegúrate de que su uso esté justificado y no aumente innecesariamente el costo de las transacciones.
2. **No abuses de ellos**: Aunque son útiles, tener demasiados modifiers puede hacer que tu código se vuelva difícil de seguir. Usa modifiers cuando realmente aporten claridad y eficiencia.
3. **Lógica de limpieza**: Si necesitas ejecutar lógica antes y después de la función, asegúrate de que la estructura del modifier refleje claramente el flujo que deseas.
