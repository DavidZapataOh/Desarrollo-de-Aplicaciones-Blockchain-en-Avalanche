---
icon: square-small
---

# Interfaces

Las **interfaces** en Solidity son como contratos abstractos que solo definen la forma de las funciones, sin implementar la lógica de estas. Imagina que son como un manual de instrucciones para que diferentes contratos sepan cómo comunicarse entre ellos. Una interfaz establece las reglas del juego, diciendo qué funciones deben existir y cómo deben ser llamadas, pero no cómo se comportan.

### ¿Qué es una interfaz?

Una interfaz es un contrato especial en Solidity que declara funciones sin cuerpo. Solo define los nombres de las funciones, sus parámetros y qué tipo de datos deben devolver, pero no contienen ninguna lógica interna. Cualquier contrato que implemente esta interfaz deberá definir la lógica de esas funciones.

**Sintaxis básica:**

```solidity
interface NombreDeLaInterfaz {
    function nombreFuncion(tipoParametro) external view returns (tipoRetorno);
}
```

Por ejemplo, una interfaz que define un contrato de tokens podría verse así:

```solidity
interface ERC20 {
    function totalSupply() external view returns (uint256);
    function balanceOf(address cuenta) external view returns (uint256);
    function transfer(address destinatario, uint256 cantidad) external returns (bool);
}
```

En este ejemplo, la interfaz `ERC20` define tres funciones que cualquier contrato de token ERC20 debería tener: `totalSupply` para el suministro total de tokens, `balanceOf` para obtener el saldo de una cuenta, y `transfer` para transferir tokens de una cuenta a otra.

En las interfaces, las funciones deben ser declaradas como `external`.

### ¿Por qué usar interfaces?

Las interfaces son súper útiles cuando necesitas que diferentes contratos interactúen entre sí de manera estandarizada. Al usar una interfaz, garantizas que un contrato cumple con ciertos requisitos mínimos para que otro contrato pueda interactuar con él sin problemas. Es como decir, “si este contrato implementa esta interfaz, sé que puedo llamarlo de esta forma”.

### Implementar una interfaz

Cuando un contrato implementa una interfaz, se compromete a definir todas las funciones que la interfaz declara. Si se te olvida alguna función, tu contrato no se podrá compilar.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

// Definimos la interfaz
interface RegistroVehiculos {
    function registrarVehiculo(string memory _placa, string memory _modelo) external;
    function obtenerVehiculo(string memory _placa) external view returns (string memory modelo);
}

// Implementamos la interfaz en un contrato
contract MiRegistroVehiculos is RegistroVehiculos {
    struct Vehiculo {
        string modelo;
    }

    mapping(string => Vehiculo) private vehiculos;

    // Implementamos la función para registrar un vehículo
    function registrarVehiculo(string memory _placa, string memory _modelo) public override {
        vehiculos[_placa] = Vehiculo(_modelo);
    }

    // Implementamos la función para obtener los datos de un vehículo
    function obtenerVehiculo(string memory _placa) public view override returns (string memory modelo) {
        return vehiculos[_placa].modelo;
    }
}
```

En este ejemplo:

* La interfaz `RegistroVehiculos` define dos funciones: `registrarVehiculo` y `obtenerVehiculo`.
* El contrato `MiRegistroVehiculos` implementa estas funciones con su propia lógica para gestionar un registro de vehículos.

### Cosas que debes saber sobre las interfaces

1. **No puedes tener funciones con lógica**: Las funciones en una interfaz solo pueden ser declaradas, no implementadas.
2. **No puedes tener variables de estado**: Las interfaces no pueden tener variables, constructores o cualquier tipo de almacenamiento.
3. **No puedes heredar de contratos**: Las interfaces solo pueden heredar de otras interfaces, no de contratos completos.
