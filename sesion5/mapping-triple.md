---
icon: square-small
---

# Mapping Triple

¡Los mappings dobles son geniales, pero los **mappings triples** llevan la organización de datos a otro nivel! Es como tener una carpeta con subcarpetas, y dentro de cada subcarpeta, aún más carpetas. Con mappings triples puedes gestionar información de tres niveles distintos, ideal para casos más complejos donde necesitas tener datos organizados por múltiples criterios.

### ¿Qué es un mapping triple?

Un **mapping triple** es simplemente un mapping dentro de otro mapping, que a su vez está dentro de otro mapping. Es como un armario con estantes, y cada estante tiene cajones, y cada cajón tiene cajas. Suena enredado, pero es súper útil cuando necesitas manejar datos que dependen de tres claves.

**Sintaxis básica:**

```solidity
mapping(tipoClave1 => mapping(tipoClave2 => mapping(tipoClave3 => tipoValor))) public nombreDelMapping;
```

Por ejemplo, supongamos que queremos llevar un registro de acceso de usuarios a diferentes módulos de una aplicación en días específicos:

```solidity
mapping(address => mapping(string => mapping(string => bool))) public accesos;
```

Aquí, `accesos` toma tres claves:

1. Una dirección (`address`) para identificar al usuario.
2. Un string (`string`) para identificar el módulo (por ejemplo, "Finanzas", "Usuarios").
3. Otro string (`string`) para la fecha específica en formato `"YYYY-MM-DD"`.

El valor almacenado es un booleano (`bool`) que indica si el usuario accedió a ese módulo en ese día específico.

### Ejemplo práctico: Registro de Accesos

Vamos a ver cómo se usa esto con un contrato para registrar accesos de usuarios:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract RegistroDeAccesos {
    // Mapping triple: usuario => (modulo => (fecha => acceso))
    mapping(address => mapping(string => mapping(string => bool))) public accesos;

    // Función para registrar acceso de un usuario a un módulo en una fecha específica
    function registrarAcceso(address usuario, string memory modulo, string memory fecha) public {
        accesos[usuario][modulo][fecha] = true;
    }

    // Función para consultar si un usuario accedió a un módulo en una fecha específica
    function consultarAcceso(address usuario, string memory modulo, string memory fecha) public view returns (bool) {
        return accesos[usuario][modulo][fecha];
    }
}
```

En este contrato, cada usuario tiene un mapping que almacena módulos, y cada módulo tiene otro mapping que almacena fechas y si hubo acceso o no. Vamos a ver cómo se vería esto en una tabla:

| **Usuario (address)** | **Módulo**  | **Fecha**    | **Acceso** |
| --------------------- | ----------- | ------------ | ---------- |
| 0x123...abc           | "Finanzas"  | "2023-09-25" | true       |
| 0x123...abc           | "Usuarios"  | "2023-09-25" | false      |
| 0x456...def           | "Finanzas"  | "2023-09-24" | true       |
| 0x789...ghi           | "Marketing" | "2023-09-23" | false      |

En esta tabla, podemos ver que el primer usuario (`0x123...abc`) accedió al módulo de "Finanzas" el 25 de septiembre de 2023, pero no al de "Usuarios". Mientras que el segundo usuario (`0x456...def`) accedió a "Finanzas" el 24 de septiembre, y el tercero (`0x789...ghi`) no accedió al módulo de "Marketing" el 23 de septiembre.

### Ventajas de los mappings triples

1. **Organización extrema**: Ideal para estructuras de datos muy complejas, como permisos de acceso a múltiples niveles, historial de transacciones categorizado, o cualquier otro caso donde necesites organizar datos por tres criterios.
2. **Acceso rápido**: Aunque parece complicado, Solidity accede a los valores de un mapping triple de manera eficiente usando las tres claves.
3. **Flexibilidad total**: Puedes agregar o quitar datos en cualquier nivel del mapping sin tener que rediseñar la estructura del contrato. Si se necesita agregar un nuevo módulo o una nueva fecha, simplemente se agrega una nueva entrada al mapping.
