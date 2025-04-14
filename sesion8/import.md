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

# Import

En Solidity, el comando `import` es como abrir la caja de herramientas y sacar justo lo que necesitas. Te permite reutilizar código de otros archivos en tu propio contrato, manteniendo tu proyecto organizado y evitando duplicaciones innecesarias. Esencialmente con `import` puedes traer contratos, librerías o interfaces de otros archivos, lo cual es especialmente útil en proyectos grandes donde cada contrato o librería está en su propio archivo.

### ¿Cómo funciona `import`?

El comando `import` te permite incluir el contenido de otro archivo en tu contrato actual. Puedes pensar en ello como una forma de “copiar y pegar” todo el código de un archivo externo, pero sin tener que hacerlo manualmente. Esto facilita la reutilización de contratos y librerías existentes, y te permite separar la lógica en diferentes archivos para mantener todo organizado.

**Sintaxis básica:**

```solidity
import "ruta/archivo.sol";
```

La ruta puede ser relativa (dentro de tu proyecto) o absoluta (si estás usando paquetes de NPM o librerías de OpenZeppelin, por ejemplo).

### Ejemplo básico de `import`

Supongamos que tienes una librería matemática en un archivo llamado `Math.sol`, y quieres usar sus funciones en tu contrato principal. La estructura de tu proyecto sería algo así:

```markdown
- contracts/
  - Math.sol
  - MiContrato.sol
```

1. **Contenido del archivo `Math.sol`:**

```solidity
// Librería matemática básica
library Math {
    function sumar(uint a, uint b) internal pure returns (uint) {
        return a + b;
    }

    function restar(uint a, uint b) internal pure returns (uint) {
        return a - b;
    }
}
```

2. **Contenido del archivo `MiContrato.sol`:**

```solidity
// Importar la librería Math
import "./Math.sol";

contract MiContrato {
    // Usar la librería Math en nuestro contrato
    function calcularSuma(uint a, uint b) public pure returns (uint) {
        return Math.sumar(a, b); // Llamada a la función sumar de la librería
    }

    function calcularResta(uint a, uint b) public pure returns (uint) {
        return Math.restar(a, b); // Llamada a la función restar de la librería
    }
}
```

#### ¿Qué está pasando aquí?

1. **Importación de `Math.sol`:** El contrato `MiContrato` importa la librería `Math` desde el archivo `Math.sol` usando la ruta relativa `./Math.sol`.
2. **Uso de funciones de la librería:** Dentro de `MiContrato`, llamamos a las funciones `sumar` y `restar` de la librería `Math` sin necesidad de redefinirlas. Esto mantiene nuestro código limpio y modular.

### Otras formas de usar `import`

1.  **Importar todo el contenido de un archivo:**

    ```solidity
    import "./Utils.sol";
    ```

    Esto importa todo el contenido de `Utils.sol` en tu contrato.
2.  **Importar con alias:** Puedes asignar alias para evitar conflictos de nombre cuando importas múltiples librerías o contratos con nombres similares.

    ```solidity
    import { Math as MathLib } from "./Math.sol";
    ```

    Ahora puedes usar `MathLib.sumar(a, b)` en lugar de `Math.sumar(a, b)`.
3.  **Importar solo elementos específicos:** Si solo necesitas ciertas funciones o contratos de un archivo grande, puedes importarlos individualmente.

    ```solidity
    import { sumar, restar } from "./Math.sol";
    ```

    Ahora solo `sumar` y `restar` están disponibles en tu contrato.

### Uso de librerías externas

Una de las grandes ventajas de `import` es la capacidad de usar contratos y librerías de terceros. Por ejemplo, puedes utilizar librerías de OpenZeppelin para implementar funciones de seguridad, administración de roles, o contratos estándar de ERC20 y ERC721.

**Ejemplo:**

```solidity
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MiToken is ERC20 {
    constructor() ERC20("MiToken", "MTK") {
        _mint(msg.sender, 1000 * 10 ** decimals());
    }
}
```

En este ejemplo:

* Estamos importando el contrato `ERC20` de la librería OpenZeppelin.
* El contrato `MiToken` hereda de `ERC20` y aprovecha todas las funcionalidades implementadas por OpenZeppelin para crear un token ERC20 estándar.

### Consideraciones importantes al usar `import`

1. **Evitar importaciones cíclicas:** Asegúrate de que dos archivos no se importen mutuamente, ya que esto causará errores de compilación.
2. **Controlar las versiones:** Asegúrate de que las versiones de los archivos importados sean compatibles con tu contrato para evitar problemas de compilación o ejecución.
3. **Mantener la organización:** Usar `import` de forma efectiva puede hacer que tu código sea mucho más manejable y modular. Organiza tus contratos y librerías en carpetas lógicas para facilitar su uso.
