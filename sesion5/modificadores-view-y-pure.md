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

# Modificadores View y Pure

En Solidity, los modificadores **`view`** y **`pure`** son como las etiquetas “no tocar” y “solo mirar” en un museo. Te dicen qué tipo de interacciones puedes hacer con las funciones y si pueden o no modificar el estado del contrato. Vamos a ver de qué se trata cada uno y cuándo deberías usarlos.

### `view`: Solo mirar, no tocar

Cuando una función tiene el modificador `view`, significa que esta función **puede leer datos del contrato**, pero no puede modificarlos. Es útil para hacer consultas sin cambiar el estado del contrato. Imagina que es como cuando le preguntas a alguien cuál es su color favorito, no estás cambiando su respuesta, solo estás obteniendo información.

```solidity
function obtenerBalance() public view returns (uint256) {
    return balance;
}
```

Aquí, la función `obtenerBalance` solo devuelve el valor de la variable `balance` sin modificar nada. ¿Ventaja? ¡No necesitas gastar gas para usarla cuando la llamas desde fuera del contrato!

### `pure`: Ni tocar, ni mirar

El modificador `pure` lleva las cosas un paso más allá. Indica que la función **no puede leer ni modificar el estado del contrato**. Solo se utiliza para operaciones que no dependen de los datos almacenados en el contrato. Es como resolver un problema de matemáticas en una hoja aparte, no estás mirando nada del contrato, solo estás usando lógica pura.

```solidity
function sumar(uint256 a, uint256 b) public pure returns (uint256) {
    return a + b;
}

```

La función `sumar` toma dos números, los suma y devuelve el resultado. No necesita acceder a ninguna variable del contrato para hacer esto.

### Ejemplo práctico

Vamos a ver un ejemplo que combine ambos tipos de funciones:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract EjemploViewPure {
    uint256 contador;

    // Función que incrementa el contador (modifica el estado)
    function incrementar() public {
        contador += 1;
    }

    // Función 'view' que lee el estado del contrato
    function obtenerContador() public view returns (uint256) {
        return contador;
    }

    // Función 'pure' que realiza un cálculo sin leer ni modificar el estado
    function calcularCuadrado(uint256 x) public pure returns (uint256) {
        return x * x;
    }
}
```

* `incrementar`: Modifica el estado del contrato aumentando el contador.
* `obtenerContador`: Solo lee el valor del contador, sin cambiar nada.
* `calcularCuadrado`: Realiza un cálculo matemático sin tocar ninguna variable del contrato.
