---
icon: square-small
---

# Llamando Contratos desde su Address

En Solidity, **llamar contratos desde su dirección** es como usar el número de teléfono de alguien para pedirle que haga algo. Tienes la dirección del contrato y, con eso, puedes llamarlo para que ejecute alguna función específica o incluso interactuar con su lógica interna. Esto te permite hacer que diferentes contratos se comuniquen entre sí de manera eficiente y modular.

### ¿Cómo funciona?

Si conoces la dirección de un contrato y sabes qué funciones tiene, puedes interactuar con ese contrato fácilmente usando una interfaz. Esto te permite realizar llamadas a contratos externos sin necesidad de copiar su código, lo cual es ideal si solo necesitas usar algunas de sus funciones.

**Paso a paso:**

1. **Define la interfaz del contrato** con las funciones que necesitas usar.
2. **Convierte la dirección** del contrato externo a un tipo de interfaz.
3. **Llama a las funciones** del contrato a través de esa interfaz.

### Ejemplo práctico

Supongamos que queremos interactuar con un contrato de tokens que sigue el estándar ERC20, y su dirección es `0x1234...`. Queremos transferir tokens a una cuenta específica. Primero, definimos la interfaz del token:

```solidity
interface IERC20 {
    function transfer(address destinatario, uint256 cantidad) external returns (bool);
    function balanceOf(address cuenta) external view returns (uint256);
}
```

Luego, usamos esta interfaz para llamar al contrato desde su dirección:

```solidity
contract InteraccionToken {
    // Función para transferir tokens a través de la dirección del contrato
    function enviarTokens(address contratoToken, address destinatario, uint256 cantidad) public {
        // Convertimos la dirección a la interfaz del token
        IERC20 token = IERC20(contratoToken);
        
        // Llamamos a la función transfer del contrato token
        bool exito = token.transfer(destinatario, cantidad);
        
        // Verificamos si la transferencia fue exitosa
        require(exito, "Transferencia fallida");
    }

    // Función para consultar el balance de una cuenta
    function consultarBalance(address contratoToken, address cuenta) public view returns (uint256) {
        // Convertimos la dirección a la interfaz del token
        IERC20 token = IERC20(contratoToken);
        
        // Llamamos a la función balanceOf del contrato token
        return token.balanceOf(cuenta);
    }
}
```

¿Qué está pasando aquí?

1. **Interfaz `IERC20`**: Define las funciones `transfer` y `balanceOf`, que son las funciones estándar de los tokens ERC20.
2. **Conversión de la dirección a interfaz**: En la función `enviarTokens`, tomamos la dirección del contrato de tokens (`contratoToken`) y la "convertimos" a la interfaz `IERC20`. Esto nos permite interactuar con el contrato usando las funciones que hemos definido en la interfaz.
3. **Llamada a `transfer`**: Luego llamamos a la función `transfer` del contrato externo usando la interfaz. Si la transferencia es exitosa, la función devuelve `true`; de lo contrario, lanzamos un error con `require`.

### Ventajas de usar interfaces para llamar a contratos externos

1. **Modularidad**: No necesitas copiar el código de otros contratos, solo defines una interfaz y llamas las funciones que necesitas.
2. **Facilidad de actualización**: Si el contrato externo actualiza su lógica pero mantiene la misma interfaz, tu contrato seguirá funcionando sin problemas.
3. **Simplicidad**: La interfaz te permite mantener tu código limpio y fácil de entender, ya que no necesitas manejar toda la lógica interna del contrato externo.
