---
icon: square-small
---

# Librerías

En Solidity, **las librerías** funcionan de forma similar a los contratos, pero están optimizadas para no ocupar espacio extra en la blockchain y para no ser desplegadas por sí mismas. En lugar de crear múltiples copias de una función en cada contrato, puedes usar una librería para centralizar la lógica y hacer que varios contratos la reutilicen. Esto ahorra gas y mantiene el código más limpio y eficiente.

### ¿Qué es una librería?

Una librería en Solidity es un conjunto de funciones que pueden ser utilizadas por otros contratos. Las librerías no pueden mantener estado, es decir, no tienen variables de estado ni pueden recibir ether. Están diseñadas para ser ligeras y modulares, y pueden definirse como "internas" o "externas", dependiendo de cómo quieras usarlas.

* **Interna**: Las funciones de la librería se copian en el contrato que las llama durante la compilación. No se requiere una dirección adicional para invocarlas.
* **Externa**: La librería se despliega como un contrato separado y luego los contratos llaman a sus funciones a través de la dirección de la librería, lo que reduce el espacio de almacenamiento.

### ¿Cómo funciona una librería?

Una librería puede contener funciones que se aplican a tipos de datos específicos o funciones más generales que otros contratos pueden invocar. La gran ventaja es que permiten reutilizar código y hacer que tus contratos sean más modulares.

**Sintaxis básica de una librería:**

```solidity
library MiLibreria {
    function incrementar(uint valor) internal pure returns (uint) {
        return valor + 1;
    }
}
```

Este es un ejemplo simple de una librería llamada `MiLibreria` con una función `incrementar` que toma un número y lo aumenta en uno. Esta función puede ser usada por otros contratos para reutilizar esta lógica, en lugar de escribirla repetidamente.

### Librería de cadena de texto

Veamos un ejemplo más interesante. Vamos a crear una librería que trabaje con cadenas de texto (strings), permitiendo convertirlas en mayúsculas.

```solidity
library StringUtils {
    // Convierte una cadena de texto a mayúsculas
    function toUpperCase(string memory str) internal pure returns (string memory) {
        bytes memory bStr = bytes(str);
        for (uint i = 0; i < bStr.length; i++) {
            if (bStr[i] >= 0x61 && bStr[i] <= 0x7A) {
                bStr[i] = bytes1(uint8(bStr[i]) - 32);
            }
        }
        return string(bStr);
    }
}
```

**¿Qué hace esta librería?**

1. **Convierte cadenas de texto**: La función `toUpperCase` convierte cualquier letra minúscula en una cadena de texto a mayúsculas.
2. **Reutilizable**: Esta lógica puede ser utilizada en cualquier contrato que necesite manipular cadenas de texto.

### Usando la librería en un contrato

Una vez que hemos definido la librería, podemos usarla en cualquier contrato. Aquí te muestro cómo hacerlo:

```solidity
import "./StringUtils.sol";

contract GestorDeCadenas {
    using StringUtils for string;

    // Devuelve una cadena en mayúsculas
    function convertir(string memory texto) public pure returns (string memory) {
        return texto.toUpperCase();
    }
}
```

En este ejemplo, estamos usando la librería `StringUtils` para convertir una cadena de texto a mayúsculas. La línea `using StringUtils for string` nos permite extender el tipo `string` y usar la función `toUpperCase` como si fuera parte de las funciones básicas de las cadenas de texto.

### Consideraciones al usar librerías

* **Funciones puras y view**: Debido a que las librerías no tienen estado, las funciones que contienen suelen ser puras (`pure`) o de solo lectura (`view`), lo que significa que no pueden modificar el estado del contrato.
* **No son contratos independientes**: Las librerías no pueden ser desplegadas por sí solas, pero pueden ser llamadas por otros contratos para ejecutar lógica.
* **Seguridad**: Usar librerías auditadas o bien probadas mejora la seguridad de tus contratos, ya que reduces el riesgo de introducir errores o vulnerabilidades.
