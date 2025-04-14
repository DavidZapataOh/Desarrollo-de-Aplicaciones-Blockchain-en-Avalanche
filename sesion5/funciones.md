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

# Funciones

Las **funciones** en Solidity son la columna vertebral de cualquier contrato inteligente. Son bloques de código reutilizables que permiten interactuar con el contrato, modificar su estado, ejecutar lógica y devolver resultados. Vamos a desglosar todo lo que necesitas saber sobre las funciones, desde su estructura básica hasta las diferentes opciones de visibilidad y modificadores que puedes usar para controlar su comportamiento.

### ¿Qué es una función en Solidity?

Una función en Solidity es un conjunto de instrucciones que realizan una tarea específica. Cada vez que se invoca una función, se ejecuta su código y, dependiendo de su diseño, puede leer o modificar el estado del contrato, interactuar con otros contratos o incluso devolver valores.

```solidity
function saludar() public pure returns (string memory) {
    return "Hola, Avalanche!";
}
```

En este ejemplo, `saludar` es una función simple que devuelve un saludo. Vamos a desglosar los elementos principales:

1. **`function`**: La palabra clave para definir una función.
2. **`saludar`**: El nombre de la función.
3. **`public`**: Especifica la visibilidad de la función.
4. **`pure`**: Indica que la función no accede ni modifica el estado del contrato.
5. **`returns (string memory)`**: Especifica que la función devuelve un dato, en esta caso una cadena de texto.

### Parametros

Las funciones en Solidity pueden recibir **parámetros** como entrada para ejecutar lógica específica. Los parámetros son variables que se pasan a la función al momento de llamarla, permitiendo personalizar su comportamiento según los valores proporcionados. Los parámetros se definen dentro de los paréntesis de la función y pueden ser de cualquier tipo de dato

```solidity
function setSaldo(uint256 nuevoSaldo, address usuario) public {
    saldos[usuario] = nuevoSaldo;
}
```

En este caso la función `setSaldo` recibe dos parámetros: `nuevoSaldo` (un número entero) y `usuario` (una dirección). Esto permite establecer el saldo de cualquier dirección específica.

### Tipos de Funciones en Solidity

#### **1. Funciones de Estado**

Estas funciones pueden modificar el estado del contrato. Es decir, pueden cambiar el valor de las variables de estado.

```solidity
function setBalance(uint256 _balance) public {
    balance = _balance;
}
```

* `setBalance` es una función que modifica la variable de estado `balance`. Este tipo de funciones conlleva costos de gas porque realizan escrituras en la blockchain.

#### **2. Funciones de Solo Lectura**

Estas funciones solo leen el estado del contrato y no lo modifican. Se declaran con el modificador `view`.

```solidity
function getBalance() public view returns (uint256) {
    return balance;
}
```

* `getBalance` devuelve el valor de `balance` sin modificarlo. Las funciones `view` no incurren en costos de gas cuando se llaman externamente (por ejemplo, desde una interfaz).

### Ejemplos de funciones

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Funciones {
    uint8 edad;

    // Función para establecer la edad (modifica el estado)
    function asignarEdad(uint8 _edad) public {
        edad = _edad;
    }

    // Función para obtener la edad (solo lectura)
    function verEdad() public view returns (uint8) {
        return edad;
    }

    // Función pura que suma dos números
    function sumar(uint a, uint b) public pure returns (uint256) {
        return a + b;
    }

    // Función que calcula la edad en días (internal)
    function edadEnDias() public view returns (uint16) {
        return edad * 365;
    }
}
```

