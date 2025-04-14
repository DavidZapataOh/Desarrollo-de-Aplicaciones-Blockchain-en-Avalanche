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

# Structs

Las **structs** en Solidity te permiten meter diferentes tipos de datos y llevarlos todos juntos. En lugar de manejar un montón de variables sueltas, las structs te permiten agrupar datos relacionados en un solo paquete. Esto es útil cuando tienes una entidad que necesita almacenar múltiples tipos de información, como el perfil de un usuario o los detalles de una transacción.

### ¿Qué es un struct?

Un `struct` te permite definir tu propio tipo de dato compuesto por múltiples variables. Cada una de estas variables puede ser de un tipo diferente, como números, direcciones, booleanos, etc. Es como crear tu propia plantilla para agrupar datos relacionados bajo un solo nombre.

**Sintaxis básica:**

```solidity
struct NombreDelStruct {
    tipoDato1 variable1;
    tipoDato2 variable2;
    tipoDato3 variable3;
}
```

Por ejemplo, supongamos que queremos almacenar la información de un usuario en nuestro contrato:

```solidity
struct Usuario {
    string nombre;
    uint edad;
    address direccion;
}
```

Aquí, la struct `Usuario` agrupa tres variables: `nombre` (cadena de texto), `edad` (número entero) y `direccion` (address). En lugar de manejar estos tres datos por separado, ahora puedes usarlos como un solo conjunto.

### Cómo usar las structs

Una vez que tienes definida una struct, puedes usarla para declarar variables que sigan ese "molde". Veamos cómo se hace:

```solidity
Usuario public usuario1;
```

Ahora, `usuario1` es una variable de tipo `Usuario` que puede almacenar un nombre, una edad y una dirección. Puedes asignar valores a cada campo del struct así:

```solidity
usuario1 = Usuario("Alice", 30, 0x1234567890123456789012345678901234567890);
```

También puedes acceder a los valores dentro de la struct utilizando el punto:

```solidity
string memory nombreUsuario = usuario1.nombre; // Accede al nombre
usuario1.edad = 31; // Modifica la edad
```

### Ejemplo práctico: Sistema de Usuarios

Vamos a ver cómo podrías usar structs para crear un sistema que registre usuarios en un contrato:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract RegistroUsuarios {
    // Definimos la struct Usuario
    struct Usuario {
        string nombre;
        uint edad;
        address direccion;
    }

    // Creamos un mapping para almacenar usuarios usando su dirección
    mapping(address => Usuario) usuarios;

    // Función para registrar un nuevo usuario
    function registrarUsuario(string memory _nombre, uint _edad) public {
        usuarios[msg.sender] = Usuario(_nombre, _edad, msg.sender);
    }

    // Función para obtener la información de un usuario
    function obtenerUsuario(address _direccion) public view returns (string memory, uint, address) {
        Usuario memory usuario = usuarios[_direccion];
        return (usuario.nombre, usuario.edad, usuario.direccion);
    }
}
```

En este ejemplo, usamos una struct `Usuario` para agrupar el nombre, la edad y la dirección de los usuarios. Luego, con el mapping `usuarios`, almacenamos la información de cada usuario bajo su dirección (`address`). Los usuarios pueden registrarse usando la función `registrarUsuario` y puedes consultar los datos de cualquier usuario con `obtenerUsuario`.

### Cosas que debes saber sobre los structs

1. **Almacenamiento en structs**: Las structs se pueden almacenar tanto en **memoria** como en **storage**. Si declaras una struct dentro de una función, debes especificar si estará en memoria o en storage, porque Solidity necesita saber dónde colocarla.
2. **Uso eficiente de gas**: Las structs pueden ahorrar espacio al agrupar datos, pero si no las optimizas bien, pueden ocupar varias slots de almacenamiento, lo que aumentará el gas necesario para su manipulación.
3. **Arrays de structs**: Puedes usar arrays de structs para manejar múltiples instancias de la misma. Por ejemplo, podrías tener un array de `Usuario[]` si necesitas manejar una lista de usuarios.
4. **Structs anidados**: También es posible tener structs dentro de otros structs. Esto es útil cuando necesitas organizar datos aún más complejos.
