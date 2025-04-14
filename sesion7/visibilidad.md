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

# Visibilidad

La **visibilidad** define quién puede ver o interactuar con las variables y funciones de tu contrato. Piensa en la visibilidad como en los filtros de privacidad de tus redes sociales ¿quieres que tu publicación la vea todo el mundo, solo tus amigos o solo tú? Aquí es igual, pero en código. Controlar bien la visibilidad es clave para mantener tu contrato seguro y organizado, así que vamos a repasar las opciones disponibles y cómo usarlas.

### Visibilidad para funciones

1.  **`public`**: ¡Todo el mundo es bienvenido! Las funciones `public` pueden ser llamadas desde dentro del contrato, por otros contratos y también desde fuera, como por una interfaz de usuario o directamente desde Core. Son como tu perfil público, visible para todos.

    ```solidity
    function saludar() public returns (string memory) {
        return "¡Hola, mundo!";
    }
    ```

    Con esta función, cualquiera puede llamarla y obtener el saludo.
2.  **`private`**: Solo para ti. Las funciones `private` solo pueden ser llamadas desde el mismo contrato. Ni siquiera los contratos que heredan de este pueden acceder a ellas. Son como tus mensajes directos, nadie más puede verlos ni interactuar con ellos.

    ```solidity
    function calculaSecreto() private view returns (uint) {
        return 42;
    }
    ```
3.  **`internal`**: Solo para la familia. Las funciones `internal` son como las `private`, pero con un poco más de apertura. Pueden ser llamadas desde el mismo contrato y también desde contratos que heredan de él. Imagina un grupo cerrado donde solo los miembros de la familia tienen acceso.

    ```solidity
    function multiplica(uint a, uint b) internal pure returns (uint) {
        return a * b;
    }
    ```
4.  **`external`**: Solo llamadas desde afuera. Las funciones `external` son como `public`, pero con un twist, solo pueden ser llamadas desde fuera del contrato. Esto las hace un poco más eficientes en cuanto a gas. Es como tener una puerta trasera especial que solo se abre desde el exterior.

    ```solidity
    function obtenerValor() external view returns (uint) {
        return valor;
    }
    ```

### Visibilidad para variables

La visibilidad de las variables de estado también es importante. Controla cómo y quién puede acceder a los datos almacenados en tu contrato.

1.  **`public`**: Igual que con las funciones, una variable `public` es visible para todos. Solidity automáticamente crea una función getter para que puedas acceder a su valor desde fuera del contrato.

    ```solidity
    uint public numeroPublico = 42;
    ```

    Con esta variable, puedes ver su valor directamente desde fuera del contrato, sin necesidad de una función de lectura adicional.
2.  **`private`**: Solo para tus ojos. Una variable `private` no puede ser leída ni modificada desde fuera del contrato. Incluso los contratos derivados no pueden acceder directamente a ella. Es como una caja fuerte a la que solo tú tienes la combinación.

    ```solidity
    uint private numeroSecreto = 123;
    ```
3.  **`internal`**: Similar a `private`, pero accesible para contratos derivados. Ideal para compartir datos dentro de una familia de contratos. Es como un documento compartido al que solo la familia tiene acceso.

    ```solidity
    uint internal numeroInterno = 100;
    ```
4. **Sin especificar**: Si no especificas la visibilidad de una variable, será `internal` por defecto. Así que, si quieres que algo sea público o privado, es mejor que lo declares explícitamente para evitar malentendidos.

### Ejemplo práctico con todo combinado

Vamos a ver cómo se vería todo esto en un contrato con funciones y variables de diferentes niveles de visibilidad:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract EjemploVisibilidad {
    // Variable pública: accesible para todos
    uint public contadorPublico = 0;

    // Variable interna: solo accesible para este contrato y derivados
    uint internal contadorInterno = 10;

    // Variable privada: nadie fuera de este contrato puede acceder
    uint private contadorSecreto = 100;

    // Función pública: todos pueden llamarla
    function incrementarPublico() public {
        contadorPublico += 1;
    }

    // Función privada: solo puede ser llamada dentro del contrato
    function incrementarSecreto() private {
        contadorSecreto += 1;
    }

    // Función interna: accesible para contratos derivados
    function incrementarInterno() internal {
        contadorInterno += 1;
    }

    // Función externa: solo llamadas desde fuera
    function obtenerContadorSecreto() external view returns (uint) {
        return contadorSecreto;
    }
}
```
