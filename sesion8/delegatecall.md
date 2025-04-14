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

# DelegateCall

El método `delegatecall` en Solidity es como permitir que alguien use tu identidad para realizar acciones en tu nombre. Básicamente, ejecuta el código de otro contrato, pero utilizando el contexto de tu propio contrato, lo que significa que puede cambiar el estado y las variables de tu contrato como si fuera propio. Es una herramienta poderosa, pero también arriesgada si no se usa correctamente, ya que da control sobre tu contrato a código externo.

### ¿Qué es `delegatecall`?

`delegatecall` es una función de bajo nivel que permite que un contrato ejecute el código de otro contrato como si fuera suyo. Esto significa que las variables de estado, balances de ether y demás propiedades del contrato que realiza el `delegatecall` se ven afectadas, no las del contrato que contiene el código.

**Sintaxis básica:**

```solidity
(bool exito, bytes memory data) = direccion.delegatecall(abi.encodeWithSignature("nombreFuncion(parametros)"));
```

* `exito` es un booleano que indica si la llamada fue exitosa.
* `data` contiene los datos devueltos por la función llamada.
* `direccion` es la dirección del contrato al que estás llamando.
* `abi.encodeWithSignature` codifica la firma de la función y sus parámetros.

### ¿Cómo funciona `delegatecall`?

Imaginemos que tienes dos contratos, un contrato principal (`Principal`) y un contrato de lógica (`Logica`). El contrato `Principal` delega la ejecución de ciertas funciones al contrato `Logica`. Esto es útil cuando quieres actualizar la lógica de tu contrato sin cambiar su estado, como si estuvieras cambiando el “cerebro” de tu contrato pero manteniendo el mismo cuerpo.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

// Contrato de lógica que contiene las funciones que queremos ejecutar
contract Logica {
    uint public numero;

    // Función para establecer el número, pero utilizando el almacenamiento del contrato que llama
    function establecerNumero(uint _numero) public {
        numero = _numero;
    }
}

// Contrato principal que usa `delegatecall` para ejecutar funciones del contrato de lógica
contract Principal {
    uint public numero;

    // Dirección del contrato de lógica
    address public direccionLogica;

    // Constructor para inicializar la dirección del contrato de lógica
    constructor(address _direccionLogica) {
        direccionLogica = _direccionLogica;
    }

    // Función que usa `delegatecall` para llamar a `establecerNumero` en el contrato de lógica
    function ejecutarDelegatecall(uint _numero) public {
        (bool exito, ) = direccionLogica.delegatecall(
            abi.encodeWithSignature("establecerNumero(uint256)", _numero)
        );
        require(exito, "Delegatecall fallida");
    }
}
```

1. **Contrato `Logica`**: Contiene una función `establecerNumero` que modifica el valor de `numero`.
2. **Contrato `Principal`**: Usa `delegatecall` para llamar a la función `establecerNumero` en el contrato `Logica`.
3. **Ejecución en el contexto del contrato `Principal`**: Aunque `establecerNumero` es una función del contrato `Logica`, `delegatecall` hace que la variable `numero` que se modifica sea la del contrato `Principal`, no la del contrato `Logica`.

### ¿Por qué usar `delegatecall`?

El `delegatecall` es extremadamente útil cuando quieres actualizar la lógica de tu contrato sin cambiar su dirección ni su estado. Esto es muy común en patrones de diseño como **proxy patterns**, donde un contrato proxy delega todas las llamadas a otro contrato que contiene la lógica. Si necesitas cambiar la lógica, simplemente apuntas el proxy a un nuevo contrato de lógica, y listo.

### Ventajas y desventajas de `delegatecall`

**Ventajas:**

1. **Actualización de lógica**: Puedes cambiar la lógica del contrato sin cambiar su dirección o estado.
2. **Reutilización de código**: Usa el mismo contrato de lógica para varios contratos, reduciendo la duplicación de código.
3. **Mantenimiento simplificado**: Si necesitas arreglar o mejorar la lógica, solo necesitas actualizar el contrato de lógica, no el principal.

**Desventajas:**

1. **Riesgo de seguridad**: Si el contrato de lógica tiene fallos de seguridad, estos se trasladan al contrato principal. Además, si alguien puede cambiar la dirección del contrato de lógica en el principal, puede apuntar a un contrato malicioso.
2. **Confusión de almacenamiento**: `delegatecall` usa el almacenamiento del contrato principal, lo que puede llevar a errores si no tienes cuidado con la organización de las variables.

### Consideraciones de seguridad

Cuando uses `delegatecall`, asegúrate de que el contrato al que estás llamando sea de confianza y que su código esté bien auditado. Cambiar la dirección del contrato de lógica en el contrato principal debe estar muy bien protegido, ya que de lo contrario alguien podría redirigir todas las llamadas a un contrato malicioso.
