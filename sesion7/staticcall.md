---
icon: square-small
---

# StaticCall

El método `staticcall` en Solidity es el modo “solo lectura” para interactuar con otros contratos. Te permite consultar información sin cambiar nada en el contrato al que llamas, lo cual es genial cuando solo necesitas obtener datos. A diferencia de `call`, `staticcall` garantiza que no se podrá modificar el estado del contrato, incluso si intentas hacerlo. Es perfecto para llamadas seguras donde no quieres preocuparte por alterar accidentalmente algo en el contrato externo.

### ¿Qué es `staticcall`?

`staticcall` es una función de bajo nivel que se utiliza para hacer llamadas a otros contratos de manera segura, asegurando que la llamada no pueda alterar el estado del contrato al que se está llamando. Si la función que intentas llamar intenta hacer cambios (como transferir tokens o modificar una variable), `staticcall` fallará. Es como decirle al contrato: "Quiero saber algo, pero prometo no tocar nada".

**Sintaxis básica:**

```solidity
(bool exito, bytes memory data) = direccion.staticcall(abi.encodeWithSignature("nombreFuncion(parametros)"));
```

* `exito` es un booleano que indica si la llamada fue exitosa.
* `data` contiene los datos devueltos por la función llamada.
* `direccion` es la dirección del contrato al que estás llamando.
* `abi.encodeWithSignature` codifica la firma de la función y sus parámetros.

### Llamando a otra función con `staticcall`

Imaginemos que queremos consultar el balance de tokens de un usuario en un contrato ERC20 sin cambiar nada en el contrato. Vamos a ver cómo se hace:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ConsultaBalance {
    // Función para consultar el balance usando `staticcall`
    function consultarBalance(address contratoToken, address cuenta) public view returns (uint256) {
        // Preparamos la llamada con `staticcall`
        (bool exito, bytes memory data) = contratoToken.staticcall(
            abi.encodeWithSignature("balanceOf(address)", cuenta)
        );
        
        // Verificamos si la llamada fue exitosa
        require(exito, "Fallo en la llamada a staticcall");
        
        // Decodificamos el resultado para obtener el balance
        return abi.decode(data, (uint256));
    }
}
```

1. **Construcción de la llamada**: Usamos `abi.encodeWithSignature` para crear la firma de la función `balanceOf`, que toma una dirección como parámetro (`cuenta`).
2. **Llamada con `staticcall`**: Llamamos a la función `balanceOf` del contrato de tokens (`contratoToken`) usando `staticcall`.
3. **Verificación del resultado**: Si `exito` es `true`, la llamada fue exitosa. Si no, la transacción falla con el mensaje "Fallo en la llamada a staticcall".
4. **Decodificación del resultado**: Usamos `abi.decode` para convertir los datos devueltos (`data`) en un número entero (`uint256`), que es el balance del usuario.

### Ventajas y desventajas de `staticcall`

**Ventajas:**

1. **Seguridad**: Garantiza que no se harán cambios en el contrato llamado, protegiendo contra modificaciones no deseadas.
2. **Eficiencia**: Las llamadas de solo lectura son más baratas en términos de gas, ya que no necesitan registrar cambios en la blockchain.
3. **Ideal para consultas**: Perfecto para consultar balances, estados de contratos y cualquier otra información que no necesite alterar el contrato.

**Desventajas:**

1. **Limitación a solo lectura**: No puedes hacer nada que modifique el estado, como transferir tokens o actualizar variables.
2. **Fallo en funciones con cambios de estado**: Si intentas llamar a una función que modifica el estado, la llamada fallará, ya que `staticcall` no permite cambios.

### Comparación con `call` y `delegatecall`

* **`call`**: Te permite hacer cualquier tipo de llamada, incluyendo cambios de estado y envío de ether. Es flexible pero potencialmente riesgoso.
* **`delegatecall`**: Ejecuta el código de otro contrato en el contexto de tu contrato. Cambia tu propio estado en lugar del contrato llamado.
* **`staticcall`**: Es la opción segura y específica para llamadas de solo lectura, asegurando que no se hagan cambios en el contrato externo.

### ¿Por qué usar `staticcall`?

Si solo necesitas consultar datos sin afectar el estado del contrato, `staticcall` es tu mejor opción. Por ejemplo, si quieres verificar balances, estados de contratos o cualquier otra información estática, `staticcall` garantiza que no ocurrirán cambios inesperados. Esto lo convierte en una herramienta esencial para evitar errores o comportamientos no deseados en tus contratos.
