---
icon: square-small
---

# Call

El método `call` en Solidity te permite enviar datos a cualquier contrato usando su dirección, a diferencia de usar una interfaz, sin importar si conoces o no su estructura. Es súper poderoso, pero también hay que usarlo con cuidado porque, como dice el Tío Ben, "un gran poder conlleva una gran responsabilidad".

### ¿Qué es `call`?

El método `call` es una función de bajo nivel que se utiliza para realizar llamadas a otros contratos o para enviar ether a una dirección. Te permite llamar a cualquier función de un contrato externo utilizando su dirección, incluso si no tienes la interfaz o el ABI del contrato. Sin embargo, es un poco arriesgado, ya que no verifica si la función existe o si los parámetros son correctos, lo que puede llevar a errores.

**Sintaxis básica:**

```solidity
(bool exito, bytes memory data) = direccion.call{value: cantidad}(abi.encodeWithSignature("nombreFuncion(parametros)"));
```

* `exito` es un booleano que indica si la llamada fue exitosa.
* `data` contiene los datos devueltos por la función llamada.
* `direccion` es la dirección del contrato al que estás llamando.
* `abi.encodeWithSignature` codifica la firma de la función y sus parámetros.

### Llamando a otra función con `call`

Imaginemos que queremos llamar a una función `establecerMensaje` en un contrato externo que cambia el mensaje almacenado. Aquí está el código:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract InteraccionCall {
    // Función para llamar a otra función en un contrato externo usando `call`
    function cambiarMensaje(address contrato, string memory nuevoMensaje) public {
        // Creamos la firma de la función que queremos llamar
        (bool exito, bytes memory data) = contrato.call(
            abi.encodeWithSignature("establecerMensaje(string)", nuevoMensaje)
        );
        
        // Verificamos si la llamada fue exitosa
        require(exito, "La llamada a la función falló");
    }
}
```

En este ejemplo:

1. **Construcción de la llamada**: Usamos `abi.encodeWithSignature` para crear la firma de la función que queremos llamar. La firma incluye el nombre de la función `establecerMensaje` y su parámetro `(string)`.
2. **Llamada con `call`**: Luego, pasamos esta firma al método `call` junto con la dirección del contrato (`contrato`) y el mensaje que queremos enviar (`nuevoMensaje`).
3. **Verificación del resultado**: Si `exito` es `true`, la llamada fue exitosa. Si no, la transacción falla con el mensaje "La llamada a la función falló".

### Ventajas y desventajas de `call`

**Ventajas:**

1. **Flexibilidad total**: Puedes llamar a cualquier función de cualquier contrato, sin importar su estructura.
2. **Envío de Ether**: Te permite enviar ether y ejecutar funciones en un solo paso.
3. **Compatibilidad**: Funciona incluso si no tienes la interfaz del contrato, siempre que conozcas la firma de la función.

**Desventajas:**

1. **No verifica la existencia de la función**: Si la firma es incorrecta o la función no existe, `call` simplemente devolverá `false` y la transacción no hará nada útil.
2. **Sin revertir cambios automáticamente**: A diferencia de `transfer` o `send`, `call` no revierte la transacción completa si falla, a menos que uses `require` o `assert` para verificar su éxito.
3. **Mayor riesgo de seguridad**: Debido a que `call` no valida la función que estás llamando, es más fácil cometer errores que pueden ser explotados por actores maliciosos.

### Otras formas de interactuar con contratos

Aunque `call` es increíblemente útil, no es la única manera de interactuar con contratos. También puedes usar `delegatecall` para ejecutar el código de otro contrato en el contexto del tuyo, o `staticcall` para realizar llamadas de solo lectura sin modificar el estado. Cada una tiene su propósito específico y sus propias implicaciones de seguridad.
