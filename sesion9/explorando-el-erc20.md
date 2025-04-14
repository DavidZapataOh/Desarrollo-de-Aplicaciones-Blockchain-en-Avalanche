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

# Explorando el ERC20

### ¿Qué es el ERC20?

El ERC20 es un estándar que define un conjunto común de funciones y eventos que todos los tokens deben implementar para ser compatibles con la mayoría de las aplicaciones y wallets. Piensa en él como un protocolo de comunicación que asegura que todos los tokens hablen el mismo “idioma”, permitiendo que se transfieran, intercambien y manejen fácilmente.

{% embed url="https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol" %}

### Componentes Clave del ERC20

El estándar ERC20 define seis funciones y dos eventos fundamentales que todos los contratos de tokens deben implementar:

**1. Funciones principales:**

1. **`constructor`:** Establece el nombre y el símbolo del token cuando se despliega el contrato. Estos valores son inmutables y no pueden cambiarse después de la creación.
   * **Parámetros:** `name_` (nombre del token) y `symbol_` (símbolo del token).
   * **Ejemplo:** Si creas un token con `constructor("MiToken", "MTK")`, el nombre será "MiToken" y el símbolo "MTK".
2. **`name()`:** Devuelve el nombre del token. Es una función de solo lectura y su valor se establece durante la construcción del contrato.
   * **Retorna:** El nombre del token como una cadena de texto (`string`).
3. **`symbol()`:** Devuelve el símbolo del token, generalmente una abreviatura o versión corta del nombre.
   * **Retorna:** El símbolo del token (`string`).
4. **`decimals()`:** Devuelve el número de decimales que usa el token para su representación. Por defecto, es 18, lo que significa que 1 token se divide en 10^18 partes.
   * **Retorna:** Un entero (`uint8`) que representa los decimales.
5. **`totalSupply()`:** Muestra la cantidad total de tokens en circulación. Este valor cambia solo cuando se crean o destruyen tokens (a través de `_mint` o `_burn`).
   * **Retorna:** La cantidad total de tokens en existencia (`uint256`).
6. **`balanceOf(address account)`:** Devuelve el saldo de tokens de una dirección específica. Permite verificar cuántos tokens posee una cuenta en particular.
   * **Parámetro:** `account` (la dirección a consultar).
   * **Retorna:** El saldo de tokens en la dirección (`uint256`).
7. `transfer(address to, uint256 value)`: Transfiere una cantidad específica de tokens desde el remitente a otra dirección.
   * **Parámetros:** `to` (dirección del receptor) y `value` (cantidad de tokens a transferir).
   * **Requisitos:** El remitente debe tener al menos `value` tokens.
   * **Retorna:** `true` si la transferencia fue exitosa.
8. `allowance(address owner, address spender)`: Muestra la cantidad de tokens que un propietario ha permitido que un tercero (spender) gaste en su nombre.
   * **Parámetros:** `owner` (propietario de los tokens) y `spender` (quien tiene permiso para gastar).
   * **Retorna:** Cantidad de tokens permitidos (`uint256`).
9. `approve(address spender, uint256 value)`: Autoriza a otra dirección a gastar una cantidad específica de tus tokens. Es útil para permitir que contratos automatizados realicen pagos en tu nombre.
   * **Parámetros:** `spender` (dirección autorizada) y `value` (cantidad de tokens permitidos).
   * **Retorna:** `true` si la aprobación fue exitosa.
10. `transferFrom(address from, address to, uint256 value)`: Permite transferir tokens desde una cuenta a otra en nombre de alguien más, siempre y cuando se haya aprobado previamente.
    * **Parámetros:** `from` (dirección de origen), `to` (dirección de destino) y `value` (cantidad de tokens a transferir).
    * **Requisitos:** `from` debe tener suficientes tokens y el remitente debe tener permiso para gastar al menos `value` tokens.
    * **Retorna:** `true` si la transferencia fue exitosa.
11. `_transfer(address from, address to, uint256 value)`: Función interna que mueve tokens de una dirección a otra. Esta función es llamada por `transfer` y `transferFrom`.
    * **Parámetros:** `from` (origen de los tokens), `to` (destino de los tokens) y `value` (cantidad de tokens transferidos).
12. `_update(address from, address to, uint256 value)`: Actualiza los saldos de las cuentas durante una transferencia, minting o burning. Si `from` es la dirección cero, se crea una nueva cantidad de tokens. Es posible sobrescribir esta función para agregar lógica personalizada, como restricciones adicionales o eventos específicos.
13. `_mint(address account, uint256 value)`: Crea nuevos tokens y se los asigna a la cuenta especificada. Aumenta la oferta total de tokens.
    * **Parámetro:** `account` (dirección a la que se asignan los tokens) y `value` (cantidad de tokens creados).
14. `_burn(address account, uint256 value)`: Destruye tokens de la cuenta especificada, reduciendo la oferta total de tokens.
    * **Parámetro:** `account` (dirección de la que se eliminan los tokens) y `value` (cantidad de tokens destruidos).
15. `_approve(address owner, address spender, uint256 value, bool emitEvent)`: Establece una cantidad específica de tokens que un `spender` puede gastar en nombre de `owner`. Si `emitEvent` es verdadero, emite un evento `Approval`.
    * **Parámetros:** `owner` (propietario de los tokens), `spender` (quien tiene permiso para gastar), `value` (cantidad de tokens permitidos) y `emitEvent` (si se debe emitir un evento).
16. `_spendAllowance(address owner, address spender, uint256 value)`: Actualiza la cantidad de tokens que un `spender` puede gastar en nombre de `owner` basado en el valor gastado. No actualiza el valor si la cantidad permitida es máxima (`type(uint256).max`).
    * **Parámetros:** `owner` (propietario de los tokens), `spender` (quien tiene permiso para gastar), `value` (cantidad gastada).

**2. Eventos principales:**

1. **`Transfer(address indexed from, address indexed to, uint256 value)`**: Se dispara cada vez que se transfieren tokens, ya sea directamente entre dos usuarios o mediante `transferFrom`. Es la forma en que los exploradores de bloques y las aplicaciones de terceros rastrean movimientos de tokens.
2. **`Approval(address indexed owner, address indexed spender, uint256 value)`**: Se emite cuando el propietario aprueba a un tercero para gastar sus tokens. Es como dejar un rastro de papel de quién tiene permiso para gastar qué cantidad de tokens.

### ¿Por qué es tan importante el ERC20?

1. **Interoperabilidad:** Cualquier dApp (aplicación descentralizada) que soporte tokens ERC20 puede interactuar con cualquier token que siga este estándar, sin necesidad de saber detalles específicos de su implementación. Esto facilita la creación de exchanges, wallets y plataformas DeFi.
2. **Estandarización:** Gracias a que todos los tokens ERC20 funcionan de la misma manera, es fácil integrar nuevos tokens en plataformas existentes. Por ejemplo, agregar un nuevo token a una wallet compatible con ERC20 es tan simple como añadir su dirección de contrato.
3. **Seguridad y confiabilidad:** El estándar reduce la posibilidad de errores y vulnerabilidades porque sigue reglas establecidas y probadas. Aunque no es infalible, usar ERC20 ayuda a evitar muchos de los problemas comunes en la creación de contratos inteligentes.

### Contrato ERC20

Aquí te muestro cómo se vería un contrato ERC20 básico utilizando OpenZeppelin, una biblioteca que simplifica la implementación de contratos seguros y estándar:

```solidity
// Importamos el contrato ERC20 de OpenZeppelin
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

// Creamos un contrato ERC20 llamado "TokenSimple"
contract TokenSimple is ERC20 {
    constructor(uint256 initialSupply) ERC20("TokenSimple", "TS") {
        _mint(msg.sender, initialSupply);
    }
}
```

1. **Importación:** Se importa la implementación estándar de ERC20 de OpenZeppelin, lo que garantiza que se sigan todas las reglas del estándar.
2. **Creación del Token:** Se inicializa un token llamado `TokenSimple` con el símbolo `TS`, y se le asigna una cantidad inicial de tokens al creador del contrato.
