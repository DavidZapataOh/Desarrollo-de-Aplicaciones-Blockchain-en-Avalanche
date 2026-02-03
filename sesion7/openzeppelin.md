---
icon: square-small
---

# Openzeppelin

**OpenZeppelin** es una biblioteca que ofrece contratos inteligentes prediseñados y auditados que te ahorran tiempo y te protegen de cometer errores comunes. Si estás desarrollando en Solidity y quieres evitar reinventar la rueda (y además asegurarte de que tu código sea lo más seguro posible), OpenZeppelin es una herramienta esencial.

### ¿Qué es OpenZeppelin?

OpenZeppelin es una colección de contratos inteligentes modulares y reutilizables, diseñada para ayudarte a construir aplicaciones descentralizadas de forma rápida y segura. Los contratos de OpenZeppelin han sido ampliamente auditados y probados, por lo que utilizarlos reduce significativamente el riesgo de introducir errores o vulnerabilidades en tu código.

**Principales ventajas:**

1. **Seguridad:** Los contratos de OpenZeppelin son desarrollados y auditados por expertos en seguridad, lo que minimiza las posibilidades de que existan vulnerabilidades.
2. **Estandarización:** Implementa fácilmente estándares como ERC20, ERC721 (NFTs) y ERC1155, garantizando que tu contrato cumpla con las especificaciones de la comunidad.
3. **Modularidad:** Puedes personalizar y extender los contratos de OpenZeppelin para adaptarlos a las necesidades específicas de tu proyecto.

### ¿Qué puedes hacer con OpenZeppelin?

OpenZeppelin te ofrece contratos prediseñados para una variedad de casos de uso:

1. **Tokens ERC20 y ERC721 (NFTs):** Implementa fácilmente tu propio token fungible (como un token de utilidad) o no fungible (como un coleccionable digital).
2. **Roles y permisos:** Controla quién puede ejecutar ciertas funciones en tu contrato mediante los contratos de roles y permisos.
3. **Gobernanza:** Construye sistemas de votación y gestión de propuestas para proyectos descentralizados.
4. **Pausabilidad y seguridad:** Implementa funciones para pausar ciertas operaciones críticas en tu contrato en caso de emergencia.

### Creando un token ERC20 con OpenZeppelin

Vamos a crear un token ERC20 simple utilizando OpenZeppelin. En lugar de escribir todo el contrato desde cero, aprovecharemos la implementación de OpenZeppelin para asegurarnos de que el contrato siga los estándares y sea seguro.

```solidity
solidityCopy code// Importamos el contrato ERC20 de OpenZeppelin
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MiToken is ERC20 {
    // Constructor para inicializar el contrato con nombre y símbolo
    constructor() ERC20("Mi Token", "MTK") {
        // Asigna todos los tokens al creador del contrato
        _mint(msg.sender, 1000000 * (10 ** uint256(decimals())));
    }
}
```

¿Qué hace este contrato?

1. **Importación del contrato ERC20:** Usamos la implementación estándar de OpenZeppelin para asegurarnos de que el contrato siga todas las especificaciones del estándar ERC20.
2. **Inicialización del contrato:** En el constructor, inicializamos el nombre (`Mi Token`) y el símbolo (`MTK`).
3. **Minting inicial:** Creamos 1 millón de tokens y se los asignamos al creador del contrato.

### Otras funcionalidades destacadas de OpenZeppelin

1. **Ownable:** Este contrato es ideal para controlar el acceso a funciones específicas, definiendo un propietario del contrato que puede transferir la propiedad a otro usuario.
2. **Pausable:** Te permite pausar y reanudar ciertas funciones críticas del contrato. Muy útil en situaciones de emergencia.
3. **SafeMath:** Previene problemas comunes como los desbordamientos y subdesbordamientos (overflow y underflow) en operaciones aritméticas. Aunque esto ya no es necesario en versiones más recientes de Solidity, sigue siendo una buena práctica para contratos más antiguos.
